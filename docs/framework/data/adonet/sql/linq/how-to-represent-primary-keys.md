---
title: "How to: Represent Primary Keys | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 63c65289-6539-42b2-8493-891c232018fa
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# How to: Represent Primary Keys
データベース列の主キーを表すプロパティまたはフィールドを指定するには、<xref:System.Data.Linq.Mapping.ColumnAttribute> 属性の [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> プロパティを使用します。  
  
 コード例については、「<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>」を参照してください。  
  
> [!NOTE]
>  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、計算列は主キーとしてサポートされません。  
  
### プロパティまたはフィールドを主キーとして指定するには  
  
1.  <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性に <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> プロパティを追加します。  
  
2.  値として `true` を指定します。  
  
## 参照  
 [The LINQ to SQL Object Model](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [How to: Customize Entity Classes by Using the Code Editor](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)