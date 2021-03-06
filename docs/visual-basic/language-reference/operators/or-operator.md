---
title: "Or 演算子 (Visual Basic) |Microsoft ドキュメント"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Or
dev_langs:
- VB
helpviewer_keywords:
- Or operator
- operators [Visual Basic], bitwise
- inclusive Or operator
- bitwise operators, OR operator
- Or keyword
- operators [Visual Basic], inclusive or
- operators [Visual Basic], disjunction
- bitwise comparison
- logical disjunction
- disjunction operator
ms.assetid: 41ed6905-bf3d-468a-9e3b-03c10d461891
caps.latest.revision: 12
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f3f6c013df6cd5c3b99e465bdc8bb0b4ead6bdf4
ms.contentlocale: ja-jp
ms.lasthandoff: 03/13/2017

---
# <a name="or-operator-visual-basic"></a>Or 演算子 (Visual Basic)
2 つの論理和を実行`Boolean`式、または&2; つの数値式に対してビット単位の論理和。  
  
## <a name="syntax"></a>構文  
  
```  
result = expression1 Or expression2  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 どの`Boolean`または数値式です。 `Boolean`比較については、`result`は&2; つの包括的論理和`Boolean`値。 ビットごとの演算`result`は&2; つの数値のビット パターンの包括的論理和を表す数値を指定します。  
  
 `expression1`  
 必須です。 どの`Boolean`または数値式です。  
  
 `expression2`  
 必須です。 どの`Boolean`または数値式です。  
  
## <a name="remarks"></a>コメント  
 `Boolean`比較については、`result`は`False`場合にのみ、両方`expression1`と`expression2`に評価される`False`します。 次の表に示す方法`result`決定されます。  
  
|If `expression1` is|`expression2`は|値`result`は|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
>  `Boolean` 、比較、`Or`演算子では、両方の式では、プロシージャの呼び出しを含めることが常に評価されます。 [OrElse 演算子](../../../visual-basic/language-reference/operators/orelse-operator.md)実行*ショート サーキット*、いる場合は`expression1`は`True`、し`expression2`は評価されません。  
  
 ビットごとの演算、`Or`演算子が&2; つの数値式の同じ位置にビットのビットごとの比較を実行し、対応するでビットを設定`result`次の表に従ってします。  
  
|場合にビット`expression1`は|でビット`expression2`は|内のビット`result`は|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|1|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
>  論理/ビット処理演算子は、他の算術演算子や関係演算子より優先順位が低いため、ビットごとの演算を正確に実行されるようにかっこで囲む必要があります。  
  
## <a name="data-types"></a>データ型  
 1 つのオペランドで構成される場合`Boolean`式と 1 つの数値式では、Visual Basic に変換します、`Boolean`数値を指定する式 (– 1`True`および 0 を`False`) し、ビットごとの演算を実行します。  
  
 `Boolean`比較については、結果のデータ型は`Boolean`です。 ビットごとの比較結果のデータ型は、数値型のデータ型に適した`expression1`と`expression2`です。 「リレーショナルとビットごとの比較」表を参照して[データ型の演算子の結果](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)します。  
  
## <a name="overloading"></a>オーバーロード  
 `Or`演算子を指定できます*オーバー ロードされた*、つまり、クラスまたは構造体を再定義できます動作オペランドは、そのクラスまたは構造体の型を持つ場合です。 コードは、このようなクラスまたは構造体で、この演算子を使用する場合は、再定義される動作を確認ください。 詳細については、次を参照してください。[演算子プロシージャ](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)します。  
  
## <a name="example"></a>例  
 次の例では、`Or`オペレーターが&2; つの式の包括的論理和を実行します。 結果は、`Boolean`を表す値が&2; つの式のいずれかのかどうか`True`します。  
  
 [!code-vb[VbVbalrOperators&#35;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/or-operator_1.vb)]  
  
 前の例の結果を生成する`True`、 `True`、および`False`、それぞれします。  
  
## <a name="example"></a>例  
 次の例では、`Or`オペレーターが&2; つの数値式のビットごとの包括的論理和を実行します。 結果パターン内のビットは、オペランドの対応するビットのいずれか 1 に設定されている場合に設定されます。  
  
 [!code-vb[VbVbalrOperators&#36;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/or-operator_2.vb)]  
  
 前の例では、それぞれ 10、14 日、14 の結果を生成します。  
  
## <a name="see-also"></a>関連項目  
 [論理/ビット演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Visual Basic の演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [OrElse 演算子](../../../visual-basic/language-reference/operators/orelse-operator.md)   
 [Visual Basic での論理/ビット処理演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)

