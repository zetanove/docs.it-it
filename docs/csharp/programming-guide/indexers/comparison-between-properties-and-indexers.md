---
title: "Confronto tra propriet&#224; e indicizzatori (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "indicizzatori [C#], e proprietà"
  - "proprietà [C#], e indicizzatori"
ms.assetid: 3358a89f-44a0-4a4d-bf8c-07237a90af39
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Confronto tra propriet&#224; e indicizzatori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli indicizzatori sono come proprietà.  A eccezione delle differenze riportate nella tabella che segue, tutte le regole definite per le funzioni di accesso delle proprietà sono valide anche per le funzioni di accesso degli indicizzatori.  
  
|Proprietà|Indicizzatore|  
|---------------|-------------------|  
|Consente di chiamare i metodi come se fossero membri dati pubblici.|Consente di accedere a elementi di una raccolta interna di un oggetto utilizzando la notazione di matrice sull'oggetto stesso.|  
|Accessibile tramite un nome semplice.|Accessibile tramite un indice.|  
|Può essere un membro statico o di istanza.|Deve essere un membro di istanza.|  
|La funzione di accesso [get](../../../csharp/language-reference/keywords/get.md) di una proprietà non ha parametri.|La funzione di accesso `get` di un indicizzatore ha lo stesso elenco di parametri formali dell'indicizzatore.|  
|La funzione di accesso [set](../../../csharp/language-reference/keywords/set.md) di una proprietà contiene il parametro implicito `value`.|La funzione di accesso `set` di un indicizzatore ha lo stesso elenco di parametri formali dell'indicizzatore, oltre al parametro [value](../../../csharp/language-reference/keywords/value.md).|  
|Supporta la sintassi abbreviata con [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).|Non supporta la sintassi abbreviata.|  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)