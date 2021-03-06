---
title: "Entity SQL と Transact-SQL の相違点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Entity SQL と Transact-SQL の相違点
このトピックでは、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] と [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] の相違点について説明します。  
  
## 継承とリレーションシップのサポート  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、エンティティの概念スキーマを直接操作し、継承やリレーションシップなどの概念モデル機能をサポートします。  
  
 継承を操作するときは、スーパータイプ インスタンスのコレクションからサブタイプのインスタンスを選択すると便利である場合がよくあります。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 内の [oftype](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md) 演算子 \(C\# シーケンスの `oftype` に相当\) によってこの機能が提供されます。  
  
## コレクションのサポート  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、コレクションをファーストクラスのエンティティとして取り扱います。  次に例を示します。  
  
-   コレクションの式は、`from` 句内で有効です。  
  
-   `in` サブクエリと `exists` サブクエリは任意のコレクションを使用できるように一般化されています。  
  
     サブクエリは一種のコレクションです。  `e1 in e2` および `exists(e)` は、これらの演算を実行する [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 構造です。  
  
-   `union`、`intersect`、`except` などの集合演算は、現在ではコレクションに対して実行されます。  
  
-   結合はコレクションに対して実行されます。  
  
## 式のサポート  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] にはサブクエリ \(テーブル\) と式 \(行と列\) があります。  
  
 コレクションおよび入れ子になったコレクションをサポートするために、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではすべてを式として取り扱います。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] よりもコンポーザブルであり、すべての式をどこにでも使用できます。  クエリ式は常に投射型のコレクションとなり、コレクション式が許可されている任意の場所で使用できます。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] でサポートされていない [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 式の詳細については、「[サポートされていない式](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md)」を参照してください。  
  
 次の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] クエリはすべて有効です。  
  
```  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}   
e1 union all e2  
set(e1)  
```  
  
## サブクエリの一貫した処理  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] は、テーブルに重点を置いてサブクエリのコンテキストを解釈します。  たとえば、`from` 句内のサブクエリは、マルチセット \(テーブル\) と見なされます。  ただし、`select` 句で使用される同じサブクエリは、スカラー サブクエリと見なされます。  同様に、`in` 演算子の左側で使用されるサブクエリはスカラー サブクエリと見なされますが、右側で使用されるサブクエリはマルチセット サブクエリと見なされます。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではこれらの違いが排除されます。  式は、使用するコンテキストに依存しない、一貫した方法で解釈されます。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、すべてのサブクエリはマルチセット サブクエリと見なされます。  サブクエリでスカラー値が必要な場合のために、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] には `anyelement` 演算子が用意されています。この演算子はコレクション \(この場合はサブクエリ\) に対して演算を行い、コレクションからシングルトン値を抽出します。  
  
