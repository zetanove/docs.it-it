---
title: 'Procedura: Trovare la differenza dei set tra due elenchi (LINQ) (C#) | Microsoft Docs'
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
ms.assetid: 8e8945f0-4aba-439d-8d5d-c8d1eeef4e71
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
ms.openlocfilehash: 5ce6d6192ca2bf0f2dc98f52d825aa265e94f2a0
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-c"></a>Procedura: Trovare la differenza dei set tra due elenchi (LINQ) (C#)
In questo esempio viene illustrato come usare LINQ per confrontare due elenchi di stringhe e restituire le righe presenti in names1.txt ma non in names2.txt.  
  
### <a name="to-create-the-data-files"></a>Per creare i file di dati  
  
1.  Copiare names1.txt e names2.txt nella cartella della soluzione come illustrato in [Procedura: Combinare e confrontare raccolte di stringhe (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-combine-and-compare-string-collections-linq.md).  
  
## <a name="example"></a>Esempio  
  
```csharp  
class CompareLists  
{          
    static void Main()  
    {  
        // Create the IEnumerable data sources.  
        string[] names1 = System.IO.File.ReadAllLines(@"../../../names1.txt");  
        string[] names2 = System.IO.File.ReadAllLines(@"../../../names2.txt");  
  
        // Create the query. Note that method syntax must be used here.  
        IEnumerable<string> differenceQuery =  
          names1.Except(names2);  
  
        // Execute the query.  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt");  
        foreach (string s in differenceQuery)  
            Console.WriteLine(s);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
     The following lines are in names1.txt but not names2.txt  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  
    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
     */  
```  
  
 Alcuni tipi di operazioni di query in C#, come ad esempio <xref:System.Linq.Enumerable.Except%2A>, <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Union%2A> e <xref:System.Linq.Enumerable.Concat%2A>, possono essere espressi solo nella sintassi basata su metodo.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto che usi .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e alle direttive `using` per gli spazi dei nomi System.Linq e System.IO.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)
