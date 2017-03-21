---
title: "Proprietà &quot;&lt;propertyname&gt;&quot; non restituisce un valore in tutti i percorsi di codice | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42107
- vbc42107
dev_langs:
- VB
helpviewer_keywords:
- BC42107
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
caps.latest.revision: 7
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
ms.openlocfilehash: e7c94d827761ad26d517b44a06734c5db4480a62
ms.lasthandoff: 03/13/2017

---
# <a name="property-39ltpropertynamegt39-doesn39t-return-a-value-on-all-code-paths"></a>Proprietà '&lt;propertyname&gt;' non restituisce un valore in tutti i percorsi di codice
Proprietà '\<propertyname >' non restituisce un valore in tutti i percorsi di codice. In fase di esecuzione, quando viene usato il risultato, potrebbe verificarsi un'eccezione dovuta a un riferimento Null.  
  
 Una proprietà `Get` procedura ha almeno un percorso possibile tramite il codice che non restituisce un valore.  
  
 È possibile restituire un valore da una proprietà `Get` procedura in uno dei modi seguenti:  
  
-   Assegnare il valore per il nome della proprietà, quindi eseguire un `Exit Property` istruzione.  
  
-   Assegnare il valore per il nome della proprietà, quindi eseguire il `End Get` istruzione.  
  
-   Includere il valore in un [istruzione Return](../../../visual-basic/language-reference/statements/return-statement.md).  
  
 Se il controllo passa al `Exit Property` o `End Get` e non è stato assegnato alcun valore per il nome della proprietà di `Get` procedura restituisce il valore predefinito del tipo di dati della proprietà. Per ulteriori informazioni, vedere "Comportamento" in [istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42107  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Controllare la logica del flusso di controllo e assicurarsi di assegnare un valore prima di ogni istruzione che provoca una restituzione.  
  
     È più semplice garantire che ogni restituito dalla routine restituisce un valore se si utilizza sempre il `Return` istruzione. In questo caso, l'ultima istruzione prima `End Get` deve essere un `Return` istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà (routine)](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property (istruzione)](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Istruzione Get](../../../visual-basic/language-reference/statements/get-statement.md)
