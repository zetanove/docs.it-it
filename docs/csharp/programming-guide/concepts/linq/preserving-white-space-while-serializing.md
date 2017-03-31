---
title: Conservazione di spazi vuoti durante la serializzazione | Microsoft Docs
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
ms.assetid: 0c4f8b98-483b-4cf8-86be-fa146eef90dc
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
ms.openlocfilehash: 1d6cebecd75bedc393b06261c1955a554c9cf18c
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-serializing"></a>Conservazione di spazi vuoti durante la serializzazione
In questo argomento viene descritto come controllare lo spazio vuoto durante la serializzazione di un albero XML.  
  
 In uno scenario comune viene letto il codice XML rientrato, viene creata una struttura ad albero XML in memoria senza nodi di testo di tipo spazio vuoto (ossia senza conservare lo spazio vuoto), vengono eseguite alcune operazioni su XML e quindi l'XML viene salvato senza rientro. Quando si serializza l'XML con la formattazione, nell'albero XML viene conservato solo lo spazio vuoto significativo. Questo è il comportamento predefinito per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 In un altro scenario comune viene letto e modificato codice XML che è già stato intenzionalmente rientrato. È possibile che si desideri non modificare questo rientro in alcun modo. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile ottenere questo risultato conservando lo spazio vuoto durante il caricamento o l'analisi XML e disabilitando la formattazione durante la serializzazione XML.  
  
## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a>Comportamento dello spazio vuoto di metodi che serializzano strutture ad albero XML  
 I metodi seguenti delle classi <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XDocument> serializzano un albero XML. È possibile serializzare un albero XML in file, <xref:System.IO.TextReader> o <xref:System.Xml.XmlReader>. Il metodo `ToString` consente di eseguire la serializzazione in una stringa.  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.ToString%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.ToString%2A?displayProperty=fullName>  
  
 Se il metodo non accetta <xref:System.Xml.Linq.SaveOptions> come argomento, formatterà il codice XML serializzato, ovvero ne imposterà il rientro. In questo caso tutto lo spazio vuoto non significativo nella struttura ad albero XML verrà ignorato.  
  
 Se il metodo accetta <xref:System.Xml.Linq.SaveOptions> come argomento, è possibile specificare di non formattare il codice XML serializzato, ovvero il metodo non ne imposterà il rientro. In questo caso tutto lo spazio vuoto nella struttura ad albero XML verrà mantenuto.  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
