---
title: "Clausola select (Riferimento C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "select_CSharpKeyword"
  - "select"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "select (clausola) [C#]"
  - "parola chiave select [C#]"
ms.assetid: df01e266-5781-4aaa-80c4-67cf28ea093f
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Clausola select (Riferimento C#)
In un'espressione di query, la clausola `select` specifica il tipo di valori che verranno prodotti quando la query sarà eseguita.  Il risultato è basato sulla valutazione di tutte le clausole precedenti e su eventuali espressioni nella clausola `select` stessa.  Un'espressione di query deve terminare con una clausola `select` o con una clausola [group](../../../csharp/language-reference/keywords/group-clause.md).  
  
 Nell'esempio seguente viene illustrata una clausola `select` semplice in un'espressione di query.  
  
 [!code-cs[cscsrefQueryKeywords#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/select-clause_1.cs)]  
  
 Il tipo della sequenza prodotta dalla clausola `select` determina il tipo della variabile di query `queryHighScores`.  Nel caso più semplice, la clausola `select` specifica solo la variabile di intervallo.  In questo modo la sequenza restituita contiene elementi dello stesso tipo dell'origine dati.  Per ulteriori informazioni, vedere [Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  La clausola `select`, tuttavia, fornisce anche un meccanismo avanzato per trasformare \(o *proiettare*\) i dati di origine in nuovi tipi.  Per ulteriori informazioni, vedere [Trasformazioni dati con LINQ \(C\#\)](../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md).  
  
## Esempio  
 Nell'esempio seguente vengono illustrati tutti i diversi form che una clausola `select` può accettare.  In ogni query, si noti la relazione tra la clausola `select` e il tipo della *variabile della query* \(`studentQuery1`, `studentQuery2`e così via\).  
  
 [!code-cs[cscsrefQueryKeywords#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/select-clause_2.cs)]  
  
 Come illustrato in `studentQuery8` dell'esempio precedente, talvolta è necessario che gli elementi della sequenza restituita contengano solo un sottoinsieme delle proprietà degli elementi di origine.  Mantenendo le dimensioni minime consentite della sequenza restituita è possibile ridurre i requisiti della memoria e aumentare la velocità dell'esecuzione della query.  È possibile ottenere questo risultato creando un tipo anonimo nella clausola `select` e utilizzando un inizializzatore di oggetto per inizializzarlo con le proprietà adatte dall'elemento di origine.  Per un esempio di come eseguire questa operazione, vedere [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
## Note  
 In fase di compilazione, la clausola `select` viene convertita in una chiamata al metodo per l'operatore query standard <xref:System.Linq.Enumerable.Select%2A>.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Clausola from](../../../csharp/language-reference/keywords/from-clause.md)   
 [parziale \(Metodo\) \(Riferimenti per C\#\)](../../../csharp/language-reference/keywords/partial-method.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)