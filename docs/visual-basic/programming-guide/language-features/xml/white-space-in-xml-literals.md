---
title: "White Space in XML Literals (Visual Basic) | Microsoft Docs"
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
  - "white space [XML in Visual Basic]"
  - "XML literals [Visual Basic], white space"
ms.assetid: dfe3a9ff-d69a-418e-a6b5-476f4ed84219
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# White Space in XML Literals (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] incorpora solo i caratteri di spazio vuoto significativi da un valore letterale XML quando crea un oggetto [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  I caratteri di spazio vuoto non significativi non vengono incorporati.  
  
## Spazi vuoti significativi e non significativi  
 I caratteri di spazio vuoto nei valori letterali XML sono significativi solo in tre casi:  
  
-   Quando sono in un valore dell'attributo.  
  
-   Quando sono parte del contenuto di testo di un elemento e il testo contiene anche altri caratteri.  
  
-   Quando sono inclusi in un'espressione incorporata per il contenuto di testo di un elemento.  
  
 Negli altri casi, il compilatore tratta i caratteri di spazio vuoto come non significativi e quindi non li include nell'oggetto [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] per il valore letterale.  
  
 Per includere spazi vuoti non significativi in un valore letterale XML, utilizzare un'espressione incorporata che contenga una stringa letterale con gli spazi vuoti.  
  
> [!NOTE]
>  Se l'attributo `xml:space` è presente in un valore letterale dell'elemento XML, il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] include l'attributo nell'oggetto <xref:System.Xml.Linq.XElement>, ma l'aggiunta di questo attributo non modifica il modo in cui il compilatore considera gli spazi vuoti.  
  
## Esempi  
 Nell'esempio seguente sono presenti due elementi XML, uno esterno e uno interno.  Entrambi gli elementi contengono spazi vuoti nel contenuto di testo.  Lo spazio vuoto nell'elemento esterno è non significativo perché questo contiene solo spazi vuoti e un elemento XML.  Lo spazio vuoto nell'elemento interno è significativo perché questo contiene spazi vuoti e testo.  
  
 [!code-vb[VbXMLSamples#29](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/white-space-in-xml-liter_1.vb)]  
  
 Quando viene eseguito questo codice viene visualizzato il seguente testo.  
  
```  
<outer>  
  <inner>  
                                          Inner text  
                                      </inner>  
</outer>  
```  
  
## Vedere anche  
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)