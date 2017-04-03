---
title: Serializzazione in base a un XmlReader (richiamo di XSLT) (C#) | Documentazione Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 4cc3ee03-ef4c-429b-a408-fedd10b728cd
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 96fed09349264710dc8f0591a0022939e9a4181a
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-to-an-xmlreader-invoking-xslt-c"></a>Serializzazione in base a un XmlReader (richiamo di XSLT) (C#)
Quando si usano le funzionalità di interoperabilità <xref:System.Xml?displayProperty=fullName> di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], è possibile impiegare <xref:System.Xml.Linq.XNode.CreateReader%2A> per creare un <xref:System.Xml.XmlReader>. Il modulo che legge dall'oggetto <xref:System.Xml.XmlReader> creato legge i nodi dell'albero XML e li elabora di conseguenza.  
  
## <a name="invoking-an-xslt-transformation"></a>Richiamo di una trasformazione XSLT  
 Un possibile utilizzo di questo metodo è il richiamo di una trasformazione XSLT. È possibile creare un albero XML, creare un oggetto <xref:System.Xml.XmlReader> dall'albero XML, creare un nuovo documento e quindi creare un oggetto <xref:System.Xml.XmlWriter> per scrivere nel nuovo documento. A questo punto è possibile richiamare la trasformazione XSLT, passando <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter>. Dopo il completamento della trasformazione, il nuovo albero XML viene popolato con i relativi risultati.  
  
```csharp  
string xslMarkup = @"<?xml version='1.0'?>  
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
</xsl:stylesheet>";  
  
XDocument xmlTree = new XDocument(  
    new XElement("Parent",  
        new XElement("Child1", "Child1 data"),  
        new XElement("Child2", "Child2 data")  
    )  
);  
  
XDocument newTree = new XDocument();  
using (XmlWriter writer = newTree.CreateWriter()) {  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione di strutture ad albero XML (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
