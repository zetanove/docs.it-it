---
title: "XML Comment Literal (Visual Basic) | Microsoft Docs"
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
  - "vb.XmlLiteralComment"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "comment literal [Visual Basic]"
  - "XML comments, adding [Visual Basic]"
  - "XML comment literal [Visual Basic]"
  - "XML literals [Visual Basic], comment"
ms.assetid: 634c1cee-5e01-48d0-88d7-2dd55e4a9e52
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML Comment Literal (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Valore letterale che rappresenta un oggetto <xref:System.Xml.Linq.XComment>.  
  
## Sintassi  
  
```  
<!-- content -->  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`<!--`|Obbligatorio.  Indica l'inizio del commento XML.|  
|`content`|Obbligatorio.  Testo che appare nel commento XML.  Non può contenere una serie di due trattini \(\-\-\) o terminare con un trattino adiacente al tag di chiusura.|  
|`-->`|Obbligatorio.  Indica la fine del commento XML.|  
  
## Valore restituito  
 Un oggetto <xref:System.Xml.Linq.XComment>.  
  
## Note  
 I valori letterali di commento di XML non contengono il contenuto del documento; contengono informazioni sul documento.  La sezione di commento XML termina con la sequenza "\-\-\>".  Questa condizione implica quanto segue:  
  
-   Non è possibile utilizzare un'espressione incorporata in un valore letterale di commento XML perché i delimitatori dell'espressione incorporata sono contenuti validi per il commento XML.  
  
-   Le sezioni di commento XML non possono essere annidate, perché `content` non può contenere il valore "\-\-\>".  
  
 È possibile assegnare un valore letterale di commento XML a una variabile, oppure includerla in un valore letterale di un elemento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga.  Questa funzionalità permette di copiare il contenuto da un documento XML e incollarlo direttamente in un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte il valore letterale di commento XML a una chiamata al costruttore <xref:System.Xml.Linq.XComment.%23ctor%2A>.  
  
## Esempio  
 Nell'esempio seguente viene creato un commento XML che contiene il testo "Questo è un commento".  
  
 [!code-vb[VbXMLSamples#9](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-comment-literal_1.vb)]  
  
## Vedere anche  
 <xref:System.Xml.Linq.XComment>   
 [XML Element Literal](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)