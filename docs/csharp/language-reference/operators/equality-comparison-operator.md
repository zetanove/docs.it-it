---
title: "Operatore == (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "==_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "== (operatore) [C#]"
  - "operatore di uguaglianza [C#]"
ms.assetid: 34c6b597-caa2-4855-a7cd-38ecdd11bd07
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Operatore == (Riferimenti per C#)
Per i tipi di valore predefiniti, l'operatore di uguaglianza \(`==`\) restituisce true se i valori degli operandi sono uguali e `false` in caso contrario.  Per i tipi di riferimento diversi da [string](../../../csharp/language-reference/keywords/string.md), l'operatore `==` restituisce `true` se i due operandi si riferiscono allo stesso oggetto.  Per il tipo `string`, l'operatore `==` confronta i valori delle stringhe.  
  
## Note  
 I tipi di valore definiti dall'utente possono eseguire l'overload dell'operatore `==` \(per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md),  al pari dei tipi di riferimento definiti dall'utente, sebbene, in base all'impostazione predefinita, l'operatore `==` si comporti come descritto in precedenza sia per tipi di riferimento predefiniti che per quelli definiti dall'utente.  Se si esegue l'overload dell'operatore `==`, è necessario sottoporre a overload anche l'operatore [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#36](../../../csharp/language-reference/operators/codesnippet/CSharp/equality-comparison-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)