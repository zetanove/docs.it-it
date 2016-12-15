---
title: "Generic parameters used as optional parameter types must be class constrained | Microsoft Docs"
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
  - "vbc32124"
  - "bc32124"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32124"
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Generic parameters used as optional parameter types must be class constrained
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È stata dichiarata una routine con un parametro facoltativo che utilizza un parametro di tipo non vincolato ad essere un tipo di riferimento.  
  
 È sempre necessario fornire un valore predefinito per ciascun parametro facoltativo.  Se il parametro è di tipo riferimento, il valore facoltativo deve essere `Nothing` che rappresenta un valore valido per qualsiasi tipo di riferimento.  Se tuttavia il parametro è di tipo valore, deve trattarsi di un tipo di dati elementare predefinito da Visual Basic  in quanto un tipo di valore composito, come ad esempio una struttura definita dall'utente, non ha un valore predefinito valido.  
  
 Quando si utilizza un parametro di tipo per un parametro facoltativo, è necessario accertarsi che sia del tipo riferimento per evitare la possibilità che venga utilizzato un parametro di tipo valore senza valore predefinito valido.  Questo implica che occorre vincolare il parametro di tipo con la parola chiave `Class` o con il nome di una classe specifica.  
  
 **ID errore:** BC32124  
  
### Per correggere l'errore  
  
-   Vincolare il parametro di tipo in modo che accetti soltanto un tipo di riferimento oppure non utilizzarlo per il parametro facoltativo.  
  
## Vedere anche  
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Type List](../../../visual-basic/language-reference/statements/type-list.md)   
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Optional Parameters](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Nothing](../../../visual-basic/language-reference/nothing.md)