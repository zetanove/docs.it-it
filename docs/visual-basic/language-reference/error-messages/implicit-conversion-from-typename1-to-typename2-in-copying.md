---
title: "Implicit conversion from &#39;&lt;typename1&gt;&#39; to &#39;&lt;typename2&gt;&#39; in copying the value of &#39;ByRef&#39; parameter &#39;&lt;parametername&gt;&#39; back to the matching argument. | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc41999"
  - "bc41999"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC41999"
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Implicit conversion from &#39;&lt;typename1&gt;&#39; to &#39;&lt;typename2&gt;&#39; in copying the value of &#39;ByRef&#39; parameter &#39;&lt;parametername&gt;&#39; back to the matching argument.
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una procedura viene chiamata con un argomento [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) di un tipo diverso da quello del suo parametro corrispondente.  
  
 Se si passa un argomento `ByRef`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] copia a volte il valore dell'argomento in una variabile locale nella routine invece di passare un riferimento.  In tal caso, al ritorno della routine stessa, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] dovrà quindi copiare il valore della variabile locale nell'argomento del codice che effettua la chiamata.  
  
 Se il valore di un argomento `ByRef` viene copiato nella procedura e l'argomento e il parametro sono dello stesso tipo, non sarà necessaria alcuna conversione.  Nel caso in cui i tipi siano diversi, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] dovrà consentire la conversione in entrambe le direzioni.  Poiché non è possibile utilizzare `CType` o una qualsiasi delle altre parole chiave di conversione su un argomento o parametro di routine, tale conversione è sempre implicita.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:**  BC41999  
  
### Per correggere l'errore  
  
-   Se possibile, utilizzare un argomento chiamante dello stesso tipo del parametro della routine in modo che [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] non debba eseguire nessun altra conversione.  
  
-   Per chiamare la procedura con un tipo di argomento diverso dal tipo di parametro ma non è necessario restituire un valore nel codice chiamante, definire il parametro in modo che sia [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) invece di `ByRef`.  
  
## Vedere anche  
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Passing Arguments by Value and by Reference](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)