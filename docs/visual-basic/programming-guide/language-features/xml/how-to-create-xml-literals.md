---
title: "How to: Create XML Literals (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML literals [Visual Basic], creating"
ms.assetid: 573a6db5-b14d-4e42-b356-8cc7e2d77745
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# How to: Create XML Literals (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile creare un documento, frammento o elemento XML direttamente nel codice utilizzando un valore letterale XML.  Negli esempi in questo argomento viene illustrato come creare un elemento XML che ha tre elementi figlio e come creare un documento XML.  
  
 È inoltre possibile utilizzare le API [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] per creare oggetti [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XElement>.  
  
### Per creare un elemento XML  
  
-   Creare l' XML inline utilizzando la sintassi letterale XML che corrisponde all'effettiva sintassi XML.  
  
     [!code-vb[VbXMLSamples#5](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-create-xml-literals_1.vb)]  
  
     Eseguire il codice.  L'output del codice è il seguente:  
  
     `<contact>`  
  
     `<name>Patrick Hines</name>`  
  
     `<phone type="home">206-555-0144</phone>`  
  
     `<phone type="work">425-555-0145</phone>`  
  
     `</contact>`  
  
### Per creare un documento XML  
  
-   Per creare il documento XML inline.  Nell'esempio di codice riportato di seguito viene creato un documento XML che ha sintassi letterale, una dichiarazione XML, un un'istruzione di elaborazione, un commento e un elemento che contiene un altro elemento.  
  
     [!code-vb[VbXMLSamples#30](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-create-xml-literals_2.vb)]  
  
     Eseguire il codice.  L'output del codice è il seguente:  
  
     `<?xml-stylesheet type="text/xsl" href="show_book.xsl"?>`  
  
     `<!-- Tests that the application works.  -->`  
  
     `<books>`  
  
     `<book/>`  
  
     `</books>`  
  
## Vedere anche  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Document Literal](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)