---
title: 'Procedura: leggere e scrivere un documento codificato (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 159d868f-5ac8-40f2-95ca-07dd925f35c6
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
ms.openlocfilehash: 3247af177066e9b50d5028766f99e7bf6589050f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-and-write-an-encoded-document-visual-basic"></a>Procedura: leggere e scrivere un documento codificato (Visual Basic)
Per creare un documento XML codificato, aggiungere un <xref:System.Xml.Linq.XDeclaration>all'albero XML, impostando la codifica per il nome della tabella codici desiderata.</xref:System.Xml.Linq.XDeclaration>  
  
 Qualsiasi valore restituito da <xref:System.Text.Encoding.WebName%2A>è un valore valido.</xref:System.Text.Encoding.WebName%2A>  
  
 Se si legge un documento codificato, la <xref:System.Xml.Linq.XDeclaration.Encoding%2A>verrà impostata per il nome della tabella codici.</xref:System.Xml.Linq.XDeclaration.Encoding%2A>  
  
 Se si imposta <xref:System.Xml.Linq.XDeclaration.Encoding%2A>a un nome di tabella codici valido, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] serializzerà con la codifica specificata.</xref:System.Xml.Linq.XDeclaration.Encoding%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono creati due documenti, uno con codifica utf-8 e uno con codifica utf-16. Vengono quindi caricati i documenti e viene stampata la codifica nella console.  
  
```vb  
Console.WriteLine("Creating a document with utf-8 encoding")  
Dim encodedDoc8 As XDocument = _  
        <?xml version='1.0' encoding='utf-8' standalone='yes'?>  
        <Root>Content</Root>   
  
encodedDoc8.Save("EncodedUtf8.xml")  
Console.WriteLine("Encoding is:{0}", encodedDoc8.Declaration.Encoding)  
Console.WriteLine()  
  
Console.WriteLine("Creating a document with utf-16 encoding")  
Dim encodedDoc16 As XDocument = _  
        <?xml version='1.0' encoding='utf-16' standalone='yes'?>  
        <Root>Content</Root>  
  
encodedDoc16.Save("EncodedUtf16.xml")  
Console.WriteLine("Encoding is:{0}", encodedDoc16.Declaration.Encoding)  
Console.WriteLine()  
  
Dim newDoc8 As XDocument = XDocument.Load("EncodedUtf8.xml")  
Console.WriteLine("Encoded document:")  
Console.WriteLine(File.ReadAllText("EncodedUtf8.xml"))  
Console.WriteLine()  
Console.WriteLine("Encoding of loaded document is:{0}", newDoc8.Declaration.Encoding)  
Console.WriteLine()  
  
Dim newDoc16 As XDocument = XDocument.Load("EncodedUtf16.xml")  
Console.WriteLine("Encoded document:")  
Console.WriteLine(File.ReadAllText("EncodedUtf16.xml"))  
Console.WriteLine()  
Console.WriteLine("Encoding of loaded document is:{0}", newDoc16.Declaration.Encoding)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Creating a document with utf-8 encoding  
Encoding is:utf-8  
  
Creating a document with utf-16 encoding  
Encoding is:utf-16  
  
Encoded document:  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root>Content</Root>  
  
Encoding of loaded document is:utf-8  
  
Encoded document:  
<?xml version="1.0" encoding="utf-16" standalone="yes"?>  
<Root>Content</Root>  
  
Encoding of loaded document is:utf-16  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XDeclaration.Encoding%2A?displayProperty=fullName></xref:System.Xml.Linq.XDeclaration.Encoding%2A?displayProperty=fullName>   
 [LINQ to XML (Visual Basic) di programmazione avanzata](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
