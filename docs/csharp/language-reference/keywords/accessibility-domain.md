---
title: "Dominio di accessibilit&#224; (Riferimenti per C#) | Microsoft Docs"
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
  - "dominio di accessibilità [C#]"
ms.assetid: 8af779c1-275b-44be-a864-9edfbca71bcc
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Dominio di accessibilit&#224; (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il dominio di accessibilità di un membro specifica in quali sezioni del programma è possibile fare riferimento al membro.  Se il membro è annidato in un altro tipo, il dominio di accessibilità dipenderà sia dal [livello di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md) del membro che dal dominio di accessibilità del tipo che lo contiene direttamente.  
  
 Il dominio di accessibilità di un tipo di primo livello corrisponde almeno al testo di programma del progetto in cui viene dichiarato.  Ovvero, il dominio include tutti i file di origine di questo progetto.  Il dominio di accessibilità di un tipo annidato corrisponde almeno al testo di programma del tipo in cui viene dichiarato,  ossia corrisponde al corpo del tipo, inclusi tutti i tipi annidati.  Il dominio di accessibilità di un tipo annidato non è mai più ampio di quello del tipo che lo contiene.  Questi concetti sono illustrati nell'esempio che segue.  
  
## Esempio  
 In questo esempio viene utilizzato un tipo di primo livello `T1` e due classi annidate, `M1` e `M2`.  Le classi contengono campi con accessibilità dichiarate differenti.  Nel metodo `Main`, ciascuna istruzione è seguita da un commento per indicare il dominio di accessibilità di ciascun membro.  Si noti che le istruzioni che tentano di fare riferimento ai membri non accessibili vengono impostate come commenti.  Per visualizzare gli errori del compilatore provocati da riferimenti a un membro inaccessibile, rimuovere i commenti uno alla volta.  
  
 [!code-cs[csrefKeywordsModifiers#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/accessibility-domain_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [Restrizioni relative all'utilizzo dei livelli di accessibilità](../../../csharp/language-reference/keywords/restrictions-on-using-accessibility-levels.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)