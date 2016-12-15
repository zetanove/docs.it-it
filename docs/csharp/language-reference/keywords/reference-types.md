---
title: "Tipi di riferimento (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "cs.referencetypes"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, tipi di riferimento"
  - "tipi di riferimento [C#]"
  - "tipi [C#], tipi di riferimento"
ms.assetid: 801cf030-6e2d-4a0d-9daf-1431b0c31f47
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Tipi di riferimento (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Esistono due generi di tipo in C\#: tipi di riferimento e tipi di valore.  Le variabili dei tipi di riferimento archiviano i riferimenti ai relativi dati \(oggetti\), mentre le variabili dei tipi di valore contengono direttamente i dati.  Con i tipi di riferimento, due variabili possono fare riferimento allo stesso oggetto. Di conseguenza le operazioni su una variabile possono influire sull'oggetto a cui fa riferimento l'altra variabile.  Con i tipi di valore, ogni variabile ha una propria copia dei dati e non è possibile che le operazioni su una variabile influiscano sull'altra \(tranne nel caso delle variabili dei parametri out e ref, vedere [ref](../../../csharp/language-reference/keywords/ref.md) e [Modificatore del parametro out](../../../csharp/language-reference/keywords/out-parameter-modifier.md)\).  
  
 Le seguenti parole chiave vengono utilizzate per dichiarare i tipi di riferimento:  
  
-   [classe](../../../csharp/language-reference/keywords/class.md)  
  
-   [interfaccia](../../../csharp/language-reference/keywords/interface.md)  
  
-   [delegato](../../../csharp/language-reference/keywords/delegate.md)  
  
 In c\# sono disponibili i seguenti tipi di riferimento predefiniti:  
  
-   [dynamic](../../../csharp/language-reference/keywords/dynamic.md)  
  
-   [object](../../../csharp/language-reference/keywords/object.md)  
  
-   [string](../../../csharp/language-reference/keywords/string.md)  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)