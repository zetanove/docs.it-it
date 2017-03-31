---
title: 'Procedura: Creare una struttura ad albero da un XmlReader (C#) | Documentazione Microsoft'
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
ms.assetid: 60951c9c-7087-406c-b5bb-c60e58609b21
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
ms.openlocfilehash: d94b2238f6908a29efeb2465c1c11babc54a3704
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-tree-from-an-xmlreader-c"></a>Procedura: Creare una struttura ad albero da un XmlReader (C#)
Questo argomento mostra come creare una struttura ad albero XML direttamente da un oggetto <xref:System.Xml.XmlReader>. Per creare un <xref:System.Xml.Linq.XElement> da un <xref:System.Xml.XmlReader>, è necessario posizionare <xref:System.Xml.XmlReader> su un nodo elemento. <xref:System.Xml.XmlReader> ignorerà i commenti e le istruzioni di elaborazione, ma se <xref:System.Xml.XmlReader> è posizionato in un nodo di testo, verrà generato un errore. Per evitare tali errori, posizionare sempre <xref:System.Xml.XmlReader> in un elemento prima di creare la struttura ad albero XML da <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Esempio  
 Questo esempio usa il documento XML seguente: [File XML di esempio: libri (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md).  
  
 Nel codice seguente viene creato un oggetto `T:System.Xml.XmlReader`, quindi vengono letti i nodi fino a individuare il primo nodo di elemento. Viene quindi caricato l'oggetto <xref:System.Xml.Linq.XElement>.  
  
```csharp  
XmlReader r = XmlReader.Create("books.xml");  
while (r.NodeType != XmlNodeType.Element)  
    r.Read();  
XElement e = XElement.Load(r);  
Console.WriteLine(e);  
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
 [Analisi di codice XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)
