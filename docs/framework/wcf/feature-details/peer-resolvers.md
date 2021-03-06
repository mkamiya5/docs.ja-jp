---
title: "ピア リゾルバー | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d86d12a1-7358-450f-9727-b6afb95adb9c
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# ピア リゾルバー
メッシュに接続するには、ピア ノードに他のノードの IP アドレスが必要です。  IP アドレスを取得するには、リゾルバー サービスにアクセスします。このサービスは、メッシュ ID を受け取り、そのメッシュ ID で登録されているノードに対応するアドレスの一覧を返します。  リゾルバーは登録されたアドレスのリストを保持します。そのリストには、メッシュ レジスタの各ノードとサービスが含まれます。  
  
 使用する PeerResolver サービスは、<xref:System.ServiceModel.NetPeerTcpBinding> の `Resolver` プロパティから指定できます。  
  
## サポートされるピア リゾルバー  
 ピア チャネルは、PNRP \(Peer Name Resolution Protocol\) サービスとカスタム リゾルバー サービスの 2 種類のリゾルバーをサポートします。  
  
 既定で、ピア チャネルは PNRP ピア リゾルバー サービスを使用して、メッシュ内のピアと近隣ノードを検出します。  PNRP が利用できない、または適切でない状況やプラットフォームでは、別の方法として、サーバー ベースの検索サービスである <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> が [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] に用意されています。  また、<xref:System.ServiceModel.PeerResolvers.IPeerResolverContract> インターフェイスを実装するクラスを書き込むと、カスタム リゾルバー サービスを明示的に定義することもできます。  
  
### PNRP \(Peer Name Resolution Protocol\)  
 PNRP \([!INCLUDE[wv](../../../../includes/wv-md.md)] の既定のリゾルバー\) は、分散型でサーバーを使用しない、名前のリゾルバー サービスです。  PNRP は、Advanced Networking Pack をインストールすれば [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] でも使用できます。  2 つのクライアントが同じバージョンの PNRP を実行している場合、特定の条件 \(途中に企業のファイアウォールが存在しないなどの条件\) を満たせば、このプロトコルを使用してお互いを検索できます。  [!INCLUDE[wv](../../../../includes/wv-md.md)] に付属する PNRP は、Advanced Networking Pack に含まれているバージョンよりも新しいバージョンです。  [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] 用の PNRP への更新については、Microsoft ダウンロード センターで確認してください。  
  
### カスタム リゾルバー サービス  
 PNRP サービスを利用できない場合、またはメッシュ形状を完全に制御する必要がある場合は、サーバー ベースのカスタム リゾルバー サービスを使用できます。  このサービスは、<xref:System.ServiceModel.PeerResolvers.IPeerResolverContract> インターフェイスを実装するリゾルバー クラスを記述するか、既定の受信トレイ実装 \(<xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>\) を使用することで、明示的に定義できます。  
  
 サービスの既定の実装では、クライアント登録は、クライアントが明示的に更新しない限り、特定の期間が経過した後に期限切れになります。  そこで、リゾルバー サービスを使用するクライアントは、登録を時間内に正常に更新するために、クライアントとサーバー間の待ち時間に上限の概念を設ける必要があります。  そのために、リゾルバー サービスに適切な更新タイムアウト \(`RefreshInterval`\) を選択します。  \(詳細については、「[CustomPeerResolverService 内部 : クライアント登録](../../../../docs/framework/wcf/feature-details/inside-the-custompeerresolverservice-client-registrations.md)」を参照してください\)。  
  
 アプリケーションを記述する際には、クライアントとカスタム リゾルバー サービス間の接続をセキュリティで保護することも考慮する必要があります。  これは、クライアントがリゾルバー サービスへのアクセスに使用する <xref:System.ServiceModel.NetTcpBinding> のセキュリティ設定を使用することで実現できます。  資格情報を使用する場合は、ピア チャネルの作成に使用する `ChannelFactory` で、それを指定する必要があります。  この資格情報は、カスタム リゾルバーへのチャネルの作成に使用される `ChannelFactory` に渡されます。  
  
> [!NOTE]
>  ローカル ネットワークや即席のネットワークでカスタム リゾルバーを使用するときは、リンク ローカル ネットワークまたは即席のネットワークを使用またはサポートするアプリケーションに、接続時に使用するリンク ローカル アドレスを 1 つだけ選択するロジックを含めることを強くお勧めします。  これにより、複数のリンク ローカル アドレスを持つコンピューターによって発生する可能性のある混乱をすべて回避できます。  このロジックに従って、ピア チャネルは、1 度に 1 つのリンク ローカル アドレスを使用することだけをサポートします。  このアドレスは、<xref:System.ServiceModel.NetPeerTcpBinding> の `ListenIpAddress` プロパティを使用して指定できます。  
  
 カスタム リゾルバーを実装する方法の例については、「[Peer Channel Custom Peer Resolver](http://msdn.microsoft.com/ja-jp/5b75a2bb-7ff1-4a14-abe7-3debf0537d23)」を参照してください。  
  
## このセクションの内容  
 [CustomPeerResolverService 内部 : クライアント登録](../../../../docs/framework/wcf/feature-details/inside-the-custompeerresolverservice-client-registrations.md)  
  
## 参照  
 [ピア チャネルの概要](../../../../docs/framework/wcf/feature-details/peer-channel-concepts.md)   
 [ピア チャネルのセキュリティ](../../../../docs/framework/wcf/feature-details/peer-channel-security.md)   
 [ピア チャネル アプリケーションの構築](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)