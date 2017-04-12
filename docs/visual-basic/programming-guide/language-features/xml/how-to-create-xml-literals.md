---
title: 'Procedura: creare valori letterali XML (Visual Basic) | Documenti di Microsoft'
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
helpviewer_keywords:
- XML literals [Visual Basic], creating
ms.assetid: 573a6db5-b14d-4e42-b356-8cc7e2d77745
caps.latest.revision: 17
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 72d96f36fc17f32ac3ee3ea97175f112fcd21681
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-xml-literals-visual-basic"></a>Procedura: creare valori letterali XML (Visual Basic)
È possibile creare un documento XML, frammento o elemento direttamente nel codice utilizzando un valore letterale XML. Negli esempi in questo argomento viene illustrato come creare un elemento XML che dispone di tre elementi figlio e come creare un documento XML.  
  
 È inoltre possibile utilizzare il [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] API per creare [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetti. Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>  
  
### <a name="to-create-an-xml-element"></a>Per creare un elemento XML  
  
-   Creare il XML inline utilizzando la sintassi del valore letterale XML, che corrisponde all'effettiva sintassi XML.  
  
     [!code-vb[VbXMLSamples n.&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-xml-literals_1.vb)]  
  
     Eseguire il codice. L'output di questo codice è:  
  
     `<contact>`  
  
     `<name>Patrick Hines</name>`  
  
     `<phone type="home">206-555-0144</phone>`  
  
     `<phone type="work">425-555-0145</phone>`  
  
     `</contact>`  
  
### <a name="to-create-an-xml-document"></a>Per creare un documento XML  
  
-   Creare il documento XML inline. Il codice seguente crea un documento XML con la sintassi letterale, una dichiarazione XML, un'istruzione di elaborazione, un commento e un elemento che contiene un altro elemento.  
  
     [!code-vb[&#30; VbXMLSamples](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-xml-literals_2.vb)]  
  
     Eseguire il codice. L'output di questo codice è:  
  
     `<?xml-stylesheet type="text/xsl" href="show_book.xsl"?>`  
  
     `<!-- Tests that the application works. -->`  
  
     `<books>`  
  
     `<book/>`  
  
     `</books>`  
  
## <a name="see-also"></a>Vedere anche  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Valore letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Valore letterale di documento XML](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)
