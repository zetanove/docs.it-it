---
title: "Parametri di tipo generico (Guida per programmatori C#) | Microsoft Docs"
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
  - "generics [C#], parametri di tipo"
  - "parametri di tipo [C#]"
ms.assetid: a03b0ab2-0606-4b41-b7bf-e64d5bb4d18f
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Parametri di tipo generico (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nella definizione di un metodo o di un tipo generico, un parametro di tipo è un segnaposto per un tipo specificato da un client al momento della creazione di un'istanza di una variabile del tipo generico.  Una classe generica, ad esempio `GenericList<T>` elencata in [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md), non può essere utilizzata così com'è perché non rappresenta effettivamente un tipo, ma è piuttosto simile a un progetto iniziale per un tipo.  Per utilizzare `GenericList<T>`, il codice client deve dichiarare e creare un'istanza di un tipo costruito specificando un argomento di tipo racchiuso tra parentesi angolari.  L'argomento di tipo per questa classe particolare può essere qualsiasi tipo riconosciuto dal compilatore.  È possibile creare un numero indefinito di istanze di tipi costruiti, ognuna delle quali utilizza un argomento di tipo diverso, come riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#7](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-type-parameters_1.cs)]  
  
 In ognuna di queste istanze di `GenericList<T>`, tutte le occorrenze di `T` nella classe verranno sostituite in fase di esecuzione con l'argomento di tipo.  Tramite questa sostituzione, sono stati creati tre diversi oggetti efficienti e indipendenti dai tipi utilizzando una sola definizione di classe.  Per ulteriori informazioni sulle modalità di esecuzione di questa sostituzione da parte di CLR, vedere [Generics nel runtime](../../../csharp/programming-guide/generics/generics-in-the-run-time.md).  
  
## Linee guida per l'assegnazione di nomi ai parametri di tipo  
  
-   **Creare** parametri di tipo generico con nomi descrittivi, a meno che un nome composto da una singola lettera non sia già di facile comprensione e un nome descrittivo sarebbe superfluo.  
  
     [!code-cs[csProgGuideGenerics#8](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-type-parameters_2.cs)]  
  
-   **Considerare** l'utilizzo di T come nome di parametro per tipi con parametri di tipo composti da una singola lettera.  
  
     [!code-cs[csProgGuideGenerics#9](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-type-parameters_3.cs)]  
  
-   **Creare** nomi di parametri di tipo con prefissi descrittivi con "T".  
  
     [!code-cs[csProgGuideGenerics#10](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-type-parameters_4.cs)]  
  
-   **Considerare** l'indicazione di vincoli posizionati su un parametro di tipo nel nome del parametro.  Ad esempio, un parametro vincolato a `ISession` potrebbe essere denominato `TSession`.  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)   
 [Differenze tra modelli C\+\+ e generics C\#](../../../csharp/programming-guide/generics/differences-between-cpp-templates-and-csharp-generics.md)