---
title: LINQ to XML per gli utenti di XPath (C#) | Microsoft Docs
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
ms.assetid: 91774511-1dca-4f06-ac0b-913746f104fe
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: db09a2438df5592f4afa0b3882d7b8d5de6fa1c1
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017


---
# <a name="linq-to-xml-for-xpath-users-c"></a>LINQ to XML per gli utenti di XPath (C#)
In questo set di argomenti vengono illustrate varie espressioni XPath e gli equivalenti [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 In tutti gli esempi viene usata la funzionalità di XPath in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] resa disponibile dai metodi di estensione in <xref:System.Xml.XPath.Extensions?displayProperty=fullName>. Negli esempi vengono eseguite sia l'espressione XPath che l'espressione [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]. Vengono quindi confrontati i risultati di entrambe le query, verificando che l'espressione XPath sia equivalente dal punto di vista funzionale alla query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]. Poiché entrambi i tipi di query restituiscono nodi dalla stessa struttura ad albero XML, il confronto dei risultati delle query viene eseguito usando l'identità referenziale.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Confronto tra XPath e LINQ to XML](../../../../csharp/programming-guide/concepts/linq/comparison-of-xpath-and-linq-to-xml.md)|Viene fornita una panoramica delle analogie e differenze tra XPath e [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].|  
|[Procedura: Trovare un elemento figlio (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-child-element-xpath-linq-to-xml.md)|Viene illustrato un confronto tra l'asse degli elementi figlio XPath e il metodo [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]<xref:System.Xml.Linq.XContainer.Element%2A>.<br /><br /> L'espressione XPath associata è:`"DeliveryNotes"`.|  
|[Procedura: Trovare un elenco di elementi figlio (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-list-of-child-elements-xpath-linq-to-xml.md)|Viene illustrato un confronto tra l'asse degli elementi figlio XPath e l'asse [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]<xref:System.Xml.Linq.XContainer.Elements%2A>.<br /><br /> L'espressione XPath associata è:`"./*"`.|  
|[Procedura: Trovare l'elemento radice (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-the-root-element-xpath-linq-to-xml.md)|Viene illustrato un confronto su come ottenere l'elemento radice con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"/PurchaseOrders"`.|  
|[Procedura: Trovare elementi discendenti (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-descendant-elements-xpath-linq-to-xml.md)|Viene illustrato un confronto su come ottenere gli elementi discendenti con un determinato nome con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"//Name"`.|  
|[Procedura: Filtrare in base a un attributo (XPath-LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/how-to-filter-on-an-attribute-xpath-linq-to-xml.md)|Viene illustrato un confronto su come ottenere gli elementi discendenti con un attributo con un valore specificato con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`".//Address[@Type='Shipping']"`.|  
|[Procedura: Trovare elementi correlati (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-related-elements-xpath-linq-to-xml.md)|Viene illustrato un confronto su come ottenere un elemento selezionando un attributo cui viene fatto riferimento dal valore di un altro elemento con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`".//Customer[@CustomerID=/Root/Orders/Order[12]/CustomerID]"`.|  
|[Procedura: Trovare elementi in uno spazio dei nomi (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-elements-in-a-namespace-xpath-linq-to-xml.md)|Viene illustrato un confronto tra l'uso della classe XPath <xref:System.Xml.XmlNamespaceManager> e l'uso della proprietà [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] della classe <xref:System.Xml.Linq.XName.Namespace%2A><xref:System.Xml.Linq.XName> per l'uso degli spazi dei nomi XML.<br /><br /> L'espressione XPath associata è:`"./aw:*"`.|  
|[Procedura: Trovare elementi di pari livello precedenti (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-preceding-siblings-xpath-linq-to-xml.md)|Viene illustrato un confronto tra l'asse `preceding-sibling` XPath e l'asse [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] figlio <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName> <br /><br /> L'espressione XPath associata è:`"preceding-sibling::*"`.|  
|[Procedura: Trovare discendenti di un elemento figlio (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-descendants-of-a-child-element-xpath-linq-to-xml.md)|Viene illustrato un confronto su come ottenere gli elementi discendenti di un elemento figlio con un determinato nome con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"./Paragraph//Text/text()"`.|  
|[Procedura: Trovare un'unione di due percorsi (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-union-of-two-location-paths-xpath-linq-to-xml.md)|Viene illustrato un confronto tra l'utilizzo dell'operatore di unione, `&#124;`, in XPath e l'utilizzo dell'operatore di query standard <xref:System.Linq.Enumerable.Concat%2A> in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"//Category&#124;//Price"`.|  
|[Procedura: Trovare nodi di pari livello (XPath-LINQ to XML)(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-sibling-nodes-xpath-linq-to-xml.md)|Viene illustrato un confronto su come trovare tutti gli elementi di pari livello di un nodo con un nome specificato con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"../Book"`.|  
|[Procedura: Trovare un attributo dell'elemento padre (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-an-attribute-of-the-parent-xpath-linq-to-xml.md)|Viene illustrato un confronto su come spostarsi all'elemento padre e trovare un attributo associato con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"../@id"`.|  
|[Procedura: Trovare attributi di elementi di pari livello con un nome specifico (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-attributes-of-siblings-with-a-specific-name-xpath-linq-to-xml.md)|Viene illustrato un confronto su come trovare attributi specifici degli elementi di pari livello del nodo di contesto con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"``../Book/@id``"`.|  
|[Procedura: Trovare elementi con un attributo specifico (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-elements-with-a-specific-attribute-xpath-linq-to-xml.md)|Viene illustrato un confronto su come trovare tutti gli elementi contenenti un attributo specifico con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"./*[@Select]"`.|  
|[Procedura: Trovare elementi figlio in base alla posizione (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-child-elements-based-on-position-xpath-linq-to-xml.md)|Viene illustrato un confronto su come trovare un elemento in base alla posizione relativa con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"Test[position() >= 2 and position() <= 4]"`.|  
|[Procedura: Trovare l'elemento di pari livello immediatamente precedente (XPath-LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml.md)|Viene illustrato un confronto su come trovare l'elemento di pari livello immediatamente precedente di un nodo con XPath e con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].<br /><br /> L'espressione XPath associata è:`"preceding-sibling::*[1]"`.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.XPath?displayProperty=fullName>   
 [Esecuzione di query su strutture ad albero XML (C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md)   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
