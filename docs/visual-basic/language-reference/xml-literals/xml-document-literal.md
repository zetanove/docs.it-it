---
title: "XML Document Literal (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralDocument"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML document literal [Visual Basic]"
  - "XML literals [Visual Basic], document"
  - "XML documents [Visual Basic], creating"
  - "document literal [Visual Basic]"
ms.assetid: f7bbee56-0911-41de-b907-96f20450137b
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# XML Document Literal (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Valore letterale che rappresenta un oggetto <xref:System.Xml.Linq.XDocument>.  
  
## Sintassi  
  
```  
<?xml version="1.0" [encoding="encoding"] [standalone="standalone"] ?>  
[ piCommentList ]  
rootElement  
[ piCommentList ]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`encoding`|Parametro facoltativo.  Testo letterale che dichiara la codifica utilizzata dal documento.|  
|`standalone`|Parametro facoltativo.  Testo letterale.  Deve essere "sì" o "no."|  
|`piCommentList`|Parametro facoltativo.  Elenco di istruzioni di elaborazione e commenti XML.  Assume il seguente formato:<br /><br /> `piComment [` `piComment` `... ]`<br /><br /> Ogni `piComment` ``  può essere uno dei seguenti:<br /><br /> -   [XML Processing Instruction Literal](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md).<br />-   [XML Comment Literal](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md).|  
|`rootElement`|Obbligatorio.  Elemento di primo livello del documento.  Il formato è uno dei seguenti:<br /><br /> <ul><li>[XML Element Literal](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).</li><li>Espressione incorporata del formato `<%=` `elementExp` `%>`.  `elementExp` restituisce uno dei seguenti:<br /><br /> <ul><li>Un oggetto <xref:System.Xml.Linq.XElement>.</li><li>Raccolta che contiene un oggetto <xref:System.Xml.Linq.XElement> e un numero qualsiasi di oggetti <xref:System.Xml.Linq.XProcessingInstruction> e <xref:System.Xml.Linq.XComment>.</li></ul></li></ul><br /> Per ulteriori informazioni, vedere [Embedded Expressions in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).|  
  
## Valore restituito  
 Un oggetto <xref:System.Xml.Linq.XDocument>.  
  
## Note  
 Un valore letterale del documento XML viene identificato dalla dichiarazione XML all'inizio del valore letterale.  Anche se ogni valore letterale del documento XML deve avere esattamente un elemento XML radice, può avere un qualsiasi numero di istruzioni di elaborazione e commenti XML.  
  
 Un valore letterale del documento XML non può trovarsi in un elemento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga.  Questo permette di copiare il contenuto da un documento XML e incollarlo direttamente in un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] converte il valore letterale del documento XML a chiamate ai costruttori <xref:System.Xml.Linq.XDocument.%23ctor%2A> e <xref:System.Xml.Linq.XDeclaration.%23ctor%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creato un documento XML che ha una dichiarazione XML, un'istruzione di elaborazione, un commento e un elemento che contiene un altro elemento.  
  
 [!code-vb[VbXMLSamples#30](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-document-literal_1.vb)]  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 <xref:System.Xml.Linq.XProcessingInstruction>   
 <xref:System.Xml.Linq.XComment>   
 <xref:System.Xml.Linq.XDocument>   
 [XML Processing Instruction Literal](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)   
 [XML Comment Literal](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)   
 [XML Element Literal](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Embedded Expressions in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)