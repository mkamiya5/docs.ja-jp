---
title: "コマンド ライン引数 (C# プログラミング ガイド)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- command-line arguments [C#]
ms.assetid: 0e597e0d-ea7a-41ba-a38a-0198122f3c26
caps.latest.revision: 27
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: f0d404ae0384ec97b0eb78c6284e07cac8065548
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="command-line-arguments-c-programming-guide"></a>コマンド ライン引数 (C# プログラミング ガイド)
`Main` メソッドに引数を渡すには、次のいずれかの方法でメソッドを定義します。  
  
 [!code-cs[csProgGuideMain#2](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_1.cs)]  
  
 [!code-cs[csProgGuideMain#3](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_2.cs)]  
  
> [!NOTE]
>  Windows フォーム アプリケーションの `Main` メソッドでコマンド ライン引数を有効にするには、program.cs の `Main` のシグネチャを手動で変更する必要があります。 Windows フォーム デザイナーが生成するコードは、入力パラメーターなしの `Main` を作成します。 <xref:System.Environment.CommandLine%2A?displayProperty=fullName> または <xref:System.Environment.GetCommandLineArgs%2A?displayProperty=fullName> を使用して、コンソールまたは Windows アプリケーション内の任意の場所からコマンド ライン引数にアクセスすることもできます。  
  
 `Main` メソッドのパラメーターは <xref:System.String> の配列で、コマンド ライン引数を表しています。 通常は、`Length` プロパティを調べて引数があるかどうかを確認します。次はその例です。  
  
 [!code-cs[csProgGuideMain#4](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_3.cs)]  
  
 また、<xref:System.Convert> クラスまたは `Parse` メソッドを使って、文字列型の引数を数値型に変換できます。 たとえば、次のステートメントでは、<xref:System.Int64.Parse%2A> メソッドを使用して `string` を `long` 値に変換します。
  
```  
long num = Int64.Parse(args[0]);  
```  
  
 C# の `long` 型を使うこともできます。これは `Int64` のエイリアスです。  
  
```  
long num = long.Parse(args[0]);  
```  
  
 また、同じ変換に `Convert` クラスの `ToInt64` メソッドを使うこともできます。  
  
```  
long num = Convert.ToInt64(s);  
```  
  
 詳細については、<xref:System.Int64.Parse%2A> および <xref:System.Convert> を参照してください。  
  
## <a name="example"></a>例  
 コンソール アプリケーションでコマンド ライン引数を使用する方法の例を次に示します。 アプリケーションは、実行時に引数を 1 つ受け取り、整数に変換し、その値の階乗を計算しています。 引数がない場合は、アプリケーションの正しい使用方法を説明するメッセージを表示します。  
  
 コマンド プロンプトからアプリケーションをコンパイルして実行するには、次の手順を実行します。  
  
1.  次のコードをテキスト エディターに貼り付け、`Factorial.cs` という名前でテキスト ファイルとして保存します。  
  
     [!code-cs[csProgGuideMain#16](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/command-line-arguments_4.cs)]  
  
2.  **[スタート]** 画面または **[スタート]** メニューから、Visual Studio の **[開発者コマンド プロンプト]** ウィンドウを開き、先ほど作成したファイルが含まれているフォルダーに移動します。  
  
3.  次のコマンドを入力してアプリケーションをコンパイルします。  
  
     `csc Factorial.cs`  
  
     アプリケーションにコンパイル エラーがなければ、`Factorial.exe` という名前の実行可能ファイルが作成されます。  
  
4.  3 の階乗を計算する次のコマンドを入力します。  
  
     `Factorial 3`  
  
5.  次の出力が生成されます: `The factorial of 3 is 6.`  
  
> [!NOTE]
>  Visual Studio でアプリケーションを実行する場合、「[[デバッグ] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/debug-page-project-designer)」のコマンド ライン引数を指定できます。  
  
 コマンド ライン引数の使用方法の例については、「[方法: コマンド ラインを使用してアセンブリを作成および使用する](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Environment?displayProperty=fullName>   
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [Main() とコマンド ライン引数](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [方法: コマンド ライン引数を表示する](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [方法: foreach を使用してコマンド ライン引数にアクセスする](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Main() の戻り値](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)   
 [クラス](../../../csharp/programming-guide/classes-and-structs/classes.md)

