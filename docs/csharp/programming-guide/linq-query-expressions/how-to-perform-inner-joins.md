---
title: "Procedura: eseguire degli inner join (Guida per programmatori C#) | Microsoft Docs"
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
  - "inner join [LINQ in C#]"
  - "join [C#], interna"
  - "query [LINQ in C#], join"
  - "query (espressioni) [LINQ in C#], join"
ms.assetid: d9edb404-8314-413e-ae51-83bb86c7a4b5
caps.latest.revision: 25
caps.handback.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire degli inner join (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In termini di database relazionale, un *inner join* produce un set di risultati dove ogni elemento della prima raccolta viene visualizzato una volta per ogni elemento corrispondente nella seconda raccolta.  Se un elemento nella prima raccolta non dispone di elementi corrispondenti, non viene visualizzato nel set di risultati.  Il metodo <xref:System.Linq.Enumerable.Join%2A>, chiamato dalla clausola `join` in C\#, implementa un inner join.  
  
 In questo argomento viene illustrato come eseguire quattro varianti di un inner join:  
  
-   Inner join semplice che correla elementi da due origini dati in base a una chiave semplice.  
  
-   Inner join che correla elementi da due origini dati in base a una chiave *composta*,  ovvero una chiave costituita da più di un valore, che consente di correlare elementi in base a più di una proprietà.  
  
-   *Join multiplo* nel quale le operazioni di join successive vengono aggiunte l'una all'altra.  
  
-   Inner join implementato utilizzando un group join.  
  
## Esempio  
  
## Esempio di join di chiave semplice  
 Nell'esempio seguente vengono create due raccolte che contengono oggetti di due tipi definiti dall'utente, `Person` e `Pet`.  La query utilizza la clausola `join` in C\# per associare gli oggetti `Person` con oggetti `Pet` per i quali il valore di `Owner` corrisponde a tale oggetto `Person`.  La clausola `select` in C\# definisce l'aspetto degli oggetti risultanti.  In questo esempio gli oggetti risultanti sono tipi anonimi costituiti del nome del proprietario e dal nome dell'animale domestico.  
  
 [!code-cs[CsLINQProgJoining#1](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_1.cs)]  
  
 Si noti che l'oggetto `Person` il cui `LastName` è "Huff" non viene visualizzato nel set di risultati perché non è disponibile alcun oggetto `Pet` il cui `Pet.Owner` sia uguale a tale `Person`.  
  
## Esempio  
  
## Esempio di join di chiave composta  
 Invece di correlare gli elementi in base a una sola proprietà, è possibile utilizzare una chiave composta per confrontare gli elementi in base a più proprietà.  A questo scopo, specificare la funzione del selettore di chiavi in modo che ogni raccolta restituisca un tipo anonimo costituito dalle proprietà che si desidera confrontare.  Se si assegna un'etichetta alle proprietà, l'etichetta deve essere la medesima nel tipo anonimo di ogni chiave.  Le proprietà devono inoltre essere visualizzate nello stesso ordine.  
  
 Nell'esempio seguente viene utilizzato un elenco di oggetti `Employee` e un elenco di oggetti `Student` per determinare quali dipendenti sono anche studenti.  Entrambi questi tipi presentano una proprietà `FirstName` e `LastName` di tipo <xref:System.String>.  Le funzioni create dalle chiavi di join dagli elementi di ogni elenco restituiscono un tipo anonimo costituito dalle proprietà `FirstName` e `LastName` di ogni elemento.  L'operazione di join verifica l'uguaglianza di queste chiavi composte e restituisce coppie di oggetti da ogni elenco dove sia il nome che il cognome corrispondono.  
  
 [!code-cs[CsLINQProgJoining#2](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_2.cs)]  
  
## Esempio  
  
## Esempio di join multiplo  
 È possibile aggiungere un numero indeterminato di operazioni di join per eseguire un join multiplo.  Ogni clausola `join` in C\# mette in correlazione un'origine dati specificata con i risultati del join precedente.  
  
 Nell'esempio seguente vengono create tre raccolte: un elenco di oggetti `Person`, un elenco di oggetti `Cat` e un elenco di oggetti `Dog`.  
  
 La prima clausola `join` in C\# associa le persone e i gatti in base a un oggetto `Person` corrispondente a `Cat.Owner`.  Restituisce una sequenza di tipi anonimi contenenti l'oggetto `Person` e `Cat.Name`.  
  
 La seconda clausola `join` in C\# mette in correlazione i tipi anonimi restituiti dal primo join con gli oggetti `Dog` nell'elenco fornito di cani, in base a una chiave composta costituita dalla proprietà `Owner` del tipo `Person`e dalla prima lettera del nome dell'animale.  Restituisce una sequenza di tipi anonimi contenenti le proprietà `Cat.Name` e `Dog.Name` da ogni coppia corrispondente.  Poiché si tratta di un inner join, vengono restituiti solo gli oggetti della prima origine dati che presentano una corrispondenza nella seconda origine dati.  
  
 [!code-cs[CsLINQProgJoining#3](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_3.cs)]  
  
## Esempio  
  
## Esempio di inner join utilizzando il join raggruppato  
 Nell'esempio seguente viene illustrato come implementare un inner join utilizzando un group join.  
  
 In `query1`, l'elenco di oggetti `Person` è unito tramite group join all'elenco di oggetti `Pet` in base all'oggetto `Person` corrispondente alla proprietà `Pet.Owner`.  Il group join crea una raccolta di gruppi intermedi, dove ogni gruppo è costituito da un oggetto `Person` e da una sequenza di oggetti `Pet` corrispondenti.  
  
 Aggiungendo una seconda clausola `from` alla query, questa sequenza di sequenze viene combinata \(o appiattita\) in una sequenza più lunga.  Il tipo degli elementi della sequenza finale è specificato dalla clausola `select`.  In questo esempio, tale tipo è un tipo anonimo costituito dalle proprietà `Person.FirstName` e `Pet.Name` per ogni coppia corrispondente.  
  
 Il risultato di `query1` è equivalente al set di risultati che sarebbe stato ottenuto utilizzando la clausola `join` senza la clausola `into` per eseguire un inner join.  La variabile `query2` dimostra questa query equivalente.  
  
 [!code-cs[CsLINQProgJoining#4](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_4.cs)]  
  
## Compilazione del codice  
  
-   Creare un nuovo progetto Applicazione console in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)].  
  
-   Aggiungere un riferimento a System.Core.dll, se non è già presente un riferimento.  
  
-   Includere lo spazio dei nomi <xref:System.Linq>.  
  
-   Copiare e incollare il codice dall'esempio nel file program.cs, sotto il metodo `Main`.  Aggiungere una riga di codice al metodo `Main` per chiamare il metodo in cui è stata eseguita l'operazione Incolla.  
  
-   Eseguire il programma.  
  
## Vedere anche  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [Procedura: eseguire dei join raggruppati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [Procedura: Eseguire i left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [Procedura: unire due raccolte tramite join](../Topic/How%20to:%20Join%20Two%20Collections%20\(C%23\)%20\(LINQ%20to%20XML\).md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)