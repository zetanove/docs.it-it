---
title: "Matrici tipizzate in modo implicito (Guida per programmatori C#) | Microsoft Docs"
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
  - "matrici [C#], tipizzate in modo implicito"
  - "linguaggio C#, matrici tipizzate in modo implicito"
  - "matrici tipizzate in modo implicito [C#]"
ms.assetid: e05be95c-6732-403d-ae42-b35f057cbbea
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Matrici tipizzate in modo implicito (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile creare una matrice tipizzata in modo implicito nella quale il tipo dell'istanza della matrice viene dedotto dagli elementi specificata nell'inizializzatore di matrice.  Le regole per qualsiasi variabile tipizzata in modo implicito si applicano anche alle matrici tipizzate in modo implicito.  Per ulteriori informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
 Le matrici tipizzate in modo implicito vengono in genere utilizzate nelle espressioni di query insieme ai tipi anonimi e agli inizializzatori di oggetto e di raccolta.  
  
 Negli esempi seguenti viene illustrato come creare una matrice tipizzata in modo implicito:  
  
 [!code-cs[csProgGuideLINQ#37](../../../csharp/programming-guide/arrays/codesnippet/CSharp/implicitly-typed-arrays_1.cs)]  
  
 Nell'esempio precedente, si noti che con le matrici tipizzate in modo implicito, non vengono utilizzate le parentesi quadre sul lato sinistro dell'istruzione di inizializzazione.  Si noti inoltre che le matrici di matrici vengono inizializzate utilizzando `new []` esattamente come le matrici unidimensionali.  
  
## Matrici tipizzate in modo implicito negli inizializzatori di oggetto  
 Quando si crea un tipo anonimo che contiene una matrice, la matrice deve essere tipizzata in modo implicito nell'inizializzatore di oggetto del tipo.  Nell'esempio seguente, `contacts` è una matrice tipizzata in modo implicito di tipi anonimi, ognuno dei quali contiene una matrice denominata `PhoneNumbers`.  Si noti che la parola chiave `var` non viene utilizzata negli inizializzatori di oggetto.  
  
 [!code-cs[csProgGuideLINQ#38](../../../csharp/programming-guide/arrays/codesnippet/CSharp/implicitly-typed-arrays_2.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)