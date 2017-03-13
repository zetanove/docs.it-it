---
title: "add (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "add_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "add (funzione di accesso agli eventi) [C#]"
ms.assetid: faf30b99-10e8-45cd-ab9a-57585d4d1d8d
caps.latest.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 7
---
# add (Riferimenti per C#)
La parola chiave contestuale `add` è utilizzata per definire una funzione di accesso di un evento personalizzato richiamata quando il codice client sottoscrive tale [evento](../../../csharp/language-reference/keywords/event.md).  Se si fornisce una funzione di accesso personalizzata `add`, è necessario fornire anche una funzione di accesso [remove](../../../csharp/language-reference/keywords/remove.md).  
  
## Esempio  
 Nell'esempio seguente viene mostrato un evento che dispone di funzioni di accesso personalizzate `add` e [remove](../../../csharp/language-reference/keywords/remove.md).  Per l'esempio completo, vedere [Procedura: implementare eventi di interfaccia](../../../csharp/programming-guide/events/how-to-implement-interface-events.md).  
  
 [!code-cs[csrefKeywordsContextual#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/add_1.cs)]  
  
 Generalmente non è necessario fornire funzioni di accesso per un evento personalizzato.  Le funzioni di accesso che vengono generate automaticamente dal compilatore quando si dichiara un evento sono sufficienti per la maggior parte degli scenari.  
  
## Vedere anche  
 [Eventi](../../../csharp/programming-guide/events/index.md)