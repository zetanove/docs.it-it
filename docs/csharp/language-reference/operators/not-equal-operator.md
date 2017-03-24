---
title: "Operatore != (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "!=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "!= (operatore) [C#]"
  - "disuguaglianza (operatore) (!=) [C#]"
  - "diverso da (operatore) (!=) [C#]"
ms.assetid: eeff7a4e-ad6f-462d-9f8d-49e9b91c6c97
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Operatore != (Riferimenti per C#)
L'operatore di disuguaglianza \(`!=`\) restituisce false se gli operandi sono uguali e true in caso contrario.  Gli operatori di disuguaglianza sono già definiti per tutti i tipi, compresi string e object.  I tipi definiti dall'utente possono eseguire l'overload dell'operatore `!=`.  
  
## Note  
 Per i tipi di valore predefiniti, l'operatore di disuguaglianza \(`!=`\) restituisce true se i valori degli operandi sono diversi e false in caso contrario.  Per i tipi di riferimento diversi da `string`, l'operatore `!=` restituisce true se i due operandi si riferiscono a oggetti diversi.  Per il tipo `string`, l'operatore `!=` confronta i valori delle stringhe.  
  
 I tipi di valore definiti dall'utente possono eseguire l'overload dell'operatore `!=` \(per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md)\),  al pari dei tipi di riferimento definiti dall'utente, sebbene, per impostazione predefinita, l'operatore `!=` si comporti come descritto in precedenza sia per tipi di riferimento predefiniti che per quelli definiti dall'utente.  Se si esegue l'overload dell'operatore `!=`, è necessario sottoporre a overload anche l'operatore [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#33](../../../csharp/language-reference/operators/codesnippet/CSharp/not-equal-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)