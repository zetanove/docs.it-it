---
title: "Set di nodi nelle trasformazioni | Microsoft Docs"
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
ms.assetid: ad034f0e-ff8b-4a71-9a4c-528c754263c4
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Set di nodi nelle trasformazioni
I set di nodi sono uno dei quattro tipi di dati principali restituiti dalle espressioni XPath \(XML Path Language\). Un set di nodi, ovvero una raccolta di nodi non ordinati senza duplicati e creati in base all'ordine con cui sono riportati del documento, può essere assegnato a una variabile in un foglio di stile.  
  
> [!NOTE]
>  La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]. È possibile eseguire le trasformazioni XSLT \(Extensible Stylesheet Language for Transformations\) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>. Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 I set di nodi sono uno dei quattro tipi di dati principali restituiti dalle espressioni XPath. Un set di nodi, ovvero una raccolta di nodi non ordinati senza duplicati e creati in base all'ordine con cui sono riportati del documento, può essere assegnato a una variabile in un foglio di stile. Il set di nodi risultante da un'espressione XPath usata in un attributo `select` per una trasformazione ha lo stesso comportamento di un set di nodi proveniente dal DOM \(Document Object Model\) XML. È possibile spostarsi all'interno di un set di nodi tramite i metodi illustrati in [Navigazione del set di nodi con XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md), mentre per la navigazione di un frammento di nodi o di un frammento di albero risultato è necessario usare il tipo <xref:System.Xml.XPath.XPathNodeIterator>.  
  
 Nell'esempio di codice seguente viene illustrato come scorrere un set di nodi quando un elemento `variable` o `parameter` di un foglio di stile viene valutato come set di nodi.  
  
## Foglio di stile  
  
```  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
    <xsl:variable name="x" select="bookstore/book/title"></xsl:variable>  
  
    <xsl:template match="/">  
        <xsl:for-each select="$x">  
            ******  
            <xsl:value-of select="."></xsl:value-of>  
            ******  
        </xsl:for-each>  
    </xsl:template>  
  
</xsl:stylesheet>  
```  
  
## Input  
  
```  
<bookstore>  
   <book style="autobiography">  
      <title>Seven Years in Trenton</title>  
   </book>  
  
   <book style="autobiography">  
      <title>Seven Years in Trenton2</title>  
   </book>  
  
   <book style="textbook">  
      <title>History of Trenton Vol 3</title>  
   </book>  
</bookstore>  
```  
  
## Output  
  
```  
******  
Seven Years in Trenton  
******  
  
******  
Seven Years in Trenton2  
******  
  
******  
History of Trenton Vol 3  
******  
```  
  
## Vedere anche  
 <xref:System.Xml.XPath.XPathNodeIterator>   
 [Trasformazioni XSLT con la classe XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)