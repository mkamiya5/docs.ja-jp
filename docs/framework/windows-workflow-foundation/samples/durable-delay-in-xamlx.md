---
title: "XAMLX における永続的な遅延 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efc38df4-2d34-453c-8e59-2c21d1307354
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# XAMLX における永続的な遅延
このサンプルでは、永続的な遅延を使用する方法を示します。これは、遅延の間、ワークフローを永続的なデバイスに永続化する遅延のことです。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Services\DurableDelayXamlx`  
  
## 説明  
 このサンプル ワークフローには、遅延によって分割された 2 つのローカル ファイルへのメッセージが含まれています。遅延が発生すると、ワークフローがアンロードされ、ワークフローはメモリに再読み込みされるまでワークフロー インスタンス ストアで 5 秒間待機します。  
  
 この .xamlx ファイルは、[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] でホストされているワークフロー サービスです。[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] は、ワークフロー サービス ホストを使用する Cassini を使用して、ワークフローをホストします。  
  
 ワークフロー サービス ホストは、ワークフローをホストするだけでなく、読み込みとアンロードを行うことによってワークフロー インスタンスを管理します。ワークフロー サービス ホストで [!INCLUDE[wf](../../../../includes/wf-md.md)] 定義のインスタンスを開始するには、ワークフローの <xref:System.ServiceModel.Activities.Receive> アクティビティにメッセージを送信するクライアントを設定します。この <xref:System.ServiceModel.Activities.Receive> は、<xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> プロパティが `true` に設定されているため、メッセージを受信した後にワークフローの新しいインスタンスを作成できます。  
  
 初期化中に、ワークフロー サービス ホストに対してインスタンスを永続化ストア \(データベース\) にアンロードするように指定する、インスタンスのアンロード動作が構成ファイルに追加されます。このサンプルでは、\(遅延が発生して\) ワークフローがアイドル状態になった直後にインスタンスがアンロードされます。  
  
#### このサンプルを使用するには  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] コマンド プロンプトを開きます。  
  
2.  DurableDelayXamlx\\CS フォルダーに移動します。  
  
3.  Setup.cmd を実行します。  
  
4.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] を管理者として実行します。  
  
5.  DurableDelayXamlx.sln ソリューション ファイルを開きます。  
  
6.  **ソリューション エクスプローラー**で、ソリューションを右クリックし、**\[プロパティ\]** をクリックします。  
  
7.  **\[マルチ スタートアップ プロジェクト\]** を選択し、両方のプロジェクトを **\[開始\]** に設定します。  
  
8.  ソリューションをビルドするには、Ctrl キーと Shift キーを押しながら B キーを押します。  
  
9. ソリューションを実行するには、Ctrl キーを押しながら F5 キーを押します。  
  
#### このサンプルをアンインストールするには  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] コマンド プロンプトを開きます。  
  
2.  DurableDelayXamlx\\CS フォルダーに移動します。  
  
3.  Cleanup.cmd を実行します。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Services\DurableDelayXamlX`