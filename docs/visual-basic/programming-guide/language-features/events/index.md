---
title: "イベント (Visual Basic)"
ms.custom: 
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
- events [Visual Basic], about events
- events [Visual Basic]
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 84f8385e1b2f16c4bcfa53ef2c77e1f0cf61e5e3
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="events-visual-basic"></a>イベント (Visual Basic)
[!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] プロジェクトとは、順に実行される一連のプロシージャと思っているかもしれませんが、実際には、ほとんどのプログラムはイベント ドリブン型です。つまり、実行の流れは、外部で発生する "*イベント*" と呼ばれる事象によって決まります。  
  
 イベントは、何らかの重要な出来事が発生したことをアプリケーションに通知するシグナルです。 たとえば、ユーザーがフォーム上のコントロールをクリックすると、フォームは、`Click` イベントを発生させて、そのイベントを処理するプロシージャを呼び出すことができます。 イベントは、複数のタスク間の通信を可能にすることもできます。 たとえば、メインのアプリケーションとは別のアプリケーションで並べ替えタスクを実行するとします。 ユーザーが並べ替えを取り消した場合、アプリケーションは並べ替え処理の停止を指示するキャンセル イベントを送信できます。  
  
## <a name="event-terms-and-concepts"></a>イベントの用語と概念  
 このセクションでは、[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] で使用される用語と概念について説明します。  
  
