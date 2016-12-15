---
title: "Initializer expected | Microsoft Docs"
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
  - "vbc30996"
  - "bc30996"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30996"
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Initializer expected
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Si è tentato di dichiarare un'istanza di una classe utilizzando un inizializzatore di oggetto in cui l'elenco di inizializzazione è vuoto, come mostrato nell'esempio seguente.  
  
 `' Not valid.`  
  
 `' Dim aStudent As New Student With {}`  
  
 È necessario che sia inizializzato almeno un campo o una proprietà nell'elenco di inizializzatori, come mostrato nell'esempio seguente.  
  
 `Dim aStudent As New Student With {.year = "Senior"}`  
  
 **ID errore:** BC30996  
  
### Per correggere l'errore  
  
1.  Inizializzare almeno un campo o una proprietà nell'inizializzatore o non utilizzare un inizializzatore di oggetto.  
  
## Vedere anche  
 [Object Initializers: Named and Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [How to: Declare an Object by Using an Object Initializer](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)