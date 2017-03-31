---
title: Conservazione dello spazio vuoto durante il caricamento o l&quot;analisi di dati XML1 | Documentazione Microsoft
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
ms.assetid: f3ff58c4-55aa-4fcd-b933-e3a2ee6e706c
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
ms.openlocfilehash: 1b2ec9b5b1bbc343fde5c9527c1e4f4ad7f14796
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>Conservazione di spazi vuoti durante il caricamento o l'analisi di dati XML
In questo argomento viene descritto come controllare il comportamento dello spazio vuoto di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] .  
  
 In uno scenario comune viene letto il codice XML rientrato, viene creata una struttura ad albero XML in memoria senza nodi di testo di tipo spazio vuoto (ossia senza conservare lo spazio vuoto), vengono eseguite alcune operazioni su XML e quindi l'XML viene salvato senza rientro. Quando si serializza l'XML con la formattazione, nell'albero XML viene conservato solo lo spazio vuoto significativo. Questo è il comportamento predefinito per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 In un altro scenario comune viene letto e modificato codice XML che è già stato intenzionalmente rientrato. È possibile che si desideri non modificare questo rientro in alcun modo. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile ottenere questo risultato conservando lo spazio vuoto durante il caricamento o l'analisi XML e disabilitando la formattazione durante la serializzazione XML.  
  
 In questo argomento viene descritto il comportamento dello spazio vuoto dei metodi che popolano l'albero XML. Per informazioni sul controllo dello spazio vuoto durante la serializzazione di strutture ad albero XML, vedere [Mantenimento dello spazio vuoto durante la serializzazione](../../../../csharp/programming-guide/concepts/linq/preserving-white-space-while-serializing.md).  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>Comportamento dei metodi che popolano gli alberi XML  
 I metodi seguenti delle classi <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XDocument> popolano una struttura ad albero XML. È possibile popolare una struttura ad albero XML da un file, un <xref:System.IO.TextReader>, un <xref:System.Xml.XmlReader> o una stringa:  
  
-   <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>  
  
 Se il metodo non accetta <xref:System.Xml.Linq.LoadOptions> come argomento, non manterrà lo spazio vuoto non significativo.  
  
 Nella maggior parte dei casi, se il metodo accetta <xref:System.Xml.Linq.LoadOptions> come argomento, facoltativamente è possibile mantenere lo spazio vuoto non significativo come nodi di testo nella struttura ad albero XML. Se invece il metodo carica l'XML da un oggetto <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlReader> determina se lo spazio vuoto verrà mantenuto o meno. Impostando <xref:System.Xml.Linq.LoadOptions> non si ottiene alcun effetto.  
  
 Se lo spazio vuoto viene mantenuto, con questi metodi lo spazio vuoto non significativo viene inserito nella struttura ad albero XML come nodi <xref:System.Xml.Linq.XText>. Se non viene conservato, i nodi di testo non vengono inseriti.  
  
 È possibile creare una struttura ad albero XML usando un <xref:System.Xml.XmlWriter>. I nodi scritti in <xref:System.Xml.XmlWriter> vengono popolati nella struttura ad albero. Tuttavia, quando si compila un albero XML usando questo metodo, vengono conservati tutti i nodi, a prescindere che corrispondano o meno a spazio vuoto e indipendentemente dal fatto che lo spazio vuoto sia o meno significativo.  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi di codice XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)
