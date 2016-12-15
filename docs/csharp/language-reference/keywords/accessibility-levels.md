---
title: "Livelli di accessibilit&#224; (Riferimenti per C#) | Microsoft Docs"
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
  - "modificatori di accesso [C#], livelli di accessibilità"
  - "livelli di accessibilità"
ms.assetid: dc083921-0073-413e-8936-a613e8bb7df4
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Livelli di accessibilit&#224; (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Utilizzare i modificatori di accesso [public](../../../csharp/language-reference/keywords/public.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o [private](../../../csharp/language-reference/keywords/private.md) per specificare uno dei seguenti livelli di accessibilità dichiarate per i membri.  
  
|Accessibilità dichiarata|Significato|  
|------------------------------|-----------------|  
|`public`|Nessuna restrizione di accesso.|  
|`protected`|L'accesso è limitato alla classe di appartenenza o ai tipi derivati dalla classe di appartenenza.|  
|`internal`|L'accesso è limitato all'assembly corrente.|  
|`protected` `internal`|L'accesso è limitato all'assembly corrente o ai tipi derivati dalla classe di appartenenza.|  
|`private`|L'accesso è limitato al tipo di appartenenza.|  
  
 È consentito utilizzare un solo modificatore di accesso per un membro o un tipo, tranne nel caso in cui si utilizzi la combinazione `protected` `internal`.  
  
 I modificatori di accesso non sono utilizzabili sugli spazi dei nomi, i quali  non presentano restrizioni di accesso.  
  
 A seconda del contesto in cui si verifica la dichiarazione di un membro, sono consentite solo determinate accessibilità dichiarate.  Se nella dichiarazione di un membro non è stato specificato alcun modificatore di accesso, verrà utilizzato un valore di accessibilità predefinito.  
  
 I tipi di primo livello, non annidati in altri tipi, possono disporre solo di un'accessibilità di tipo `internal` o `public`.  L'accessibilità predefinita per questi tipi è `internal`.  
  
 I tipi annidati, che sono membri di altri tipi, possono avere le accessibilità dichiarate elencate nella tabella seguente.  
  
|Membro di|Accessibilità predefinita del membro|Accessibilità dichiarata consentita per il membro|  
|---------------|------------------------------------------|-------------------------------------------------------|  
|`enum`|`public`|Nessuno|  
|`class`|`private`|`public`<br /><br /> `protected`<br /><br /> `internal`<br /><br /> `private`<br /><br /> `protected` `internal`|  
|`interface`|`public`|Nessuno|  
|`struct`|`private`|`public`<br /><br /> `internal`<br /><br /> `private`|  
  
 L'accessibilità di un tipo annidato dipende dal [dominio di accessibilità](../../../csharp/language-reference/keywords/accessibility-domain.md), che varia a seconda dell'accessibilità dichiarata del membro e del dominio di accessibilità del tipo che lo contiene direttamente.  Tuttavia il dominio di accessibilità di un tipo annidato non può essere superiore a quello del tipo che lo contiene.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Dominio di accessibilità](../../../csharp/language-reference/keywords/accessibility-domain.md)   
 [Restrizioni relative all'utilizzo dei livelli di accessibilità](../../../csharp/language-reference/keywords/restrictions-on-using-accessibility-levels.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)