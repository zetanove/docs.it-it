---
title: "Vincolo new (Riferimenti per C#) | Microsoft Docs"
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
  - "new (parola chiave di vincolo) [C#]"
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Vincolo new (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il vincolo `new` specifica che qualsiasi argomento di tipo di una dichiarazione di classe generica deve disporre di un costruttore pubblico senza parametri.  Per utilizzare il nuovo vincolo, il tipo non può essere astratto.  
  
## Esempio  
 Applicare il vincolo `new` a un parametro del tipo quando la classe generica crea nuove istanze del tipo, come illustrato nel seguente esempio:  
  
 [!code-cs[csrefKeywordsOperator#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-constraint_1.cs)]  
  
## Esempio  
 Quando il vincolo `new()` viene utilizzato con altri vincoli, è necessario specificarlo per ultimo:  
  
 [!code-cs[csrefKeywordsOperator#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-constraint_2.cs)]  
  
 Per ulteriori informazioni, vedere [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)