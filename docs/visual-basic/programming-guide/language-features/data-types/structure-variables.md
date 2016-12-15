---
title: "Structure Variables (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "structures, variables"
  - "structures, structure variables"
  - "variables [Visual Basic], structure variables"
  - "structure variables"
ms.assetid: 156872f8-aabc-4454-8e2d-f2253c3c13c9
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Structure Variables (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Dopo aver creato una struttura, è possibile dichiarare variabili a livello di routine e a livello di modulo con tale tipo.  Ad esempio, è possibile creare una struttura che registri informazioni relative a un sistema di computer.  Nell'esempio che segue viene illustrato quanto descritto.  
  
```  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public purchaseDate As Date  
End Structure  
```  
  
 Sarà quindi possibile dichiarare variabili di tale tipo.  Nella dichiarazione che segue viene illustrato quanto descritto.  
  
```  
Dim mySystem, yourSystem As systemInfo  
```  
  
> [!NOTE]
>  L'impostazione predefinita per le strutture dichiarate con l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) nelle classi e nei moduli è l'accesso pubblico.  Se si desidera che una struttura sia privata, accertarsi di dichiararla con la parola chiave [Private](../../../../visual-basic/language-reference/modifiers/private.md).  
  
## Accesso ai valori di una struttura  
 Per assegnare e recuperare valori dagli elementi di una variabile di struttura, si ricorre alla stessa sintassi utilizzata per impostare e visualizzare le proprietà di un oggetto.  L'operatore di accesso ai membri \(`.`\) deve essere collocato tra il nome della variabile di struttura e il nome dell'elemento.  Nell'esempio che segue si accede agli elementi delle variabili dichiarate in precedenza come tipo `systemInfo`.  
  
```  
mySystem.cPU = "486"  
Dim tooOld As Boolean  
If yourSystem.purchaseDate < #1/1/1992# Then tooOld = True  
```  
  
## Assegnazione di variabili di struttura  
 È inoltre possibile assegnare una variabile a un'altra se entrambe presentano lo stesso tipo di struttura.  In questo modo tutti gli elementi di una struttura vengono copiati nei corrispondenti elementi dell'altra.  Nella dichiarazione che segue viene illustrato quanto descritto.  
  
```  
yourSystem = mySystem  
```  
  
 Se un elemento di struttura è un tipo riferimento, quale `String`, `Object` o matrice, verrà copiato il puntatore al dato.  Se in `systemInfo` fosse stata inclusa una variabile oggetto, l'esempio precedente avrebbe consentito la copia del puntatore da `mySystem` a `yourSystem` e una modifica apportata ai dati dell'oggetto mediante una struttura sarebbe risultata attiva se l'accesso a tali dati fosse stato effettuato mediante l'altra struttura.  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [How to: Declare a Structure](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Structures and Other Programming Elements](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [Structures and Classes](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md)