---
title: Materializzazione intermedia (C#) | Microsoft Docs
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
ms.assetid: 7922d38f-5044-41cf-8e17-7173d6553a5e
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4807224faef5968828e16a4e1f11614e7ac6cf73
ms.lasthandoff: 03/13/2017


---
# <a name="intermediate-materialization-c"></a>Materializzazione intermedia (C#)
Se non si presta la dovuta attenzione, in alcune situazioni è possibile modificare drasticamente il profilo di memoria e prestazioni dell'applicazione, generando la materializzazione prematura delle raccolte nelle query. Alcuni operatori di query standard provocano la materializzazione della propria raccolta di origine prima di restituire un solo elemento. Ad esempio, <xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=fullName> prima esegue l'iterazione dell'intera raccolta di origine, quindi ordina tutti gli elementi e infine restituisce il primo elemento. Questo significa che ottenere il primo elemento di una raccolta ordinata è costoso, mentre ogni elemento successivo non lo è. Questo comportamento è normale: sarebbe impossibile per questo operatore di query fare altrimenti.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene modificato l'esempio precedente. Il metodo `AppendString` chiama <xref:System.Linq.Enumerable.ToList%2A> e quindi esegue l'iterazione attraverso l'origine. Ciò provoca la materializzazione.  
  
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
        // the following statement materializes the source collection in a List<T>  
        // before iterating through it  
        foreach (string str in source.ToList())  
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
ToUpper: source >ghi<  
AppendString: source >ABC<  
Main: str >ABC!!!<  
  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
 In questo esempio è possibile osservare che a seguito della chiamata a <xref:System.Linq.Enumerable.ToList%2A> `AppendString` enumera l'intera origine prima di restituire il primo elemento. Se l'origine fosse una matrice di grandi dimensioni, il profilo di memoria dell'applicazione verrebbe modificato in modo significativo.  
  
 Gli operatori di query standard possono anche essere concatenati. Nell'argomento finale dell'esercitazione verrà illustrato questo aspetto.  
  
-   [Concatenamento di operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/chaining-standard-query-operators-together.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: Concatenamento di query (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)
