---
title: Spazi vuoti nei valori letterali XML (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- white space [XML in Visual Basic]
- XML literals [Visual Basic], white space
ms.assetid: dfe3a9ff-d69a-418e-a6b5-476f4ed84219
caps.latest.revision: 14
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
ms.openlocfilehash: b98a88696f24cc0b95401812471d13acea4faa6d
ms.lasthandoff: 03/13/2017

---
# <a name="white-space-in-xml-literals-visual-basic"></a>Spazi vuoti nei valori letterali XML (Visual Basic)
Il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore incorpora solo i caratteri spazio vuoto significativo da un valore letterale XML quando viene creato un [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetto. I caratteri spazi vuoti non significativi non vengono incorporati.  
  
## <a name="significant-and-insignificant-white-space"></a>Spazi vuoti significativi e non significativi  
 Gli spazi vuoti nei valori letterali XML sono significativi solo tre aree:  
  
-   Quando si trovano in un valore di attributo.  
  
-   Quando fanno parte dell'elemento contenuto di testo e il testo contiene anche altri caratteri.  
  
-   Quando si trovano in un'espressione incorporata per il contenuto di testo dell'elemento.  
  
 In caso contrario, il compilatore considera gli spazi vuoti non significativi e non li include nel [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetto per il valore letterale.  
  
 Per includere spazi vuoti non significativi in un valore letterale XML, utilizzare un'espressione incorporata che contiene una stringa letterale con lo spazio vuoto.  
  
> [!NOTE]
>  Se il `xml:space` attributo viene visualizzato in un elemento XML letterale, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore include l'attributo di <xref:System.Xml.Linq.XElement>oggetto, ma l'aggiunta di questo attributo non modifica il modo in cui il compilatore considera gli spazi vuoti.</xref:System.Xml.Linq.XElement>  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente contiene due elementi XML, esterni e interni. Entrambi gli elementi contengono spazi vuoti nel contenuto di testo. Lo spazio vuoto nell'elemento esterno non è significativo perché contiene solo spazi vuoti e un elemento XML. Lo spazio vuoto nell'elemento interno è significativo perché contiene spazi vuoti e testo.  
  
 [!code-vb[VbXMLSamples&#29;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/white-space-in-xml-literals_1.vb)]  
  
 Durante l'esecuzione, questo codice viene visualizzato il testo seguente.  
  
```  
<outer>  
  <inner>  
                                          Inner text  
                                      </inner>  
</outer>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
