---
title: "メッセージ フローのトレースの構成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15571ca2-bee2-47fb-ba10-fcbc09152ad0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# メッセージ フローのトレースの構成
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] のアクティビティ トレースが有効な場合は、エンド ツー エンド アクティビティ ID が、[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] スタック全体で論理アクティビティに割り当てられます。  [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] では、この機能の高パフォーマンス バージョンが導入されており、"メッセージ フローのトレース" と呼ばれる Event Tracing for Windows \(ETW\) と連携します。  この機能が有効な場合は、エンド ツー エンド アクティビティ ID が受信メッセージから取得され \(空の場合は割り当てられ\)、チャネルによってメッセージがデコードされた後に生成されたすべてのトレース イベントに伝達されます。  ユーザーはこの機能を使用して、デコード後に、異なるサービスから取得したトレース ログでメッセージ フローを再構築できます。  
  
 トレースは、アプリケーションで問題が検出された後に有効にし、その問題が解決された後は無効にすることができます。  
  
## トレースの有効化  
 メッセージ フローのトレースを有効にするには、次の例に示すように、.NET Framework 4 の `messageFlowTracing` 構成要素を `true` に設定します。  
  
```  
<system.servicemodel>  
  <diagnostics>  
    <endToEndTracing propagateActivity="true" messageFlowTracing="true" />  
  </diagnostics>  
</system.servicemodel>  
  
```  
  
> [!NOTE]
>  `endToEndTracing` 構成要素は Web.config ファイル内にあるため、ETW と同じ方法で動的に構成することはできません。  `endToEndTracing` 構成要素を有効にするには、アプリケーションをリサイクルする必要があります。  
  
 アクティビティはアクティビティ ID と呼ばれる識別子の交換によって関連付けられます。  この識別子は GUID で、System.Diagnostics.CorrelationManager クラスによって生成されます。  System.Diagnostics.Trace.CorrelationManager.ActivityID を操作する場合は、実行の制御が WCF コードに転送を返すときに値を元の値に設定するようにしてください。  また、非同期 WCF プログラミング モデルを使用する場合は、System.Diagnostics.Trace.CorrelationManager.ActivityID がスレッド間で転送されるようにしてください。  
  
## メッセージ フローのトレース REST サービス  
 メッセージ フローのトレースでは、要求をエンドツーエンドでトレースできます。  SOAP ベースのサービスでは、アクティビティ ID は、SOAP メッセージのヘッダー内で送信されます。  REST 要求にはこのヘッダーは含まれないため、代わりに、特殊な HTTP イベント ヘッダーが使用されます。  次のコード スニペットには、アクティビティ ID をプログラムで取得する方法が示されています。  
  
```vb  
  
Object output = null;                    
if (OperationContext.Current.IncomingMessageProperties.TryGetValue(HttpRequestMessageProperty.Name, out output))  
{  
   HttpRequestMessageProperty httpHeaders = output as HttpRequestMessageProperty;       
   // Retrieve the Activity Id from the HTTP header    string e2eId = httpHeaders.Headers["E2EActivity"];  
   // ...  
}  
  
```  
  
 次のコードを使用するとプログラムでヘッダーを追加できます。  
  
```csharp  
  
HttpContent content = new StreamContent(contentStream);  
Guid correlation = Guid.NewGuid();  
content.Headers.Add("E2EActivity", Convert.ToBase64String(correlation.ToByteArray()));  
  
```