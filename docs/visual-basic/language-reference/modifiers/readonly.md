---
title: "ReadOnly (Visual Basic) | Microsoft Docs"
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
  - "vb.ReadOnly"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ReadOnly keyword"
  - "variables [Visual Basic], read-only"
  - "ReadOnly property"
  - "properties [Visual Basic], read-only"
  - "read-only variables"
ms.assetid: e868185d-6142-4359-a2fd-a7965cadfce8
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# ReadOnly (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che è possibile leggere ma non scrivere una variabile o una proprietà.  
  
## Note  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare la parola chiave `ReadOnly` solo a livello di modulo.  In altri termini, il contesto della dichiarazione per un elemento `ReadOnly` deve essere una classe, una struttura o un modulo e non può essere un file di origine, uno spazio dei nomi o una routine.  
  
-   **Modificatori combinati.** Non è possibile specificare `ReadOnly` insieme a `Static` nella stessa dichiarazione.  
  
-   **Assegnazione di un valore.** Il codice che utilizza una proprietà `ReadOnly` non può impostarne il valore,  ma il codice che può accedere alla memoria sottostante può assegnare o modificare tale valore in qualsiasi momento.  
  
     È possibile assegnare un valore a una variabile `ReadOnly` solo nella relativa dichiarazione o nel costruttore di una classe o di una struttura in cui la variabile è definita.  
  
## Utilizzo di una variabile ReadOnly  
 Esistono casi in cui non è possibile utilizzare un'[Const Statement](../../../visual-basic/language-reference/statements/const-statement.md) per dichiarare e assegnare un valore costante.  Ad esempio, è possibile che l'istruzione `Const` non accetti il tipo di dati che si desidera assegnare o che non si sia in grado di calcolare il valore in fase di compilazione con un'espressione costante.  È possibile perfino che non si conosca tale valore in fase di compilazione.  In questi casi, è possibile utilizzare una variabile `ReadOnly` per contenere un valore costante.  
  
> [!IMPORTANT]
>  Se il tipo di dati della variabile è un tipo di riferimento, ad esempio una matrice o un'istanza di classe, i relativi membri possono essere modificati anche se la variabile stessa è `ReadOnly`.  Questa condizione è illustrata nell'esempio che segue.  
  
 `ReadOnly characterArray() As Char = {"x"c, "y"c, "z"c}`  
  
 `Sub changeArrayElement()`  
  
 `characterArray(1) = "M"c`  
  
 `End Sub`  
  
 Una volta inizializzata, la matrice a cui punta `characterArray()` conterrà "x", "y" e "z".  Poiché la variabile `characterArray` è `ReadOnly`, non è possibile modificarne il valore dopo l'inizializzazione, ovvero non è possibile assegnare ad essa una nuova matrice.  È tuttavia possibile modificare i valori di uno o più membri della matrice.  In seguito a una chiamata alla routine `changeArrayElement`, la matrice a cui punta `characterArray()` conterrà "x", "M" e "z".  
  
 Questa situazione equivale a dichiarare un parametro di routine [ByVal](../../../visual-basic/language-reference/modifiers/byval.md), impedendo alla routine di modificare l'argomento chiamante ma non i relativi membri.  
  
## Esempio  
 Nell'esempio riportato di seguito viene definita una proprietà `ReadOnly` per la data di assunzione di un dipendente.  La classe memorizza internamente il valore della proprietà come variabile `Private` e tale valore può essere modificato solo dal codice interno alla classe.  Tuttavia, poiché la proprietà è `Public`, può essere letta da qualsiasi codice in grado di accedere alla classe.  
  
 [!code-vb[VbVbalrKeywords#4](../../../visual-basic/language-reference/codesnippet/VisualBasic/readonly_1.vb)]  
  
 Il modificatore `ReadOnly` può essere utilizzato nei seguenti contesti:  
  
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## Vedere anche  
 [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)