---
title: "Protected (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Protected"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Protected Friend keyword combination"
  - "Protected keyword, and Friend"
  - "Protected keyword, syntax"
  - "Protected access modifier"
  - "Protected keyword"
ms.assetid: 74ad3d56-309f-49d2-b60c-1d0157d010e8
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Protected (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che uno o più elementi di programmazione dichiarati sono accessibili solo dall'interno delle rispettive classi o da una classe derivata.  
  
## Note  
 Talvolta un elemento di programmazione dichiarato in una classe contiene dati sensibili o codice con restrizioni cui si desidera limitare l'accesso.  Se, tuttavia, la classe è ereditabile e si prevede una gerarchia di classi derivate, potrebbe essere necessario consentire l'accesso ai dati o al codice da parte di tali classi derivate.  In questo caso, si desidera che l'elemento sia accessibile sia dalla classe base che da tutte le classi derivate.  Per limitare l'accesso a un elemento in questo modo, è possibile eseguirne la dichiarazione mediante `Protected`.  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare `Protected` solo a livello di classe.  In altri termini, il contesto della dichiarazione per un elemento `Protected` deve essere una classe e non un file di origine, uno spazio dei nomi, un'interfaccia, un modulo, una struttura o una routine.  
  
-   **Modificatori combinati.** È possibile utilizzare il modificatore `Protected` insieme al modificatore [Friend](../../../visual-basic/language-reference/modifiers/friend.md) nella stessa dichiarazione.  Questa combinazione rende gli elementi dichiarati accessibili da qualsiasi punto dello stesso assembly, dalla rispettiva classe e dalle classi derivate.  È possibile specificare `Protected Friend` solo su membri di classi.  
  
## Comportamento  
  
-   **Livello di accesso.** Tutto il codice presente in una classe può accedere agli elementi di tale classe.  Il codice di una classe che deriva da una classe base può accedere a tutti gli elementi `Protected` della classe base.  Ciò è valido per tutte le generazioni di derivazione  e indica che una classe può accedere a elementi `Protected` della classe base della classe base e così via.  
  
     L'accesso Protected non è un superset o un sottoinsieme dell'accesso Friend.  
  
-   **Modificatori di accesso.** Le parole chiave che specificano il livello di accesso sono dette *modificatori di accesso*.  Per un confronto tra i modificatori di accesso, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Il modificatore `Protected` può essere utilizzato nei seguenti contesti:  
  
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
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)