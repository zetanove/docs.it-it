---
title: "Procedura: Archiviare i risultati di una query in memoria (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "archiviazione dei risultati delle query LINQ [LINQ in C#]"
  - "query (espressioni) [LINQ in C#], archiviazione dei risultati"
ms.assetid: 7271597f-3523-4f7b-b088-1eeffe913b2d
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: Archiviare i risultati di una query in memoria (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una query è fondamentalmente un insieme di istruzioni per il recupero e l'organizzazione dei dati.  L'esecuzione della query richiede una chiamata al metodo <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>.  Questa chiamata viene eseguita quando si utilizza un ciclo `foreach` per scorrere gli elementi.  Per valutare una query e archiviare i risultati senza eseguire un ciclo di `foreach`, è sufficiente chiamare uno dei seguenti metodi sulla variabile di query:  
  
-   <xref:System.Linq.Enumerable.ToList%2A>  
  
-   <xref:System.Linq.Enumerable.ToArray%2A>  
  
-   <xref:System.Linq.Enumerable.ToDictionary%2A>  
  
-   <xref:System.Linq.Enumerable.ToLookup%2A>  
  
 Quando si archiviano i risultati della query, si consiglia di assegnare l'oggetto Collection restituito a una nuova variabile come illustrato nell'esempio seguente:  
  
## Esempio  
 [!code-cs[csProgGuideLINQ#25](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-store-the-results-of-a-query-in-memory_1.cs)]  
  
## Compilazione del codice  
  
-   Creare un progetto [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] per .NET Framework versione 3.5.  Per impostazione predefinita, il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi System.Linq.  
  
-   Copiare il codice nel progetto.  
  
-   Premere F5 per compilare ed eseguire il programma.  
  
-   Premere un tasto per chiudere la finestra della console.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)