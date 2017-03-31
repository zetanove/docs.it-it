---
title: Esempio di esecuzione posticipata (C#) | Microsoft Docs
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
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 652ea21bab0bf32e71e270c75d50d53a3a2bbac7
ms.lasthandoff: 03/13/2017


---
# <a name="deferred-execution-example-c"></a>Esempio di esecuzione posticipata (C#)
In questo argomento vengono illustrati gli effetti dell'esecuzione posticipata e della valutazione lazy sulle query LINQ to XML.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è illustrato l'ordine di esecuzione quando si usa un metodo di estensione basato su esecuzione posticipata. Viene dichiarata una matrice di tre stringhe. Viene quindi scorsa la raccolta restituita da `ConvertCollectionToUpperCase`.  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 Questo esempio produce il seguente output:  
  
```  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 Si noti che quando si scorre la raccolta restituita da `ConvertCollectionToUpperCase`, ogni elemento viene recuperato dalla matrice di stringhe di origine e viene convertito in lettere maiuscole prima del recupero dell'elemento successivo.  
  
 L'intera matrice di stringhe non viene convertita in lettere maiuscole prima dell'elaborazione nel ciclo `foreach` di `Main` di ogni elemento della raccolta restituita.  
  
 Nell'argomento successivo di questa esercitazione viene illustrato il concatenamento di query:  
  
-   [Esempio di concatenamento di query (C#)](../../../../csharp/programming-guide/concepts/linq/chaining-queries-example.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: Concatenamento di query (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)
