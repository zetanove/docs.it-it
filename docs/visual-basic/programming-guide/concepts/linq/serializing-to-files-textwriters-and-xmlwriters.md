---
title: La serializzazione per il file, TextWriter e XmlWriters3 | Documenti di Microsoft
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
ms.assetid: 7a0c24df-79ef-41a0-87f5-e6cf79382da9
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
ms.openlocfilehash: 98662b8d84459ed051d048084c2755fa7aaf8247
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-to-files-textwriters-and-xmlwriters"></a>Serializzazione in base a File, TextWriter e XmlWriter
È possibile serializzare gli alberi XML in un <xref:System.IO.File>, <xref:System.IO.TextWriter>, o un <xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter> </xref:System.IO.TextWriter> </xref:System.IO.File>  
  
 È possibile serializzare qualsiasi componente XML, tra cui <xref:System.Xml.Linq.XDocument>e <xref:System.Xml.Linq.XElement>, in una stringa utilizzando il `ToString` (metodo).</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument>  
  
 Se si desidera eliminare la formattazione durante la serializzazione in una stringa, è possibile utilizzare il <xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=fullName>(metodo).</xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=fullName>  
  
 Thedefault comportamento durante la serializzazione in un file implica la formattazione (rientri) il documento XML. Quando si impostano i rientri, lo spazio vuoto non significativo nell'albero XML non viene conservato. Per serializzare e formattare, utilizzare uno degli overload dei metodi seguenti che non accettano <xref:System.Xml.Linq.SaveOptions>come argomento:</xref:System.Xml.Linq.SaveOptions>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 Se si desidera che l'opzione di non impostare i rientri e conservare lo spazio vuoto non significativo nella struttura ad albero XML, utilizzare uno degli overload dei metodi seguenti che accetta <xref:System.Xml.Linq.SaveOptions>come argomento:</xref:System.Xml.Linq.SaveOptions>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 Per gli esempi, vedere l'argomento di riferimento appropriato.  
  
## <a name="see-also"></a>Vedere anche  
 [La serializzazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md)
