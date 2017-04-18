---
title: Eseguire inner join
description: Come eseguire degli inner join.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 45bceed6-f549-4114-a9b1-b44feb497742
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6492e536976b74fa0a0b06cdc94d8aad9584e5be
ms.lasthandoff: 03/13/2017

---
# <a name="perform-inner-joins"></a>Eseguire inner join

In termini di database relazionale, un *inner join* produce un set di risultati in cui ogni elemento della prima raccolta viene visualizzato una volta per ogni elemento corrispondente nella seconda raccolta. Se un elemento nella prima raccolta non ha corrispondenti, non viene visualizzato nel set di risultati. Il metodo <xref:System.Linq.Enumerable.Join%2A>, chiamato dalla clausola `join` in C#, implementa un inner join.  
  
 In questo argomento viene illustrato come eseguire quattro varianti di un inner join:  
  
-   Un inner join semplice che correla gli elementi di due origini dati in base a una chiave semplice.  
  
-   Un inner join che correla gli elementi di due origini dati in base a una chiave *composta*. Una chiave composta, che è una chiave costituita da più di un valore, consente di correlare gli elementi in base a più di una proprietà.  
  
-   Un *join multiplo* in cui le operazioni di join successive vengono aggiunte l'una all'altra.  
  
-   Un inner join che viene implementato usando un group join.  
  
## <a name="example"></a>Esempio  
  
## <a name="simple-key-join-example"></a>Esempio di join con chiave semplice  
 Nell'esempio seguente vengono create due raccolte che contengono oggetti di due tipi definiti dall'utente, `Person` e `Pet`. La query usa la clausola `join` in C# per la corrispondenza degli oggetti `Person` con gli oggetti `Pet` per il cui il valore di `Owner` è `Person`. La clausola `select` in C# definisce l'aspetto degli oggetti risultanti. In questo esempio gli oggetti risultanti sono tipi anonimi costituiti dal nome del proprietario (owner) e dal nome dell'animale domestico (pet).  
  
 [!code-cs[CsLINQProgJoining#1](../../../samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_1.cs)]  
  
 Notare che l'oggetto `Person` il cui valore `LastName` è "Huff" non viene visualizzato nel set di risultati perché non esiste un oggetto `Pet` con `Pet.Owner` uguale a `Person`.  
  
## <a name="example"></a>Esempio  
  
## <a name="composite-key-join-example"></a>Esempio di join con chiave composta  
 Anziché correlare gli elementi in base a una sola proprietà, è possibile usare una chiave composta per confrontare gli elementi in base a più proprietà. Per eseguire questa operazione, specificare la funzione del selettore di chiave per ogni raccolta in modo da restituire un tipo anonimo che include le proprietà da confrontare. Se si applicano etichette alle proprietà, l'etichetta deve essere la stessa in ogni tipo anonimo della chiave. Le proprietà devono inoltre apparire nello stesso ordine.  
  
 L'esempio seguente usa un elenco di oggetti `Employee` e un elenco di oggetti `Student` per determinare quali dipendenti sono anche studenti. Entrambi questi tipi presentano una proprietà `FirstName` e una proprietà `LastName` di tipo <xref:System.String>. Le funzioni che creano le chiavi di join dagli elementi di ogni elenco restituiscono un tipo anonimo costituito dalle proprietà `FirstName` e `LastName` di ogni elemento. L'operazione di join confronta le chiavi composte per verificarne l'uguaglianza e restituisce coppie di oggetti da ogni elenco in cui sia il nome che il cognome corrispondono.  
  
 [!code-cs[CsLINQProgJoining#2](../../../samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_2.cs)]  
  
## <a name="example"></a>Esempio  
  
## <a name="multiple-join-example"></a>Esempio di join multiplo  
 È possibile collegare tra loro qualsiasi numero di operazioni di join per eseguire un join multiplo. Ogni clausola `join` in C# consente di correlare un'origine dati specificata con i risultati del join precedente.  
  
 Il seguente esempio crea tre raccolte: un elenco di oggetti `Person`, un elenco di oggetti `Cat` e un elenco di oggetti `Dog`.  
  
 La prima clausola `join` in C# associa le persone e i gatti in base a un oggetto `Person` corrispondente a `Cat.Owner`. Restituisce una sequenza di tipi anonimi che contengono l'oggetto `Person` e `Cat.Name`.  
  
 La seconda clausola `join` in C# consente di correlare i tipi anonimi restituiti dal primo join con gli oggetti `Dog` dell'elenco di cani, in base a una chiave costituita dalla proprietà `Owner` del tipo `Person` e dalla prima lettera del nome dell'animale. Restituisce una sequenza di tipi anonimi che contengono le proprietà `Cat.Name` e `Dog.Name` di ogni coppia corrispondente. Poiché si tratta di un inner join, vengono restituiti solo gli oggetti della prima origine dati per cui esiste una corrispondenza nella seconda origine dati.  
  
 [!code-cs[CsLINQProgJoining#3](../../../samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_3.cs)]  
  
## <a name="example"></a>Esempio  
  
## <a name="inner-join-by-using-grouped-join-example"></a>Inner join usando l'esempio con join raggruppati  
 Nell'esempio seguente viene illustrato come implementare un inner join usando un group join.  
  
 In `query1` l'elenco di oggetti `Person` viene collegato con un group join all'elenco di oggetti `Pet` in base all'oggetto `Person` corrispondente alla proprietà `Pet.Owner`. Il group join crea una raccolta di gruppi intermedi, dove ogni gruppo è costituito da un oggetto `Person` e una sequenza di oggetti `Pet` corrispondenti.  
  
 Aggiungendo una seconda clausola `from` alla query, questa sequenza di sequenze viene combinata (o appiattita) in un'unica sequenza più lunga. Il tipo degli elementi della sequenza finale viene specificato dalla clausola `select`. In questo esempio il tipo è un tipo anonimo costituito dalle proprietà `Person.FirstName` e `Pet.Name` per ogni coppia corrispondente.  
  
 Il risultato di `query1` è equivalente al set di risultati che si ottiene usando la clausola `join` senza la clausola `into` per eseguire un inner join. La variabile `query2` dimostra questa query equivalente.  
  
 [!code-cs[CsLINQProgJoining#4](../../../samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_4.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Eseguire join raggruppati](perform-grouped-joins.md)   
 [Eseguire left outer join](perform-left-outer-joins.md)   
 [Tipi anonimi](../programming-guide/classes-and-structs/anonymous-types.md)   
 
