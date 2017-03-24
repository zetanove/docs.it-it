---
title: "MustOverride (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.MustOverride"
  - "MustOverride"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "virtual elements, pure"
  - "elements, pure virtual"
  - "properties [Visual Basic], redefining"
  - "procedures, overriding"
  - "overriding, MustOverride keyword"
  - "procedures, redefining"
  - "pure virtual elements"
  - "MustOverride keyword"
  - "properties [Visual Basic], overriding"
ms.assetid: 6e9d9ad6-bb64-433f-b32b-3ef84293bf96
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# MustOverride (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che una proprietà o una routine non è implementata in questa classe e deve essere sottoposta a override in una classe derivata per poter essere utilizzata.  
  
## Note  
 È possibile utilizzare `MustOverride` solo in un'istruzione per la dichiarazione di proprietà o routine.  La proprietà o la routine che specifica `MustOverride` deve essere membro di una classe contrassegnata con [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md).  
  
## Regole  
  
-   **Dichiarazione incompleta.** Quando si specifica `MustOverride`, non si forniscono righe aggiuntive di codice per la proprietà o la routine, né per l'istruzione `End Function`, `End Property` o `End Sub`.  
  
-   **Modificatori combinati.** Non è possibile specificare `MustOverride` insieme a `NotOverridable`, `Overridable` o `Shared` nella stessa dichiarazione.  
  
-   **Shadowing e override.** Sebbene lo shadowing e l'override ridefiniscano entrambi un elemento ereditato, esistono sostanziali differenze tra i due metodi.  Per ulteriori informazioni, vedere [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md).  
  
-   **Termini alternativi.** Un elemento che non può essere utilizzato tranne che in un override viene talvolta definito elemento *virtuale puro*.  
  
 Il modificatore `MustOverride` può essere utilizzato nei seguenti contesti:  
  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)