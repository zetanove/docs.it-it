---
title: Valore letterale commento XML (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralComment
dev_langs:
- VB
helpviewer_keywords:
- comment literal [Visual Basic]
- XML comments, adding [Visual Basic]
- XML comment literal [Visual Basic]
- XML literals [Visual Basic], comment
ms.assetid: 634c1cee-5e01-48d0-88d7-2dd55e4a9e52
caps.latest.revision: 19
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 88cfb984be42345ae1e5c998cf82aa1415d2455e
ms.lasthandoff: 03/13/2017

---
# <a name="xml-comment-literal-visual-basic"></a>Valore letterale di commento XML (Visual Basic)
Un valore letterale che rappresenta un <xref:System.Xml.Linq.XComment>oggetto.</xref:System.Xml.Linq.XComment>  
  
## <a name="syntax"></a>Sintassi  
  
```  
<!-- content -->  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`<!--`|Obbligatorio. Indica l'inizio del commento XML.|  
|`content`|Obbligatorio. Testo da visualizzare nel commento XML. Non può contenere una serie di due trattini (-) o terminare con un trattino adiacente al tag di chiusura.|  
|`-->`|Obbligatorio. Indica la fine del commento XML.|  
  
## <a name="return-value"></a>Valore restituito  
 Un <xref:System.Xml.Linq.XComment>oggetto.</xref:System.Xml.Linq.XComment>  
  
## <a name="remarks"></a>Note  
 Valori letterali di commento XML non contengono il contenuto del documento; esse contengono informazioni relative al documento. La sezione di commento XML termina con la sequenza "-->". Ciò implica i seguenti punti:  
  
-   È possibile utilizzare un'espressione incorporata in un valore letterale di commento XML perché i delimitatori di espressione incorporata sono contenuti di commento XML validi.  
  
-   Le sezioni di commento XML non possono essere annidate, perché `content` non può contenere il valore "-->".  
  
 È possibile assegnare un valore letterale di commento XML a una variabile oppure è possibile includere in un valore letterale elemento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga. Questa funzionalità consente di copiare il contenuto di un documento XML e incollarlo direttamente in un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma.  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte il valore letterale di commento XML a una chiamata al <xref:System.Xml.Linq.XComment.%23ctor%2A>costruttore.</xref:System.Xml.Linq.XComment.%23ctor%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un commento XML che contiene il testo "Questo è un commento".  
  
 [!code-vb[9 VbXMLSamples](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-comment-literal_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XComment>   
 [Valore letterale elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
