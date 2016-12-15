---
title: "Overridable (Visual Basic) | Microsoft Docs"
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
  - "Overridable"
  - "vb.Overridable"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "elements, concrete"
  - "properties [Visual Basic], redefining"
  - "overriding, Overridable keyword"
  - "elements, virtual"
  - "virtual elements"
  - "procedures, overriding"
  - "concrete elements"
  - "procedures, redefining"
  - "Overridable keyword"
  - "properties [Visual Basic], overriding"
ms.assetid: 612581e7-8a4c-4a5d-beff-3402fffa6f35
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Overridable (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che a una routine o a una proprietà omonima di una classe derivata è consentito eseguire l'override di una routine o una proprietà definita.  
  
## Note  
 `Overridable` il modificatore consente una proprietà o un metodo in una classe di cui eseguire l'override in una classe derivata.  [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md) il modificatore impedisce una proprietà o un metodo venga sottoposto a override in una classe derivata.  Per ulteriori informazioni, vedere [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md).  
  
 se `Overridable` o  `NotOverridable` il modificatore non viene specificato, per impostazione predefinita dipende dal fatto che la proprietà o il metodo esegue l'override di una proprietà o un metodo di classe base.  Se la proprietà o il metodo esegue l'override di una proprietà o un metodo di classe base, l'impostazione predefinita è `Overridable`; in caso contrario, viene  `NotOverridable`.  
  
 È possibile eseguire lo shadow e l'override per ridefinire un elemento ereditato, ma tra i due approcci esistono differenze notevoli.  Per ulteriori informazioni, vedere [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md).  
  
 Un elemento sottoponibile a override è talvolta definito *virtuale*.  Se può essere sottoposto a override, ma non è necessario che l'override venga eseguito, talvolta viene definito anche elemento *concreto*.  
  
 È possibile utilizzare `Overridable` solo in un'istruzione per la dichiarazione di proprietà o routine.  
  
## modificatori combinati  
 Non è possibile specificare `Overridable` o  `NotOverridable` per una proprietà  `Private` metodo.  
  
 Non è possibile specificare `Overridable` insieme a `MustOverride`, `NotOverridable` o `Shared` nella stessa dichiarazione.  
  
 Poiché un elemento che esegue l'override può essere implicitamente sottoposto a override, non è possibile combinare `Overridable` e `Overrides`.  
  
## Utilizzo  
 Il modificatore `Overridable` può essere utilizzato nei seguenti contesti:  
  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Modifiers](../../../visual-basic/language-reference/modifiers/index.md)   
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)