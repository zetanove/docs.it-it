---
title: Operazioni di proiezione (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 98df573a-aad9-4b8c-9a71-844be2c4fb41
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 232afc23e180ab868bfa825d680b7fe4371b3805
ms.lasthandoff: 03/13/2017

---
# <a name="projection-operations-c"></a>Operazioni di proiezione (C#)
La proiezione si riferisce all'operazione di trasformazione di un oggetto in un nuovo form costituito spesso solo dalle proprietà che verranno usate successivamente. Utilizzando la proiezione, è possibile costruire un nuovo tipo compilato in base a ogni oggetto. È possibile proiettare una proprietà ed eseguirvi una funzione matematica. È anche possibile proiettare l'oggetto originale senza modificarlo.  
  
 Nella sezione seguente sono elencati i metodi dell'operatore query standard che eseguono la proiezione.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi di espressione della query C#|Altre informazioni|  
|-----------------|-----------------|---------------------------------|----------------------|  
|Seleziona|Proietta i valori che si basano su una funzione di trasformazione.|`select`|<xref:System.Linq.Enumerable.Select%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Select%2A?displayProperty=fullName>|  
|SelectMany|Proietta le sequenze di valori che si basano su una funzione di trasformazione semplificandoli in un'unica sequenza.|Usare più clausole `from`|<xref:System.Linq.Enumerable.SelectMany%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.SelectMany%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>Esempi di sintassi delle espressioni di query  
  
### <a name="select"></a>Seleziona  
 L'esempio seguente usa la clausola `select` per proiettare la prima lettera di ogni stringa di un elenco di stringhe.  
  
```csharp  
List<string> words = new List<string>() { "an", "apple", "a", "day" };  
  
var query = from word in words  
            select word.Substring(0, 1);  
  
foreach (string s in query)  
    Console.WriteLine(s);  
  
/* This code produces the following output:  
  
    a  
    a  
    a  
    d  
*/  
```  
  
### <a name="selectmany"></a>SelectMany  
 L'esempio seguente usa più clausole `from` per proiettare tutte le parole di ogni stringa di un elenco di stringhe.  
  
```csharp  
List<string> phrases = new List<string>() { "an apple a day", "the quick brown fox" };  
  
var query = from phrase in phrases  
            from word in phrase.Split(' ')  
            select word;  
  
foreach (string s in query)  
    Console.WriteLine(s);  
  
/* This code produces the following output:  
  
    an  
    apple  
    a  
    day  
    the  
    quick  
    brown  
    fox  
*/  
```  
  
## <a name="select-versus-selectmany"></a>Confronto tra Select e SelectMany  
 La funzione di `Select()` e `SelectMany()` è produrre uno o più valori risultato dai valori di origine. `Select()` produce un valore risultato per ogni valore di origine. Il risultato complessivo è pertanto una raccolta contenente lo stesso numero di elementi della raccolta di origine. Al contrario, `SelectMany()` produce un singolo risultato complessivo che contiene sottoraccolte concatenate di ogni valore di origine. La funzione di trasformazione passata come argomento a `SelectMany()` deve restituire una sequenza enumerabile di valori per ogni valore di origine. Queste sequenze enumerabili vengono quindi concatenate da `SelectMany()` per creare un'unica grande sequenza.  
  
 Le due figure seguenti illustrano la differenza concettuale tra le azioni di questi due metodi. In ogni caso, si supponga che la funzione del selettore (trasformazione) selezioni la matrice di fiori di ogni valore di origine.  
  
 La figura mostra che `Select()` restituisce una raccolta contenente lo stesso numero di elementi della raccolta di origine.  
  
 ![Figura concettuale dell'azione di Select&#40;&#41;](../../../../csharp/programming-guide/concepts/linq/media/selectaction.png "SelectAction")  
  
 La figura mostra che `SelectMany()` concatena la sequenza intermedia di matrici in un unico valore risultato finale contenente tutti i valori di ogni matrice intermedia.  
  
 ![Figura che mostra l'azione di SelectMany&#40;&#41;.](../../../../csharp/programming-guide/concepts/linq/media/selectmany.png "SelectMany")  
  
### <a name="code-example"></a>Esempio di codice  
 L'esempio seguente confronta il comportamento di `Select()` e `SelectMany()`. Il codice crea un "bouquet" di fiori prendendo i primi due elementi di ogni elenco di nomi di fiori nella raccolta di origine. In questo esempio il "valore singolo" usato dalla funzione di trasformazione <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>è anch'esso una raccolta di valori. Questo richiede il ciclo `foreach` aggiuntivo in modo da enumerare tutte le stringhe di ogni sottosequenza.  
  
```csharp  
class Bouquet  
{  
    public List<string> Flowers { get; set; }  
}  
  
static void SelectVsSelectMany()  
{  
    List<Bouquet> bouquets = new List<Bouquet>() {  
        new Bouquet { Flowers = new List<string> { "sunflower", "daisy", "daffodil", "larkspur" }},  
        new Bouquet{ Flowers = new List<string> { "tulip", "rose", "orchid" }},  
        new Bouquet{ Flowers = new List<string> { "gladiolis", "lily", "snapdragon", "aster", "protea" }},  
        new Bouquet{ Flowers = new List<string> { "larkspur", "lilac", "iris", "dahlia" }}  
    };  
  
    // *********** Select ***********              
    IEnumerable<List<string>> query1 = bouquets.Select(bq => bq.Flowers);  
  
    // ********* SelectMany *********  
    IEnumerable<string> query2 = bouquets.SelectMany(bq => bq.Flowers);  
  
    Console.WriteLine("Results by using Select():");  
    // Note the extra foreach loop here.  
    foreach (IEnumerable<String> collection in query1)  
        foreach (string item in collection)  
            Console.WriteLine(item);  
  
    Console.WriteLine("\nResults by using SelectMany():");  
    foreach (string item in query2)  
        Console.WriteLine(item);  
  
    /* This code produces the following output:  
  
       Results by using Select():  
        sunflower  
        daisy  
        daffodil  
        larkspur  
        tulip  
        rose  
        orchid  
        gladiolis  
        lily  
        snapdragon  
        aster  
        protea  
        larkspur  
        lilac  
        iris  
        dahlia  
  
       Results by using SelectMany():  
        sunflower  
        daisy  
        daffodil  
        larkspur  
        tulip  
        rose  
        orchid  
        gladiolis  
        lily  
        snapdragon  
        aster  
        protea  
        larkspur  
        lilac  
        iris  
        dahlia  
    */  
  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq>   
 [Cenni preliminari sugli operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola Select](../../../../csharp/language-reference/keywords/select-clause.md)   
 [Procedura: Popolare le raccolte di oggetti da più origini (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)   
 [Procedura: Suddividere un file in molti file usando i gruppi (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-split-a-file-into-many-files-by-using-groups-linq.md)
