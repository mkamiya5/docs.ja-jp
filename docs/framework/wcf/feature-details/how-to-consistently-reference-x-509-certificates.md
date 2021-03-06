---
title: "方法 : 一貫性を保って X.509 証明書を参照する | Microsoft Docs"
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
  - "証明書 [WCF], X.509 証明書の参照"
ms.assetid: a6de1c63-e450-4640-ad08-ad7302dbfbfc
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 方法 : 一貫性を保って X.509 証明書を参照する
証明書を識別する方法には、証明書のハッシュを使用する方法、発行者とシリアル番号を使用する方法、またはサブジェクト キー識別子 \(SKI\) を使用する方法があります。SKI を使用すると、証明書のサブジェクト公開キーを一意に識別できます。SKI は、XML デジタル署名を処理する場合によく使用されます。SKI の値は、通常、*X.509 証明書の拡張*として X.509 証明書の一部を構成します。SKI 拡張が証明書に見つからない場合、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] は、発行者とシリアル番号を使用する既定の*参照スタイル*を使用します。証明書に SKI 拡張が含まれる場合、既定の参照スタイルは SKI を使用してその証明書を識別します。アプリケーションの開発中に、SKI 拡張を使用しない証明書から SKI 拡張を使用する証明書に切り替えた場合、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] が生成するメッセージに使用される参照スタイルも変更されます。  
  
 SKI 拡張が存在するかどうかに関係なく、一貫性のある参照スタイルが必要な場合は、次のコードに示されているような参照スタイルを構成できます。  
  
## 使用例  
 次の例では、1 つの一貫した参照スタイル \(ユーザー名とシリアル番号\) を使用するカスタム セキュリティ バインド要素を作成します。  
  
 [!code-csharp[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_referencingcertificatesconsistently/cs/source.cs#1)]
 [!code-vb[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_referencingcertificatesconsistently/vb/source.vb#1)]  
  
## コードのコンパイル  
 次の名前空間は以下のコードのコンパイルに必要です。  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
-   <xref:System.ServiceModel.Security.Tokens>  
  
## 参照  
 [証明書の使用](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)