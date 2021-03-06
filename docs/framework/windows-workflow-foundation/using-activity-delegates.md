---
title: "アクティビティ デリゲートの使用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e33cf876-8979-440b-9b23-4a12d1139960
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# アクティビティ デリゲートの使用
アクティビティ デリゲートを使用すると、アクティビティの作成者は、特定の署名を持つコールバックを公開できます。アクティビティのユーザーは、この署名用のアクティビティベースのハンドラーを提供できます。2 種類のアクティビティ デリゲートを使用できます。<xref:System.Activities.ActivityAction%601> は、戻り値を持たないアクティビティ デリゲートを定義する場合に使用され、<xref:System.Activities.ActivityFunc%601> は戻り値を持つアクティビティ デリゲートを定義する場合に使用されます。  
  
 アクティビティ デリゲートは、子アクティビティが特定の署名を持つように制限する必要がある場合に便利です。たとえば、<xref:System.Activities.Statements.While> アクティビティは制約のないあらゆる型のアクティビティを含めることができますが、<xref:System.Activities.Statements.ForEach%601> アクティビティの本体は <xref:System.Activities.ActivityAction%601> であるため、最終的には <xref:System.Activities.Statements.ForEach%601> によって実行されるその子アクティビティは、<xref:System.Activities.Statements.ForEach%601> が列挙するコレクションのメンバーと同じ型である <xref:System.Activities.InArgument%601> を持つ必要があります。  
  
## ActivityAction の使用  
 いくつかの [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] アクティビティ \(<xref:System.Activities.Statements.Catch> アクティビティや <xref:System.Activities.Statements.ForEach%601> アクティビティなど\) では、アクティビティ アクションが使用されます。それぞれの場合において、アクティビティ アクションは、これらのアクティビティのいずれかを使用してワークフローを作成するときに、ワークフローの作成者が目的の動作を提供するアクティビティを指定する場所を表します。次の例では、<xref:System.Activities.Statements.ForEach%601> アクティビティを使用してコンソール ウィンドウにテキストを表示します。<xref:System.Activities.Statements.ForEach%601> の本体は、<xref:System.Activities.Statements.ForEach%601> の型 \(文字列\) に一致する <xref:System.Activities.ActivityAction%601> を使用して指定します。<xref:System.Activities.ActivityDelegate.Handler%2A> で指定された <xref:System.Activities.Statements.WriteLine> アクティビティには、<xref:System.Activities.Statements.ForEach%601> アクティビティによって反復処理されるコレクションの文字列値にバインドされる <xref:System.Activities.Statements.WriteLine.Text%2A> 引数があります。  
  
 [!code-csharp[CFX_ActivityExample#6](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#6)]  
  
 actionArgument は、コレクション内の各項目を WriteLine にフローするために使用されます。このワークフローが呼び出されると、次の出力がコンソールに表示されます。  
  
 **Hello**   
**World.**  このトピックの例では、オブジェクトの初期化の構文を使用します。オブジェクトの初期化の構文は、コードでワークフロー定義を作成する場合に便利な方法です。これは、ワークフローのアクティビティの階層ビューが提供され、アクティビティ間の関係が示されるためです。プログラムからワークフローを作成する場合に、オブジェクトの初期化の構文を使用しなければならないという要件はありません。次の例は、機能的には前のサンプルと同じです。  
  
 [!code-csharp[CFX_ActivityExample#7](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#7)]  
  
 オブジェクト初期化子[!INCLUDE[crabout](../../../includes/crabout-md.md)]、「[方法: コンストラクターを呼び出さずにオブジェクトを初期化する \(C\# プログラミング ガイド\)](http://go.microsoft.com/fwlink/?LinkId=161015)」および「[方法: オブジェクト初期化子を使用してオブジェクトを宣言する](http://go.microsoft.com/fwlink/?LinkId=161016)」を参照してください。  
  
 次の例では、ワークフローで <xref:System.Activities.Statements.TryCatch> アクティビティを使用します。ワークフローによって <xref:System.ApplicationException> がスローされ、<xref:System.Activities.Statements.Catch%601> アクティビティによってこの例外が処理されます。<xref:System.Activities.Statements.Catch%601> アクティビティのアクティビティ アクションのハンドラーは <xref:System.Activities.Statements.WriteLine> アクティビティで、例外の詳細は `ex` <xref:System.Activities.DelegateInArgument%601> を介してこのハンドラーにフローされます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#33](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#33)]  
  
 <xref:System.Activities.ActivityAction%601> を定義するカスタム アクティビティを作成する場合は、<xref:System.Activities.Statements.InvokeAction%601> を使用して <xref:System.Activities.ActivityAction%601> の呼び出しをモデル化します。次の例では、カスタムの `WriteLineWithNotification` アクティビティを定義します。このアクティビティは、<xref:System.Activities.Statements.WriteLine> アクティビティが含まれ、その後に 1 つの文字列引数を取る <xref:System.Activities.ActivityAction%601> を呼び出す <xref:System.Activities.Statements.InvokeAction%601> が続く <xref:System.Activities.Statements.Sequence> で構成されます。  
  
 [!code-csharp[CFX_ActivityExample#1](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#1)]  
  
 `WriteLineWithNotification` アクティビティを使用してワークフローを作成する場合、ワークフローの作成者は、アクティビティ アクションの <xref:System.Activities.ActivityDelegate.Handler%2A> で必要なカスタム ロジックを指定します。次の例では、`WriteLineWithNotification` アクティビティを使用してワークフローを作成し、<xref:System.Activities.ActivityDelegate.Handler%2A> として <xref:System.Activities.Statements.WriteLine> アクティビティを使用します。  
  
 [!code-csharp[CFX_ActivityExample#2](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#2)]  
  
 1 つ以上の引数を渡すために <xref:System.Activities.Statements.InvokeAction%601> および <xref:System.Activities.ActivityAction%601> のジェネリック バージョンが複数用意されています。  
  
## ActivityFunc の使用  
 <xref:System.Activities.ActivityAction%601> はアクティビティから結果値が返されない場合に役立ち、<xref:System.Activities.ActivityFunc%601> は結果値が返される場合に使用されます。<xref:System.Activities.ActivityFunc%601> を定義するカスタム アクティビティを作成する場合は、<xref:System.Activities.Expressions.InvokeFunc%601> を使用して <xref:System.Activities.ActivityFunc%601> の呼び出しをモデル化します。次の例では、`WriteFillerText` アクティビティを定義します。充てんテキストを提供するために、整数の引数を取って文字列の結果を持つ <xref:System.Activities.Expressions.InvokeFunc%601> を指定します。充てんテキストが取得されると、<xref:System.Activities.Statements.WriteLine> アクティビティを使用してコンソールに表示されます。  
  
 [!code-csharp[CFX_ActivityExample#3](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#3)]  
  
 テキストを提供するには、`int` の引数を 1 つ取って文字列の結果を持つアクティビティを使用する必要があります。次の例では、これらの要件を満たす `TextGenerator` アクティビティを示します。  
  
 [!code-csharp[CFX_ActivityExample#4](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#4)]  
  
 `TextGenerator` アクティビティと `WriteRandomText` アクティビティを一緒に使用するには、<xref:System.Activities.ActivityDelegate.Handler%2A> として指定します。  
  
 [!code-csharp[CFX_ActivityExample#5](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#5)]  
  
## 参照  
 [ActivityAction の公開と呼び出し](../../../docs/framework/windows-workflow-foundation/samples/exposing-and-invoking-activityactions.md)