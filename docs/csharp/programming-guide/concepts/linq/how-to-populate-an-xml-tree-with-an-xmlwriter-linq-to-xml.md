---
title: 'Procedura: Popolare un albero XML con XmlWriter (LINQ to XML) (C#) | Microsoft Docs'
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
ms.assetid: cd5674d1-5c54-4efc-ba68-e23b2875295f
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
ms.openlocfilehash: 225aa8a39a973ba8d4f199ccfce68e2dc16d8aa2
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-c"></a>Procedura: Popolare un albero XML con XmlWriter (LINQ to XML) (C#)
Per popolare un albero XML è possibile usare <xref:System.Xml.Linq.XContainer.CreateWriter%2A> per creare un <xref:System.Xml.XmlWriter> e quindi scrivere in <xref:System.Xml.XmlWriter>. L'albero XML viene popolato con tutti i nodi scritti in <xref:System.Xml.XmlWriter>.  
  
 In genere si usa questo metodo quando si usa [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] con un'altra classe che prevede di scrivere in <xref:System.Xml.XmlWriter>, ad esempio <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
## <a name="example"></a>Esempio  
 È possibile usare <xref:System.Xml.Linq.XContainer.CreateWriter%2A> per richiamare una trasformazione XSLT. In questo esempio vengono creati un albero XML, un oggetto <xref:System.Xml.XmlReader> dall'albero XML, un nuovo documento e infine un oggetto <xref:System.Xml.XmlWriter> per scrivere nel nuovo documento. In seguito viene richiamata la trasformazione XSLT, passando <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter>. Dopo il completamento della trasformazione, il nuovo albero XML viene popolato con i relativi risultati.  
  
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
using (XmlWriter writer = newTree.CreateWriter())  
{  
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
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A>   
 <xref:System.Xml.XmlWriter>   
 <xref:System.Xml.Xsl.XslCompiledTransform>   
 [Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)
