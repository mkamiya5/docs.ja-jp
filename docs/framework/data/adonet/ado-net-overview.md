---
title: "ADO.NET の概要 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee3bc1d8-11db-4be4-89eb-c708cf04117d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# ADO.NET の概要
ADO.NET は、SQL Server や XML などのデータ ソースや、OLE DB や ODBC 経由で公開されるデータ ソースに対する一貫性を持ったアクセス機能を実現します。  データを共有する消費者向けアプリケーションで ADO.NET を使用することで、そのようなデータ ソースへの接続や、データ ソースに格納されているデータの取得、操作、更新を実行できます。  
  
 ADO.NET は、データ操作の中からデータ アクセス機能を分離し、個別にまたは組み合わせて使用できる、独立したコンポーネントへと分解します。  ADO.NET には、データベースとの接続、コマンドの実行、および結果の取得を行うための .NET Framework データ プロバイダーが含まれます。  この結果は直接処理され、ADO.NET <xref:System.Data.DataSet> オブジェクトに格納されます。この結果は、ユーザーに暫定的に公開したり、複数のソースからのデータと組み合わせたり、層間で受け渡したりするために使用されます。  `DataSet` オブジェクトを .NET Framework データ プロバイダーに関係なく使用した場合でも、アプリケーションにとってローカルなデータや XML から提供されたデータを管理できます。  
  
 ADO.NET クラスは System.Data.dll にあり、System.Xml.dll に含まれている XML クラスに統合されています。  データベースに接続してデータを取得した後、そのデータをコンソール ウィンドウに表示するサンプル コードについては、「[ADO.NET のコード例](../../../../docs/framework/data/adonet/ado-net-code-examples.md)」を参照してください。  
  
 マネージ コードを作成する開発者は、ADO.NET により、ネイティブのコンポーネント オブジェクト モデル \(COM\) 開発者が ActiveX Data Object \(ADO\) によって利用できる機能と同等の機能を利用できます。  .NET アプリケーションでのデータのアクセスには、ADO ではなく ADO.NET を使用することをお勧めします。  
  
 ADO.NET は、.NET Framework におけるデータ アクセスの最も直接的な方法を提供します。  基になるストレージ モデルではなく概念モデルをアプリケーションで使用できるようにするための高度な抽象化については、「[ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md)」を参照してください。  
  
 **プライバシーに関する声明** : System.Data.dll、System.Data.Design.dll、System.Data.OracleClient.dll、System.Data.SqlXml.dll、System.Data.Linq.dll、System.Data.SqlServerCe.dll、System.Data.DataSetExtensions.dll の各アセンブリでは、ユーザーの個人データとそれ以外のデータが区別されません。  これらのアセンブリによって、ユーザーの個人データの収集、格納、送信が実行されることはありません。  ただし、サードパーティ製のアプリケーションでこれらのアセンブリが使用され、ユーザーの個人データの収集、格納、送信が行われる可能性はあります。  
  
## このセクションの内容  
 [ADO.NET のアーキテクチャ](../../../../docs/framework/data/adonet/ado-net-architecture.md)  
 ADO.NET のアーキテクチャとコンポーネントの概要を説明します。  
  
 [ADO.NET テクノロジのオプションとガイドライン](../../../../docs/framework/data/adonet/ado-net-technology-options-and-guidelines.md)  
 エンティティ データ プラットフォームに含まれている製品とテクノロジを説明します。  
  
 [LINQ と ADO.NET](../../../../docs/framework/data/adonet/linq-and-ado-net.md)  
 ADO.NET での統合言語クエリ \(LINQ\) の実装方法を説明し、関連項目へのリンクを示します。  
  
 [.NET Framework データ プロバイダー](../../../../docs/framework/data/adonet/data-providers.md)  
 .NET Framework データ プロバイダーと、ADO.NET に同梱される .NET Framework データ プロバイダーのデザインの概要を説明します。  
  
 [ADO.NET の DataSet](../../../../docs/framework/data/adonet/ado-net-datasets.md)  
 `DataSet` のデザインとコンポーネントの概要を説明します。  
  
 [ADO.NET での side\-by\-side 実行](../../../../docs/framework/data/adonet/side-by-side-execution.md)  
 ADO.NET のバージョン間の相違と、その相違が side\-by\-side 実行とアプリケーションの互換性に及ぼす影響について説明します。  
  
 [ADO.NET のコード例](../../../../docs/framework/data/adonet/ado-net-code-examples.md)  
 ADO.NET データ プロバイダーを使用してデータを取得するコード サンプルです。  
  
## 関連項目  
 [ADO.NET の新機能](../../../../docs/framework/data/adonet/whats-new.md)  
 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] の新機能について説明します。  
  
 [ADO.NET アプリケーションのセキュリティ保護](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 ADO.NET を使用する場合の安全なコーディング方法について説明します。  
  
 [ADO.NET でのデータ型のマッピング](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)  
 .NET Framework データ型と .NET Framework データ プロバイダーとの間のデータ型のマッピングについて説明します。  
  
 [ADO.NET でのデータの取得および変更](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 データ ソースへの接続、データの取得、データの変更の方法について説明します。  これには、`DataReaders` と `DataAdapters` が含まれます。  
  
## 参照  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [Visual Studio でのデータへのアクセス](../Topic/Accessing%20data%20in%20Visual%20Studio.md)   
 [ADO.NET Managed Providers and DataSet Developer Center \(ADO.NET マネージ プロバイダーと DataSet デベロッパー センター\)](http://go.microsoft.com/fwlink/?LinkId=217917)