---
title: "Clausola orderby (Riferimento C#) | Microsoft Docs"
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
  - "orderby"
  - "orderby_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "orderby (clausola) [C#]"
  - "parola chiave orderby [C#]"
ms.assetid: 21f87f48-d69d-4e95-9a52-6fec47b37e1f
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Clausola orderby (Riferimento C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In un'espressione di query, la clausola `orderby` fa in modo che la sequenza o la sottosequenza \(gruppo\) restituita venga ordinata in ordine crescente o decrescente.  È possibile specificare più chiavi per eseguire una o più operazioni di ordinamento secondarie.  L'ordinamento viene eseguito dall'operatore di confronto predefinito per il tipo dell'elemento.  Per impostazione predefinita, gli elementi vengono ordinati in ordinamento crescente.  Inoltre è possibile specificare un operatore di confronto personalizzato.  È tuttavia disponibile solo se si utilizza la sintassi basata sul metodo.  Per ulteriori informazioni, vedere [Sorting Data](../../../visual-basic/programming-guide/concepts/linq/sorting-data.md).  
  
## Esempio  
 Nell'esempio seguente, la prima query ordina le parole alfabeticamente a partire da A e la seconda query ordina le medesime parole in ordine decrescente.  La parola chiave `ascending` è il valore di ordinamento predefinito e può essere omessa.  
  
 [!code-cs[cscsrefQueryKeywords#20](../../../csharp/language-reference/keywords/codesnippet/CSharp/orderby-clause_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene eseguito un ordinamento primario sui cognomi degli studenti e quindi un ordinamento secondario sui nomi.  
  
 [!code-cs[cscsrefQueryKeywords#22](../../../csharp/language-reference/keywords/codesnippet/CSharp/orderby-clause_2.cs)]  
  
## Note  
 In fase di compilazione, la clausola `orderby` viene convertita in una chiamata al metodo <xref:System.Linq.Enumerable.OrderBy%2A>.  Chiavi multiple nella clausola `orderby` vengono convertite in chiamate del metodo <xref:System.Linq.Enumerable.ThenBy%2A>.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola group](../../../csharp/language-reference/keywords/group-clause.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)