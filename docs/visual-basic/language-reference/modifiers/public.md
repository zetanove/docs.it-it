---
title: "Public (Visual Basic) | Microsoft Docs"
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
  - "vb.Public"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Public keyword"
  - "Public keyword, syntax"
  - "Public access modifier"
ms.assetid: 284c9e1b-ed23-499b-9bc9-ad87c11485a5
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Public (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che uno o più elementi di programmazione dichiarati non presentano restrizioni di accesso.  
  
## Note  
 Se si pubblica un componente o un insieme di componenti, ad esempio una libreria di classi, solitamente si richiede che gli elementi di programmazione siano accessibili a tutto il codice che interagisce con l'assembly.  Per conferire tale accesso illimitato a un elemento, è possibile dichiararlo con la parola chiave `Public`.  
  
 L'accesso pubblico è il livello normale per un elemento di programmazione a cui non sia necessario limitare l'accesso.  Se non diversamente dichiarato, il livello di accesso di un elemento dichiarato all'interno di un'interfaccia, un modulo, una classe o una struttura è per impostazione predefinita `Public`.  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare la parola chiave `Public` solo a livello di modulo, di interfaccia o di spazio dei nomi.  In altri termini, il contesto della dichiarazione per un elemento `Public` deve essere un file di origine, uno spazio dei nomi, un'interfaccia, un modulo, una classe o una struttura, ma non può essere una routine.  
  
## Comportamento  
  
-   **Livello di accesso.** Tutto il codice in grado di accedere a un modulo, una classe o una struttura può accedere ai relativi elementi `Public`.  
  
-   **Accesso predefinito.** Le variabili locali all'interno di una routine per impostazione predefinita dispongono di accesso pubblico e non è possibile utilizzare modificatori di accesso per tali variabili.  
  
-   **Modificatori di accesso.** Le parole chiave che specificano il livello di accesso sono dette *modificatori di accesso*.  Per un confronto tra i modificatori di accesso, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Il modificatore `Public` può essere utilizzato nei seguenti contesti:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Istruzione Const](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Istruzione Enum](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Istruzione Module](../../../visual-basic/language-reference/statements/module-statement.md)  
  
 [Istruzione Operator](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)