---
title: "カスタム属性の記述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "AllowMultiple プロパティ"
  - "属性クラス, 宣言"
  - "属性 [.NET Framework], カスタム"
  - "AttributeTargets 列挙型"
  - "AttributeUsageAttribute クラス, カスタム属性"
  - "カスタム属性"
  - "Inherited プロパティ"
  - "複数の属性インスタンス"
ms.assetid: 97216f69-bde8-49fd-ac40-f18c500ef5dc
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# カスタム属性の記述
独自のカスタム属性をデザインするために、多くの新しい概念を習得する必要はありません。 オブジェクト指向プログラミングに精通してクラスをデザインする方法を理解しているなら、必要な知識をほぼすべて持っています。 カスタム属性は、基本的には、<xref:System.Attribute?displayProperty=fullName> から直接的に派生したか間接的に派生した従来のクラスです。 従来のクラスと同じように、カスタム属性には、データを格納したり取得したりするメソッドが含まれます。  
  
 カスタム属性クラスを適切にデザインするための主要な手順は次のとおりです。  
  
-   [AttributeUsageAttribute を適用する](#cpconapplyingattributeusageattribute)  
  
-   [属性クラスを宣言する](#cpcondeclaringattributeclass)  
  
-   [コンストラクターを宣言する](#cpcondeclaringconstructors)  
  
-   [プロパティを宣言する](#cpcondeclaringproperties)  
  
 このセクションでは、これらの各手順について説明し、最後に[カスタム属性の例](#cpconcustomattributeexample)について説明します。  
  
<a name="cpconapplyingattributeusageattribute"></a>   
## AttributeUsageAttribute を適用する  
 カスタム属性宣言は **AttributeUsageAttribute** で始まり、属性クラスの主な特性のいくつかを定義します。 たとえば、属性が他のクラスによって継承されるかどうかを指定したり、属性を適用する要素を指定したりすることができます。 次のコード フラグメントは、**AttributeUsageAttribute** の使い方を示しています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#5)]
 [!code-csharp[Conceptual.Attributes.Usage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#5)]
 [!code-vb[Conceptual.Attributes.Usage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#5)]  
  
 <xref:System.AttributeUsageAttribute?displayProperty=fullName> には、カスタム属性を作成するために重要な 3 つのメンバーがあります。それらは、[AttributeTargets](#cpconwritingcustomattributesanchor1)、[Inherited](#cpconwritingcustomattributesanchor2)、[AllowMultiple](#cpconwritingcustomattributesanchor3) です。  
  
<a name="cpconwritingcustomattributesanchor1"></a>   
### AttributeTargets メンバー  
 前の例では、**AttributeTargets.All** を指定し、この属性をすべてのプログラム要素に適用できることが示されています。 代わりに、属性をクラスにのみ適用できることを示す **AttributeTargets.Class** を指定するか、属性をメソッドにのみ適用できることを示す **AttributeTargets.Method** を指定できます。 この方法で、カスタム属性を使って、説明としてすべてのプログラム要素をマークすることができます。  
  
 また、<xref:System.AttributeTargets> の複数のインスタンスを渡すこともできます。 次のコード フラグメントは、すべてのクラスやメソッドに適用できるカスタム属性を指定します。  
  
 [!code-cpp[Conceptual.Attributes.Usage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#6)]
 [!code-csharp[Conceptual.Attributes.Usage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#6)]
 [!code-vb[Conceptual.Attributes.Usage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#6)]  
  
<a name="cpconwritingcustomattributesanchor2"></a>   
### Inherited プロパティ  
 <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=fullName> プロパティは、属性が、その属性が適用されたクラスから派生したクラスによって継承可能かどうかを示します。 このプロパティは、**true** \(既定\) か **false** フラグのいずれかを使います。 たとえば、次の例で、`MyAttribute` は **true** の既定の <xref:System.AttributeUsageAttribute.Inherited%2A> 値が指定されていますが、`YourAttribute` は **false** の <xref:System.AttributeUsageAttribute.Inherited%2A> 値が指定されています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Attributes.Usage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#7)]
 [!code-vb[Conceptual.Attributes.Usage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#7)]  
  
 その後、2 つの属性が基底クラス `MyClass` に適用されます。  
  
 [!code-cpp[Conceptual.Attributes.Usage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#9)]
 [!code-csharp[Conceptual.Attributes.Usage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#9)]
 [!code-vb[Conceptual.Attributes.Usage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#9)]  
  
 最後に、クラス `YourClass` が基底クラス `MyClass` から継承されます。 メソッド `MyMethod` は `MyAttribute` を表示しますが、`YourAttribute` を表示しません。  
  
 [!code-cpp[Conceptual.Attributes.Usage#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#10)]
 [!code-csharp[Conceptual.Attributes.Usage#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#10)]
 [!code-vb[Conceptual.Attributes.Usage#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#10)]  
  
<a name="cpconwritingcustomattributesanchor3"></a>   
### AllowMultiple プロパティ  
 <xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=fullName> プロパティは、1 つの要素に、属性の複数のインスタンスが存在できるかどうかを示します。**true** に設定されている場合、複数のインスタンスが許可され、**false** \(既定\) に設定されている場合、1 つのインスタンスのみが許可されます。  
  
 次の例では、`MyAttribute` は **false** の既定の <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 値が指定されていますが、`YourAttribute` は **true** の値が指定されています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#11)]
 [!code-csharp[Conceptual.Attributes.Usage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#11)]
 [!code-vb[Conceptual.Attributes.Usage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#11)]  
  
 これらの属性の複数のインスタンスが適用されると、`MyAttribute` ではコンパイラ エラーが発生します。 次のコード例は、`YourAttribute` の正しい使い方と `MyAttribute` の正しくない使い方を示しています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#13)]
 [!code-csharp[Conceptual.Attributes.Usage#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#13)]
 [!code-vb[Conceptual.Attributes.Usage#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#13)]  
  
 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> プロパティと <xref:System.AttributeUsageAttribute.Inherited%2A> プロパティの両方が **true** に設定されている場合、別のクラスから継承されるクラスは属性を継承し、同じ子クラスに適用される同じ属性の別のインスタンスを持つことができます。<xref:System.AttributeUsageAttribute.AllowMultiple%2A> が **false** に設定されている場合、親クラスのすべての属性の値は、子クラスの同じ属性の新しいインスタンスによって上書きされます。  
  
<a name="cpcondeclaringattributeclass"></a>   
## 属性クラスを宣言する  
 <xref:System.AttributeUsageAttribute> を適用すると、属性を具体的に定義できるようになります。 属性クラスの宣言は、次のコードに示すように、従来のクラスの宣言に似ています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#14)]
 [!code-csharp[Conceptual.Attributes.Usage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#14)]
 [!code-vb[Conceptual.Attributes.Usage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#14)]  
  
 この属性定義は、次の点を示します。  
  
-   属性クラスはパブリック クラスとして宣言する必要があります。  
  
-   規則により、属性クラスの名前の終わりに **Attribute** という単語を付けます。 必須ではありませんが、読みやすさの向上のために、この規定をお勧めします。 属性を適用すると、Attribute という単語を含める必要はなくなります。  
  
-   すべての属性クラスは、**System.Attribute** から直接的に継承するか間接的に継承する必要があります。  
  
-   Microsoft Visual Basic では、すべてのカスタム属性クラスは **AttributeUsageAttribute** 属性が必要です。  
  
<a name="cpcondeclaringconstructors"></a>   
## コンストラクターを宣言する  
 属性は、従来のクラスと同じ方法で、コンストラクターで初期化されます。 次のコード フラグメントは、一般的な属性のコンストラクターを示しています。 このパブリック コンストラクターは、パラメーターを使って、メンバー変数と同じ値を設定します。  
  
 [!code-cpp[Conceptual.Attributes.Usage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#15)]
 [!code-csharp[Conceptual.Attributes.Usage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#15)]
 [!code-vb[Conceptual.Attributes.Usage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#15)]  
  
 さまざまな値の組み合わせに対応するように、コンストラクターをオーバーロードできます。 カスタム属性クラスの[プロパティ](../Topic/Properties%20Overview.md)も定義する場合、属性を初期化する際に、名前付きパラメーターと位置指定パラメーターの組み合わせを使うことができます。 通常、必須パラメーターすべてを位置指定パラメーター、省略可能なパラメーターすべてを名前付きパラメーターとして定義します。 この場合、属性は必須パラメーターがないと初期化できません。 その他のすべてのパラメーターは省略できます。 Visual Basic では、属性クラスのコンストラクターで ParamArray 引数を使うべきではないことに注意してください。  
  
 次のコード例は、省略可能なパラメーターと必須パラメーターを使って、前のコンストラクターを使う属性を適用できることを示しています。 ここでは、属性には、必須のブール値 1 つと省略可能な文字列のプロパティ 1 つが含まれていることを前提としています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#17)]
 [!code-csharp[Conceptual.Attributes.Usage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#17)]
 [!code-vb[Conceptual.Attributes.Usage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#17)]  
  
<a name="cpcondeclaringproperties"></a>   
## プロパティを宣言する  
 名前付きパラメーターを定義するか、属性によって格納される値を簡単に返すことができるようにする場合、[プロパティ](../Topic/Properties%20Overview.md)を宣言します。 属性プロパティは、返されるデータ型の記述を添えて、パブリック エンティティとして宣言する必要があります。 プロパティの値を保持する変数を定義して、その変数を **get** メソッドと **set** メソッドに関連付けます。 次のコード例は、属性に単純なプロパティを実装する方法を示しています。  
  
 [!code-cpp[Conceptual.Attributes.Usage#16](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#16)]
 [!code-csharp[Conceptual.Attributes.Usage#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#16)]
 [!code-vb[Conceptual.Attributes.Usage#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#16)]  
  
<a name="cpconcustomattributeexample"></a>   
## カスタム属性の例  
 このセクションには、前の情報が含まれており、コードのセクションの作成者に関する情報を文書化する単純な属性をデザインする方法を示しています。 この例の属性は、プログラマの名前とレベル、またコードを確認したかどうかを格納します。 保存する実際の値を格納するため、3 つのプライベート変数を使います。 各変数は、値を取得して設定するパブリック プロパティで表されます。 最後に、コンストラクターを 2 つの必須パラメーターを使って定義します。  
  
 [!code-cpp[Conceptual.Attributes.Usage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#4)]
 [!code-csharp[Conceptual.Attributes.Usage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#4)]
 [!code-vb[Conceptual.Attributes.Usage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#4)]  
  
 完全名 `DeveloperAttribute` や省略名 `Developer` を使って、次のいずれかの方法でこの属性を適用できます。  
  
 [!code-cpp[Conceptual.Attributes.Usage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#12)]
 [!code-csharp[Conceptual.Attributes.Usage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#12)]
 [!code-vb[Conceptual.Attributes.Usage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#12)]  
  
 最初の例は、必須の名前付きパラメーターのみを使って適用された属性を示し、2 番目の例は、必須パラメーターと省略可能なパラメーターの両方を使って適用された属性を示しています。  
  
## 参照  
 <xref:System.Attribute?displayProperty=fullName>   
 <xref:System.AttributeUsageAttribute>   
 [属性](../../../docs/standard/attributes/index.md)