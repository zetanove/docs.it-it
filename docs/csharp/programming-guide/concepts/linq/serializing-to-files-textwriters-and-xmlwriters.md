---
title: Serializzazione in base a File, TextWriter e XmlWriter1 | Documentazione Microsoft
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
ms.assetid: bd3ea6f7-895b-4ff4-a625-fe2bb55b1886
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
ms.openlocfilehash: f61324395e81509e5800e99b654a8c669d4397f0
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-to-files-textwriters-and-xmlwriters"></a>Serializzazione in base a File, TextWriter e XmlWriter
È possibile serializzare l'albero XML in un oggetto <xref:System.IO.File>, <xref:System.IO.TextWriter> o <xref:System.Xml.XmlWriter>.  
  
 È possibile serializzare qualsiasi componente XML, tra cui <xref:System.Xml.Linq.XDocument> e <xref:System.Xml.Linq.XElement> in una stringa tramite il metodo `ToString`.  
  
 Se si desidera eliminare la formattazione durante la serializzazione in una stringa, è possibile usare il metodo <xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=fullName>.  
  
 Il comportamento predefinito quando si esegue la serializzazione in un file implica la formattazione, ovvero l'impostazione di rientri, nel documento XML. Quando si impostano i rientri, lo spazio vuoto non significativo nell'albero XML non viene conservato. Per serializzare e formattare al contempo il documento, usare uno degli overload dei metodi seguenti che non accettano <xref:System.Xml.Linq.SaveOptions> come argomento:  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 Se si desidera applicare l'opzione per non impostare i rientri e conservare lo spazio vuoto non significativo nell'albero XML, usare uno degli overload dei metodi seguenti che accettano <xref:System.Xml.Linq.SaveOptions> come argomento:  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 Per gli esempi, vedere l'argomento di riferimento appropriato.  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione di strutture ad albero XML (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
