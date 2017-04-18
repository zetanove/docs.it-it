---
title: Valore letterale documento XML (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralDocument
dev_langs:
- VB
helpviewer_keywords:
- XML document literal [Visual Basic]
- XML literals [Visual Basic], document
- XML documents [Visual Basic], creating
- document literal [Visual Basic]
ms.assetid: f7bbee56-0911-41de-b907-96f20450137b
caps.latest.revision: 20
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
ms.openlocfilehash: 5d64faddad66eba4029969654388ba7df17e5854
ms.lasthandoff: 03/13/2017

---
# <a name="xml-document-literal-visual-basic"></a>Valore letterale di documento XML (Visual Basic)
Un valore letterale che rappresenta un <xref:System.Xml.Linq.XDocument>oggetto.</xref:System.Xml.Linq.XDocument>  
  
## <a name="syntax"></a>Sintassi  
  
```  
<?xml version="1.0" [encoding="encoding"] [standalone="standalone"] ?>  
[ piCommentList ]  
rootElement  
[ piCommentList ]  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`encoding`|Facoltativo. Utilizza il testo letterale che dichiara la codifica del documento.|  
|`standalone`|Facoltativo. Testo letterale. Deve essere "yes" o "no".|  
|`piCommentList`|Facoltativo. Elenco di istruzioni di elaborazione e commenti XML. Accetta il formato seguente:<br /><br /> `piComment [` `piComment` `... ]`<br /><br /> Ogni `piComment`può essere uno dei seguenti:<br /><br /> -   [Valore letterale istruzione di elaborazione XML](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md).<br />-   [Valore letterale commento XML](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md).|  
|`rootElement`|Obbligatorio. Elemento radice del documento. Il formato è uno dei seguenti:<br /><br /> <ul><li>[Valore letterale elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).</li><li>Espressione incorporata del formato `<%=` `elementExp` `%>`. Il `elementExp` restituisce uno dei seguenti:<br /><br /> <ul><li>Un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement></li><li>Una raccolta che contiene un <xref:System.Xml.Linq.XElement>oggetto e un numero qualsiasi di <xref:System.Xml.Linq.XProcessingInstruction>e <xref:System.Xml.Linq.XComment>oggetti.</xref:System.Xml.Linq.XComment> </xref:System.Xml.Linq.XProcessingInstruction> </xref:System.Xml.Linq.XElement></li></ul></li></ul><br /> Per ulteriori informazioni, vedere [espressioni incorporate in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).|  
  
## <a name="return-value"></a>Valore restituito  
 Un <xref:System.Xml.Linq.XDocument>oggetto.</xref:System.Xml.Linq.XDocument>  
  
## <a name="remarks"></a>Note  
 Un valore letterale documento XML viene identificato dalla dichiarazione XML all'inizio del valore letterale. Sebbene ogni valore letterale documento XML deve avere esattamente un elemento XML radice, può contenere un numero qualsiasi di istruzioni di elaborazione e commenti XML.  
  
 Un valore letterale documento XML non può trovarsi in un elemento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga. Ciò consente di copiare il contenuto da un documento XML e incollarlo direttamente in un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma.  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte il valore letterale documento XML in chiamate per il <xref:System.Xml.Linq.XDocument.%23ctor%2A>e <xref:System.Xml.Linq.XDeclaration.%23ctor%2A>costruttori.</xref:System.Xml.Linq.XDeclaration.%23ctor%2A> </xref:System.Xml.Linq.XDocument.%23ctor%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un documento XML che dispone di una dichiarazione XML, un'istruzione di elaborazione, un commento e un elemento che contiene un altro elemento.  
  
 [!code-vb[&#30; VbXMLSamples](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-document-literal_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 <xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XProcessingInstruction>   
 <xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XComment>   
 <xref:System.Xml.Linq.XDocument></xref:System.Xml.Linq.XDocument>   
 [Valore letterale istruzione di elaborazione XML](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)   
 [Valore letterale commento XML](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)   
 [Valore letterale elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Espressioni incorporate in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
