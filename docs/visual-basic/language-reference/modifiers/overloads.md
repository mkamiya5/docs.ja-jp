---
title: "Overloads (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Overloads"
  - "Overloads"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Overloads keyword"
  - "hiding by signature"
  - "Shadows keyword"
  - "signature, hiding by"
ms.assetid: 0c6820b8-25b2-4664-bc59-5ca93c99c042
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Overloads (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

プロパティまたはプロシージャが、同じ名前の 1 つ以上の既存のプロパティまたはプロシージャを再度宣言することを示します。  
  
## 解説  
 *オーバーロード*とは、特定のプロパティ名またはプロシージャ名に対し、同じスコープ内で複数の定義を与えることです。  異なるシグネチャでプロパティまたはプロシージャを再度宣言することは、*シグネチャによる隠ぺい*とも呼ばれます。  
  
## 規則  
  
-   **宣言コンテキスト。** `Overloads` は、プロパティまたはプロシージャの宣言ステートメントでのみ使用できます。  
  
-   **結合された修飾子。** 同じプロシージャ宣言内で `Overloads` を [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md) と共に指定することはできません。  
  
-   **必要な相違点。** この宣言内の*シグネチャ*は、オーバーロードされるすべてのプロパティまたはプロシージャのシグネチャとは異なる必要があります。  シグネチャは、プロパティまたはプロシージャの名前と以下の項目で構成されます。  
  
    -   パラメーターの数  
  
    -   パラメーターの順序  
  
    -   パラメーターのデータ型  
  
    -   型パラメーターの数 \(ジェネリック プロシージャの場合\)  
  
    -   戻り値の型 \(変換演算子プロシージャの場合のみ\)  
  
     すべてのオーバーロードを同じ名前にする必要はありますが、各オーバーロードは、前の項目の 1 つ以上において他のすべてのオーバーロードと異なっている必要があります。  これにより、コンパイラは、コードでプロパティまたはプロシージャが呼び出すときに使用するバージョンを区別できます。  
  
-   **許可されない相違点。** 以下の項目はシグネチャに含まれないため、これらの項目の 1 つ以上を変更しても、プロパティまたはプロシージャのオーバーロードには有効ではありません。  
  
    -   値を返すかどうか \(プロシージャの場合\)  
  
    -   戻り値のデータ型 \(変換演算子を除く\)  
  
    -   パラメーターまたは型パラメーターの名前  
  
    -   型パラメーターに対する制約 \(ジェネリック プロシージャの場合\)  
  
    -   パラメーター修飾子キーワード \(`ByRef` や `Optional` など\)  
  
    -   プロパティまたはプロシージャ修飾子キーワード \(`Public` や `Shared` など\)  
  
-   **省略可能な修飾子。** 同じクラス内でオーバーロードされるプロパティまたはプロシージャを複数定義する場合、`Overloads` 修飾子を使用する必要はありません。  ただし、宣言の 1 つで `Overloads` を使用した場合は、すべての宣言で Overloads を使用する必要があります。  
  
-   **シャドウとオーバーロード。** `Overloads` は、基底クラスで既存のメンバーや一連のオーバーロードされたメンバーをシャドウする場合にも使用できます。  この方法で `Overloads` を使用する場合は、基底クラスのメンバーと同じ名前とパラメーター リストを使用してプロパティまたはメソッドを宣言し、`Shadows` キーワードは指定しません。  
  
 `Overrides` を使用する場合は、ライブラリ API と C\# が連携しやすくなるように、コンパイラが暗黙的に `Overloads` を追加します。  
  
 `Overloads` 修飾子は、次のコンテキストで使用できます。  
  
 [Function ステートメント](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property ステートメント](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub ステートメント](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 参照  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Procedure Overloading](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Visual Basic におけるジェネリック型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define a Conversion Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)