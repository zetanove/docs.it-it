---
title: "Procedura: utilizzare espressioni lambda in una query (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "espressioni lambda [C#], in LINQ"
ms.assetid: 3cac4d25-d11f-4abd-9e7c-0f02e97ae06d
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Procedura: utilizzare espressioni lambda in una query (Guida per programmatori C#)
Le espressioni lambda non vengono utilizzate direttamente nella sintassi della query ma vengono utilizzate nelle chiamate al metodo e le espressioni di query possono contenere le chiamate al metodo.  Alcune operazioni di query possono infatti essere espresse solo nella sintassi del metodo.  Per ulteriori informazioni sulla differenza tra la sintassi della query e la sintassi del metodo, vedere [Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un'espressione lambda in una query basata sul metodo utilizzando l'operatore di query standard <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName>.  Tenere presente che il metodo <xref:System.Linq.Enumerable.Where%2A> in questo esempio contiene un parametro di input del tipo di delegato <xref:System.Func%601> e che il delegato accetta un intero come input e restituisce un valore booleano.  L'espressione lambda può essere convertita in tale delegato.  Se si utilizza una query [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq-md.md)] con il metodo <xref:System.Linq.Queryable.Where%2A?displayProperty=fullName>, il tipo di parametro è `Expression<Func\<int,bool>>` mentre l'espressione lambda è esattamente la stessa.  Per ulteriori informazioni sul tipo di espressione, vedere <xref:System.Linq.Expressions.Expression?displayProperty=fullName>.  
  
 [!code-cs[csProgGuideLINQ#1](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-use-lambda-expressions-in-a-query_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un'espressione lambda in una chiamata al metodo di un'espressione di query.  L'espressione lambda è necessaria poiché l'operatore di query standard <xref:System.Linq.Enumerable.Sum%2A> non può essere richiamato utilizzando la sintassi della query.  
  
 La query prima raggruppa gli studenti in base all'anno scolastico, come definito nell'enumerazione `GradeLevel`.  Quindi per ciascun gruppo aggiunge il punteggio totale di ogni studente.  A tale scopo sono necessarie due operazioni `Sum`.  L'operazione `Sum` interna calcola il punteggio totale di ogni studente mentre l'operazione `Sum` esterna gestisce un totale parziale complessivo di tutti gli studenti del gruppo.  
  
 [!code-cs[csProgGuideLINQ#2](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-use-lambda-expressions-in-a-query_2.cs)]  
  
## Compilazione del codice  
 Per eseguire questo codice, copiare e incollare il metodo nella classe `StudentClass` fornita in [Procedura: eseguire query in una raccolta di oggetti](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md) e chiamarla dal metodo `Main`.  
  
## Vedere anche  
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)