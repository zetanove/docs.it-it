---
title: "Clausola from (Riferimento C#) | Microsoft Docs"
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
  - "from_CSharpKeyword"
  - "from"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "from (clausola) [C#]"
  - "parola chiave from [C#]"
ms.assetid: 1aefd18c-1314-47f8-99ec-9bcefb09e699
caps.latest.revision: 27
caps.handback.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Clausola from (Riferimento C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'espressione di query deve iniziare con la clausola `from`.  Inoltre, un'espressione di query può contenere sottoquery che iniziano anch'esse con la clausola `from`.  La clausola `from` specifica gli elementi seguenti:  
  
-   Origine dati su cui la query o la sottoquery verrà eseguita.  
  
-   *Variabile di intervallo* locale che rappresenta ogni elemento nella sequenza di origine.  
  
 Sia la variabile di intervallo che l'origine dati sono fortemente tipizzate.  L'origine dati a cui si fa riferimento nella clausola `from` deve contenere un tipo di <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601> o un tipo derivato, ad esempio <xref:System.Linq.IQueryable%601>.  
  
 Nell'esempio riportato di seguito, `numbers` è l'origine dati e `num` è la variabile di intervallo.  Si noti che entrambe le variabili sono fortemente tipizzate anche se viene utilizzata la parola chiave [var](../../../csharp/language-reference/keywords/var.md).  
  
 [!code-cs[cscsrefQueryKeywords#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/from-clause_1.cs)]  
  
## Variabile di intervallo  
 Tramite l'inferenza, il compilatore deriva il tipo della variabile di intervallo quando l'origine dati implementa <xref:System.Collections.Generic.IEnumerable%601>.  Se, ad esempio, l'origine dispone di un tipo di `IEnumerable<Customer>`, la variabile di intervallo dedotta sarà `Customer`.  È necessario specificare il tipo in modo esplicito unicamente quando l'origine è un tipo `IEnumerable` non generico, ad esempio <xref:System.Collections.ArrayList>.  Per ulteriori informazioni, vedere la classe [How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md).  
  
 Nell'esempio precedente, si deduce che `num` è di tipo `int`.  Poiché la variabile di intervallo è fortemente tipizzata, è possibile chiamare metodi su di essa o utilizzarla in altre operazioni.  Ad esempio, anziché scrivere `select num`, è possibile scrivere `select num.ToString()` in modo che l'espressione di query restituisca una sequenza di stringhe anziché numeri interi.  Oppure è possibile scrivere `select n + 10` in modo che l'espressione restituisca la sequenza 14, 11, 13, 12 10.  Per ulteriori informazioni, vedere [Clausola select](../../../csharp/language-reference/keywords/select-clause.md).  
  
 La variabile di intervallo è analoga a una variabile di iterazione nell'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md) eccetto che per una differenza molto importante: una variabile di intervallo non archivia effettivamente mai dati dall'origine.  Si tratta semplicemente di un vantaggio sintattico che consente alla query di descrivere ciò che si verificherà quando la query verrà eseguita.  Per ulteriori informazioni, vedere la classe [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
## Clausole from composte  
 In alcuni casi, ogni elemento nella sequenza di origine può essere una sequenza o contenere una sequenza.  Ad esempio, l'origine dati può essere un oggetto `IEnumerable<Student>` in cui ciascun elemento studente della sequenza contiene un elenco di punteggi del test.  Per accedere all'elenco interno in ogni elemento `Student` è possibile utilizzare clausole `from` composte.  La tecnica è analoga all'uso di istruzioni [foreach](../../../csharp/language-reference/keywords/foreach-in.md) annidate.  È possibile aggiungere clausole [where](../../../csharp/language-reference/keywords/partial-method.md) o [orderby](../../../csharp/language-reference/keywords/orderby-clause.md) a una delle due clausole `from` per filtrare i risultati.  Nell'esempio seguente viene illustrata una sequenza di oggetti `Student`, ognuno dei quali contiene un `List` interno di numeri interi che rappresentano i punteggi del test.  Per accedere all'elenco interno, utilizzare una clausola `from` composta.  Se necessario, è possibile inserire delle clausole tra le due clausole `from`.  
  
 [!code-cs[cscsrefQueryKeywords#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/from-clause_2.cs)]  
  
## Utilizzo di più clausole from per eseguire join  
 Una clausola `from` composta viene utilizzata per accedere a raccolte interne in una sola origine dati.  Una query può tuttavia contenere anche più clausole `from` che generano query supplementari dalle origini dati indipendenti.  Questa tecnica consente di eseguire determinati tipi di operazioni di join che non sono possibili utilizzando la [clausola join](../../../csharp/language-reference/keywords/join-clause.md).  
  
 Nell'esempio seguente viene mostrato come due clausole `from` possono essere utilizzate per formare un cross join completo di due origini dati.  
  
 [!code-cs[cscsrefQueryKeywords#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/from-clause_3.cs)]  
  
 Per ulteriori informazioni sulle operazioni di join che utilizzano più clausole `from`, vedere [Procedura: eseguire operazioni di join personalizzate](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md).  
  
## Vedere anche  
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)