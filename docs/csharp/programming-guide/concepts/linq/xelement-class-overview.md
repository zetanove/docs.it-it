---
title: Panoramica della classe XElement (C#) | Microsoft Docs
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
ms.assetid: 2b9f0cd8-a1d1-4037-accf-0f38a410fa11
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
ms.openlocfilehash: 193ae8193d73d57638835c96c3f7dfd28d320473
ms.lasthandoff: 03/13/2017

---
# <a name="xelement-class-overview-c"></a>Panoramica della classe XElement (C#)
La classe <xref:System.Xml.Linq.XElement> è una delle classi fondamentali di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]. Rappresenta un elemento XML. Può essere usata per creare elementi, modificare il contenuto dell'elemento, aggiungere, modificare o eliminare elementi figlio, aggiungere attributi a un elemento oppure serializzare il contenuto di un elemento in formato testo. È possibile interagire anche con altre classi di <xref:System.Xml?displayProperty=fullName>, ad esempio <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> e <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
## <a name="xelement-functionality"></a>Funzionalità di XElement  
 In questo argomento viene descritta la funzionalità definita dalla classe <xref:System.Xml.Linq.XElement>.  
  
### <a name="constructing-xml-trees"></a>Costruzione di alberi XML  
 È possibile costruire alberi XML in diversi modi:  
  
-   È possibile costruire un albero XML nel codice. Per altre informazioni, vedere [Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md).  
  
-   È possibile analizzare il codice XML di origini diverse, ad esempio un oggetto <xref:System.IO.TextReader>, file di testo o un indirizzo Web (URL). Per altre informazioni, vedere [Analisi di codice XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md).  
  
-   È possibile usare un oggetto <xref:System.Xml.XmlReader> per popolare l'albero. Per altre informazioni, vedere <xref:System.Xml.Linq.XNode.ReadFrom%2A>.  
  
-   Se si usa un modulo in grado di scrivere contenuto in un oggetto <xref:System.Xml.XmlWriter>, è possibile usare il metodo <xref:System.Xml.Linq.XContainer.CreateWriter%2A> per creare un writer, passare il writer al modulo e quindi usare il contenuto scritto in <xref:System.Xml.XmlWriter> per popolare l'albero XML.  
  
 Tuttavia, il modo più comune per creare un albero XML è il seguente:  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 Un'altra tecnica molto comune per la creazione di un albero XML implica l'uso dei risultati di una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per popolare un albero XML, come illustrato nell'esempio seguente:  
  
```csharp  
XElement srcTree = new XElement("Root",  
    new XElement("Element", 1),  
    new XElement("Element", 2),  
    new XElement("Element", 3),  
    new XElement("Element", 4),  
    new XElement("Element", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    from el in srcTree.Elements()  
    where (int)el > 2  
    select el  
);  
Console.WriteLine(xmlTree);  
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
 È possibile serializzare l'albero XML in un oggetto <xref:System.IO.File>, <xref:System.IO.TextWriter> o <xref:System.Xml.XmlWriter>.  
  
 Per altre informazioni, vedere l'articolo sulla [serializzazione delle strutture ad albero XML in C#](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md).  
  
### <a name="retrieving-xml-data-via-axis-methods"></a>Recupero di dati XML tramite metodi dell'asse  
 È possibile usare metodi dell'asse per recuperare attributi, elementi figlio, elementi discendenti ed elementi predecessori. Le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] vengono eseguite sui metodi dell'asse e forniscono numerose funzionalità flessibili e potenti per spostarsi in un albero XML ed elaborarla.  
  
 Per altre informazioni, vedere [Assi LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md).  
  
### <a name="querying-xml-trees"></a>Esecuzione di query su strutture ad albero XML  
 È possibile scrivere query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per estrarre dati da un albero XML.  
  
 Per altre informazioni, vedere [Esecuzione di query su strutture ad albero XML (C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md).  
  
### <a name="modifying-xml-trees"></a>Modifica di strutture ad albero XML  
 È possibile modificare un elemento in modi diversi, ad esempio modificandone il contenuto o gli attributi. È inoltre possibile rimuovere un elemento dal relativo elemento padre.  
  
 Per altre informazioni, vedere [Modifica degli alberi XML (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica della programmazione con LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
