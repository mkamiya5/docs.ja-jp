---
title: "XPath ユーザー向けの LINQ to XML (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 91774511-1dca-4f06-ac0b-913746f104fe
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 4d350826d23e31463666ee4bd861867b6c40eb55
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-xml-for-xpath-users-c"></a>XPath ユーザー向けの LINQ to XML (C#)
次に示す一連のトピックでは、さまざまな XPath 式、およびそれらに関連する [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の式について説明します。  
  
 拡張メソッドによって [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] で使用可能になる <xref:System.Xml.XPath.Extensions?displayProperty=fullName> の XPath 機能をすべての例で使用します。 各例では、XPath 式と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 式の両方を実行します。 次に、両方のクエリの結果を比較して、XPath 式と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] クエリが機能的に等価であることを検証します。 両方の種類のクエリは同じ XML ツリーからノードを返すため、クエリ結果は参照 ID を使用して比較されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[XPath と LINQ to XML の比較](../../../../csharp/programming-guide/concepts/linq/comparison-of-xpath-and-linq-to-xml.md)|XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の類似点および相違点についての概要を説明します。|  
|[方法: 子要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-child-element-xpath-linq-to-xml.md)|XPath の子要素軸と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の <xref:System.Xml.Linq.XContainer.Element%2A> メソッドを比較します。<br /><br /> 関連する XPath 式は `"DeliveryNotes"` です。|  
|[方法: 子要素の一覧を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-list-of-child-elements-xpath-linq-to-xml.md)|XPath の子要素軸と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の <xref:System.Xml.Linq.XContainer.Elements%2A> 軸を比較します。<br /><br /> 関連する XPath 式は `"./*"` です。|  
|[方法: ルート要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-the-root-element-xpath-linq-to-xml.md)|ルート要素を取得する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"/PurchaseOrders"` です。|  
|[方法: 子孫要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-descendant-elements-xpath-linq-to-xml.md)|特定の名前を持つ子孫要素を取得する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"//Name"` です。|  
|[方法: 属性をフィルター処理する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-filter-on-an-attribute-xpath-linq-to-xml.md)|指定した名前を持ち、かつ指定した値の属性を持つ子孫要素を取得する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `".//Address[@Type='Shipping']"` です。|  
|[方法: 関連要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-related-elements-xpath-linq-to-xml.md)|別の要素の値によって参照される属性に基づいて要素を取得する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `".//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]"` です。|  
|[方法: 名前空間内の要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-elements-in-a-namespace-xpath-linq-to-xml.md)|XML 名前空間の操作について、XPath の <xref:System.Xml.XmlNamespaceManager> クラスを使用する方法と、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の <xref:System.Xml.Linq.XName> クラスの <xref:System.Xml.Linq.XName.Namespace%2A> プロパティを使用する方法を比較します。<br /><br /> 関連する XPath 式は `"./aw:*"` です。|  
|[方法: 先行する兄弟を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-preceding-siblings-xpath-linq-to-xml.md)|XPath の `preceding-sibling` 軸と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の子 <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName> 軸を比較します。<br /><br /> 関連する XPath 式は `"preceding-sibling::*"` です。|  
|[方法: 子要素の子孫を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-descendants-of-a-child-element-xpath-linq-to-xml.md)|特定の名前を持つ子要素の子孫要素を取得する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"./Paragraph//Text/text()"` です。|  
|[方法: 2 つのロケーション パスの和集合を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-union-of-two-location-paths-xpath-linq-to-xml.md)|XPath の UNION 演算子 `&#124;` と <xref:System.Linq.Enumerable.Concat%2A> の [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 標準クエリ演算子を比較します。<br /><br /> 関連する XPath 式は `"//Category&#124;//Price"` です。|  
|[方法: 兄弟ノードを検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-sibling-nodes-xpath-linq-to-xml.md)|特定の名前を持つノードのすべての兄弟を検索する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"../Book"` です。|  
|[方法: 親の属性を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-an-attribute-of-the-parent-xpath-linq-to-xml.md)|親要素に移動してその属性を検索する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"../@id"` です。|  
|[方法: 特定の名前を持つ兄弟の属性を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-attributes-of-siblings-with-a-specific-name-xpath-linq-to-xml.md)|コンテキスト ノードの兄弟に関する特定の属性を検索する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"``../Book/@id``"` です。|  
|[方法: 特定の属性を持つ要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-elements-with-a-specific-attribute-xpath-linq-to-xml.md)|特定の属性を持つすべての要素を検索する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"./*[@Select]"` です。|  
|[方法: 位置に基づいて子要素を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-child-elements-based-on-position-xpath-linq-to-xml.md)|相対的位置に基づいて要素を検索する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"Test[position() >= 2 and position() <= 4]"` です。|  
|[方法: 直前の兄弟を検索する (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml.md)|ノードの直前の兄弟を検索する方法を、XPath と [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の間で比較します。<br /><br /> 関連する XPath 式は `"preceding-sibling::*[1]"` です。|  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Xml.XPath?displayProperty=fullName>   
 [XML ツリーのクエリ (C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md)   
 [XPath データ モデルを使用した XML データの処理](../../../../standard/data/xml/process-xml-data-using-the-xpath-data-model.md)

