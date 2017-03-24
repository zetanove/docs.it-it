---
title: Cenni preliminari sulla classe XElement (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 52331fcd-6023-4d19-b423-7b24f2d86ded
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
ms.openlocfilehash: 4b46f3cb5e0d59105fbc31424a0408c3421d9cac
ms.lasthandoff: 03/13/2017

---
# <a name="xelement-class-overview-visual-basic"></a>Cenni preliminari sulla classe XElement (Visual Basic)
Il <xref:System.Xml.Linq.XElement>è una delle classi fondamentali di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].</xref:System.Xml.Linq.XElement> Rappresenta un elemento XML. Può essere usata per creare elementi, modificare il contenuto dell'elemento, aggiungere, modificare o eliminare elementi figlio, aggiungere attributi a un elemento oppure serializzare il contenuto di un elemento in formato testo. È possibile anche interagire con altre classi di <xref:System.Xml?displayProperty=fullName>, ad esempio <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter>e <xref:System.Xml.Xsl.XslCompiledTransform>.</xref:System.Xml.Xsl.XslCompiledTransform> </xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> </xref:System.Xml?displayProperty=fullName>  
  
## <a name="xelement-functionality"></a>Funzionalità di XElement  
 In questo argomento viene descritta la funzionalità fornita dalla <xref:System.Xml.Linq.XElement>classe.</xref:System.Xml.Linq.XElement>  
  
### <a name="constructing-xml-trees"></a>Costruzione di alberi XML  
 È possibile costruire alberi XML in diversi modi:  
  
-   È possibile costruire un albero XML nel codice. Per ulteriori informazioni, vedere [la creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md).  
  
-   È possibile analizzare il codice XML da origini diverse, incluso un <xref:System.IO.TextReader>, file di testo o un indirizzo Web (URL).</xref:System.IO.TextReader> Per ulteriori informazioni, vedere [l'analisi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md).  
  
-   È possibile utilizzare un <xref:System.Xml.XmlReader>per popolare l'albero.</xref:System.Xml.XmlReader> Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XNode.ReadFrom%2A>.</xref:System.Xml.Linq.XNode.ReadFrom%2A>  
  
-   Se si dispone di un modulo può scrivere contenuto in un <xref:System.Xml.XmlWriter>, è possibile utilizzare il <xref:System.Xml.Linq.XContainer.CreateWriter%2A>per creare un writer, passare il writer al modulo e quindi usare il contenuto che viene scritto il <xref:System.Xml.XmlWriter>per popolare l'albero XML.</xref:System.Xml.XmlWriter> </xref:System.Xml.Linq.XContainer.CreateWriter%2A> </xref:System.Xml.XmlWriter>  
  
 Tuttavia, il modo più comune per creare un albero XML è il seguente:  
  
```vb  
Dim contacts As XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone>206-555-0144</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
 Un'altra tecnica molto comune per la creazione di una struttura ad albero XML implica l'utilizzo dei risultati di una [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query per popolare una struttura ad albero XML, come illustrato nell'esempio seguente:  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where el.Value > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
### <a name="serializing-xml-trees"></a>Serializzazione di strutture ad albero XML  
 È possibile serializzare l'albero XML in un <xref:System.IO.File>, <xref:System.IO.TextWriter>, o un <xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter> </xref:System.IO.TextWriter> </xref:System.IO.File>  
  
 Per ulteriori informazioni, vedere [la serializzazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md).  
  
### <a name="retrieving-xml-data-via-axis-methods"></a>Recupero di dati XML tramite metodi dell'asse  
 È possibile usare metodi dell'asse per recuperare attributi, elementi figlio, elementi discendenti ed elementi predecessori. Le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] vengono eseguite sui metodi dell'asse e forniscono numerose funzionalità flessibili e potenti per spostarsi in un albero XML ed elaborarla.  
  
 Per ulteriori informazioni, vedere [assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md).  
  
### <a name="querying-xml-trees"></a>Esecuzione di query su strutture ad albero XML  
 È possibile scrivere [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query che consentono di estrarre dati da un albero XML.  
  
 Per ulteriori informazioni, vedere [query su strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/querying-xml-trees.md).  
  
### <a name="modifying-xml-trees"></a>Modifica di strutture ad albero XML  
 È possibile modificare un elemento in modi diversi, ad esempio modificandone il contenuto o gli attributi. È inoltre possibile rimuovere un elemento dal relativo elemento padre.  
  
 Per ulteriori informazioni, vedere [la modifica di strutture ad albero XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md).  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Cenni preliminari sulla programmazione XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
