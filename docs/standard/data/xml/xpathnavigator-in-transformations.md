---
title: "変換における XPathNavigator | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 118f97d1-7110-4d1b-b0bd-4143252c0bb0
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 変換における XPathNavigator
<xref:System.Xml.XPath.XPathNavigator> クラスは、データへの読み取り専用のランダム アクセスを提供し、XSLT \(Extensible Stylesheet Language for Transformations\) への入力として使用することを目的に設計されています。  このクラスは、<xref:System.Xml.XPath.XPathDocument>、<xref:System.Xml.XmlDataDocument>、および <xref:System.Xml.XmlDocument> に実装されます。  <xref:System.Xml.XPath.XPathNavigator> は、『XML Path Language \(XPath\)』勧告のセクション 5 で規定されている W3C \(World Wide Web Consortium\) データ モデルに準拠しています。  
  
 <xref:System.Xml.XPath.XPathNavigator> は、任意のストアに対するカーソル モデルを定義し、任意のデータ ストアに対する高速で読み取り専用の XPath クエリを提供します。  <xref:System.Xml.XPath.XPathNavigator> クラスは、結果ツリー フラグメントの反復処理でも使用されます。  
  
 この API を使用すると、ストア内の現在のノードから情報を取得し、接続されているノードに移動することができます。  <xref:System.Xml.XPath.XPathNavigator> は、一連の **Move** メソッドを使用してストアの走査を実行するカーソル スタイルのモデルです。  <xref:System.Xml.XPath.XPathNavigator> は、常にノード上に配置されます。  **Move** メソッドが失敗した場合、<xref:System.Xml.XPath.XPathNavigator> は変更されません。  
  
 <xref:System.Xml.XPath.XPathNavigator> クラスは、結果ツリー フラグメントの反復処理で使用されます。  XML を含む `fragment` パラメーターを指定して関数を呼び出すことにより、スタイル シート内で結果ツリー フラグメントを作成するコード サンプルを次に示します。  
  
## test.xsl  
  
```  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl ="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.adventure-works.com"  
                version="1.0">  
  
<xsl:variable name="fragment">  
    <authorlist>  
       <author>Joe</author>  
    </authorlist>  
</xsl:variable>  
  
<msxsl:script language="C#" implements-prefix="user">  
<![CDATA[  
   string NodeFragment(XPathNavigator nav)  
   {  
      if (nav.HasChildren)  
        return nav.Value;  
      else  
        return "";  
   }  
]]>  
</msxsl:script>  
  
<xsl:template match="/">  
     <xsl:value-of select="user:NodeFragment($fragment)"/>  
</xsl:template>  
  
</xsl:stylesheet>  
  
```  
  
## test.xml  
  
```  
<root>Some text</root>  
```  
  
 次の例では、**test.xsl** スタイル シートと **test.xml** 入力データを使用しています。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
Public Class sample  
  
    Public Shared Sub Main()  
        Dim xslt As New XslTransform()  
        xslt.Load("test.xsl")  
  
        Dim xd As New XPathDocument("test.xml")  
  
        Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
        xslt.Transform(xd, Nothing, strmTemp, Nothing)  
    End Sub 'Main  
End Class 'sample  
  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Xsl;  
using System.Xml.XPath;  
using System.Text;  
  
public class sample  
{  
    public static void Main()  
    {  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, null, strmTemp, null);  
    }  
}  
```  
  
## 出力  
 変換結果はファイル **out.xml** に出力されます。  
  
```  
<?xml version="1.0" encoding="utf-8"?>Joe  
  
```  
  
## 参照  
 [XslTransform クラスによる XSLT プロセッサの実装](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)