---
title: Assi LINQ to XML (C#) | Microsoft Docs
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
ms.assetid: 3f7d54ff-b608-43a1-9e2d-e70668b72df8
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
ms.openlocfilehash: 696a9057d5eb9d2a8c3a263c02571a0913af89f3
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-axes-c"></a>Assi LINQ to XML (C#)
Dopo aver creato un albero XML o aver caricato un documento XML in un albero XML, è possibile eseguire query su di essa per cercare elementi e attributi e recuperarne i valori.  
  
 Prima di scrivere eventuali query, è necessario conoscere gli assi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]. Per gli assi sono disponibili due tipi di metodi. Il primo tipo include i metodi che vengono chiamati per un unico oggetto <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XDocument> o <xref:System.Xml.Linq.XNode>. Questi metodi operano su un unico oggetto e restituiscono una raccolta di oggetti <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute> o <xref:System.Xml.Linq.XNode>. Il secondo tipo include i metodi di estensione che operano su raccolte e restituiscono raccolte. I metodi di estensione enumerano la raccolta di origine, chiamano il metodo dell'asse appropriato su ogni elemento della raccolta e concatenano i risultati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Panoramica degli assi LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes-overview.md)|Viene fornita una definizione degli assi e ne viene illustrato l'uso nel contesto di query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].|  
|[Procedura: Recuperare una raccolta di elementi (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|Viene presentato il metodo <xref:System.Xml.Linq.XContainer.Elements%2A>, che consente di recuperare una raccolta degli elementi figlio di un elemento.|  
|[Procedura: Recuperare il valore di un elemento (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|Viene spiegato come ottenere i valori di elementi.|  
|[Procedura. Filtrare in base a nomi di elementi (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-filter-on-element-names-linq-to-xml.md)|Viene illustrato come filtrare in base a nomi di elemento quando si usano gli assi.|  
|[Procedura: Concatenare chiamate al metodo dell'asse (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-chain-axis-method-calls-linq-to-xml.md)|Viene illustrato come concatenare chiamate ai metodi degli assi.|  
|[Procedura: Recuperare un singolo elemento figlio (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)|Viene illustrato come recuperare un singolo elemento figlio di un elemento, dato il relativo nome di tag.|  
|[Procedura: Recuperare una raccolta di attributi (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|Viene illustrato il metodo <xref:System.Xml.Linq.XElement.Attributes%2A>, che consente di recuperare gli attributi di un elemento.|  
|[Procedura: Recuperare un singolo attributo (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-single-attribute-linq-to-xml.md)|Viene illustrato come recuperare un singolo attributo di un elemento, dato il relativo nome.|  
|[Procedura: Recuperare il valore di un attributo (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|Viene spiegato come ottenere i valori di attributi.|  
|[Procedura: Recuperare il valore superficiale di un elemento](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-shallow-value-of-an-element.md)|Viene illustrato come recuperare il valore superficiale di un elemento|  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [Guida per programmatori (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
