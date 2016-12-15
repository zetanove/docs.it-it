---
title: "Clausola where (Riferimento C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "whereclause_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "where (clausola) [C#]"
  - "where (parola chiave) [C#]"
ms.assetid: 7f9bf952-7744-4f91-b676-cddb55d107c3
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Clausola where (Riferimento C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La clausola `where` viene utilizzata in un'espressione di query per specificare gli elementi dell'origine dati che verranno restituiti nell'espressione di query.  Applica una condizione booleana \(*predicato*\) a ogni elemento di origine, a cui fa riferimento la variabile di intervallo, e restituisce quelli per cui la condizione specificata è vera.  Una singola espressione di query può contenere più clausole `where` e una singola clausola può contenere più sottoespressioni di predicato.  
  
## Esempio  
 Nell'esempio seguente la clausola `where` esclude tutti i numeri tranne quelli che sono minori di cinque.  Se si rimuove la clausola `where`, vengono restituiti tutti i numeri dell'origine dati.  L'espressione `num < 5` è il predicato applicato a ogni elemento.  
  
 [!code-cs[cscsrefQueryKeywords#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-clause_1.cs)]  
  
## Esempio  
 All'interno di una singola clausola `where` è possibile specificare tutti i predicati necessari utilizzando gli operatori [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) e [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md).  Nell'esempio seguente la query specifica due predicati per selezionare solo i numeri pari minori di cinque.  
  
 [!code-cs[cscsrefQueryKeywords#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-clause_2.cs)]  
  
## Esempio  
 La clausola `where` può contenere uno o più metodi che restituiscono valori booleani.  Nell'esempio seguente la clausola `where` utilizza un metodo per determinare se il valore corrente della variabile di intervallo è pari o dispari.  
  
 [!code-cs[cscsrefQueryKeywords#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-clause_3.cs)]  
  
## Note  
 La clausola `where` rappresenta un meccanismo di filtro.  Può essere posizionata quasi ovunque in un'espressione di query, ma non può essere la prima o l'ultima clausola.  La clausola `where` può essere posizionata prima o dopo una clausola [group](../../../csharp/language-reference/keywords/group-clause.md) a seconda che gli elementi di origine debbano essere filtrati prima o dopo essere stati raggruppati.  
  
 Se un predicato specificato non è valido per gli elementi dell'origine dati, verrà generato un errore in fase di compilazione.  Si tratta di un vantaggio del rigido controllo dei tipi fornito da [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].  
  
 In fase di compilazione la parola chiave `where` viene convertita in una chiamata al metodo di operatore query standard <xref:System.Linq.Enumerable.Where%2A>.  
  
## Vedere anche  
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Clausola from](../../../csharp/language-reference/keywords/from-clause.md)   
 [Clausola select](../../../csharp/language-reference/keywords/select-clause.md)   
 [Filtering Data](../../../visual-basic/programming-guide/concepts/linq/filtering-data.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)