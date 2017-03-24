---
title: "Operatore -- (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "--_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-- (operatore) [C#]"
  - "decremento (operatore) (--) [C#]"
ms.assetid: 6b9cfe86-63c7-421f-9379-c9690fea8720
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Operatore -- (Riferimenti per C#)
L'operatore di decremento \(`--`\) decrementa il proprio operando di 1.  L'operatore di decremento può essere visualizzato prima o dopo il proprio operando: `--variable` e `variable--`.  Il primo formato rappresenta un'operazione di decremento prefissa.  Il risultato dell'operazione corrisponde al valore dell'operando dopo il decremento.  Il secondo formato rappresenta un'operazione di decremento suffissa.  Il risultato dell'operazione corrisponde al valore dell'operando prima del decremento.  
  
## Note  
 I tipi numerici e di enumerazione hanno operatori di decremento già definiti.  
  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `--`. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#8](../../../csharp/language-reference/operators/codesnippet/CSharp/decrement-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)