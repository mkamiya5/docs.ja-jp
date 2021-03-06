---
title: "クエリ式の例外の処理"
description: "クエリ式の例外を処理する方法。"
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2bf0c397-13fb-4f68-bc2b-531c6c88a167
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: d13387c4468a5c89cbe838139c767f0f95ab418d
ms.contentlocale: ja-jp
ms.lasthandoff: 05/10/2017

---
# <a name="handle-exceptions-in-query-expressions"></a>クエリ式の例外の処理

クエリ式のコンテキストで任意のメソッドを呼び出すことができます。 ただし、データ ソースのコンテンツが変更されたり例外がスローされたりするなどの副作用が生じる可能性のあるクエリ式では、メソッドを呼び出さないようにすることをお勧めします。 この例では、クエリ式でメソッドを呼び出すときに、例外処理に関する .NET Framework の全般的なガイドラインに違反することなく例外の発生を避ける方法を示します。 ガイドラインでは、特定のコンテキストで特定の例外がスローされる理由がわかっているときにその例外をキャッチすることは認められています。 詳細については、「[例外の推奨事項](../../standard/exceptions/best-practices-for-exceptions.md)」を参照してください。  
  
 最後の例では、クエリの実行中に例外をスローする必要がある場合の処理方法を示します。  
  
## <a name="example"></a>例  

 次の例では、例外処理コードをクエリ式の外側に移動する方法を説明します。 この方法は、メソッドがクエリのローカル変数に依存しない場合にのみ可能です。  
  
 [!code-cs[csProgGuideLINQ#10](../../../samples/snippets/csharp/concepts/linq/how-to-handle-exceptions-in-query-expressions_1.cs)]  
  
## <a name="example"></a>例 

 場合によっては、クエリ内からスローされる例外に対する最適な応答は、クエリの実行をすぐに停止することです。 次の例では、クエリ本体の内部からスローされる例外を処理する方法を示します。 `SomeMethodThatMightThrow` で、クエリの実行を停止することが必要な例外が発生する可能性があるとします。  
  
 `try` ブロックは `foreach` ループを囲み、クエリ自体を囲むのではありません。 その理由は、`foreach` ループがクエリの実際の実行ポイントであるためです。 詳細については、「[LINQ クエリの概要](../programming-guide/concepts/linq/introduction-to-linq-queries.md)」を参照してください。  
  
 [!code-cs[csProgGuideLINQ#12](../../../samples/snippets/csharp/concepts/linq/how-to-handle-exceptions-in-query-expressions_2.cs)]  
  

## <a name="see-also"></a>関連項目  
 [LINQ クエリ式](index.md)

