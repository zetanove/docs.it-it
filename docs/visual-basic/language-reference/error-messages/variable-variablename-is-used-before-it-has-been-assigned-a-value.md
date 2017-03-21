---
title: Variabile &quot;&lt;NomeVariabile&gt;&quot; viene utilizzato prima che sia stato assegnato un valore | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42104
- BC42104
dev_langs:
- VB
helpviewer_keywords:
- BC42104
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
caps.latest.revision: 10
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
ms.openlocfilehash: 7ad1f392fae2f90e366277b7b531d96011648866
ms.lasthandoff: 03/13/2017

---
# <a name="variable-39ltvariablenamegt39-is-used-before-it-has-been-assigned-a-value"></a>Variabile '&lt;NomeVariabile&gt;' viene utilizzato prima che sia stato assegnato un valore
Variabile '\<nomevariabile >' viene utilizzato prima che sia stato assegnato un valore. È possibile che in fase di esecuzione venga restituita un'eccezione dovuta a un riferimento Null.  
  
 Un'applicazione dispone di almeno un percorso possibile tramite il codice che legge una variabile prima che venga assegnato qualsiasi valore.  
  
 Se a una variabile non è mai stato assegnato alcun valore, questa manterrà il valore predefinito per il tipo di dati. Per un tipo di dati di riferimento, il valore predefinito è [nulla](../../../visual-basic/language-reference/nothing.md). Lettura di una variabile di riferimento con un valore di `Nothing` può causare un <xref:System.NullReferenceException>in alcune circostanze.</xref:System.NullReferenceException>  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42104  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Controllare la logica del flusso di controllo e assicurarsi che la variabile ha un valore valido prima che il controllo passa all'istruzione che legge.  
  
-   Un modo per garantire che la variabile ha sempre un valore valido consiste nell'inizializzare come parte della relativa dichiarazione. Vedere "Inizializzazione" in [istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Dichiarazione di variabile](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Risoluzione dei problemi relativi alle variabili](../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)
