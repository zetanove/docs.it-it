---
title: "Type arguments could not be inferred from the delegate | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36564"
  - "vbc36564"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36564"
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# Type arguments could not be inferred from the delegate
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'istruzione di assegnazione utilizza `AddressOf` per assegnare l'indirizzo di una routine generica a un delegato, ma non fornisce alcun argomento di tipo alla routine generica.  
  
 Generalmente, quando si richiama un tipo generica, si fornisce un argomento di tipo per ogni parametro di tipo definito dal tipo generico.  Se non viene fornito alcun argomento di tipo, il compilatore tenta di dedurre i tipi da passare ai parametri di tipo.  Se il contesto non fornisce informazioni sufficienti per consentire al compilatore di dedurre i tipi, verrà generato un errore.  
  
 **ID errore:** BC36564  
  
### Per correggere l'errore  
  
-   Specificare gli argomenti di tipi per la routine generica nell'espressione `AddressOf`.  
  
## Vedere anche  
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [AddressOf Operator](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Generic Procedures in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)   
 [Type List](../../../visual-basic/language-reference/statements/type-list.md)   
 [Metodi di estensione](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)