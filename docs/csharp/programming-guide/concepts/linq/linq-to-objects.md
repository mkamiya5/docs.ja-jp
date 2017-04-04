---
title: LINQ to Objects (C#) | Microsoft Docs
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
ms.assetid: c5c2c178-3529-4f6c-b3df-2d5267af7f22
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 33402b552672fa79925fd1264444f39b19c02cd9
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-objects-c"></a>LINQ to Objects (C#)
"LINQ to Objects" という用語は、[LINQ to SQL](https://msdn.microsoft.com/library/bb386976) や [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13) などの中間 LINQ プロバイダーや API を使用せず、任意の <xref:System.Collections.IEnumerable> コレクションまたは <xref:System.Collections.Generic.IEnumerable%601> コレクションを直接使用して、LINQ クエリを実行することを意味します。 LINQ を使用すると、<xref:System.Collections.Generic.List%601>、<xref:System.Array>、<xref:System.Collections.Generic.Dictionary%602> などの列挙可能なコレクションを照会できます。 このコレクションは、ユーザー定義のコレクションでも、.NET Framework API から返されたコレクションでもかまいません。  
  
 本質的に、LINQ to Objects は、コレクションを扱うための新しい方法です。 従来の方法では、複雑な `foreach` ループを記述して、コレクションからデータを取得する方法を指定する必要がありました。 LINQ を使用する場合は、何を取得するかを表す宣言コードを記述します。  
  
 また、LINQ クエリには、従来の `foreach` ループと比べて、次の 3 つの重要な利点があります。  
  
1.  簡潔で読みやすい (特に複数の条件をフィルター処理する場合)。  
  
2.  強力なフィルター処理、並べ替え、およびグループ化機能を最小限のアプリケーション コードで実現できる。  
  
3.  ほとんど、またはまったく変更せずに、他のデータ ソースに移植できる。  
  
 通常、データに対して実行する操作が複雑なほど、従来の反復処理手法の代わりに LINQ を使用する利便性が高くなります。  
  
 このセクションでは、いくつか例を挙げながら、LINQ を使った方法を具体的に説明します。 ただし、すべてを網羅したものではありません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [LINQ と文字列 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)  
 LINQ を使用して、文字列および文字列のコレクションの照会と変換を行う方法について説明します。 これらの基本原則を具体的に示すトピックへのリンクも含まれます。  
  
 [LINQ とリフレクション (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-reflection.md)  
 LINQ でリフレクションを使用する方法を示すサンプルへのリンクを示します。  
  
 [LINQ とファイル ディレクトリ (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)  
 LINQ を使用して、ファイル システムとやり取りする方法について説明します。 これらの概念を具体的に示すトピックへのリンクも含まれます。  
  
 [方法: LINQ を使用して ArrayList を照会する (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)  
 C# で ArrayList を照会する方法を示します。  
  
 [方法: LINQ クエリのカスタム メソッドを追加する (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)  
 <xref:System.Collections.Generic.IEnumerable%601> インターフェイスに拡張メソッドを追加して、LINQ クエリに使用できるメソッド セットを拡張する方法について説明します。  
  
 [統合言語クエリ (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)  
 LINQ について説明しているトピックへのリンクと、クエリを実行するコードの例を示します。