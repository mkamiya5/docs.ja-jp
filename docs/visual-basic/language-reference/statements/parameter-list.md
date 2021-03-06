---
title: "パラメーターの一覧 (Visual Basic) |Microsoft ドキュメント"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic code, procedures
- parameters, Visual Basic
- parameters, lists
- parameter lists
- Visual Basic code, parameter lists
- arguments [Visual Basic], Visual Basic
- procedures, parameter lists
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: abadaa8e035bfa4c92acc30ab633d6a7e958676c
ms.lasthandoff: 03/13/2017

---
# <a name="parameter-list-visual-basic"></a>パラメーターの一覧 (Visual Basic)
プロシージャが呼び出された場合に想定パラメーターを指定します。 複数のパラメーターは、コンマで区切られます。 1 つのパラメーターの構文を次に示します。  
  
## <a name="syntax"></a>構文  
  
```  
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]   
parametername[( )] [ As parametertype ] [ = defaultvalue ]  
```  
  
## <a name="parts"></a>指定項目  
 `attributelist`  
 省略可能です。 このパラメーターに適用される属性の一覧です。 囲む必要があります、[属性リスト](../../../visual-basic/language-reference/statements/attribute-list.md)山かっこで ("`<`「と」`>`") です。  
  
 `Optional`  
 省略可能です。 プロシージャが呼び出されたときに、このパラメーターは必要ないことを指定します。  
  
 `ByVal`  
 省略可能です。 プロシージャが置換または呼び出し元のコードで対応する引数の基になる変数の要素を再割り当てできませんを指定します。  
  
 `ByRef`  
 省略可能です。 いるプロシージャ要素を変更できます、基になる変数、呼び出し元コードに呼び出し元コード自体と同じよう指定します。  
  
 `ParamArray`  
 省略可能です。 パラメーター リストの最後のパラメーターが指定されたデータ型の要素の省略可能な配列であることを示します。 これには、呼び出し元のコードをプロシージャに任意の数の引数を渡すことができます。  
  
 `parametername`  
 必須です。 パラメーターを表すローカル変数の名前です。  
  
 `parametertype`  
 必要な場合`Option Strict`は`On`です。 パラメーターを表すローカル変数のデータ型。  
  
 `defaultvalue`  
 必要な`Optional`パラメーター。 パラメーターのデータ型に評価される定数または定数式です。 型の場合`Object`、クラス、インターフェイス、配列、または構造体では、既定値は、必ずまたは`Nothing`です。  
  
## <a name="remarks"></a>コメント  
 パラメーターはかっこで囲まれているし、コンマで区切っています。 パラメーターは、任意のデータ型で宣言することができます。 指定しない場合`parametertype`、既定値は`Object`です。  
  
 呼び出し元のコードはプロシージャを呼び出す際に渡して、*引数*各必須パラメーターにします。 詳細については、次を参照してください。[の相違点の間でパラメーターと引数](../../../visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md)します。  
  
 呼び出し元のコードは、各パラメーターに渡す引数は、呼び出し元のコード内の基になる要素へのポインターです。 この要素は場合*不変*(定数、リテラル、列挙体、または式)、すべてのコードを変更することはできません。 ある場合、*変数*要素 (宣言された変数、フィールド、プロパティ、配列の要素、または構造体の要素)、呼び出し元のコードで変更できます。 詳細については、次を参照してください。[変更間の相違点と変更できない引数](../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)します。  
  
 Variable 要素が渡された場合`ByRef`プロシージャが同様に変更できます。 詳細については、次を参照してください。[の相違点の間の値と参照渡しによって引数の渡し](../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)します。  
  
## <a name="rules"></a>ルール  
  
-   **かっこです。** パラメーター リストを指定する場合は、かっこで囲む必要があります。 パラメーターがない場合、空のリストを囲むかっこを使用することができます。 これにより、要素は、プロシージャを明確にすることによって、コードの読みやすさが向上します。  
  
-   **省略可能なパラメーターです。** 使用する場合、`Optional`パラメーターに対する修飾子は、一覧に続くすべてのパラメーターはオプションもありを使用して宣言する、`Optional`修飾子です。  
  
     すべての省略可能なパラメーター宣言を指定する必要があります、`defaultvalue`句。  
  
     詳細については、次を参照してください。[省略可能なパラメーター](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)します。  
  
-   **パラメーターの配列。** 指定する必要があります`ByVal`の`ParamArray`パラメーター。  
  
     両方を使用することはできません`Optional`と`ParamArray`同じパラメーター リストにします。  
  
     詳細については、次を参照してください。[パラメーター配列](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)します。  
  
-   **値渡し。** すべての引数に対して既定のメカニズムは`ByVal`プロシージャは基になる可変要素は変更できません。 ただし、要素が参照型の場合は、プロシージャが変更できます内容または基になるオブジェクトのメンバーでも置き換えることも、オブジェクト自体を再割り当てできません。  
  
-   **パラメーター名。** 次のパラメーターのデータ型が配列の場合は、`parametername`かっこの直後にします。 パラメーター名の詳細については、次を参照してください。[宣言された要素の名前](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)します。  
  
## <a name="example"></a>例  
 例を次に、 `Function`&2; つのパラメーターを定義するプロシージャです。  
  
 [!code-vb[VbVbalrStatements&#2;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/parameter-list_1.vb)]  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Runtime.InteropServices.DllImportAttribute></xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Function ステートメント](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub ステートメント](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare ステートメント](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Structure ステートメント](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Option Strict ステートメント](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [属性の概要](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [方法 : コード内でステートメントを分割および連結する](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
