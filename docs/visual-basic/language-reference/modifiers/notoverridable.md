---
title: "NotOverridable (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.NotOverridable"
  - "NotOverridable"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "sealed methods"
  - "NotOverridable keyword"
  - "properties [Visual Basic], redefining"
  - "elements, sealed"
  - "sealed elements"
  - "procedures, overriding"
  - "procedures, redefining"
  - "overriding"
  - "methods [Visual Basic], sealed"
  - "properties [Visual Basic], overriding"
ms.assetid: 66ec6984-f5f5-4857-b362-6a3907aaf9e0
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# NotOverridable (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che non è possibile eseguire l'override di una proprietà o di una routine in una classe derivata.  
  
## Note  
 `NotOverridable` il modificatore impedisce una proprietà o un metodo venga sottoposto a override in una classe derivata.  [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md) il modificatore consente una proprietà o un metodo in una classe di cui eseguire l'override in una classe derivata.  Per ulteriori informazioni, vedere [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md).  
  
 se `Overridable` o  `NotOverridable` il modificatore non viene specificato, per impostazione predefinita dipende dal fatto che la proprietà o il metodo esegue l'override di una proprietà o un metodo di classe base.  Se la proprietà o il metodo esegue l'override di una proprietà o un metodo di classe base, l'impostazione predefinita è `Overridable`; in caso contrario, viene  `NotOverridable`.  
  
 Un elemento non sottoponibile a override è talvolta definito *sealed*.  
  
 È possibile utilizzare `NotOverridable` solo in un'istruzione per la dichiarazione di proprietà o routine.  L'impostazione di `NotOverridable` è consentita solo in una proprietà o routine che esegue l'override di un'altra proprietà o routine, ovvero solo in combinazione con `Overrides`.  
  
## modificatori combinati  
 Non è possibile specificare `Overridable` o  `NotOverridable` per una proprietà  `Private` metodo.  
  
 Non è possibile specificare `NotOverridable` insieme a `MustOverride`, `Overridable` o `Shared` nella stessa dichiarazione.  
  
## Utilizzo  
 Il modificatore `NotOverridable` può essere utilizzato nei seguenti contesti:  
  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Modifiers](../../../visual-basic/language-reference/modifiers/index.md)   
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)