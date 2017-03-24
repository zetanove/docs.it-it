---
title: Panoramica LINQ to XML (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 502661e0-bc5d-438d-94c2-7efb63bb6fbd
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
ms.openlocfilehash: 05d756bc5cd7655a5220c3564d120f90a59ce901
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-overview-visual-basic"></a>Panoramica LINQ to XML (Visual Basic)
XML è stato ampiamente adottato per la formattazione dei dati in una vasta gamma di contesti. Viene ad esempio usato in applicazioni Web, file di configurazione, file di Microsoft Office Word e in database.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] costituisce un approccio aggiornato e ridisegnato alla programmazione con XML. Fornisce funzionalità di modifica dei documenti in memoria di Document Object Model (DOM) e supporta espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]. Sebbene sintatticamente diverse da XPath, queste espressioni di query offrono funzionalità simili.  
  
## <a name="linq-to-xml-developers"></a>Sviluppatori LINQ to XML  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è destinato a diversi tipi di sviluppatori. Per un sviluppatore medio che desidera solo poter eseguire una determinata operazione, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] semplifica il codice XML e consente di eseguire query in modo simile a SQL. Sono poi sufficienti competenze minime per consentire a un programmatore di imparare a scrivere query potenti e meno estese nel linguaggio di programmazione desiderato.  
  
 Gli sviluppatori professionisti possono usare [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per incrementare notevolmente la propria produttività. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consente di scrivere una minor quantità di codice, che tuttavia risulta più espressivo, compatto e potente. È inoltre possibile usare espressioni di query da più domini di dati contemporaneamente.  
  
## <a name="what-is-linq-to-xml"></a>Informazioni su LINQ to XML  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è un'interfaccia di programmazione XML in memoria con supporto LINQ che consente di usare codice XML dall'interno dei linguaggi di programmazione di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]è ad esempio il modello DOM (Document Object) in quanto porta in memoria il documento XML. È quindi possibile eseguire query e modificare il documento e dopo averlo modificato salvarlo in un file o serializzarlo e inviarlo tramite Internet. Tuttavia, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] diverso da DOM: fornisce un nuovo modello a oggetti più leggero e facile da usare con, e che si avvale delle funzionalità del linguaggio Visual Basic.  
  
 Il principale vantaggio di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è costituito dall'integrazione con [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]. Grazie a tale integrazione è possibile scrivere query sul documento XML in memoria per recuperare raccolte di elementi e di attributi. La funzionalità di query di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è paragonabile a XPath e XQuery, dal punto di vista funzionale ma non sintattico. L'integrazione di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] in Visual Basic fornisce più forte tipizzazione, in fase di compilazione, controllo e supporto migliorato del debugger.  
  
 Un altro vantaggio di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è la possibilità di usare i risultati della query come parametri <xref:System.Xml.Linq.XElement>e <xref:System.Xml.Linq.XAttribute>costruttori di oggetti consente un approccio potente per la creazione di strutture ad albero XML.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> Questo approccio, denominato *costruzione funzionale*, consente agli sviluppatori di trasformare facilmente alberi XML da una forma a un'altra.  
  
 Ad esempio, potrebbe essere un file XML tipico ordine di acquisto come descritto in [File XML di esempio: tipico ordine di acquisto (LINQ to XML)](http://msdn.microsoft.com/library/0606c09f-6e43-4f8d-95c8-e8e2e08d2348). Usando [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], è possibile eseguire la query seguente per ottenere il valore dell'attributo relativo al numero di parte di ciascun articolo incluso dell'ordine di acquisto:  
  
```vb  
Dim partNos = _  
    From item In purchaseOrder...<Item> _  
    Select item.@PartNumber  
```  
  
 Si supponga ancora, ad esempio, di voler creare un elenco, ordinato in base al numero di parte, degli articoli il cui valore è maggiore di&100; dollari. Per ottenere queste informazioni, è possibile eseguire la query seguente:  
  
```vb  
Dim partNos = _  
From item In purchaseOrder...<Item> _  
Where (item.<Quantity>.Value * _  
       item.<USPrice>.Value) > 100 _  
Order By item.<PartNumber>.Value _  
Select item  
```  
  
 Oltre a queste [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] funzionalità, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] fornisce un'interfaccia di programmazione XML migliorata. Usando [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile:  
  
-   Caricare codice XML da file o flussi.  
  
-   Serializzare codice XML in file o flussi.  
  
-   Creare codice XML nuovo usando la costruzione funzionale.  
  
-   Eseguire una query su codice XML usando assi simili a XPath.  
  
-   Modificare la struttura ad albero XML in memoria usando metodi, ad esempio <xref:System.Xml.Linq.XContainer.Add%2A>, <xref:System.Xml.Linq.XNode.Remove%2A>, <xref:System.Xml.Linq.XNode.ReplaceWith%2A>e <xref:System.Xml.Linq.XElement.SetValue%2A>.</xref:System.Xml.Linq.XElement.SetValue%2A> </xref:System.Xml.Linq.XNode.ReplaceWith%2A> </xref:System.Xml.Linq.XNode.Remove%2A> </xref:System.Xml.Linq.XContainer.Add%2A>  
  
-   Convalidare alberi XML usando lo schema XSD.  
  
-   Usare una combinazione di queste funzionalità per trasformare strutture ad albero XML da una forma in un altra.  
  
## <a name="creating-xml-trees"></a>Creazione di strutture ad albero XML  
 Uno dei vantaggi più significativi della programmazione con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è rappresentato dalla facilità con cui è possibile creare alberi XML. Ad esempio, per creare un piccolo albero XML, è possibile scrivere codice come segue:  
  
```vb  
Dim contacts = _  
<Contacts>  
    <Contact>  
        <Name>Patrick Hines</Name>  
        <Phone Type="Home">206-555-0144</Phone>  
        <Phone Type="Work">425-555-0145</Phone>  
        <Address>  
            <Street1>123 Main St</Street1>  
            <City>Mercer Island</City>  
            <State>WA</State>  
            <Postal>68042</Postal>  
        </Address>  
    </Contact>  
</Contacts>  
```  
  
 Il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte i valori letterali XML in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] chiamate al metodo.  
  
 Per ulteriori informazioni, vedere [la creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq>   
 [Guida introduttiva (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/getting-started-linq-to-xml.md)   
 [Panoramica di LINQ to XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