### <a name="declaring-events"></a>イベントの宣言  
 イベントは、次の例に示すように、`Event` キーワードを使用して、クラス、構造体、モジュール、およびインターフェイス内で宣言します。  
  
 [!code-vb[VbVbalrEvents#24](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_1.vb)]  
  
### <a name="raising-events"></a>イベントの発生  
 イベントは、重要な出来事が発生したことを通知するメッセージに似ています。 メッセージをブロードキャストする動作は、"*イベントの発生*" と呼ばれます。 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] では、次の例に示すように、`RaiseEvent` ステートメントを使用してイベントを発生させます。  
  
 [!code-vb[VbVbalrEvents#25](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_2.vb)]  
  
 イベントは、イベントを宣言しているクラス、モジュール、または構造体のスコープ内で発生させる必要があります。 たとえば、基本クラスから継承された派生クラスでイベントを発生させることはできません。  
  
### <a name="event-senders"></a>イベントの送信元  
 イベントを発生させる機能を持つオブジェクトが "*イベントの送信元*" になります。これは "*イベント ソース*" とも呼ばれます。 イベントの送信元の例として、フォーム、コントロール、およびユーザー定義オブジェクトがあります。  
  
### <a name="event-handlers"></a>イベント ハンドラー  
 "*イベント ハンドラー*" は、対応するイベントが発生したときに呼び出されるプロシージャです。 イベント ハンドラーと一致するシグネチャを持つ任意の有効なサブルーチンを使用できます。 ただし、関数はイベント ソースに値を返すことができないため、イベント ハンドラーとして使用することはできません。  
  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] では、イベント ハンドラーの標準的な名前付け規則である、イベントの送信元、アンダースコア、およびイベントの名前の組み合わせを使用しています。 たとえば、`button1` という名前のボタンの `Click` イベントには、`Sub button1_Click` という名前が付けられます。  
  
> [!NOTE]
>  独自のイベントに対するイベント ハンドラーを定義するときは、この名前付け規則を使用することをお勧めしますが、使用は必須ではありません。任意の有効なサブルーチン名を付けることができます。  
  
## <a name="associating-events-with-event-handlers"></a>イベントとイベント ハンドラーの関連付け  
 イベント ハンドラーを使用する前に、`Handles` ステートメントまたは `AddHandler` ステートメントを使用して、イベントをイベント ハンドラーに関連付けておく必要があります。  
  
### <a name="withevents-and-the-handles-clause"></a>WithEvents と Handles 句  
 `WithEvents` ステートメントと `Handles` 句を使用して、指定するイベント ハンドラーを宣言できます。 `WithEvents` キーワードを使用して宣言されたオブジェクトによって発生したイベントは、次の例に示すように、そのイベント用の `Handles` ステートメントがある任意のプロシージャで処理できます。  
  
 [!code-vb[VbVbalrEvents#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_3.vb)]  
  
 多くの場合、イベント ハンドラーを指定するための最善の選択は、`WithEvents` ステートメントと `Handles` 句を使用することです。これは、宣言型の構文により簡単にコーディング、読み取り、デバッグを実行できるためです。 ただし、`WithEvents` 変数には、次の使用制限があることに注意してください。  
  
-   `WithEvents` 変数をオブジェクト変数として使用することはできません。 つまり、`Object` として宣言することはできません。変数を宣言するときは、クラス名を指定する必要があります。  
  
-   共有イベントはクラス インスタンスに関連付けられないため、`WithEvents` を使用して共有イベントを宣言によって処理することはできません。 同様に、`WithEvents` または`Handles` を使用して `Structure` からイベントを処理することはできません。 どちらの場合も、`AddHandler` ステートメント使用して、これらのイベントを処理することができます。  
  
-   `WithEvents` 変数の配列を作成することはできません。  
  
 `WithEvents` 変数を使用して、1 つのイベント ハンドラーで 1 つまたは複数の種類のイベントを、または 1 つまたは複数のイベント ハンドラーで同じ種類のイベントを処理することができます。  
  
 `Handles` 句は、イベントをイベント ハンドラーに関連付けるための標準的な方法ですが、イベントをイベント ハンドラーに関連付ける動作はコンパイル時に限定されます。  
  
 場合によっては (フォームやコントロールに関連付けられたイベントなど)、[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] は、空のイベント ハンドラーを自動的にスタブとして作成し、それをイベントに関連付けます。 たとえば、デザイン モードでフォームのコマンド ボタンをダブルクリックすると、次のコードに示すように、[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] はコマンド ボタン用の空のイベント ハンドラーと `WithEvents` 変数を作成します。  
  
 [!code-vb[VbVbalrEvents#26](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_4.vb)]  
  
### <a name="addhandler-and-removehandler"></a>AddHandler と RemoveHandler  
 `AddHandler` ステートメントは、イベント ハンドラーを指定できるという点で `Handles` 句に似ています。 ただし、`AddHandler` を `RemoveHandler` と一緒に使用すると、`Handles` 句よりも柔軟性が増し、イベントに関連付けられたイベント ハンドラーを動的に追加、削除、変更することができます。 共有イベントまたは構造体からのイベントを処理する場合は、`AddHandler` を使用する必要があります。  
  
 `AddHandler` は 2 つの引数 (コントロールなどのイベントの送信元から渡されるイベント名と、デリゲートを評価する式) を使用します。 `AddHandler` を使用する場合はデリゲート クラスを明示的に指定する必要がありません。これは、`AddressOf` ステートメントが常にデリゲートへの参照を返すためです。 次の例では、オブジェクトによって発生するイベントにイベント ハンドラーを関連付けます。  
  
 [!code-vb[VbVbalrEvents#28](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_5.vb)]  
  
 イベントとイベント ハンドラーと関連付けを解除する `RemoveHandler` は、`AddHandler` と同じ構文を使用します。 例:  
  
 [!code-vb[VbVbalrEvents#29](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_6.vb)]  
  
 次の例では、イベントにイベント ハンドラーが関連付けられた後、イベントが発生します。 イベント ハンドラーがイベントをキャッチし、メッセージを表示します。  
  
 次に、最初のイベント ハンドラーが削除され、別のイベント ハンドラーがイベントに関連付けられます。 もう一度イベントが発生し、別のメッセージが表示されます。  
  
 最後に、2 つ目のイベント ハンドラーが削除され、3 回目のイベントが発生します。 イベントに関連付けられているイベント ハンドラーがないため、何も実行されません。  
  
 [!code-vb[VbVbalrEvents#38](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_7.vb)]  
  
## <a name="handling-events-inherited-from-a-base-class"></a>基本クラスから継承されたイベントの処理  
 "*派生クラス*" は基本クラスから特性を継承したクラスであり、基本クラスによって発生したイベントを `Handles``MyBase` ステートメントを使用して処理できます。  
  
#### <a name="to-handle-events-from-a-base-class"></a>基本クラスのイベントを処理するには  
  
-   イベント ハンドラー プロシージャの宣言行に `Handles MyBase.`*eventname* ステートメントを追加して、派生クラスのイベント ハンドラーを宣言します。*eventname* は処理する基本クラスのイベント名です。 例:  
  
     [!code-vb[VbVbalrEvents#12](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_8.vb)]  
  
## <a name="related-sections"></a>関連項目  
  
|タイトル|説明|  
|-----------|-----------------|  
|[チュートリアル : イベントの宣言と発生](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)|クラスのイベントを宣言して発生させる方法を手順を追って説明します。|  
|[チュートリアル : イベントの処理](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)|イベント ハンドラー プロシージャの記述方法を示します。|  
|[方法: カスタム イベントを宣言してブロックを回避する](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)|イベント ハンドラーを非同期に呼び出すことができるカスタム イベントの定義方法を示します。|  
|[方法: カスタム イベントを宣言してメモリを節約する](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)|イベントを処理するときにのみ、メモリを使用するカスタム イベントを定義する方法を示します。|  
|[Visual Basic での継承されたイベント ハンドラーのトラブルシューティング](../../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)|継承されたコンポーネントのイベント ハンドラーで生じる一般的な問題を一覧表示します。|  
|[イベント](../../../../standard/events/index.md)|[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] のイベント モデルについて概説します。|  
|[Windows フォーム内のイベント ハンドラーの作成](https://msdn.microsoft.com/library/dacysss4.aspx)|Windows フォーム オブジェクトに関連付けられているイベントの処理方法について説明します。|  
|[デリゲート](../../../../visual-basic/programming-guide/language-features/delegates/index.md)|Visual Basic でのデリゲートの概要を示します。|

