---
title: "Operatori di conversione (Guida per programmatori C#) | Microsoft Docs"
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
  - "C# (linguaggio), operatori di conversione"
  - "operatori di conversione [C#]"
  - "operatori [C#], conversione"
  - "conversioni definite dall'utente [C#]"
ms.assetid: c5ad73a3-d57b-4d2b-b4c9-24e3c2856efc
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatori di conversione (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il linguaggio C\# consente ai programmatori di dichiarare conversioni su classi o strutture in modo che le classi o le strutture possano essere convertite in e\/o da altre classi o strutture oppure tipi di base.  Le conversioni vengono definite come operatori e vengono denominate sulla base del tipo verso cui viene effettuata la conversione.  Il tipo dell'argomento da convertire oppure il tipo del risultato della conversione, ma non entrambi, deve essere il tipo che lo contiene.  
  
 [!code-cs[csProgGuideStatements#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/conversion-operators_1.cs)]  
  
## Cenni preliminari sugli operatori di conversione  
 Di seguito sono riportate le caratteristiche principali degli operatori di conversione:  
  
-   Le conversioni dichiarate come `implicit` vengono eseguite automaticamente in caso di necessità.  
  
-   Per chiamare conversioni dichiarate come `explicit`, è necessario un cast.  
  
-   Tutte le conversioni devono essere dichiarate `static`.  
  
## Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Utilizzo degli operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md)  
  
-   [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
  
-   [Procedura: implementare conversioni tra struct definite dall'utente](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)  
  
-   [esplicita](../../../csharp/language-reference/keywords/explicit.md)  
  
-   [impliciti](../../../csharp/language-reference/keywords/implicit.md)  
  
-   [statiche](../../../csharp/language-reference/keywords/static.md)  
  
## Vedere anche  
 <xref:System.Convert>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Conversioni esplicite definite dall'utente concatenate in C](http://go.microsoft.com/fwlink/?LinkId=112384)