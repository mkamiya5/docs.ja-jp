---
title: "&lt;UseRandomizedStringHashAlgorithm&gt; 要素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<UseRandomizedStringHashAlgorithm> 要素"
  - "UseRandomizedStringHashAlgorithm 要素"
ms.assetid: c08125d6-56cc-4b23-b482-813ff85dc630
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# &lt;UseRandomizedStringHashAlgorithm&gt; 要素
共通言語ランタイムがアプリケーション ドメインごとに文字列のハッシュ コードを計算するかどうかを判定します。  
  
## 構文  
  
```  
<UseRandomizedStringHashAlgorithm   
   enabled=0|1 />  
```  
  
## 属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### 属性  
  
|Attribute|説明|  
|---------------|--------|  
|`enabled`|必須の属性です。<br /><br /> アプリケーション ドメインごとに文字列のハッシュ コードを計算するかどうかを指定します。|  
  
## enabled 属性  
  
|値|説明|  
|-------|--------|  
|`0`|共通言語ランタイムは、アプリケーション ドメインごとに文字列のハッシュ コードを計算しません。1 つのアルゴリズムを使用して文字列のハッシュ コードを計算します。  これは、既定の設定です。|  
|`1`|共通言語ランタイムは、アプリケーション ドメインごとに文字列のハッシュ コードを計算します。  異なるアプリケーション ドメインや異なるプロセスで同一の文字列のハッシュ コードは異なります。|  
  
### 子要素  
 なし。  
  
### 親要素  
  
|要素|説明|  
|--------|--------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|  
  
## 解説  
 既定では、<xref:System.StringComparer> のクラスと <xref:System.String.GetHashCode%2A?displayProperty=fullName> のメソッドは、アプリケーション ドメイン間で一貫したハッシュ コードを生成する単一のハッシュ アルゴリズムを使用します。  これは、`<UseRandomizedStringHashAlgorithm>` 要素の `enabled` 属性を `0` に設定することと同じです。  これは [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] で使用されるハッシュ アルゴリズムです。  
  
 <xref:System.StringComparer> クラスと <xref:System.String.GetHashCode%2A?displayProperty=fullName> メソッドは、別のハッシュ アルゴリズムを使用してアプリケーション ドメインごとのハッシュ コードを計算することもできます。  その結果、同じ文字列のハッシュ コードが、アプリケーション ドメイン間で異なります。  これはオプトイン機能であり、この機能を利用するには、`<UseRandomizedStringHashAlgorithm>` 要素の `enabled` 属性を `1` に設定する必要があります。  
  
 ハッシュ テーブルの文字列検索は、通常 O\(1\) 操作です。  ただし、多くの競合が発生すると、検索は O\(n<sup>2</sup>\) 操作になることがあります。  特にハッシュ コードを計算するキーがユーザーによる入力データに基づいている場合、`<UseRandomizedStringHashAlgorithm>` 構成要素を使用して、アプリケーション ドメインごとにランダムなハッシュ アルゴリズムを生成でき、潜在的な競合の数を制限できます。  
  
## 使用例  
 次の例では、値が「This is a string.」であるプライベート文字列定数 `s` を含む `DisplayString` クラスを定義します。また、メソッドを実行しているアプリケーション ドメインの名前と共に文字列値とハッシュ コードを表示する `ShowStringHashCode` メソッドも含まれています。  
  
 [!code-csharp[System.String.GetHashCode#2](../../../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.String.GetHashCode/CS/perdomain.cs#2)]
 [!code-vb[System.String.GetHashCode#2](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.String.GetHashCode/VB/perdomain.vb#2)]  
  
 構成ファイルを指定せずにこの例を実行すると、次のような出力が表示されます。  文字列のハッシュ コードが 2 つアプリケーション ドメインで同じであることに注意してください。  
  
```  
  
String 'This is a string.' in domain 'PerDomain.exe': 941BCEAC  
String 'This is a string.' in domain 'NewDomain': 941BCEAC  
  
```  
  
 ただし、例のディレクトリに次の構成ファイルを追加して例を実行すると、同じ文字列のハッシュ コードがアプリケーション ドメインによって異なります。  
  
```  
  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <UseRandomizedStringHashAlgorithm enabled="1" />  
   </runtime>  
</configuration>  
  
```  
  
 構成ファイルが存在する場合、次の出力が表示されます。  
  
```  
  
String 'This is a string.' in domain 'PerDomain.exe': 5435776D  
String 'This is a string.' in domain 'NewDomain': 75CC8236  
  
```  
  
## 参照  
 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.String.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.Object.GetHashCode%2A?displayProperty=fullName>