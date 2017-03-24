---
title: 'Procedura: incorporare espressioni nei valori letterali XML (Visual Basic) | Documenti di Microsoft'
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
- embedded expressions [Visual Basic]
- XML literals [Visual Basic], embedded expressions
ms.assetid: 75016fad-0141-42de-8564-5051be29487e
caps.latest.revision: 16
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
ms.openlocfilehash: 40b0e4273223093262bc54a2b13d28fc93a44c69
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-embed-expressions-in-xml-literals-visual-basic"></a>Procedura: incorporare espressioni nei valori letterali XML (Visual Basic)
È possibile combinare i valori letterali XML con espressioni incorporate per creare un documento XML, frammento o elemento che contiene contenuto creato in fase di esecuzione. Nell'esempio seguente viene illustrato come utilizzare le espressioni incorporate per popolare i nomi degli elementi, attributi e contenuto di un elemento in fase di esecuzione.  
  
 La sintassi per un'espressione incorporata è `<%=` `exp` `%>`, che è la stessa sintassi che [!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] utilizza. Per ulteriori informazioni, vedere [espressioni incorporate in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 È inoltre possibile utilizzare il [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] API per creare [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetti. Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>  
  
## <a name="procedures"></a>Procedure  
  
#### <a name="to-insert-text-as-element-content"></a>Per inserire un testo come contenuto dell'elemento  
  
-   Nell'esempio seguente viene illustrato come inserire il testo contenuto nel `contactName` variabile tra gli elementi di nomi di apertura e chiusura.  
  
     [!code-vb[VbXMLSamples&#39;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_1.vb)]  
  
     Questo esempio produce il seguente output:  
  
    ```  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-as-an-attribute-value"></a>Per inserire un testo come valore di attributo  
  
-   Nell'esempio seguente viene illustrato come inserire il testo contenuto nel `phoneType` come valore della variabile di `type` attributo.  
  
     [!code-vb[&#40; VbXMLSamples](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_2.vb)]  
  
     Questo esempio produce il seguente output:  
  
    ```  
    <contact>  
      <phone type="home">206-555-0144</phone>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-for-an-element-name"></a>Per inserire del testo per un nome di elemento  
  
-   Nell'esempio seguente viene illustrato come inserire il testo contenuto nel `elementName` variabile come il nome di un elemento.  
  
     Quando si creano elementi utilizzando questa tecnica, è necessario chiudere con il \</ > tag.  
  
     [!code-vb[VbXMLSamples n.&41;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-embed-expressions-in-xml-literals_3.vb)]  
  
     Questo esempio produce il seguente output:  
  
    ```  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: creare valori letterali XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-create-xml-literals.md)   
 [Espressioni incorporate in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
