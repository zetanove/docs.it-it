---
title: "Checked e Unchecked (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "checked (istruzione) [C#]"
  - "eccezioni [C#], controllo di overflow"
  - "operatori [C#], checked e unchecked"
  - "controllo di overflow [C#]"
  - "istruzioni [C#], checked e unchecked"
  - "unchecked (istruzione) [C#]"
ms.assetid: a84bc877-2c7f-4396-8735-1ce97c42f35e
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Checked e Unchecked (Riferimenti per C#)
È possibile eseguire istruzioni C\# in contesti verificati o non verificati.  In un contesto verificato l'overflow aritmetico genera un'eccezione.  In un contesto non verificato l'overflow aritmetico viene ignorato e il risultato è troncato.  
  
-   [checked](../../../csharp/language-reference/keywords/checked.md) Specificare il contesto verificato.  
  
-   [unchecked](../../../csharp/language-reference/keywords/unchecked.md) Specificare il contesto non verificato.  
  
 Se né `checked` né `unchecked` vengono specificati, il contesto predefinito dipende da fattori esterni, ad esempio le opzioni del compilatore.  
  
 Le operazioni seguenti sono interessate dal controllo di overflow:  
  
-   Espressioni che usano gli operatori predefiniti seguenti su tipi integrali:  
  
     `++`  `--` \- \(unary\)   `+` \-   `*` `/`  
  
-   Conversioni numeriche esplicite tra tipi integrali.  
  
 L'opzione del compilatore [\/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md) consente di specificare il contesto verificato o non verificato per tutte le istruzioni aritmetiche integrali che non rientrano in modo esplicito nell'ambio di una parola chiave `checked` o `unchecked`.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per le istruzioni](../../../csharp/language-reference/keywords/statement-keywords.md)