---
title: 'Procedura: creare una struttura ad albero da XmlReader (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 6de683d8-177d-402b-b0de-d0539f1ce5d8
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
ms.openlocfilehash: a8dff4e518d8850b4050389e5677ac81ecd1e074
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-tree-from-an-xmlreader-visual-basic"></a>Procedura: creare una struttura ad albero da XmlReader (Visual Basic)
In questo argomento viene illustrato come creare una struttura ad albero XML direttamente da un <xref:System.Xml.XmlReader>.</xref:System.Xml.XmlReader> Per creare un <xref:System.Xml.Linq.XElement>da un <xref:System.Xml.XmlReader>, è necessario posizionare il <xref:System.Xml.XmlReader>su un nodo elemento.</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> </xref:System.Xml.Linq.XElement> Il <xref:System.Xml.XmlReader>ignorerà i commenti e istruzioni di elaborazione, ma se il <xref:System.Xml.XmlReader>è posizionato in un nodo di testo, verrà generato un errore.</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> Per evitare tali errori, posizionare <xref:System.Xml.XmlReader>su un elemento prima di creare una struttura ad albero XML da <xref:System.Xml.XmlReader>.</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader>  
  
## <a name="example"></a>Esempio  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: libri (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md).  
  
 Nel codice seguente viene creato un oggetto `T:System.Xml.XmlReader`, quindi vengono letti i nodi fino a individuare il primo nodo di elemento. Viene quindi caricato il <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim r As XmlReader = XmlReader.Create("books.xml")  
Do While r.NodeType <> XmlNodeType.Element  
    r.Read()  
Loop  
Dim e As XElement = XElement.Load(r)  
Console.WriteLine(e)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Catalog>  
   <Book id="bk101">  
      <Author>Garghentini, Davide</Author>  
      <Title>XML Developer's Guide</Title>  
      <Genre>Computer</Genre>  
      <Price>44.95</Price>  
      <PublishDate>2000-10-01</PublishDate>  
      <Description>An in-depth look at creating applications   
      with XML.</Description>  
   </Book>  
   <Book id="bk102">  
      <Author>Garcia, Debra</Author>  
      <Title>Midnight Rain</Title>  
      <Genre>Fantasy</Genre>  
      <Price>5.95</Price>  
      <PublishDate>2000-12-16</PublishDate>  
      <Description>A former architect battles corporate zombies,   
      an evil sorceress, and her own childhood to become queen   
      of the world.</Description>  
   </Book>  
</Catalog>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
