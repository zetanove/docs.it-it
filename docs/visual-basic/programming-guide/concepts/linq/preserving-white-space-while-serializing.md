---
title: Conservando lo spazio vuoto durante la Serializing2 | Documenti di Microsoft
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
ms.assetid: 2d7abbd4-37f4-422b-89dd-0a694b5edc17
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
ms.openlocfilehash: 9efa2940af9321401e7f9c01d6fb9d1f48616711
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-serializing"></a>Conservazione di spazi vuoti durante la serializzazione
In questo argomento viene descritto come controllare lo spazio vuoto durante la serializzazione di un albero XML.  
  
 In uno scenario comune viene letto il codice XML rientrato, viene creata una struttura ad albero XML in memoria senza nodi di testo di tipo spazio vuoto (ossia senza conservare lo spazio vuoto), vengono eseguite alcune operazioni su XML e quindi l'XML viene salvato senza rientro. Quando si serializza l'XML con la formattazione, nell'albero XML viene conservato solo lo spazio vuoto significativo. Questo è il comportamento predefinito per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 In un altro scenario comune viene letto e modificato codice XML che è già stato intenzionalmente rientrato. È possibile che si desideri non modificare questo rientro in alcun modo. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile ottenere questo risultato conservando lo spazio vuoto durante il caricamento o l'analisi XML e disabilitando la formattazione durante la serializzazione XML.  
  
## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a>Comportamento dello spazio vuoto di metodi che serializzano strutture ad albero XML  
 I metodi seguenti di <xref:System.Xml.Linq.XElement>e <xref:System.Xml.Linq.XDocument>classi serializzano una struttura ad albero XML.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> È possibile serializzare una struttura ad albero XML in un file, un <xref:System.IO.TextReader>, o un <xref:System.Xml.XmlReader>.</xref:System.Xml.XmlReader> </xref:System.IO.TextReader> Il metodo `ToString` consente di eseguire la serializzazione in una stringa.  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.ToString%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.ToString%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.ToString%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.ToString%2A?displayProperty=fullName>  
  
 Se il metodo non accetta <xref:System.Xml.Linq.SaveOptions>come argomento, il metodo verrà formattazione (rientro) il codice XML serializzato.</xref:System.Xml.Linq.SaveOptions> In questo caso tutto lo spazio vuoto non significativo nella struttura ad albero XML verrà ignorato.  
  
 Se il metodo accetta <xref:System.Xml.Linq.SaveOptions>come argomento, è possibile specificare che il metodo di non formattare (rientro) il codice XML serializzato.</xref:System.Xml.Linq.SaveOptions> In questo caso tutto lo spazio vuoto nella struttura ad albero XML verrà mantenuto.  
  
## <a name="see-also"></a>Vedere anche  
 [La serializzazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md)
