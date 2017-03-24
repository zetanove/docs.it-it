---
title: Utilizzo di XSLT per trasformare un albero XML (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 3390ca68-c270-4e1d-b64b-6a063a77017c
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
ms.openlocfilehash: 226a802cd640f2f251e1849486dab4a5c4af3497
ms.lasthandoff: 03/13/2017

---
# <a name="using-xslt-to-transform-an-xml-tree-visual-basic"></a>Utilizzo di XSLT per trasformare un albero XML (Visual Basic)
È possibile creare una struttura ad albero XML, creare un <xref:System.Xml.XmlReader>dall'albero XML, creare un nuovo documento e creare un <xref:System.Xml.XmlWriter>che scriverà nel documento nuovo.</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> Quindi, è possibile richiamare la trasformazione XSLT, passando il <xref:System.Xml.XmlReader>e <xref:System.Xml.XmlWriter>alla trasformazione.</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> Dopo il completamento della trasformazione, il nuovo albero XML viene popolato con i relativi risultati.  
  
## <a name="example"></a>Esempio  
  
```vb  
Dim xslMarkup As XDocument = _   
    <?xml version='1.0'?>  
    <xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
        <xsl:template match='/Parent'>  
            <Root>  
                <C1>  
                    <xsl:value-of select='Child1'/>  
                </C1>  
                <C2>  
                    <xsl:value-of select='Child2'/>  
                </C2>  
            </Root>  
        </xsl:template>  
    </xsl:stylesheet>  
  
Dim xmlTree As XElement = _   
    <Parent>  
        <Child1>Child1 data</Child1>  
        <Child2>Child2 data</Child2>  
    </Parent>  
  
Dim newTree As XDocument = New XDocument()  
  
Using writer As XmlWriter = newTree.CreateWriter()  
    ' Load the style sheet.  
    Dim xslt As XslCompiledTransform = _  
        New XslCompiledTransform()  
    xslt.Load(xslMarkup.CreateReader())  
  
    ' Execute the transform and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer)  
End Using  
  
Console.WriteLine(newTree)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.CreateWriter%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XNode.CreateReader%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.CreateReader%2A?displayProperty=fullName>   
 [LINQ to XML (Visual Basic) di programmazione avanzata](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
