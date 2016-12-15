---
title: "parziale (Metodo) (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "partialmethod_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "metodi parziali [C#]"
ms.assetid: 43f40242-17e0-4452-8573-090503ad3137
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# parziale (Metodo) (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un metodo parziale ha la firma definita in una parte di un tipo parziale e l'implementazione definita in un'altra parte del tipo.  I metodi parziali consentono a Progettazione classi di fornire gli hook del metodo, analoghi ai gestori eventi, che gli sviluppatori possono decidere se implementare.  Se lo sviluppatore non fornisce un'implementazione, il compilatore rimuove la firma in fase di compilazione.  Ai metodi parziali si applicano le seguenti condizioni:  
  
-   Le firme in entrambe le parti del tipo parziale devono corrispondere.  
  
-   Il metodo deve restituire void.  
  
-   Non è consentito nessun modificatore di accesso.  I metodi parziali sono implicitamente privati.  
  
 Nell'esempio seguente viene illustrato un metodo parziale definito in due parti di una classe parziale:  
  
 [!code-cs[csrefKeywordsContextual#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/partial-method_1.cs)]  
  
 Per ulteriori informazioni, vedere [Classi e metodi parziali](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [parziale \(Tipo\)](../../../csharp/language-reference/keywords/partial-type.md)