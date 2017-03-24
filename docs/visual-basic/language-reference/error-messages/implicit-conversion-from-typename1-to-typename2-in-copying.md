---
title: La conversione implicita da &quot;&lt;NomeTipo1&gt;&quot;a&quot;&lt;in NomeTipo2&gt;&quot;in copiando il valore del parametro &quot;ByRef&quot; &quot;&lt;parametername&gt;&quot; argomento corrispondente. | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc41999
- bc41999
dev_langs:
- VB
helpviewer_keywords:
- BC41999
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
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
ms.openlocfilehash: e397241aab78e17ea4efde0ea682d0e237fb8f8a
ms.lasthandoff: 03/13/2017

---
# <a name="implicit-conversion-from-39lttypename1gt39-to-39lttypename2gt39-in-copying-the-value-of-39byref39-parameter-39ltparameternamegt39-back-to-the-matching-argument"></a>La conversione implicita da '&lt;NomeTipo1&gt;'a'&lt;in NomeTipo2&gt;'in copiando il valore del parametro 'ByRef' '&lt;parametername&gt;' argomento corrispondente.
Viene chiamata una routine con un [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) argomento di tipo diverso rispetto a quello del parametro corrispondente.  
  
 Se si passa un argomento `ByRef`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] talvolta copia il valore dell'argomento in una variabile locale nella routine anziché passare un riferimento. In tal caso, quando viene restituito, la procedura [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] dovrà quindi copiare il valore della variabile locale nell'argomento nel codice chiamante.  
  
 Se un valore dell'argomento `ByRef` viene copiato nella routine e l'argomento e il parametro sono dello stesso tipo, non è necessaria alcuna conversione. Tuttavia, se i tipi sono diversi, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] necessario convertirli in entrambe le direzioni. Poiché non è possibile utilizzare `CType` o una delle altre parole chiave di conversione in un argomento di routine o parametro, tale conversione è sempre implicita.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC41999  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se possibile, utilizzare un argomento chiamante dello stesso tipo del parametro di routine, pertanto [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non è necessario effettuare alcuna conversione.  
  
-   Se è necessario chiamare la routine con un argomento di tipo diverso dal tipo di parametro ma non è necessario restituire un valore nell'argomento di chiamata, definire il parametro come [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) anziché `ByRef`.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Gli argomenti e parametri di routine](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Passaggio di argomenti per valore e per riferimento](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Conversioni implicite ed esplicite](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
