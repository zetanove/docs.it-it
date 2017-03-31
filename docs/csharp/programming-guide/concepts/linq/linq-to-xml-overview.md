---
title: Panoramica di LINQ to XML (C#) | Microsoft Docs
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
ms.assetid: 716b94d3-0091-4de1-8e05-41bc069fa9dd
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
ms.openlocfilehash: 05a1eab1470094405f66345515c275edfb26da45
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-overview-c"></a>Panoramica di LINQ to XML (C#)
XML è stato ampiamente adottato per la formattazione dei dati in una vasta gamma di contesti. Viene ad esempio usato in applicazioni Web, file di configurazione, file di Microsoft Office Word e in database.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] costituisce un approccio aggiornato e ridisegnato alla programmazione con XML. Fornisce funzionalità di modifica dei documenti in memoria di Document Object Model (DOM) e supporta espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]. Sebbene sintatticamente diverse da XPath, queste espressioni di query offrono funzionalità simili.  
  
## <a name="linq-to-xml-developers"></a>Sviluppatori LINQ to XML  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è destinato a diversi tipi di sviluppatori. Per un sviluppatore medio che desidera solo poter eseguire una determinata operazione, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] semplifica il codice XML e consente di eseguire query in modo simile a SQL. Sono poi sufficienti competenze minime per consentire a un programmatore di imparare a scrivere query potenti e meno estese nel linguaggio di programmazione desiderato.  
  
 Gli sviluppatori professionisti possono usare [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per incrementare notevolmente la propria produttività. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consente di scrivere una minor quantità di codice, che tuttavia risulta più espressivo, compatto e potente. È inoltre possibile usare espressioni di query da più domini di dati contemporaneamente.  
  
## <a name="what-is-linq-to-xml"></a>Informazioni su LINQ to XML  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è un'interfaccia di programmazione XML in memoria con supporto LINQ che consente di usare codice XML dall'interno dei linguaggi di programmazione di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è simile al modello DOM (Document Object Model) in quanto porta in memoria il documento XML. È quindi possibile eseguire query e modificare il documento e dopo averlo modificato salvarlo in un file o serializzarlo e inviarlo tramite Internet. Tuttavia, a differenza di DOM, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] offre un nuovo modello a oggetti più leggero e facile da usare che sfrutta le funzionalità del linguaggio in C#.  
  
 Il principale vantaggio di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è costituito dall'integrazione con [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]. Grazie a tale integrazione è possibile scrivere query sul documento XML in memoria per recuperare raccolte di elementi e di attributi. La funzionalità di query di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è paragonabile a XPath e XQuery, dal punto di vista funzionale ma non sintattico. L'integrazione di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] in C# offre una tipizzazione più forte, il controllo in fase di compilazione e il supporto migliorato del debugger.  
  
 Un altro vantaggio di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è costituito dalla possibilità di usare i risultati delle query come parametri di costruttori di oggetti <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XAttribute> offrendo un approccio efficace per la creazione di alberi XML. Questo approccio, chiamato *costruzione funzionale* consente agli sviluppatori di trasformare facilmente gli alberi XML da una forma all'altra.  
  
 Ad esempio, è possibile avere un ordine d'acquisto XML tipico come descritto in [Sample XML File: Typical Purchase Order (LINQ to XML)](http://msdn.microsoft.com/library/0606c09f-6e43-4f8d-95c8-e8e2e08d2348) (File XML di esempio: ordine d'acquisto tipico (LINQ to XML). Usando [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], è possibile eseguire la query seguente per ottenere il valore dell'attributo relativo al numero di parte di ciascun articolo incluso dell'ordine di acquisto:  
  
```csharp  
IEnumerable<string> partNos =  
from item in purchaseOrder.Descendants("Item")  
select (string) item.Attribute("PartNumber");  
```  
  
 Si supponga ancora, ad esempio, di voler creare un elenco, ordinato in base al numero di parte, degli articoli il cui valore è maggiore di 100 dollari. Per ottenere queste informazioni, è possibile eseguire la query seguente:  
  
```csharp  
IEnumerable<XElement> partNos =  
from item in purchaseOrder.Descendants("Item")  
where (int) item.Element("Quantity") *  
    (decimal) item.Element("USPrice") > 100  
orderby (string)item.Element("PartNumber")  
select item;  
```  
  
 Oltre alle funzionalità [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] include un'interfaccia di programmazione XML migliorata. Usando [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile:  
  
-   Caricare codice XML da file o flussi.  
  
-   Serializzare codice XML in file o flussi.  
  
-   Creare codice XML nuovo usando la costruzione funzionale.  
  
-   Eseguire una query su codice XML usando assi simili a XPath.  
  
-   Modificare l'albero XML in memoria usando metodi come <xref:System.Xml.Linq.XContainer.Add%2A>, <xref:System.Xml.Linq.XNode.Remove%2A>, <xref:System.Xml.Linq.XNode.ReplaceWith%2A> e <xref:System.Xml.Linq.XElement.SetValue%2A>.  
  
-   Convalidare alberi XML usando lo schema XSD.  
  
-   Usare una combinazione di queste funzionalità per trasformare strutture ad albero XML da una forma in un altra.  
  
## <a name="creating-xml-trees"></a>Creazione di strutture ad albero XML  
 Uno dei vantaggi più significativi della programmazione con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è rappresentato dalla facilità con cui è possibile creare alberi XML. Ad esempio, per creare un piccolo albero XML, è possibile scrivere il codice seguente:  
  
```csharp  
XElement contacts =  
new XElement("Contacts",  
    new XElement("Contact",  
        new XElement("Name", "Patrick Hines"),  
        new XElement("Phone", "206-555-0144",   
            new XAttribute("Type", "Home")),  
        new XElement("phone", "425-555-0145",  
            new XAttribute("Type", "Work")),  
        new XElement("Address",  
            new XElement("Street1", "123 Main St"),  
            new XElement("City", "Mercer Island"),  
            new XElement("State", "WA"),  
            new XElement("Postal", "68042")  
        )  
    )  
);  
```  
  
 Per altre informazioni, vedere [Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq>   
 [Introduzione (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/getting-started-linq-to-xml.md)
