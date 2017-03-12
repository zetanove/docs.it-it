---
title: "Declaration Contexts and Default Access Levels (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "module level, defined"
  - "declaration contexts, Visual Basic"
  - "procedure level, defined"
  - "namespace level, defined"
  - "access levels, Visual Basic"
  - "access levels, default levels"
ms.assetid: bf63b96e-e825-4745-88c8-5dae222728db
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Declaration Contexts and Default Access Levels (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento vengono descritti i tipi di Visual Basic che è possibile dichiarare all'interno di altri tipi e i relativi livelli di accesso predefiniti qualora non ne venga specificato uno in particolare.  
  
## Livelli dei contesti delle dichiarazioni  
 Il *contesto della dichiarazione* di un elemento di programmazione è l'area del codice in cui viene dichiarato.  Si tratta spesso di un altro elemento di programmazione, che viene quindi definito *elemento contenitore*.  
  
 Di seguito sono riportati i livelli dei contesti delle dichiarazioni:  
  
-   *Livello dello spazio dei nomi*: all'interno di un file di origine o di uno spazio dei nomi, ma non in una classe, una struttura, un modulo o un'interfaccia  
  
-   *Livello del modulo*: all'interno di una classe, una struttura, un modulo o un'interfaccia, ma non in una routine o in un blocco  
  
-   *Livello della routine*: all'interno di una routine o di un blocco, ad esempio `If` o `For`  
  
 Nella tabella riportata di seguito vengono illustrati i livelli di accesso predefiniti per diversi elementi di programmazione dichiarati, in base al rispettivo contesto della dichiarazione.  
  
|Elemento dichiarato|Livello dello spazio dei nomi|Livello del modulo|Livello della routine|  
|-------------------------|-----------------------------------|------------------------|---------------------------|  
|Variabile \([Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)\)|Non consentito|`Private` \(`Public` in `Structure`, non consentito in `Interface`\)|`Public`|  
|Costante \([Const Statement](../../../visual-basic/language-reference/statements/const-statement.md)\)|Non consentito|`Private` \(`Public` in `Structure`, non consentito in `Interface`\)|`Public`|  
|Enumerazione \([Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md)\)|`Friend`|`Public`|Non consentito|  
|Classe \([Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)\)|`Friend`|`Public`|Non consentito|  
|Struttura \([Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)\)|`Friend`|`Public`|Non consentito|  
|Modulo \([Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)\)|`Friend`|Non consentito|Non consentito|  
|Interfaccia \([Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)\)|`Friend`|`Public`|Non consentito|  
|Routine \([Function Statement](../../../visual-basic/language-reference/statements/function-statement.md), [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)\)|Non consentito|`Public`|Non consentito|  
|Riferimento esterno \([Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)\)|Non consentito|`Public` \(non consentito in `Interface`\)|Non consentito|  
|Operatore \([Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)\)|Non consentito|`Public` \(non consentito in `Interface` o `Module`\)|Non consentito|  
|Proprietà \([Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)\)|Non consentito|`Public`|Non consentito|  
|Proprietà predefinita \([Default](../../../visual-basic/language-reference/modifiers/default.md)\)|Non consentito|`Public` \(non consentito in `Module`\)|Non consentito|  
|Evento \([Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)\)|Non consentito|`Public`|Non consentito|  
|Delegato \([Delegate Statement](../../../visual-basic/language-reference/statements/delegate-statement.md)\)|`Friend`|`Public`|Non consentito|  
  
 Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Vedere anche  
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)