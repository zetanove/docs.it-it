---
title: Guida per programmatori (LINQ to XML) (C#) | Microsoft Docs
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
ms.assetid: 4b1ffd10-ab81-4a0d-a0ca-e9876478d924
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5e1e95d92123b2874aace0c36005a8a07a6203fc
ms.contentlocale: it-it
ms.lasthandoff: 05/24/2017

---
# <a name="programming-guide-linq-to-xml-c"></a>Guida per programmatori (LINQ to XML) (C#)
Contenuto della sezione vengono fornite informazioni di carattere concettuale e procedurale sulla programmazione con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
## <a name="who-should-read-this-documentation"></a>Destinatari  
 Questa documentazione è destinata agli sviluppatori che già conoscono C# e alcuni aspetti di base di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 L'obiettivo di questa documentazione è facilitare l'uso di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per tutti i tipi di sviluppatori. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] semplifica la programmazione XML. Non è quindi necessario essere uno sviluppatore esperto per poterlo usare.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è basato soprattutto sulle classi generiche. È pertanto molto importante comprendere l'uso di tali classi. Può inoltre risultare utile conoscere delegati dichiarati come tipi con parametri. Se non si conoscono le classi generiche di C#, vedere [Classi generiche](../../../../csharp/programming-guide/generics/generic-classes.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Panoramica della programmazione con LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)|Viene fornita una panoramica sulle classi di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], nonché informazioni dettagliate sulle tre classi principali: <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute> e <xref:System.Xml.Linq.XDocument>.|  
|[Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)|Vengono fornite informazioni di carattere concettuale e sulle attività correlate alla creazione di alberi XML. È possibile creare alberi XML usando la costruzione funzionale oppure analizzando il testo XML di una stringa o di un file. È inoltre possibile usare un oggetto <xref:System.Xml.XmlReader> per popolare un albero XML.|  
|[Uso degli spazi dei nomi XML (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)|Vengono fornite informazioni dettagliate sulla creazione di alberi XML che usano spazi dei nomi.|  
|[Serializzazione di strutture ad albero XML (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)|Vengono descritti i diversi approcci disponibili per la serializzazione di un albero XML e vengono fornite istruzioni sulla scelta dell'approccio da usare.|  
|[Assi LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)|Enumera e descrive i metodi dell'asse di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] che è necessario conoscere prima di poter scrivere query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].|  
|[Esecuzione di query su alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md)|Vengono forniti esempi comuni relativi all'esecuzione di query su alberi XML.|  
|[Modifica degli alberi XML (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)|Analogamente al modello DOM (Document Object Model), [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consente di modificare un albero XML sul posto.|  
|[Programmazione LINQ to XML avanzata (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)|Vengono fornite informazioni su annotazioni, eventi, flusso e altri scenari avanzati.|  
|[Sicurezza in LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-security.md)|Vengono descritti i problemi di sicurezza associati all'utilizzo di LINQ to XML e viene fornito materiale sussidiario per ridurre l'esposizione ai rischi.|  
|[Documenti XML di esempio (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)|Sono contenuti i documenti XML di esempio usati nei numerosi esempi di questa documentazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/getting-started-linq-to-xml.md)   
 [LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml.md)
