---
title: "Procedura: ordinare i risultati di una clausola join (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "join (clausola) [C#]"
  - "join [C#], ordinamento dei risultati"
  - "query [LINQ in C#], join"
  - "query (espressioni) [LINQ in C#], join"
ms.assetid: 83f36f16-2ba3-453f-8b9f-7d02b415610e
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: ordinare i risultati di una clausola join (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In questo esempio viene illustrato come ordinare i risultati di un'operazione di join.  Notare che l'ordinamento viene eseguito dopo l'operazione di join.  In genere, sebbene sia possibile, non è consigliabile utilizzare la clausola `orderby` con una o più sequenze di origine prima dell'operazione join.  Alcuni provider [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] potrebbero non mantenere tale ordinamento dopo l'operazione join.  
  
## Esempio  
 Questa query crea un join di gruppo e quindi ordina i gruppi in base all'elemento categoria che è ancora nell'ambito.  Nell'inizializzatore di tipi anonimi una sottoquery ordina tutti gli elementi corrispondenti della sequenza di prodotti.  
  
 [!code-cs[csProgGuideLINQ#81](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-order-the-results-of-a-join-clause_1.cs)]  
  
## Compilazione del codice  
  
-   Creare un progetto [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] per .NET Framework versione 3.5.  Per impostazione predefinita, il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi System.Linq.  
  
-   Copiare il codice nel progetto.  
  
-   Premere F5 per compilare ed eseguire il programma.  
  
-   Premere un tasto per chiudere la finestra della console.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola orderby](../../../csharp/language-reference/keywords/orderby-clause.md)   
 [Clausola join](../../../csharp/language-reference/keywords/join-clause.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)