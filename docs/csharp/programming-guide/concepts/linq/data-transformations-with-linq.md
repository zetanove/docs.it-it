---
title: "Trasformazioni dati con LINQ (C#) | Microsoft Docs"
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
  - "LINQ [C#], trasformazioni di dati"
  - "elementi di origine [LINQ in C#]"
  - "unione di più input [LINQ in C#]"
  - "più output in un'unica sequenza di output [LINQ in C#]"
  - "subset di elementi di origine [LINQ in C#]"
  - "origini dati [LINQ in C#], trasformazioni di dati"
  - "trasformazioni di dati [LINQ in C#]"
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
caps.latest.revision: 17
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Trasformazioni dati con LINQ (C#)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] non viene utilizzato solo per il recupero dei dati,  ma è anche un potente strumento per la trasformazione dei dati.  Utilizzando una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], è possibile utilizzare una sequenza di origine come input e modificarla in molti modi per creare una nuova sequenza di output.  È possibile modificare la sequenza senza modificare gli elementi ordinandoli e raggruppandoti. Ma le funzionalità più potente di query di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] è la possibilità di creare nuovi tipi.  mediante la clausola [select](../../../../csharp/language-reference/keywords/select-clause.md).  Ad esempio, è possibile effettuare le seguenti attività:  
  
-   Unire più sequenze di input in un'unica sequenza di output contenente un nuovo tipo.  
  
-   Creare sequenze di output i cui elementi sono costituiti da una o più proprietà di ogni elemento presente nella sequenza di origine.  
  
-   Creare sequenze di output i cui elementi sono costituiti dai risultati di operazioni eseguite sui dati di origine.  
  
-   Creare sequenze di output in un formato diverso.  Ad esempio, è possibile trasformare i dati da file di testo o righe SQL in XML.  
  
 Questi sono solo alcuni esempi.  Queste trasformazioni possono ovviamente essere combinate in diversi modi nella stessa query.  Inoltre, la sequenza di output di una query può essere utilizzata come sequenza di input per una nuova query.  
  
## Unione di più input in un'unica sequenza di output  
 È possibile utilizzare una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per creare una sequenza di output contenente elementi di più sequenze di input.  Nell'esempio seguente viene illustrato come combinare due strutture dei dati in memoria, ma gli stessi principi possono essere applicati per combinare dati da XML o SQL o origini dataset.  Si supponga di utilizzare i due tipi di classe seguenti:  
  
 [!code-cs[CsLINQGettingStarted#7](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_1.cs)]  
  
 Nell'esempio seguente viene illustrata la query:  
  
 [!code-cs[CSLinqGettingStarted#8](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_2.cs)]  
  
 Per ulteriori informazioni, vedere [Clausola join](../../../../csharp/language-reference/keywords/join-clause.md) e [Clausola select](../../../../csharp/language-reference/keywords/select-clause.md).  
  
## Selezione di un sottoinsieme di ogni elemento di origine  
 Sono disponibili due metodi principali per selezionare un sottoinsieme di ogni elemento nella sequenza di origine:  
  
1.  Per selezionare solo un membro dell'elemento di origine, utilizzare l'operazione punto.  Nell'esempio seguente si supponga che un oggetto `Customer` contenga diverse proprietà pubbliche inclusa una stringa denominata `City`.  Quando questa query viene eseguita, genererà una sequenza di stringhe di output.  
  
    ```  
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2.  Per creare elementi che contengano più proprietà dall'elemento di origine, è possibile utilizzare un inizializzatore di oggetto con un oggetto denominato o con un tipo anonimo.  Nell'esempio seguente viene illustrato l'utilizzo di un tipo anonimo per incapsulare due proprietà da ogni elemento `Customer`:  
  
    ```  
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 Per ulteriori informazioni, vedere [Inizializzatori di oggetto e di raccolta](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md) e [Tipi anonimi](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
## Trasformazione di oggetti in memoria in XML  
 Le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] consentono di trasformare facilmente i dati tra strutture dei dati in memoria, database SQL, dataset [!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] e flussi o documenti XML.  Nell'esempio seguente gli oggetti in una struttura dei dati in memoria vengono trasformati in elementi XML.  
  
 [!code-cs[CsLINQGettingStarted#9](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_3.cs)]  
  
 Il codice genera il seguente output XML:  
  
```  
< Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 Per ulteriori informazioni, vedere [Creazione di alberi XML in C\#](../Topic/Creating%20XML%20Trees%20in%20C%23%20\(LINQ%20to%20XML\)1.md).  
  
## Esecuzione di operazioni sugli elementi di origine  
 È possibile che una sequenza di output non contenga tutti gli elementi o le proprietà degli elementi della sequenza di origine.  L'output potrebbe invece essere costituito da una sequenza di valori calcolata utilizzando gli elementi di origine come argomenti di input.  Quando viene eseguita la query semplice riportata di seguito, viene generata una sequenza di stringhe i cui valori rappresentano un calcolo basato sulla sequenza di origine di elementi di tipo `double`.  
  
> [!NOTE]
>  Le chiamate ai metodi nelle espressioni di query non sono supportate se la query viene convertita in altri domini.  Ad esempio, non è possibile chiamare un metodo C\# comune in [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] poiché SQL Server non ne supporta il contesto.  È tuttavia possibile eseguire il mapping delle stored procedure ai relativi metodi e chiamare quindi le stored procedure.  Per ulteriori informazioni, vedere [Stored procedure](../Topic/Stored%20Procedures.md).  
  
 [!code-cs[CsLINQGettingStarted#10](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_4.cs)]  
  
## Vedere anche  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)   
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)   
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola select](../../../../csharp/language-reference/keywords/select-clause.md)   
 [How to: Combine Data with Joins](../../../../visual-basic/programming-guide/language-features/linq/how-to-combine-data-with-linq-by-using-joins.md)