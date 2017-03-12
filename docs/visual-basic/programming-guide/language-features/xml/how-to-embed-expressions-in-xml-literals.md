---
title: "How to: Embed Expressions in XML Literals (Visual Basic) | Microsoft Docs"
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
  - "embedded expressions [Visual Basic]"
  - "XML literals [Visual Basic], embedded expressions"
ms.assetid: 75016fad-0141-42de-8564-5051be29487e
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# How to: Embed Expressions in XML Literals (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile combinare i valori letterali XML con le espressioni incorporate per creare un documento, un frammento o un elemento XML che contengono il contenuto creato in fase di esecuzione.  Negli esempi seguenti viene illustrato come utilizzare le espressioni incorporate per popolare in fase di esecuzione contenuto dell'elemento, gli attributi e i nomi dell'elemento.  
  
 La sintassi per un'espressione incorporata è `<%=``exp``%>`, che è la stessa sintassi che utilizza [!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp-md.md)]. Per ulteriori informazioni, vedere [Embedded Expressions in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 È inoltre possibile utilizzare le API [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] per creare oggetti [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XElement>.  
  
## Procedure  
  
#### Inserire testo come contenuto dell'elemento  
  
-   Nell'esempio seguente viene illustrato come inserire il testo contenuto nella variabile `contactName` tra gli elementi nomi di apertura e chiusura.  
  
     [!code-vb[VbXMLSamples#39](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-embed-expressions_1.vb)]  
  
     Questo esempio produce il seguente output:  
  
    ```  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
#### Inserire testo come valore dell'attributo  
  
-   Nell'esempio seguente viene illustrato come inserire il testo contenuto nella variabile `phoneType` come valore dell'attributo di `type`.  
  
     [!code-vb[VbXMLSamples#40](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-embed-expressions_2.vb)]  
  
     Questo esempio produce il seguente output:  
  
    ```  
    <contact>  
      <phone type="home">206-555-0144</phone>  
    </contact>  
    ```  
  
#### Inserire testo per un nome di elemento  
  
-   Nell'esempio seguente viene illustrato come inserire il testo contenuto nella variabile `elementName` come nome di un elemento.  
  
     Quando si creano elementi utilizzando questa tecnica, è necessario chiuderli con il tag \<\/\>.  
  
     [!code-vb[VbXMLSamples#41](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-embed-expressions_3.vb)]  
  
     Questo esempio produce il seguente output:  
  
    ```  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
## Vedere anche  
 [How to: Create XML Literals](../../../../visual-basic/programming-guide/language-features/xml/how-to-create-xml-literals.md)   
 [Embedded Expressions in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)