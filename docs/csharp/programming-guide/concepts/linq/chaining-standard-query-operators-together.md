---
title: Concatenamento di operatori di query standard (C#) | Microsoft Docs
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
ms.assetid: 66f2b0a9-2c23-4735-988e-bbc9dfb55c7b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8e9da047fcc224176d028f8caef8b57bc134dc21
ms.lasthandoff: 03/13/2017


---
# <a name="chaining-standard-query-operators-together-c"></a>Concatenamento di operatori di query standard (C#)
Questo è l'argomento finale dell'[Esercitazione: concatenamento di query (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)  
  
 È anche possibile concatenare gli operatori di query standard. Ad esempio, è possibile interrompere l'operatore <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName>, ma funziona anche in modalità lazy. Questo operatore non materializza nessun risultato intermedio.  
  
## <a name="example"></a>Esempio  
 In questo esempio, il metodo <xref:System.Linq.Enumerable.Where%2A> viene chiamato prima di chiamare `ConvertCollectionToUpperCase`. Il metodo <xref:System.Linq.Enumerable.Where%2A> funziona quasi allo stesso modo dei metodi lazy usati negli esempi precedenti di questa esercitazione, `ConvertCollectionToUpperCase` e `AppendString`.  
  
 La sola differenza è che in questo caso il metodo <xref:System.Linq.Enumerable.Where%2A> esegue l'iterazione nella raccolta di origine, determina che il primo elemento non passi il predicato e quindi va all'elemento successivo, che invece passa. Infine restituisce il secondo elemento.  
  
 Tuttavia, l'idea di base è la stessa: le raccolte intermedie vengono materializzate solo se è necessario.  
  
 Quando si usano le espressioni di query, vengono convertite in chiamate agli operatori di query standard e si applicano gli stessi principi.  
  
 Tutti gli esempi di questa sezione in cui vengono eseguite query su documenti Office Open XML si basano sullo stesso principio. Le idee di esecuzione posticipata e valutazione lazy sono alcuni dei concetti fondamentali che è necessario comprendere per usare LINQ e LINQ to XML in modo efficace.  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source >{0}<", str);  
            yield return str.ToUpper();  
        }  
    }  
  
    public static IEnumerable<string>  
      AppendString(this IEnumerable<string> source, string stringToAppend)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("AppendString: source >{0}<", str);  
            yield return str + stringToAppend;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        IEnumerable<string> q1 =  
            from s in stringArray.ConvertCollectionToUpperCase()  
            where s.CompareTo("D") >= 0  
            select s;  
  
        IEnumerable<string> q2 =  
            from s in q1.AppendString("!!!")  
            select s;  
  
        foreach (string str in q2)  
        {  
            Console.WriteLine("Main: str >{0}<", str);  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
 Questo esempio produce il seguente output:  
  
```  
ToUpper: source >abc<  
ToUpper: source >def<  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
ToUpper: source >ghi<  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: concatenamento di query (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)
