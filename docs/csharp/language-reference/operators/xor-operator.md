---
title: "Operatore ^ (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "^_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "^ (operatore) [C#]"
  - "operatore OR esclusivo bit per bit [C#]"
ms.assetid: b09bc815-570f-4db6-a637-5b4ed99d014a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Operatore ^ (Riferimenti per C#)
Gli operatori `^` binari sono predefiniti per i tipi integrali e `bool`.  Per i tipi integrali, l'operatore `^` calcola l'OR esclusivo bit per bit degli operandi.  Per gli operandi `bool`, l'operatore `^` calcola l'OR esclusivo logico degli operandi. Il risultato sarà `true` se e solo se uno degli operandi è `true`.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `^`. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#30](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#30)]  
  
 Il calcolo di `0xf8 ^ 0x3f` nell'esempio precedente applica un operatore OR esclusivo bit per bit ai due valori binari seguenti che corrispondono ai valori esadecimali F8 e 3F:  
  
 `1111 1000`  
  
 `0011 1111`  
  
 Il risultato dell'operatore OR esclusivo è `1100 0111`, che corrisponde al valore esadecimale C7.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)