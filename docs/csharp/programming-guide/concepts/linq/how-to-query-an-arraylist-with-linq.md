---
title: 'Procedura: Eseguire una query su un ArrayList con LINQ (C#) | Microsoft Docs'
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
ms.assetid: 2bfb471c-6e9a-4e60-bd83-4a1778abde11
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
ms.openlocfilehash: 09489e2dabd34da0446a623e91cd85de35c3c70b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-an-arraylist-with-linq-c"></a>Procedura: Eseguire una query su un ArrayList con LINQ (C#)
Quando si usa LINQ per eseguire una query su raccolte <xref:System.Collections.IEnumerable> non generiche, come ad esempio <xref:System.Collections.ArrayList>, è necessario dichiarare in modo esplicito il tipo della variabile di intervallo in base al tipo specifico di oggetti nella raccolta. Ad esempio, se si ha un <xref:System.Collections.ArrayList> di oggetti `Student`, la [clausola from](../../../../csharp/language-reference/keywords/from-clause.md) dovrebbe essere così:  
  
```  
  
var query = from Student s in arrList  
...  
  
```  
  
 Specificando il tipo della variabile di intervallo, si esegue il cast di ogni elemento dell'<xref:System.Collections.ArrayList> in `Student`.  
  
 L'uso di una variabile di intervallo tipizzata in modo esplicito in un'espressione di query è equivalente alla chiamata del metodo <xref:System.Linq.Enumerable.Cast%2A>. <xref:System.Linq.Enumerable.Cast%2A> genera un'eccezione se non è possibile eseguire il cast specificato. <xref:System.Linq.Enumerable.Cast%2A> e <xref:System.Linq.Enumerable.OfType%2A> sono i due metodi di operatore query standard che operano su tipi <xref:System.Collections.IEnumerable> non generici. Per altre informazioni, vedere [Relazioni tra i tipi nelle operazioni di query LINQ](../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata una semplice query su un <xref:System.Collections.ArrayList>. Si noti che in questo esempio vengono usati gli inizializzatori di oggetto quando il codice chiama il metodo <xref:System.Collections.ArrayList.Add%2A>, ma questo non è un requisito.  
  
```csharp  
using System;  
using System.Collections;  
using System.Linq;  
  
namespace NonGenericLINQ  
{  
    public class Student  
    {  
        public string FirstName { get; set; }  
        public string LastName { get; set; }  
        public int[] Scores { get; set; }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ArrayList arrList = new ArrayList();  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Svetlana", LastName = "Omelchenko", Scores = new int[] { 98, 92, 81, 60 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Claire", LastName = "O’Donnell", Scores = new int[] { 75, 84, 91, 39 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Sven", LastName = "Mortensen", Scores = new int[] { 88, 94, 65, 91 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Cesar", LastName = "Garcia", Scores = new int[] { 97, 89, 85, 82 }  
                    });  
  
            var query = from Student student in arrList  
                        where student.Scores[0] > 95  
                        select student;  
  
            foreach (Student s in query)  
                Console.WriteLine(s.LastName + ": " + s.Scores[0]);  
  
            // Keep the console window open in debug mode.  
            Console.WriteLine("Press any key to exit.");  
            Console.ReadKey();  
        }  
    }  
}  
/* Output:   
    Omelchenko: 98  
    Garcia: 97  
*/  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)
