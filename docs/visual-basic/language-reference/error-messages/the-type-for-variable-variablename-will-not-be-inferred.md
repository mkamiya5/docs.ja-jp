---
title: "変数の型 &quot;&lt;variablename&gt;&quot; は、外側のスコープ内のフィールドにバインドされているので、推論できません |。Microsoft ドキュメント"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42110
- bc42110
dev_langs:
- VB
helpviewer_keywords:
- BC42110
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
caps.latest.revision: 33
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ab7d69c34a58dc898553868258c4fdf6b81db343
ms.contentlocale: ja-jp
ms.lasthandoff: 03/13/2017

---
# <a name="the-type-for-variable-39ltvariablenamegt39-will-not-be-inferred-because-it-is-bound-to-a-field-in-an-enclosing-scope"></a>変数の型 '&lt;variablename&gt;' は、外側のスコープ内のフィールドにバインドされているので、推論できません。
変数の型 '\<variablename >' は、外側のスコープ内のフィールドにバインドされているので、推論できません。 名前を変更するか '\<variablename >'、または完全修飾名 (:"Me.variablename"や"MyBase.variablename") を使用します。  
  
 コードのループ制御変数は、クラスまたは他の外側のスコープ内のフィールドと同じ名前を持っています。 制御変数は、`As` 句なしで使用されるため、外側のスコープ内のフィールドにバインドされ、コンパイラがこれに対して新しい変数を作成したり、その型を推論したりすることはありません。  
  
 次の例では、`Index` (`For` ステートメントの制御変数) が、`Index` クラスの `Customer` フィールドにバインドされています。 コンパイラが制御変数 `Index` に対して新しい変数を作成したり、その型を推論したりすることはありません。  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
    ' The following line will raise this warning.  
        For Index = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
```  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法または警告をエラーとして処理する方法については、次を参照してください。 [Visual Basic での警告の構成](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)します。  
  
 **エラー ID:** BC42110  
  
### <a name="to-address-this-warning"></a>この警告に対処するには  
  
-   ループ制御変数の名前を、クラスのフィールドの名前とは異なる識別子に変更して、この変数をローカルにします。  
  
    ```  
    For I = 1 To 10  
    ```  
  
-   変数名の前に `Me.` を付けることにより、クラス フィールドにループ制御変数がバインドされていることを明確にします。  
  
    ```  
    For Me.Index = 1 To 10  
    ```  
  
-   ローカル型の推定ではなく `As` 句を使用して、ループ制御変数に型を指定します。  
  
    ```  
    For Index As Integer = 1 To 10  
    ```  
  
## <a name="example"></a>例  
 次のコードは、上の例に最初の修正を行ったものです。  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
        For I = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
```  
  
## <a name="see-also"></a>関連項目  
 [Option Infer ステートメント](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [各.次のステートメント](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [.次のステートメント](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [方法: オブジェクトの現在のインスタンスを参照してください](../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [ローカル型推論](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Me、My、MyBase、および MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)

