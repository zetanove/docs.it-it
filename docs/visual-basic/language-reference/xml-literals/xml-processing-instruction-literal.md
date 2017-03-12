---
title: "XML Processing Instruction Literal (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralProcessingInstruction"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML literals [Visual Basic], processing instruction"
  - "XML processing instruction literal [Visual Basic]"
  - "processing instruction literal [Visual Basic]"
ms.assetid: cef4f7f8-0011-4f64-8602-795077ad4f15
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# XML Processing Instruction Literal (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Valore letterale che rappresenta un oggetto <xref:System.Xml.Linq.XProcessingInstruction>.  
  
## Sintassi  
  
```  
<?piName [ = piData ] ?>  
```  
  
## Parti  
 `<?`  
 Obbligatorio.  Indica l'inizio del valore letterale dell'istruzione di elaborazione XML.  
  
 `piName`  
 Obbligatorio.  Nome che indica l'applicazione di destinazione dell'istruzione di elaborazione.  Non può iniziare con "xml" o "XML".  
  
 `piData`  
 Parametro facoltativo.  Stringa che indica come l'applicazione di destinazione per `piName` deve elaborare il documento XML.  
  
 `?>`  
 Obbligatorio.  Indica la fine dell'istruzione di elaborazione.  
  
## Valore restituito  
 Un oggetto <xref:System.Xml.Linq.XProcessingInstruction>.  
  
## Note  
 I valori letterali di istruzione di elaborazione XML indicano quali applicazioni devono elaborare un documento XML.  Quando un'applicazione carica un documento XML, l'applicazione può controllare le istruzioni di elaborazione XML per determinare come elaborare il documento.  L'applicazione interpreta il significato di `piName` e `piData`.  
  
 Il valore letterale del documento XML utilizza una sintassi che è simile a quella dell'istruzione di elaborazione XML.  Per ulteriori informazioni, vedere [XML Document Literal](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md).  
  
> [!NOTE]
>  L'elemento `piName` non può iniziare con le stringhe "xml" o "XML", perché nelle specifiche XML 1.0 tali identificatori sono riservati.  
  
 È possibile assegnare un'istruzione di elaborazione XML a una variabile, oppure includerla in un valore letterale di un documento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza richiedere caratteri di continuazione di riga.  Questo permette di copiare il contenuto da un documento XML e incollarlo direttamente in un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] converte il valore letterale di un'istruzione di elaborazione XML a una chiamata al costruttore <xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A>.  
  
## Esempio  
 Nell'esempio seguente viene creata un'istruzione di elaborazione che identifica un foglio di stile per un documento XML.  
  
 [!code-vb[VbXMLSamples#28](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-processing-instructi_1.vb)]  
  
## Vedere anche  
 <xref:System.Xml.Linq.XProcessingInstruction>   
 [XML Document Literal](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)