---
title: Conservando lo spazio vuoto durante il caricamento o l&quot;analisi XML2 | Documenti di Microsoft
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
ms.assetid: ef6518e0-2c8d-462c-8b92-a16e9dc737ad
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 39e4270acc0e9a9df5c3855f8c087f41d9612197
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>Conservazione di spazi vuoti durante il caricamento o l'analisi di dati XML
In questo argomento viene descritto come controllare il comportamento dello spazio vuoto di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] .  
  
 In uno scenario comune viene letto il codice XML rientrato, viene creata una struttura ad albero XML in memoria senza nodi di testo di tipo spazio vuoto (ossia senza conservare lo spazio vuoto), vengono eseguite alcune operazioni su XML e quindi l'XML viene salvato senza rientro. Quando si serializza l'XML con la formattazione, nell'albero XML viene conservato solo lo spazio vuoto significativo. Questo è il comportamento predefinito per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 In un altro scenario comune viene letto e modificato codice XML che è già stato intenzionalmente rientrato. È possibile che si desideri non modificare questo rientro in alcun modo. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile ottenere questo risultato conservando lo spazio vuoto durante il caricamento o l'analisi XML e disabilitando la formattazione durante la serializzazione XML.  
  
 In questo argomento viene descritto il comportamento dello spazio vuoto dei metodi che popolano l'albero XML. Per informazioni su come controllare gli spazi vuoti durante la serializzazione di strutture ad albero XML, vedere [conservare gli spazi vuoti durante la serializzazione](../../../../visual-basic/programming-guide/concepts/linq/preserving-white-space-while-serializing.md).  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>Comportamento dei metodi che popolano gli alberi XML  
 I metodi seguenti di <xref:System.Xml.Linq.XElement>e <xref:System.Xml.Linq.XDocument>classi popolano un albero XML.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> È possibile popolare un albero XML da un file, un <xref:System.IO.TextReader>, un <xref:System.Xml.XmlReader>, o una stringa:</xref:System.Xml.XmlReader> </xref:System.IO.TextReader>  
  
-   <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>  
  
 Se il metodo non accetta <xref:System.Xml.Linq.LoadOptions>come argomento, il metodo non mantiene gli spazi vuoti non significativi.</xref:System.Xml.Linq.LoadOptions>  
  
 Nella maggior parte dei casi, se il metodo accetta <xref:System.Xml.Linq.LoadOptions>come argomento, facoltativamente è possibile conservare spazio vuoto non significativo come nodi di testo nell'albero XML.</xref:System.Xml.Linq.LoadOptions> Tuttavia, se il metodo carica il XML da un <xref:System.Xml.XmlReader>, il <xref:System.Xml.XmlReader>determina se lo spazio vuoto verrà conservato o meno.</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> L'impostazione <xref:System.Xml.Linq.LoadOptions>avrà alcun effetto.</xref:System.Xml.Linq.LoadOptions>  
  
 Con questi metodi, se lo spazio vuoto viene conservato, spazio vuoto non significativo viene inserito nell'albero XML come <xref:System.Xml.Linq.XText>nodi.</xref:System.Xml.Linq.XText> Se non viene conservato, i nodi di testo non vengono inseriti.  
  
 È possibile creare una struttura ad albero XML utilizzando un <xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter> I nodi che vengono scritti i <xref:System.Xml.XmlWriter>vengono popolati nell'albero.</xref:System.Xml.XmlWriter> Tuttavia, quando si compila un albero XML usando questo metodo, vengono conservati tutti i nodi, a prescindere che corrispondano o meno a spazio vuoto e indipendentemente dal fatto che lo spazio vuoto sia o meno significativo.  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