### サブクエリの暗黙の強制型変換の回避  
 サブクエリの一貫した処理に伴う二次的作用として、スカラー値へのサブクエリの暗黙的な変換があります。  具体的には、[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、単一フィールドの行のマルチセットはそのフィールドのデータ型を持つスカラー値に暗黙的に変換されます。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、この暗黙の強制型変換をサポートしていません。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、コレクションからシングルトン値を抽出するための ANYELEMENT 演算子と、クエリ式の実行中に row ラッパーの作成を回避するための `select value` 句が提供されています。  
  
## SELECT VALUE: 暗黙の row ラッパーの回避  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] サブクエリ内の SELECT 句では、句内の項目に row ラッパーを暗黙的に作成します。  これは、スカラーやオブジェクトのコレクションを作成できないことを意味します。  [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、1 つのフィールドの RowType と、同じデータ型のシングルトン値との間の暗黙の強制型変換を許可しています。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] には、暗黙の行の構築をスキップする `select value` 句が用意されています。  `select value` 句には 1 つの項目のみを指定できます。  このような句を使用した場合、`select` 句内の項目には row ラッパーは構築されず、目的の構造を持つコレクションを作成できます。たとえば、`select value a` のように指定します。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] には、任意の行を構築するための行コンストラクターも用意されています。  `select` は、投影の 1 つ以上の要素を受け取り、結果はフィールドを持つデータ レコードになります。次のように指定します。  
  
 `select a, b, c`  
  
## 左の相関関係と別名定義  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、1 つのスコープ内の式 \(`select` または `from` のような単一句\) は同じスコープ内で先に定義された式を参照できません。  一部の SQL 言語仕様 \([!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] を含む\) では、`from` 句でこれらを制限付きでサポートしています。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では `from` 句における左の相関関係を一般化し、一貫した方法でこれらを取り扱います。  `from` 句内の式は、追加の構文を使用せずに、同じ句内で先に作成された定義 \(左側の定義\) を参照できます。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、`group by` 句を伴うクエリにも制限を課しています。  このようなクエリの `select` 句および `having` 句内の式は、別名を使用した場合にのみ `group by` キーを参照できます。  次の構造は [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では有効ですが、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では無効です。  
  
```  
select t.x + t.y from T as t group by t.x + t.y  
```  
  
 これを [!INCLUDE[esql](../../../../../../includes/esql-md.md)] で実行するには、次のように指定します。  
  
```  
select k from T as t group by (t.x + t.y) as k  
```  
  
## テーブル \(コレクション\) の列 \(プロパティ\) の参照  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 内の列の参照は、すべてテーブルの別名を使用して修飾する必要があります。  次の構造は [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では有効ですが、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では無効です \(`a` がテーブル `T` の有効な列である場合\)。  
  
```  
select a from T  
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の形式は次のとおりです。  
  
```  
select t.a as A from T as t  
```  
  
 テーブルの別名は `from` 句では省略できます。  テーブル名は暗黙的な別名として使用されます。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では次の形式も使用できます。  
  
```  
select Tab.a from Tab  
```  
  
## オブジェクト間の移動  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] ではテーブルの列または行の参照に "." 表記を使用します。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではこの表記法を拡張し \(プログラミング言語から借用\)、オブジェクトのプロパティ間の移動をサポートしています。  
  
 たとえば、`p` が Person 型の式である場合、この人の住所の市区町村を参照するには次の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 構文が使用されます。  
  
```  
p.Address.City   
```  
  
## \* のサポートなし  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では修飾されていない \* 構文を行全体の別名としてサポートしており、修飾された \* 構文 \(t.\*\) をそのテーブルのフィールドのショートカットとしてサポートしています。  また、[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では NULL を含む特殊な count\(\*\) 集計も使用できます。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、\* 構造をサポートしていません。  `select * from T` および `select T1.* from T1, T2...` の形式の [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] クエリは、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではそれぞれ `select value t from T as t` および `select value t1 from T1 as t1, T2 as t2...` として表すことができます。  また、これらの構造は継承 \(値の置換可能性\) に対応していますが、`select *` Variant 型では宣言された型の最上位レベルのプロパティに限定されています。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は `count(*)` 集計をサポートしていません。  代わりに、`count(0)` を使用してください。  
  
## Group By への変更  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では `group by` キーの別名定義をサポートしています。  `select` 句および `having` 句内の式は、これらの別名を使用して `group by` キーを参照する必要があります。たとえば、次のような [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 構文があるとします。  
  
```  
select k1, count(t.a), sum(t.a)  
from T as t  
group by t.b + t.c as k1  
```  
  
 これは、次の [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] と同じです。  
  
```  
select b + c, count(*), sum(a)   
from T  
group by b + c  
```  
  
## コレクションベースの集計  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、2 種類の集計をサポートしています。  
  
 コレクションベースの集計は、コレクションに対して演算を行い、集計結果を生成します。  これらはクエリ内の任意の場所で使用でき、`group by` 句を必要としません。  次に例を示します。  
  
```  
select t.a as a, count({1,2,3}) as b from T as t     
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、SQL スタイルの集計もサポートしています。  次に例を示します。  
  
```  
select a, sum(t.b) from T as t group by t.a as a  
```  
  
## ORDER BY 句の使用法  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、ORDER BY 句は最上位の SELECT .. FROM ..  WHERE ブロックでのみ指定できます。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、入れ子になった ORDER BY 式を使用でき、それをクエリ内の任意の場所に配置できますが、入れ子になったクエリ内の順序は保持されません。  
  
```  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## 識別子  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、識別子の比較は現在のデータベースの照合順序に基づきます。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の識別子では、常に大文字と小文字は区別されず、アクセントは区別されます \(つまり、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではアクセントのある文字とアクセントのない文字が区別されます。たとえば 'a' と 'ấ' は等しくありません\)。[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、同じように表示される文字であってもコード ページが異なる場合は、異なる文字と見なされます。  詳細については、「[入力文字セット](../../../../../../docs/framework/data/adonet/ef/language-reference/input-character-set-entity-sql.md)」を参照してください。  
  
## Entity SQL では使用できない Transact\-SQL 機能  
 次の [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 機能は [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では使用できません。  
  
 DML  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は現在、DML ステートメント \(insert、update、delete\) をサポートしていません。  
  
 DDL  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の現在のバージョンでは DDL はサポートされていません。  
  
 命令型プログラミング  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] とは異なり、命令型プログラミングをサポートしていません。  代わりにプログラミング言語を使用します。  
  
 グループ化関数  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではグループ化関数 \(CUBE, ROLLUP、GROUPING\_SET など\) はサポートしていません。  
  
 分析関数  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では分析関数はまだサポートしていません。  
  
 組み込み関数、演算子  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] の組み込み関数と演算子のサブセットをサポートしています。  これらの演算子と関数の多くは、主要なストア プロバイダーによりサポートされています。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、プロバイダー マニフェストで宣言されたストア固有の関数を使用します。  また、[!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] では [!INCLUDE[esql](../../../../../../includes/esql-md.md)] が使用する既存の組み込みストア関数とユーザー定義ストア関数を宣言できます。  
  
 ヒント  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ではクエリ ヒントのメカニズムは提供していません。  
  
 クエリ結果のバッチ処理  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、クエリ結果のバッチ処理はサポートされていません。  たとえば、次の [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] は有効です \(バッチとして送信\)。  
  
```  
select * from products;  
select * from catagories;  
```  
  
 ただし、同等の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] はサポートされていません。  
  
```  
Select value p from Products as p;  
Select value c from Categories as c;  
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、コマンドごとに 1 つの結果生成クエリ ステートメントのみをサポートします。  
  
## 参照  
 [Entity SQL の概要](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [サポートされていない式](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md)