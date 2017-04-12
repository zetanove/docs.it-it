---
title: Valore letterale CDATA XML (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralCdata
dev_langs:
- VB
helpviewer_keywords:
- CDATA literal [Visual Basic]
- XML CDATA literal [Visual Basic]
- XML literals [Visual Basic], CDATA
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
caps.latest.revision: 16
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
ms.openlocfilehash: 24e52bf203ff3df57e26137da24abcc2cb7e8e20
ms.lasthandoff: 03/13/2017

---
# <a name="xml-cdata-literal-visual-basic"></a>Valore letterale CDATA XML (Visual Basic)
Un valore letterale che rappresenta un <xref:System.Xml.Linq.XCData>oggetto.</xref:System.Xml.Linq.XCData>  
  
## <a name="syntax"></a>Sintassi  
  
```  
<![CDATA[content]]>  
```  
  
## <a name="parts"></a>Parti  
 `<![CDATA[`  
 Obbligatorio. Indica l'inizio della sezione CDATA XML.  
  
 `content`  
 Obbligatorio. Contenuto di testo da visualizzare nella sezione CDATA XML.  
  
 `]]>`  
 Obbligatorio. Indica la fine della sezione.  
  
## <a name="return-value"></a>Valore restituito  
 Un <xref:System.Xml.Linq.XCData>oggetto.</xref:System.Xml.Linq.XCData>  
  
## <a name="remarks"></a>Note  
 Le sezioni CDATA XML contengono testo non elaborato che deve essere inclusa, ma non analizzato, con il codice XML che lo contiene. Una sezione CDATA XML può contenere qualsiasi testo. Sono inclusi caratteri XML riservati. La sezione CDATA XML termina con la sequenza "]] >". Ciò implica i seguenti punti:  
  
-   È possibile utilizzare un'espressione incorporata in un valore letterale CDATA XML perché i delimitatori di espressione incorporata sono contenuti CDATA XML validi.  
  
-   Le sezioni CDATA XML non possono essere annidate, perché `content` non può contenere il valore "]] >".  
  
 È possibile assegnare un valore letterale CDATA XML a una variabile o includerlo in un valore letterale elemento XML.  
  
> [!NOTE]
>  Un valore letterale XML può estendersi su più righe ma non utilizza caratteri di continuazione di riga. Ciò consente di copiare il contenuto da un documento XML e incollarlo direttamente in un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma.  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte il valore letterale CDATA XML a una chiamata al <xref:System.Xml.Linq.XCData.%23ctor%2A>costruttore.</xref:System.Xml.Linq.XCData.%23ctor%2A>  
  
## <a name="example"></a>Esempio  
 L'esempio seguente crea una sezione CDATA che contiene il testo "può contenere un valore letterale \<XML > tag".  
  
 [!code-vb[VbXMLSamples&#23;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-cdata-literal_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XCData></xref:System.Xml.Linq.XCData>   
 [Valore letterale elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
