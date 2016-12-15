---
title: "Overrides (Visual Basic) | Microsoft Docs"
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
  - "Overrides"
  - "vb.Overrides"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "properties [Visual Basic], redefining"
  - "procedures, overriding"
  - "procedures, redefining"
  - "overriding"
  - "Overrides keyword"
  - "overriding, Overrides keyword"
  - "properties [Visual Basic], overriding"
ms.assetid: 9f5e6144-ce10-465e-842b-1a8f8760af90
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Overrides (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che una proprietà o una routine esegue l'override di una proprietà o una routine con nome identico ereditata da una classe base.  
  
## Note  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile usare `Overrides` solo in un'istruzione per la dichiarazione di proprietà o routine.  
  
-   **Modificatori combinati.** Non è possibile specificare `Overrides` insieme a `Shadows` o `Shared` nella stessa dichiarazione.  Poiché un elemento che esegue l'override può essere implicitamente sottoposto a override, non è possibile combinare `Overridable` e `Overrides`.  
  
-   **Firme corrispondenti.** La firma di questa dichiarazione deve corrispondere esattamente alla *firma* della proprietà o della routine sottoposta a override.  In altre parole, gli elenchi di parametri devono presentare lo stesso numero di parametri, nel medesimo ordine, e contenere gli stessi tipi di dati.  
  
     Oltre alla firma, la dichiarazione che esegue l'override deve anche corrispondere esattamente a quanto segue.  
  
    -   Livello di accesso  
  
    -   Tipo restituito, se disponibile  
  
-   **Firme generiche.** Nel caso di una routine generica la firma include il numero di parametri del tipo.  La dichiarazione che esegue l'override, quindi, deve corrispondere alla versione della classe base anche in relazione a tali caratteristiche.  
  
-   **Corrispondenze aggiuntive.** Oltre a corrispondere alla firma della versione della classe base, la dichiarazione deve presentare anche le corrispondenze seguenti:  
  
    -   Modificatore a livello di accesso \(ad esempio [Public](../../../visual-basic/language-reference/modifiers/public.md)\)  
  
    -   Meccanismo di passaggio di ogni parametro \([ByVal](../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../visual-basic/language-reference/modifiers/byref.md)\)  
  
    -   Elenchi di vincoli su ogni parametro di tipo di una routine generica  
  
-   **Shadowing e override.** Sebbene lo shadowing e l'override ridefiniscano entrambi un elemento ereditato, tra i due metodi esistono differenze sostanziali.  Per altre informazioni, vedere [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md).  
  
 Se si usa `Overrides`, il compilatore aggiunge implicitamente `Overloads` in modo che le API della libreria funzionino più facilmente con C\#.  
  
 Il modificatore `Overrides` può essere usato nei contesti seguenti:  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Type List](../../../visual-basic/language-reference/statements/type-list.md)