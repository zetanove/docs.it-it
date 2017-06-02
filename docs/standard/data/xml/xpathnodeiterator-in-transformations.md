---
title: "XPathNodeIterator nelle trasformazioni | Microsoft Docs"
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
ms.assetid: 2bc6ddc6-674a-4f75-b264-abc35e4e5857
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XPathNodeIterator nelle trasformazioni
La classe <xref:System.Xml.XPath.XPathNodeIterator> fornisce i metodi per eseguire un'iterazione in un set di nodi creato come risultato di una query XPath \(XML Path Language\) o un frammento di albero risultato convertito in un set di nodi usando il metodo node\-set.  La classe <xref:System.Xml.XPath.XPathNodeIterator> consente di eseguire un'iterazione tra i nodi all'interno di quel determinato set.  Una volta recuperato il set di nodi, la classe <xref:System.Xml.XPath.XPathNodeIterator> fornisce al set di nodi selezionato un cursore forward\-only di sola lettura.  Il set di nodi viene creato in base all'ordine con cui è riportato nel documento, quindi la chiamata a questo metodo consente di spostarsi al nodo successivo nell'ordine del documento.  L'oggetto <xref:System.Xml.XPath.XPathNodeIterator> non compila un albero con tutti i nodi del set,  bensì fornisce una finestra per i dati di ogni singolo nodo, esponendo il nodo sottostante a cui si riferisce quando il cursore viene spostato all'interno dell'albero.  I metodi e le proprietà disponibili nella classe <xref:System.Xml.XPath.XPathNodeIterator> consentono di ottenere informazioni dal nodo corrente.  Per un elenco dei metodi e delle proprietà disponibili, vedere [Membri XPathNodeIterator](frlrfsystemxmlxpathxpathnodeiteratormemberstopic).  
  
 Poiché <xref:System.Xml.XPath.XPathNodeIterator> si sposta in un set di nodi creato da una query XPath e scorre solo in avanti, per spostarsi è necessario usare il metodo <xref:System.Xml.XPath.XPathNodeIterator.MoveNext%2A>.  Il tipo restituito dal metodo è `Boolean`, con valore `true` se viene eseguito lo spostamento al nodo successivo selezionato e `false` se non vi sono altri nodi selezionati.  Se viene restituito `true`, nell'elenco seguente verranno illustrate le proprietà disponibili:  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.Current%2A>  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.CurrentPosition%2A>  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.Count%2A>  
  
 La prima volta che si visualizza un set di nodi, è necessario eseguire una chiamata al metodo <xref:System.Xml.XPath.XPathNodeIterator.MoveNext%2A> per posizionare il tipo <xref:System.Xml.XPath.XPathNodeIterator> sul primo nodo del set selezionato.  In questo modo è possibile scrivere un ciclo while.  
  
 Nell'esempio di codice seguente viene descritto come passare un tipo <xref:System.Xml.XPath.XPathNodeIterator> a un <xref:System.Xml.Xsl.XslTransform> come parametro nel tipo <xref:System.Xml.Xsl.XsltArgumentList>.  L'input per il codice è **books.xml** e il foglio di stile è **text.xsl**.  Il file **test.xml** è il tipo <xref:System.Xml.XPath.XPathDocument>.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
  
Public Class sample  
  
   Public Shared Sub Main()  
      Dim Doc As New XPathDocument("books.xml")  
      Dim nav As XPathNavigator = Doc.CreateNavigator()  
      Dim Iterator As XPathNodeIterator = nav.Select("/bookstore/book")  
  
      Dim arg As New XsltArgumentList()  
      arg.AddParam("param1", "", Iterator)  
  
      Dim xslt As New XslTransform()  
      xslt.Load("test.xsl")  
  
      Dim xd As New XPathDocument("test.xml")  
  
      Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
      xslt.Transform(xd, arg, strmTemp, Nothing)  
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
        XPathDocument Doc = new XPathDocument("books.xml");  
        XPathNavigator nav = Doc.CreateNavigator();  
        XPathNodeIterator Iterator = nav.Select("/bookstore/book");  
  
        XsltArgumentList arg = new XsltArgumentList();  
        arg.AddParam("param1", "", Iterator);  
  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, arg, strmTemp, null);  
    }  
}  
```  
  
## books.xml  
  
```  
<?xml version='1.0'?>  
<!-- This file represents a fragment of a book store inventory database. -->  
<bookstore specialty="novel">  
    <book style="autobiography">  
    <title>Seven Years in Trenton</title>  
        <author>  
            <first-name>Jay</first-name>  
            <last-name>Adams</last-name>  
            <award>Trenton Literary Review Honorable Mention</award>  
            <country>USA</country>  
        </author>  
        <price>12</price>  
    </book>  
    <book style="textbook">  
        <title>History of Trenton</title>  
        <author>  
            <first-name>Kim</first-name>  
            <last-name>Akers</last-name>  
            <publication>  
                Selected Short Stories of  
                <first-name>Scott</first-name>  
                <last-name>Bishop</last-name>  
                <country>US</country>  
            </publication>  
        </author>  
        <price>55</price>  
    </book>  
</bookstore>  
```  
  
## test.xsl  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
xmlns:msxsl="urn:schemas-microsoft-com:xslt" exclude-result-prefixes="msxsl">  
  
<xsl:output method="xml" indent="yes"/>  
<xsl:param name="param1"/>  
  
<xsl:template match="/">  
    <out>  
        <xsl:for-each select="$param1/title">  
            <title><xsl:value-of select="."/></title>  
        </xsl:for-each>  
    </out>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
## test.xml  
  
```  
<Title attr="Test">this is a test</Title>  
```  
  
## Output \(out.xml\)  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<out>  
  <title>Seven Years in Trenton</title>  
  <title>History of Trenton</title>  
</out>  
```  
  
## Vedere anche  
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)