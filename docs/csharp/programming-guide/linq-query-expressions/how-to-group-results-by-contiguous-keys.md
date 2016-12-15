---
title: "Procedura: raggruppare i risultati per chiavi contigue (Guida per programmatori C#) | Microsoft Docs"
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
  - "chiavi contigue [LINQ in C#]"
ms.assetid: 0f0f48a8-e13b-4274-8903-3b73f68cd18e
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: raggruppare i risultati per chiavi contigue (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nell'esempio seguente viene mostrato come raggruppare elementi in blocchi che rappresentano sottosequenze di chiavi contigue.  Si supponga di avere la sequenza di coppie chiave\-valore riportata di seguito:  
  
|Chiave|Valore|  
|------------|------------|  
|A|We|  
|A|think|  
|A|that|  
|B|Linq|  
|C|is|  
|A|really|  
|B|cool|  
|B|\!|  
  
 I gruppi seguenti verranno creati in quest'ordine:  
  
1.  We, think, that  
  
2.  Linq  
  
3.  is  
  
4.  really  
  
5.  cool, \!  
  
 La soluzione viene implementata come metodo di estensione thread\-safe che restituisce i risultati in modalità di flusso.  In altre parole, i gruppi vengono prodotti man mano che ci si sposta lungo la sequenza di origine.  A differenza degli operatori `group` o `orderby`, questa soluzione può iniziare a restituire gruppi al chiamante prima che sia stata letta tutta la sequenza.  
  
 La caratteristica thread\-safe viene ottenuta effettuando una copia di ogni gruppo o blocco nel corso dell'iterazione della sequenza di origine, come spiegato nei commenti del codice sorgente.  Se nella sequenza di origine è inclusa una serie numerosa di elementi contigui, Common Language Runtime potrebbe generare <xref:System.OutOfMemoryException>.  
  
## Esempio  
 Nell'esempio seguente viene mostrato sia il metodo di estensione che il codice client che lo utilizza.  
  
 [!code-cs[cscsrefContiguousGroups#1](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-group-results-by-contiguous-keys_1.cs)]  
  
 Per utilizzare il metodo di estensione nel progetto, copiare la classe statica `MyExtensions` in un file di codice sorgente nuovo o esistente e, se richiesto, aggiungere una direttiva `using` per lo spazio dei nomi in cui si trova.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Classification of Standard Query Operators by Manner of Execution](../../../visual-basic/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)