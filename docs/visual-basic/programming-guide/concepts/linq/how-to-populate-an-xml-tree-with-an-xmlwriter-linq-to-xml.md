---
title: 'Procedura: popolare una struttura ad albero XML con un XmlWriter (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 5792a0eb-94ee-440d-b601-58cca8c0ee0b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dfd10ec04e7293d90929d6f629201868028819ad
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-visual-basic"></a>Procedura: popolare una struttura ad albero XML con un XmlWriter (LINQ to XML) (Visual Basic)
Per popolare una struttura ad albero XML è possibile utilizzare <xref:System.Xml.Linq.XContainer.CreateWriter%2A>per creare un <xref:System.Xml.XmlWriter>e quindi scrivere in <xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlWriter> </xref:System.Xml.Linq.XContainer.CreateWriter%2A> La struttura ad albero XML viene popolato con tutti i nodi scritti in <xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter>  
  
 In genere si utilizza questo metodo quando si utilizza [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] con un'altra classe che prevede di scrivere in un <xref:System.Xml.XmlWriter>, ad esempio <xref:System.Xml.Xsl.XslCompiledTransform>.</xref:System.Xml.Xsl.XslCompiledTransform> </xref:System.Xml.XmlWriter>  
  
## <a name="example"></a>Esempio  
 Un possibile utilizzo di <xref:System.Xml.Linq.XContainer.CreateWriter%2A>è il richiamo di una trasformazione XSLT.</xref:System.Xml.Linq.XContainer.CreateWriter%2A> In questo esempio viene creato un albero XML, un <xref:System.Xml.XmlReader>dall'albero XML, crea un nuovo documento e quindi crea un <xref:System.Xml.XmlWriter>da scrivere nel documento nuovo.</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> Viene quindi richiamata la trasformazione XSLT, passando <xref:System.Xml.XmlReader>e <xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> Dopo il completamento della trasformazione, il nuovo albero XML viene popolato con i relativi risultati.  
  
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
  
Dim xmlTree As XDocument = _  
    <?xml version='1.0'?>  
    <Parent>  
        <Child1>Child1 data</Child1>  
        <Child2>Child2 data</Child2>  
    </Parent>  
  
Dim newTree As XDocument = New XDocument()  
Using writer As XmlWriter = newTree.CreateWriter()  
    ' Load the style sheet.  
    Dim xslt As XslCompiledTransform = New XslCompiledTransform()  
    xslt.Load(xslMarkup.CreateReader())  
  
    ' Execute the transformation and output the results to a writer.  
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
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A></xref:System.Xml.Linq.XContainer.CreateWriter%2A>   
 <xref:System.Xml.XmlWriter></xref:System.Xml.XmlWriter>   
 <xref:System.Xml.Xsl.XslCompiledTransform></xref:System.Xml.Xsl.XslCompiledTransform>   
 [Creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
