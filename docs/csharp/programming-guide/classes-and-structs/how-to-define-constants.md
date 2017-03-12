---
title: "Procedura: definire le costanti in C# | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, costanti"
  - "costanti [C#]"
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
caps.latest.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 7
---
# Procedura: definire le costanti in C# #
Le costanti sono campi cui i valori vengono impostati in fase di compilazione e non possono mai essere modificati.  Utilizzare le costanti per specificare nomi significativi anziché valori letterali numerici \("numeri chiave"\) per particolari valori.  
  
> [!NOTE]
>  In C\# la direttiva per il preprocessore [\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) non può essere utilizzata per definire le costanti nel modo adottato in genere in C e C\+\+.  
  
 Per definire i valori costanti di tipi integrali \(`int`, `byte` e così via\) utilizzare un tipo enumerato.  Per ulteriori informazioni, vedere [enum](../../../csharp/language-reference/keywords/enum.md).  
  
 Per definire le costanti non integrali, è possibile raggrupparle in una sola classe statica denominata `Constants`.  A questo scopo sarà necessario che tutti i riferimenti alle costanti siano preceduti dal nome della classe, come illustrato nell'esempio seguente.  
  
## Esempio  
 [!code-cs[csProgGuideObjects#89](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-define-constants_1.cs)]  
  
 L'utilizzo del qualificatore del nome della classe consente di fare in modo che tutti gli utenti che utilizzano la costante comprendano che si tratta di una costante e che non può essere modificata.  
  
## Vedere anche  
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)