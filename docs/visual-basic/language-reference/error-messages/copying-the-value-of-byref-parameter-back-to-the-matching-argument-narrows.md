---
title: "Copying the value of &#39;ByRef&#39; parameter &#39;&lt;parametername&gt;&#39; back to the matching argument narrows from type &#39;&lt;typename1&gt;&#39; to type &#39;&lt;typename2&gt;&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32053"
  - "vbc32053"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32053"
ms.assetid: 281564b7-99f7-451f-b10d-f985e831bb25
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Copying the value of &#39;ByRef&#39; parameter &#39;&lt;parametername&gt;&#39; back to the matching argument narrows from type &#39;&lt;typename1&gt;&#39; to type &#39;&lt;typename2&gt;&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine viene chiamata con un argomento che viene convertito nel tipo di parametro corrispondente più grande, mentre la conversione dal parametro all'argomento è verso un tipo di dati più piccolo.  
  
 Quando viene definita una classe o struttura, è possibile definire uno o più operatori di conversione per convertire quel tipo di classe o struttura in altri tipi.  È inoltre possibile definire operatori di conversione inversa per riconvertire gli altri tipi nel tipo di classe o struttura di origine.  Quando si utilizza il tipo di classe o struttura in una chiamata di routine, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] può utilizzare questi operatori di conversione per convertire il tipo di un argomento nel tipo del parametro corrispondente.  
  
 Se si passa l'argomento [ByRef](../../../visual-basic/language-reference/modifiers/byref.md), talvolta [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] copia il valore dell'argomento in una variabile locale nella routine anziché passare un riferimento.  In tal caso, al ritorno della routine stessa, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] dovrà quindi copiare il valore della variabile locale nell'argomento del codice che effettua la chiamata.  
  
 Se il valore di un argomento `ByRef` viene copiato nella procedura e l'argomento e il parametro sono dello stesso tipo, non sarà necessaria alcuna conversione.  Nel caso in cui i tipi siano diversi, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] dovrà consentire la conversione in entrambe le direzioni.  Se uno dei tipi corrisponde al tipo della classe o struttura, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] deve convertirlo da e verso l'altro tipo.  Se una di queste conversioni è verso un tipo di dati più grande, la conversione inversa è verso un tipo di dati più piccolo.  
  
 **ID errore:** BC32053  
  
### Per correggere l'errore  
  
-   Se possibile, utilizzare un argomento chiamante dello stesso tipo del parametro della routine in modo che [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] non debba eseguire nessun altra conversione.  
  
-   Per chiamare la procedura con un tipo di argomento diverso dal tipo di parametro ma non è necessario restituire un valore nel codice chiamante, definire il parametro in modo che sia [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) invece di `ByRef`.  
  
-   Se è necessario che venga restituito un valore nell'argomento di chiamata, definire l'operatore di conversione inversa come [Widening](../../../visual-basic/language-reference/modifiers/widening.md), se possibile.  
  
## Vedere anche  
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Passing Arguments by Value and by Reference](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [How to: Define an Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [How to: Define a Conversion Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Type Conversions in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)