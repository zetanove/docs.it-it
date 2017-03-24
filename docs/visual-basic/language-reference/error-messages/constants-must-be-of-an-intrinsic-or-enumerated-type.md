---
title: "Constants must be of an intrinsic or enumerated type, not a class, structure, type parameter, or array type | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30424"
  - "bc30424"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30424"
ms.assetid: 2d402c2f-27ad-428b-b699-d45cd62f7196
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Constants must be of an intrinsic or enumerated type, not a class, structure, type parameter, or array type
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Si è tentato di dichiarare una costante come tipo classe, struttura o matrice oppure come parametro di tipo definito da un tipo generico che lo contiene.  
  
 Le costanti devono essere di tipo intrinseco \(`Boolean`, `Byte`, `Date`, `Decimal`, `Double`, `Integer`, `Long`, `Object`, `SByte`, `Short`, `Single`, `String`, `UInteger`, `ULong` o `UShort`\) o di tipo `Enum` basato su uno dei tipi integrali.  
  
 **ID errore:** BC30424  
  
### Per correggere l'errore  
  
1.  Dichiarare la costante come intrinseca o di tipo `Enum`.  
  
2.  Una costante può anche essere costituita da un valore speciale, ad esempio `True`, `False` o `Nothing`.  Il compilatore considera tali valori predefiniti del tipo intrinseco appropriato.  
  
## Vedere anche  
 [Constants and Enumerations](../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [Riepilogo dei tipi di dati](../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)