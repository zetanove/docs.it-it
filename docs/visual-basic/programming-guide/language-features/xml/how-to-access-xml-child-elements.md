---
title: "How to: Access XML Child Elements (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML axis [Visual Basic], child"
  - "child axis property [Visual Basic]"
  - "XML child axis property [Visual Basic]"
  - "XML [Visual Basic], accessing"
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Access XML Child Elements (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Nell'esempio viene illustrato come utilizzare una proprietà axis dell'elemento figlio per accedere a tutti gli elementi figlio XML che hanno un nome specificato in un elemento XML.  In particolare, utilizza la proprietà <xref:System.Xml.Linq.XElement.Value%2A> per ottenere il valore del primo elemento nella raccolta restituita dalla proprietà axis dell'elemento figlio `name`.  La proprietà axis dell'elemento figlio `name` recupera tutti gli elementi figlio denominati `phone` nell'oggetto `contact`.  Nell'esempio viene anche utilizzata la proprietà axis dell'elemento figlio `phone` per accedere a tutti gli elementi figlio denominati `phone` inclusi nell'oggetto `contact`.  
  
## Esempio  
 [!code-vb[VbXMLSamples#10](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-access-xml-child-elements_1.vb)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un riferimento allo spazio dei nomi <xref:System.Xml.Linq>.  
  
## Vedere anche  
 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>   
 [XML Child Axis Property](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)   
 [XML Value Property](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)   
 [Accessing XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)