---
title: "非同期プログラム (Visual Basic) でフロー制御 |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: b0443af7-c586-4cb0-b476-742ae4098a96
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 15e02fbc023db9ae2f3ee9f40598faa7c9c027a0
ms.lasthandoff: 03/13/2017

---
# <a name="control-flow-in-async-programs-visual-basic"></a>(Visual Basic) の非同期プログラムにおける制御フロー
`Async` キーワードと `Await` キーワードを使用すると、非同期のプログラムの作成と保守をより簡単に行えます。 ただし、プログラムがどのように動作するかを理解しないと、その結果は予想に反するものになる場合があります。 このトピックでは、簡単な非同期プログラムによる制御フローをトレースして、制御があるメソッドから別のメソッドに移るタイミングと、その都度転送される情報について説明します。  
  
> [!NOTE]
>  `Async` キーワードおよび `Await` キーワードは、Visual Studio 2012 で導入されました。  
  
 一般を使用した非同期コードを含むメソッドをマークする、 [Async](../../../../visual-basic/language-reference/modifiers/async.md)修飾子です。 Async 修飾子でマークされているメソッドで使用することができます、 [Await (Visual Basic)](../../../../visual-basic/language-reference/operators/await-operator.md)メソッドが呼び出された非同期プロセスを完了するまで待機する一時停止を指定する演算子です。 詳細については、次を参照してください。 [Async と Await (Visual Basic) を使用した非同期プログラミング](../../../../visual-basic/programming-guide/concepts/async/index.md)します。  
  
 次の例では、非同期メソッドを使用して、指定した Web サイトのコンテンツを文字列としてダウンロードし、その文字列の長さを表示します。 この例には、次の&2; つのメソッドが含まれています。  
  
-   `startButton_Click` を呼び出して結果を表示する `AccessTheWebAsync`。  
  
-   Web サイトのコンテンツを文字列としてダウンロードして、その文字列の長さを返す `AccessTheWebAsync`。 `AccessTheWebAsync`非同期を使用して<xref:System.Net.Http.HttpClient>メソッド、 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>、コンテンツをダウンロードします</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29></xref:System.Net.Http.HttpClient>。  
  
 番号付き表示行はプログラム全体で重要なポイントを示し、プログラムがどのように実行され、マークされている各ポイントで何が発生するかを理解するために役立ちます。 表示行には「1」から「6」までのラベルが付けられています。 このラベルは、プログラムがこれらのコード行に到達する順序を表します。  
  
 次のコードは、プログラムの概要を示します。  
  
```vb  
Class MainWindow  
  
    Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click  
  
        ' ONE  
        Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()  
  
        ' FOUR  
        Dim contentLength As Integer = Await getLengthTask  
  
        ' SIX  
        ResultsTextBox.Text &=  
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
  
    End Sub  
  
    Async Function AccessTheWebAsync() As Task(Of Integer)  
  
        ' TWO  
        Dim client As HttpClient = New HttpClient()   
        Dim getStringTask As Task(Of String) =   
            client.GetStringAsync("http://msdn.microsoft.com")  
  
        ' THREE  
        Dim urlContents As String = Await getStringTask  
  
        ' FIVE  
        Return urlContents.Length  
    End Function  
  
End Class  
  
```  
  
 「1」から「6」までのそれぞれのラベルの位置は、プログラムの現在の状態に関する情報を表示します。 次の出力が生成されます。  
  
```  
  
ONE:   Entering startButton_Click.  
           Calling AccessTheWebAsync.  
  
TWO:   Entering AccessTheWebAsync.  
           Calling HttpClient.GetStringAsync.  
  
THREE: Back in AccessTheWebAsync.  
           Task getStringTask is started.  
           About to await getStringTask & return a Task<int> to startButton_Click.  
  
FOUR:  Back in startButton_Click.  
           Task getLengthTask is started.  
           About to await getLengthTask -- no caller to return to.  
  
FIVE:  Back in AccessTheWebAsync.  
           Task getStringTask is complete.  
           Processing the return statement.  
           Exiting from AccessTheWebAsync.  
  
SIX:   Back in startButton_Click.  
           Task getLengthTask is finished.  
           Result from AccessTheWebAsync is stored in contentLength.  
           About to display contentLength and exit.  
  
Length of the downloaded string: 33946.  
```  
  
## <a name="set-up-the-program"></a>プログラムをセットアップする  
 このトピックで使用するコードは、MSDN からダウンロードするか、または自分でビルドできます。  
  
