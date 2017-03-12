---
title: "How to: Access XML Descendant Elements (Visual Basic) | Microsoft Docs"
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
  - "XML descendent axis property [Visual Basic]"
  - "XML axis [Visual Basic], descendent"
  - "descendent axis property [Visual Basic]"
  - "XML [Visual Basic], accessing"
ms.assetid: aabfa258-4112-4e7e-bab9-403f96072ef7
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# How to: Access XML Descendant Elements (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'esempio viene illustrato come utilizzare la proprietà axis descendant per accedere a tutti gli elementi XML che hanno un nome specificato e che sono contenuti in un elemento XML.  In particolare, viene utilizzata la proprietà `Value` per ottenere il valore del primo elemento nella raccolta restituita dalla proprietà axis descendant `name`.  La proprietà axis descendant `name` ottiene tutti gli elementi denominati `name` contenuti nell'oggetto `contacts`.  Nell'esempio viene anche utilizzata la proprietà axis descendant `phone` per accedere a tutti gli elementi discendenti denominati `phone` inclusi nell'oggetto `contacts`.  
  
## Esempio  
 [!code-vb[VbXMLSamples#31](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-access-xml-descen_1.vb)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un riferimento allo spazio dei nomi <xref:System.Xml.Linq>.  
  
## Vedere anche  
 <xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName>   
 [XML Descendant Axis Property](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)   
 [XML Value Property](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)   
 [Accessing XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)