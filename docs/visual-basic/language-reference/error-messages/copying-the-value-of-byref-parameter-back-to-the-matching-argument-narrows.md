---
title: Quando il valore del parametro &quot;ByRef&quot; &quot;&lt;parametername&gt;&quot;argomento corrispondente viene convertito dal tipo&quot;&lt;NomeTipo1&gt;&quot; al tipo&quot;&lt;in NomeTipo2&gt;&quot; | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc32053
- vbc32053
dev_langs:
- VB
helpviewer_keywords:
- BC32053
ms.assetid: 281564b7-99f7-451f-b10d-f985e831bb25
caps.latest.revision: 8
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
ms.openlocfilehash: 84574006b2e2ccc669fdd83ebfb6eec06b00f041
ms.lasthandoff: 03/13/2017

---
# <a name="copying-the-value-of-39byref39-parameter-39ltparameternamegt39-back-to-the-matching-argument-narrows-from-type-39lttypename1gt39-to-type-39lttypename2gt39"></a>Quando il valore del parametro 'ByRef' '&lt;parametername&gt;'argomento corrispondente viene convertito dal tipo'&lt;NomeTipo1&gt;' al tipo'&lt;in NomeTipo2&gt;'
Una procedura viene chiamata con un argomento che può ampliarsi nel tipo di parametro corrispondente, e la conversione dal parametro dell'argomento è più piccolo.  
  
 Quando si definisce una classe o una struttura, è possibile definire uno o più operatori di conversione per convertire il tipo della classe o della struttura in altri tipi. È anche possibile definire operatori di conversione inversi per riconvertire gli altri tipi nel tipo della classe o della struttura originale. Quando si utilizza il tipo di classe o struttura in una chiamata di procedura [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] possibile utilizzare gli operatori di conversione per convertire il tipo di un argomento per il tipo del parametro corrispondente.  
  
 Se si passa l'argomento [ByRef](../../../visual-basic/language-reference/modifiers/byref.md), [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] talvolta copia il valore dell'argomento in una variabile locale nella procedura anziché passare un riferimento. In tal caso, quando viene restituito, la procedura [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] dovrà quindi copiare il valore della variabile locale nell'argomento nel codice chiamante.  
  
 Se un valore dell'argomento `ByRef` viene copiato nella routine e l'argomento e il parametro sono dello stesso tipo, non è necessaria alcuna conversione. Tuttavia, se i tipi sono diversi, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] necessario convertirli in entrambe le direzioni. Se uno dei tipi è il tipo di classe o struttura, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] deve convertire da e verso l'altro tipo. Se una di queste conversioni è un ampliamento, potrebbe limitare la conversione inversa.  
  
 **ID errore:** BC32053  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se possibile, utilizzare un argomento chiamante dello stesso tipo del parametro di routine, pertanto [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non è necessario effettuare alcuna conversione.  
  
-   Se è necessario chiamare la routine con un argomento di tipo diverso dal tipo di parametro ma non è necessario restituire un valore nell'argomento di chiamata, definire il parametro come [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) anziché `ByRef`.  
  
-   Se si desidera restituire un valore nell'argomento di chiamata, definire l'operatore di conversione inversa come [Widening](../../../visual-basic/language-reference/modifiers/widening.md), se possibile.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Gli argomenti e parametri di routine](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Passaggio di argomenti per valore e per riferimento](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Routine di operatore](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Operator (istruzione)](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Procedura: definire un operatore](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [Procedura: definire un operatore di conversione](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Conversioni di tipi in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Conversioni di ampliamento e restrizione](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