> [!NOTE]
>  例を実行するには、Visual Studio 2012 以降と .NET Framework 4.5 が必要または以降のコンピューターにインストールします。  
  
### <a name="download-the-program"></a>プログラムをダウンロードする  
 このトピックからのアプリケーションをダウンロードする[Async サンプル: 非同期プログラムにおける制御のフロー](http://go.microsoft.com/fwlink/?LinkId=255285)します。 次の手順でプログラムを開いて実行します。  
  
1.  ダウンロードしたファイルを解凍し、Visual Studio を開始します。  
  
2.  メニュー バーで **[ファイル]**、 **[開く]**、 **[プロジェクト/ソリューション]**の順に選択します。  
  
3.  解凍したサンプル コードが含まれるフォルダーに移動し、ソリューション (.sln) ファイルを開き、F5 キーを押してプロジェクトをビルドし、実行します。  
  
### <a name="build-the-program-yourself"></a>プログラムを手動でビルドする  
 次の Windows Presentation Foundation (WPF) プロジェクトには、このトピックのコード例が含まれています。  
  
 このプロジェクトを実行するには、次の手順を実行します。  
  
1.  Visual Studio を起動します。  
  
2.  メニュー バーで、 **[ファイル]**、 **[新規作成]**、 **[プロジェクト]**の順にクリックします。  
  
     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  **インストールされたテンプレート** ウィンドウで、選択**Visual Basic**、にして**WPF アプリケーション**プロジェクトの種類の一覧からです。  
  
4.  入力`AsyncTracer`として、プロジェクトの名前を選択し、 **ok**  ボタンをクリックします。  
  
     新しいプロジェクトに表示されます**ソリューション エクスプ ローラー**します。  
  
5.  Visual Studio コード エディターで、 **[MainWindow.xaml]** タブをクリックします。  
  
     タブが表示されない場合で MainWindow.xaml のショートカット メニューを開き**ソリューション エクスプ ローラー**、にして**コードの表示**します。  
  
6.  **XAML** MainWindow.xaml のビューで、コードを次のコードに置き換えます。  
  
    ```vb  
    <Window  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="MainWindow"  
        Title="Control Flow Trace" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="221,10,0,0" VerticalAlignment="Top" Width="75"/>  
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="510" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" d:LayoutOverrides="HorizontalMargin"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     テキスト ボックスとボタンを含む簡単なウィンドウに表示、**デザイン**MainWindow.xaml のビューです。  
  
7.  <xref:System.Net.Http>。</xref:System.Net.Http>への参照を追加します。  
  
8.  **ソリューション エクスプ ローラー**MainWindow.xaml.vb のショートカット メニューを開き、クリックして**コードの表示**します。  
  
9. MainWindow.xaml.vb で、コードを次のコードに置き換えます。  
  
    ```vb  
    ' Add an Imports statement and a reference for System.Net.Http.  
    Imports System.Net.Http  
  
    Class MainWindow  
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click  
  
            ' The display lines in the example lead you through the control shifts.  
            ResultsTextBox.Text &= "ONE:   Entering StartButton_Click." & vbCrLf &  
                "           Calling AccessTheWebAsync." & vbCrLf  
  
            Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()  
  
            ResultsTextBox.Text &= vbCrLf & "FOUR:  Back in StartButton_Click." & vbCrLf &  
                "           Task getLengthTask is started." & vbCrLf &  
                "           About to await getLengthTask -- no caller to return to." & vbCrLf  
  
            Dim contentLength As Integer = Await getLengthTask  
  
            ResultsTextBox.Text &= vbCrLf & "SIX:   Back in StartButton_Click." & vbCrLf &  
                "           Task getLengthTask is finished." & vbCrLf &  
                "           Result from AccessTheWebAsync is stored in contentLength." & vbCrLf &  
                "           About to display contentLength and exit." & vbCrLf  
  
            ResultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
        End Sub  
  
        Async Function AccessTheWebAsync() As Task(Of Integer)  
  
            ResultsTextBox.Text &= vbCrLf & "TWO:   Entering AccessTheWebAsync."  
  
            ' Declare an HttpClient object.  
            Dim client As HttpClient = New HttpClient()  
  
            ResultsTextBox.Text &= vbCrLf & "           Calling HttpClient.GetStringAsync." & vbCrLf  
  
            ' GetStringAsync returns a Task(Of String).   
            Dim getStringTask As Task(Of String) = client.GetStringAsync("http://msdn.microsoft.com")  
  
            ResultsTextBox.Text &= vbCrLf & "THREE: Back in AccessTheWebAsync." & vbCrLf &  
                "           Task getStringTask is started."  
  
            ' AccessTheWebAsync can continue to work until getStringTask is awaited.  
  
            ResultsTextBox.Text &=  
                vbCrLf & "           About to await getStringTask & return a Task(Of Integer) to StartButton_Click." & vbCrLf  
  
            ' Retrieve the website contents when task is complete.  
            Dim urlContents As String = Await getStringTask  
  
            ResultsTextBox.Text &= vbCrLf & "FIVE:  Back in AccessTheWebAsync." &  
                vbCrLf & "           Task getStringTask is complete." &  
                vbCrLf & "           Processing the return statement." &  
                vbCrLf & "           Exiting from AccessTheWebAsync." & vbCrLf  
  
            Return urlContents.Length  
        End Function  
  
    End Class  
    ```  
  
10. F5 キーを押してプログラムを実行し、 **[Start]** を複数回クリックします。  
  
     次の出力が表示されます。  
  
    ```  
    ONE:   Entering startButton_Click.  
               Calling AccessTheWebAsync.  
  
    TWO:   Entering AccessTheWebAsync.  
               Calling HttpClient.GetStringAsync.  
  
    THREE: Back in AccessTheWebAsync.  
               Task getStringTask is started.  
               About to await getStringTask & return a Task<int> to startButton_Click.  
  
    FOUR:  Back in startButton_Click.  
               Task getLengthTask is started.  
               About to await getLengthTask -- no caller to return to.  
  
    FIVE:  Back in AccessTheWebAsync.  
               Task getStringTask is complete.  
               Processing the return statement.  
               Exiting from AccessTheWebAsync.  
  
    SIX:   Back in startButton_Click.  
               Task getLengthTask is finished.  
               Result from AccessTheWebAsync is stored in contentLength.  
               About to display contentLength and exit.  
  
    Length of the downloaded string: 33946.  
    ```  
  
## <a name="trace-the-program"></a>プログラムのトレース  
  
### <a name="steps-one-and-two"></a>手順&1;. および&2;.  
 最初の&2; つの表示行がパスをトレースする`startButton_Click`呼び出し`AccessTheWebAsync`、および`AccessTheWebAsync`非同期<xref:System.Net.Http.HttpClient><xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>.</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>メソッド</xref:System.Net.Http.HttpClient>を呼び出す 次の図は、メソッドからメソッドへの呼び出しを示しています。  
  
 ![手順&1;. および&2;](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace ONETWO")  
  
 両方の戻り値の型`AccessTheWebAsync`と`client.GetStringAsync` <xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601>は、 `AccessTheWebAsync` では、TResult は整数です。 `GetStringAsync` では、TResult は文字列です。 非同期メソッドの戻り値の型の詳細については、次を参照してください。 [Async を返す型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)します。  
  
 タスクを返す非同期のメソッドは、制御が呼び出し元に戻ると、タスク インスタンスを返します。 呼び出し元に、非同期メソッドから制御が戻りますいずれかの場合、`Await`演算子が呼び出されたメソッドまたは呼び出されたメソッドが終了した場合に検出されました。 「3」から「6」のラベルの付いた表示行はこのプロセスの部分をトレースします。  
  
### <a name="step-three"></a>手順&3;.  
 `AccessTheWebAsync`、非同期メソッド<xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>対象 web ページのコンテンツをダウンロードするために呼び出される</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>。 `client.GetStringAsync` が制御を返すと、`AccessTheWebAsync` から `client.GetStringAsync` に制御が戻ります。  
  
 `client.GetStringAsync` メソッドは、`getStringTask` の `AccessTheWebAsync` 変数に割り当てる文字列のタスクを返します。 プログラム例の次の行は、`client.GetStringAsync` の呼び出しと割り当てを示しています。  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 このタスクは `client.GetStringAsync` により実際の文字列が最終的に生成される約束と見なすことができます。 `AccessTheWebAsync` には `client.GetStringAsync` から約束された文字列に依存しない処理がある場合、その処理は `client.GetStringAsync` を待機している間は、続行できます。 この例では、「3」のラベルの付いた行の出力は、独立した処理を行う機会を表します。  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
 次のステートメントは `AccessTheWebAsync` が待機中の場合 `getStringTask` の進行を中断します。  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
 次の図は、コントロールからのフローを示しています。`client.GetStringAsync`への割り当てへ`getStringTask`との作成から`getStringTask`Await 演算子のアプリケーションにします。  
  
 ![ステップ&3;](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace&3;")  
  
 await 式は `AccessTheWebAsync` が制御を返すまで `client.GetStringAsync` を中断します。 その間、コントロールは `AccessTheWebAsync` の呼び出し元である `startButton_Click` に戻されます。  
  
> [!NOTE]
>  通常、直ちに非同期メソッドへの呼び出しの待機状態となります。 たとえば、次の割り当てで作成し、それを待機する前のコードを置き換えられます`getStringTask`:`Dim urlContents As String = Await client.GetStringAsync("http://msdn.microsoft.com")`  
>   
>  このトピックでは、await 演算子が後で適用され、プログラムでの制御フローを示す出力行を格納します。  
  
### <a name="step-four"></a>手順&4;.  
 戻り値の型の宣言、`AccessTheWebAsync`は`Task(Of Integer)`です。 したがって、`AccessTheWebAsync` が中断されると、`startButton_Click` に整数のタスクを返します。 返されたタスクは `getStringTask` ではないことに注意する必要があります。 返されたタスクは、中断されたメソッド `AccessTheWebAsync` での未処理を表す、整数の新しいタスクです。 これにより、タスクが完了したときに `AccessTheWebAsync` が整数を生成することが保証されます。  
  
 次のステートメントはこのタスクを `getLengthTask` 変数に割り当てます。  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
 `AccessTheWebAsync` と同様に、`startButton_Click` は、非同期タスク (`getLengthTask`) の結果に依存しない処理を、タスクが待機するまで続行できます。 次の出力行はその処理を表します。  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 `startButton_Click` が待機すると、`getLengthTask` の進行は中断します。 次の代入ステートメントは、`startButton_Click` が完了するまで `AccessTheWebAsync` を中断します。  
  
<CodeContentPlaceHolder>10</CodeContentPlaceHolder>  
 次の図で、矢印は `AccessTheWebAsync` の await 式から `getLengthTask` への値の割り当てへの制御のフロー、および `startButton_Click` が待機するまでの `getLengthTask` の通常の処理を示しています。  
  
 ![ステップ&4;](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace&4;")  
  
### <a name="step-five"></a>手順&5;.  
 `client.GetStringAsync` が終了を通知すると、`AccessTheWebAsync` の処理は中断から解放され、await ステートメントを越えて続行できます。 次の出力行は、処理の再開を表します。  
  
<CodeContentPlaceHolder>11</CodeContentPlaceHolder>  
 return ステートメントのオペランド `urlContents.Length` は `AccessTheWebAsync` が返すタスクに格納されます。 await 式はその値を `getLengthTask` の `startButton_Click` から取得します。  
  
 次の図は、`client.GetStringAsync` (および `getStringTask`) が完了した後の制御の移動を示します。  
  
 ![ステップ&5;](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "AsyncTrace&5;")  
  
 `AccessTheWebAsync` は完了するまで実行され、完了を待機していた `startButton_Click` に制御が戻ります。  
  
### <a name="step-six"></a>手順&6;.  
 `AccessTheWebAsync` が終了を通知すると、処理は `startButton_Async` の await ステートメントを越えて続行できます。 実際、プログラムはそれ以上行うことがありません。  
  
 次の出力行は、`startButton_Async` の処理の再開を表します。  
  
<CodeContentPlaceHolder>12</CodeContentPlaceHolder>  
 await 式は `getLengthTask` から `AccessTheWebAsync` の return ステートメントのオペランドである整数値を取得します。 次のステートメントはその値を `contentLength` 変数に割り当てます。  
  
<CodeContentPlaceHolder>13</CodeContentPlaceHolder>  
 次の図は `AccessTheWebAsync` から `startButton_Click` に制御が戻ることを示しています。  
  
 ![ステップ&6;](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace&6;")  
  
## <a name="see-also"></a>関連項目  
 [非同期プログラミングを Async と Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [非同期の戻り値の型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [チュートリアル: Async を使用して Web へのアクセスと Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [(C# および Visual Basic)、非同期プログラムにおける制御フローの非同期のサンプル:](http://go.microsoft.com/fwlink/?LinkId=255285)
