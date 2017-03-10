---
title: "Private (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Private"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Private keyword"
  - "Private keyword, syntax"
ms.assetid: aba74a2e-5824-4613-bf63-b9ec7787f4e6
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Private (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che uno o più elementi di programmazione dichiarati sono accessibili solo nel rispettivo contesto della dichiarazione, anche all'interno di eventuali tipi contenuti.  
  
## Note  
 L'accesso a un elemento di programmazione che rappresenta una funzionalità proprietaria o contiene dati riservati viene generalmente limitato il più possibile.   Per ottenere il livello massimo di limitazione, consentire l'accesso all'elemento solo al modulo, alla classe o alla struttura che lo definiscono.  Per limitare l'accesso a un elemento in questo modo, è possibile eseguirne la dichiarazione mediante `Private`.  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare la parola chiave `Private` solo a livello di modulo.  In altri termini, il contesto della dichiarazione per un elemento `Private` deve essere un modulo, una classe o una struttura e non può essere un file di origine, uno spazio dei nomi, un'interfaccia o una routine.  
  
## Comportamento  
  
-   **Livello di accesso.** Tutto il codice presente in un contesto della dichiarazione può accedere agli elementi `Private` di tale contesto.  Viene incluso quindi anche il codice all'interno di un tipo contenuto, ad esempio una classe annidata o un'espressione di assegnazione in un'enumerazione.  Il codice al di fuori del contesto della dichiarazione non può accedere agli elementi `Private` di tale contesto.  
  
-   **Modificatori di accesso.** Le parole chiave che specificano il livello di accesso sono dette *modificatori di accesso*.  Per un confronto tra i modificatori di accesso, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Il modificatore `Private` può essere utilizzato nei seguenti contesti:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Istruzione Const](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Istruzione Enum](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)