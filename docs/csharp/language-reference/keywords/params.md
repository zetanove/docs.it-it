---
title: "params (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "params_CSharpKeyword"
  - "params"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "parametri [C#], params"
  - "params (parola chiave) [C#]"
ms.assetid: 1690815e-b52b-4967-8380-5780aff08012
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# params (Riferimenti per C#)
Utilizzando la parola chiave `params`, è possibile specificare un [parametro di metodo](../../../csharp/language-reference/keywords/method-parameters.md) che utilizza un numero variabile di argomenti.  
  
 È possibile inviare un elenco di argomenti separato da virgole del tipo specificato nella dichiarazione di parametri o una matrice di argomenti del tipo specificato.  È inoltre possibile non inviare alcun argomento.  Se non vengono inviati argomenti, la lunghezza dell'elenco `params` è zero.  
  
 In una dichiarazione di metodo non è possibile aggiungere ulteriori parametri dopo la parola chiave `params` ed è consentito l'uso di una sola parola chiave `params`.  
  
## Esempio  
 Nell'esempio seguente vengono dimostrate le varie modalità nelle quali è possibile inviare argomenti al parametro `params`.  
  
 [!code-cs[csrefKeywordsMethodParams#5](../../../csharp/language-reference/keywords/codesnippet/csharp/params_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parametri di metodo](../../../csharp/language-reference/keywords/method-parameters.md)