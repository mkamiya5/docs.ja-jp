---
title: "方法 : コードを使用してサービスのメタデータを公開する | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 51407e6d-4d87-42d5-be7c-9887b8652006
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# 方法 : コードを使用してサービスのメタデータを公開する
これは、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] サービスのメタデータの公開方法を説明する 2 つの「方法」トピックの 1 つです。構成ファイルとコードを使用して、サービスがメタデータを公開する手段を指定する方法は 2 つあります。このトピックでは、コードを使用してサービスのメタデータを公開する方法について説明します。  
  
> [!CAUTION]
>  このトピックでは、セキュリティで保護されていない方法でメタデータを公開する方法について説明します。クライアントは、サービスからメタデータを取得できます。セキュリティで保護された方法でメタデータを公開するサービスが必要な場合は、[カスタム セキュア メタデータ エンドポイント](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md) を参照してください。  
  
 構成ファイル内の公開メタデータ[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、「[方法 : 構成ファイルを使用してサービスのメタデータを公開する](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)」を参照してください。メタデータを公開すると、クライアントが `?wsdl` クエリ文字列を使用した WS\-Transfer GET 要求または HTTP\/GET 要求によりメタデータを取得できるようになります。コードを機能させるには、基本的な WCF サービスを作成する必要があります。次のコードは基本的な自己ホスト型サービスの例です。  
  
 [!code-csharp[htPublishMetadataCode#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#0)]
 [!code-vb[htPublishMetadataCode#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#0)]  
  
### コードでメタデータを公開するには  
  
1.  コンソール アプリケーションのメイン メソッド内で、サービス型とベース アドレスを渡して <xref:System.ServiceModel.ServiceHost> オブジェクトをインスタンス化します。  
  
     [!code-csharp[htPublishMetadataCode#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#1)]
     [!code-vb[htPublishMetadataCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#1)]  
  
2.  手順 1. のコードのすぐ下に try ブロックを作成します。これにより、サービスの実行中にスローされる例外がすべてキャッチされます。  
  
     [!code-csharp[htPublishMetadataCode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#2)]
     [!code-vb[htPublishMetadataCode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#2)]  
  
     [!code-csharp[htPublishMetadataCode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#3)]
     [!code-vb[htPublishMetadataCode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#3)]  
  
3.  サービス ホストに <xref:System.ServiceModel.Description.ServiceMetadataBehavior> が含まれているかどうかを確認し、含まれていない場合は、新しい <xref:System.ServiceModel.Description.ServiceMetadataBehavior> インスタンスを作成します。  
  
     [!code-csharp[htPublishMetadataCode#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#4)]
     [!code-vb[htPublishMetadataCode#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#4)]  
  
4.  <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> プロパティを `true.` に設定します。  
  
     [!code-csharp[htPublishMetadataCode#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#5)]
     [!code-vb[htPublishMetadataCode#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#5)]  
  
5.  <xref:System.ServiceModel.Description.ServiceMetadataBehavior> には <xref:System.ServiceModel.Description.MetadataExporter> プロパティが含まれています。<xref:System.ServiceModel.Description.MetadataExporter> には <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> プロパティが含まれています。<xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> プロパティの値を <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> に設定します。<xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> プロパティを <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A> に設定することもできます。<xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> に設定すると、WS\-Policy 1.5 に準拠したメタデータでポリシー情報がメタデータ エクスポーターによって生成されます。<xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A> に設定すると、WS\-Policy 1.2 に準拠したポリシー情報がメタデータ エクスポーターによって生成されます。  
  
     [!code-csharp[htPublishMetadataCode#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#6)]
     [!code-vb[htPublishMetadataCode#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#6)]  
  
6.  <xref:System.ServiceModel.Description.ServiceMetadataBehavior> インスタンスをサービス ホストの動作コレクションに追加します。  
  
     [!code-csharp[htPublishMetadataCode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#7)]
     [!code-vb[htPublishMetadataCode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#7)]  
  
7.  メタデータ交換エンドポイントをサービス ホストに追加します。  
  
     [!code-csharp[htPublishMetadataCode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#8)]
     [!code-vb[htPublishMetadataCode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#8)]  
  
8.  アプリケーション エンドポイントをサービス ホストに追加します。  
  
     [!code-csharp[htPublishMetadataCode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#9)]
     [!code-vb[htPublishMetadataCode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#9)]  
  
    > [!NOTE]
    >  エンドポイントをサービスに追加しない場合、ランタイムによって既定のエンドポイントが追加されます。この例では、サービスには `true` に設定された <xref:System.ServiceModel.Description.ServiceMetadataBehavior> があるので、サービスで公開メタデータも有効化されています。既定のエンドポイント[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、「[簡略化された構成](../../../../docs/framework/wcf/simplified-configuration.md)」および「[WCF サービスの簡略化された構成](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)」を参照してください。  
  
9. サービス ホストを開き、受信呼び出しを待ちます。ユーザーが Enter キーを押すと、サービス ホストが終了します。  
  
     [!code-csharp[htPublishMetadataCode#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#10)]
     [!code-vb[htPublishMetadataCode#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#10)]  
  
10. コンソール アプリケーションのビルドと実行  
  
11. Internet Explorer を使用してサービスのベース アドレス \(この例では、http:\/\/localhost:8001\/MetadataSample\) を参照し、メタデータの公開が有効になっていることを確認します。上部の "サービスを作成しました" のすぐ下に "Simple Service" と表示された Web ページが表示されます。有効になっていない場合は、"このサービスのメタデータ公開は現在は無効になっています。" というメッセージが結果ページの上部に表示されます。  
  
## 使用例  
 次のコード例は、コードを使用してサービスのメタデータを公開する基本的な [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] サービスの実装を示しています。  
  
 [!code-csharp[htPublishMetadataCode#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#11)]
 [!code-vb[htPublishMetadataCode#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#11)]  
  
## 参照  
 [方法 : マネージ アプリケーションで WCF サービスをホストする](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)   
 [自己ホスト](../../../../docs/framework/wcf/samples/self-host.md)   
 [メタデータ アーキテクチャの概要](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)   
 [メタデータを使用する](../../../../docs/framework/wcf/feature-details/using-metadata.md)   
 [方法 : 構成ファイルを使用してサービスのメタデータを公開する](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)