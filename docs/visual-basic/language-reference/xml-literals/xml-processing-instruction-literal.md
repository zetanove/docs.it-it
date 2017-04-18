---
title: Valore letterale istruzione (Visual Basic) di elaborazione XML | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlLiteralProcessingInstruction
dev_langs:
- VB
helpviewer_keywords:
- XML literals [Visual Basic], processing instruction
- XML processing instruction literal [Visual Basic]
- processing instruction literal [Visual Basic]
ms.assetid: cef4f7f8-0011-4f64-8602-795077ad4f15
caps.latest.revision: 19
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
ms.openlocfilehash: 2903297fa22cd8dc10bc4b12abaa754d4f6284f2
ms.lasthandoff: 03/13/2017

---
# <a name="xml-processing-instruction-literal-visual-basic"></a>Valore letterale istruzione di elaborazione XML (Visual Basic)
Un valore letterale che rappresenta un <xref:System.Xml.Linq.XProcessingInstruction>oggetto.</xref:System.Xml.Linq.XProcessingInstruction>  
  
## <a name="syntax"></a>Sintassi  
  
```  
<?piName [ = piData ] ?>  
```  
  
## <a name="parts"></a>Parti  
 `<?`  
 Obbligatorio. Indica l'inizio dell'istruzione di elaborazione XML letterale.  
  
 `piName`  
 Obbligatorio. Assegnare un nome che indica l'applicazione di destinazioni delle istruzioni di elaborazione. Non può iniziare con "xml" o "XML".  
  
 `piData`  
 Facoltativo. Stringa che indica come l'applicazione di destinazione da `piName` deve elaborare il documento XML.  
  
 `?>`  
 Obbligatorio. Indica la fine dell'istruzione di elaborazione.  
  
## <a name="return-value"></a>Valore restituito  
 Un <xref:System.Xml.Linq.XProcessingInstruction>oggetto.</xref:System.Xml.Linq.XProcessingInstruction>  
  
## <a name="remarks"></a>Note  
 Valori letterali di istruzione di elaborazione XML indicano quali applicazioni devono elaborare un documento XML. Quando un'applicazione viene caricato un documento XML, l'applicazione può controllare le istruzioni di elaborazione XML per determinare come elaborare il documento. L'applicazione interpreta il significato di `piName` e `piData`.  
  
 Il valore letterale documento XML utilizza una sintassi simile a quello dell'istruzione di elaborazione XML. Per ulteriori informazioni, vedere [XML Document Literal](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md).  
  
> [!NOTE]
>  Il `piName` elemento non può iniziare con le stringhe "xml" o "XML", perché la specifica XML 1.0 tali identificatori sono riservati.  
  
 È possibile assegnare una valore letterale istruzione di elaborazione di XML a una variabile o includerlo in un valore letterale documento XML.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza caratteri di continuazione di riga. Ciò consente di copiare il contenuto da un documento XML e incollarlo direttamente in un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma.  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte il valore letterale istruzione di elaborazione di XML a una chiamata al <xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A>costruttore.</xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creata un'istruzione di elaborazione che identifica un foglio di stile per un documento XML.  
  
 [!code-vb[28 VbXMLSamples](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-processing-instruction-literal_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XProcessingInstruction>   
 [Valore letterale documento XML](../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
