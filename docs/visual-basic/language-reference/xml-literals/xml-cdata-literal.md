---
title: "XML CDATA Literal (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralCdata"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CDATA literal [Visual Basic]"
  - "XML CDATA literal [Visual Basic]"
  - "XML literals [Visual Basic], CDATA"
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML CDATA Literal (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Valore letterale che rappresenta un oggetto <xref:System.Xml.Linq.XCData>.  
  
## Sintassi  
  
```  
<![CDATA[content]]>  
```  
  
## Parti  
 `<![CDATA[`  
 Obbligatorio.  Indica l'inizio della sezione CDATA XML.  
  
 `content`  
 Obbligatorio.  Contenuto di testo che viene visualizzato nella sezione CDATA XML.  
  
 `]]>`  
 Obbligatorio.  Indica la fine della sezione.  
  
## Valore restituito  
 Un oggetto <xref:System.Xml.Linq.XCData>.  
  
## Note  
 Le sezioni CDATA XML contengono testo non elaborato che deve essere incluso, ma non analizzato, nell'XML che lo contiene.  Una sezione CDATA XML può contenere qualsiasi testo.  Inclusi caratteri XML riservati.  La sezione CDATA XML termina con la sequenza"\]\] \> ".  Questa condizione implica quanto segue:  
  
-   Non è possibile utilizzare un'espressione incorporata in un valore letterale CDATA XML perché i delimitatori dell'espressione incorporata sono contenuti CDATA XML validi.  
  
-   Le sezioni CDATA XML non possono essere annidate, perché `content` non può contenere il valore"\]\] \> ".  
  
 È possibile assegnare un valore letterale CDATA XML a una variabile, o includerla in un valore letterale di un elemento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe ma non utilizzare caratteri di continuazione di riga.  Questo permette di copiare il contenuto da un documento XML e incollarlo direttamente in un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte il valore letterale CDATA XML in una chiamata al costruttore <xref:System.Xml.Linq.XCData.%23ctor%2A>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come crea una sezione CDATA che contiene il testo "Può contenere i tag del valore letterale \<XML\>"  
  
 [!code-vb[VbXMLSamples#23](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-cdata-literal_1.vb)]  
  
## Vedere anche  
 <xref:System.Xml.Linq.XCData>   
 [XML Element Literal](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)