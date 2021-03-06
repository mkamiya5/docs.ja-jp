---
title: "方法 : メッセージ リプレイ検出を有効にする | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "リプレイ検出 [WCF]"
  - "WCF セキュリティ"
  - "WCF, カスタム バインディング"
  - "WCF, セキュリティ"
ms.assetid: 8b847e91-69a3-49e1-9e5f-0c455e50d804
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 方法 : メッセージ リプレイ検出を有効にする
リプレイ攻撃は、攻撃者がメッセージのストリームを 2 つのパーティ間でコピーし、そのストリームを他の 1 つ以上のパーティにリプレイすることで発生します。攻撃が止むまで、攻撃対象になったコンピューターはストリームを正当なメッセージとして処理しようとし、その結果、命令が重複するなど、望ましくない状況に陥ります。  
  
 メッセージ リプレイ検出[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、「[メッセージ リプレイ検出](http://go.microsoft.com/fwlink/?LinkId=88536)」を参照してください。  
  
 以下の手順では、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] でリプレイ検出を制御するために使用できるさまざまなプロパティを示します。  
  
### コードを使用してクライアントでのリプレイ検出を制御するには  
  
1.  <xref:System.ServiceModel.Channels.CustomBinding> で使用する <xref:System.ServiceModel.Channels.SecurityBindingElement> を作成します。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][方法 : SecurityBindingElement を使用してカスタム バインディングを作成する](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).次の例では、<xref:System.ServiceModel.Channels.SecurityBindingElement> クラスの <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> を使用して作成された <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> を使用します。  
  
2.  <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A> プロパティを使用して <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> クラスへの参照を返し、次のプロパティを適切な値に設定します。  
  
    1.  `DetectReplay`.ブール値。サーバーからのリプレイをクライアントが検出するかどうかを制御します。既定値は `true` です。  
  
    2.  `MaxClockSkew`.<xref:System.TimeSpan> 値。リプレイ機構に許容されるクライアントとサーバー間の時刻のずれを制御します。セキュリティ機構は送信されたメッセージのタイム スタンプを調べ、メッセージが古すぎるかどうかを決定します。既定値は 5 分です。  
  
    3.  `ReplayWindow`.`TimeSpan` 値。メッセージがサーバーによって送信されてから \(中継局を通過して\) クライアントに到達するまで、ネットワーク内に存在できる期間を制御します。クライアントは、リプレイ検出のため、最新の `ReplayWindow` 内で送信されたメッセージの署名を追跡します。  
  
    4.  `ReplayCacheSize`.整数値。クライアントは、メッセージの署名をキャッシュに格納します。この設定は、キャッシュに格納できる署名の数を指定します。最新のリプレイ ウィンドウ内の送信されたメッセージの数がキャッシュ制限に達すると、キャッシュされた最も古い署名が制限時間に達するまで、新しいメッセージは拒否されます。既定値は 500000 です。  
  
### コードを使用してサービスでのリプレイ検出を制御するには  
  
1.  <xref:System.ServiceModel.Channels.CustomBinding> で使用する <xref:System.ServiceModel.Channels.SecurityBindingElement> を作成します。  
  
2.  <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A> プロパティを使用して <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> クラスへの参照を返し、前述のように各プロパティを設定します。  
  
### クライアントまたはサービスの構成でリプレイ検出を制御するには  
  
1.  [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)を作成します。  
  
2.  `<security>` 要素を作成します。  
  
3.  [\<localClientSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)または [\<localServiceSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)を作成します。  
  
4.  `detectReplays`、`maxClockSkew`、`replayWindow`、および `replayCacheSize` の各属性値を適切に設定します。`<localServiceSettings>``<localClientSettings> 要素と`  要素の両方の属性を設定する例を次に示します。  
  
    ```  
    <customBinding>  
      <binding name="NewBinding0">  
       <textMessageEncoding />  
        <security>  
         <localClientSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
         <localServiceSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
        <secureConversationBootstrap />  
       </security>  
      <httpTransport />  
     </binding>  
    </customBinding>  
    ```  
  
## 使用例  
 次の例は、<xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> メソッドを使用して <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> を作成し、作成されたバインディングのリプレイ プロパティを設定します。  
  
 [!code-csharp[c_ReplayDetection#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_replaydetection/cs/source.cs#1)]
 [!code-vb[c_ReplayDetection#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_replaydetection/vb/source.vb#1)]  
  
## リプレイのスコープ : メッセージ セキュリティのみ  
 次の手順は、メッセージ セキュリティ モードにのみ適用されます。トランスポート モードとメッセージ資格情報付きトランスポート モードでは、トランスポート機構がリプレイを検出します。  
  
## セキュリティで保護されたメッセージ交換に関するメモ  
 セキュリティで保護されたメッセージ交換を有効にするバインディングでは、アプリケーション チャネルとセキュリティで保護されたメッセージ交換のブートストラップ バインディングの両方で、上記の設定を調整できます。たとえば、アプリケーション チャネルに対するリプレイを無効にして、セキュリティで保護されたメッセージ交換を確立するブートストラップ チャネルに対するリプレイを有効にできます。  
  
 セキュリティで保護されたメッセージ交換セッションを使用しない場合、サーバー ファームのシナリオでのリプレイや、プロセスをリサイクルしたときのリプレイについては、リプレイ検出による検出が保証されません。これは、次のシステム指定のバインディングに当てはまります。  
  
-   <xref:System.ServiceModel.BasicHttpBinding>.  
  
-   <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> プロパティが `false` に設定された <xref:System.ServiceModel.WSHttpBinding>。  
  
## コードのコンパイル  
  
-   コードのコンパイルには次の名前空間が必要です。  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
## 参照  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>   
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 [セキュリティ保護されたメッセージ交換とセッション](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)   
 [\<localClientSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)   
 [方法 : SecurityBindingElement を使用してカスタム バインディングを作成する](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)