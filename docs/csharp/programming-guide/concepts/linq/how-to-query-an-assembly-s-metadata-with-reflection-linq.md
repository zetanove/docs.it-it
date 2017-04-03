---
title: 'Procedura: Eseguire una query sui metadati di un assembly tramite reflection (LINQ) (C#) | Microsoft Docs'
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
ms.assetid: c4cdce49-b1c8-4420-b12a-9ff7e6671368
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 50409af2add7f5ca3d591ac9d942e45ccce409af
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-query-an-assembly39s-metadata-with-reflection-linq-c"></a>Procedura: Eseguire una query sui metadati di un assembly tramite reflection (LINQ) (C#)
Nell'esempio seguente viene illustrato come LINQ può essere usato con il processo di reflection per recuperare metadati specifici sui metodi che corrispondono a un criterio di ricerca specificato. In questo caso la query individuerà i nomi di tutti i metodi dell'assembly che restituiscono tipi enumerabili, ad esempio matrici.  
  
## <a name="example"></a>Esempio  
  
```csharp  
using System.Reflection;  
using System.IO;  
namespace LINQReflection  
{  
    class ReflectionHowTO  
    {  
        static void Main(string[] args)  
        {  
            Assembly assembly = Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089");  
            var pubTypesQuery = from type in assembly.GetTypes()  
                        where type.IsPublic  
                            from method in type.GetMethods()  
                            where method.ReturnType.IsArray == true   
                                || ( method.ReturnType.GetInterface(  
                                    typeof(System.Collections.Generic.IEnumerable<>).FullName ) != null  
                                && method.ReturnType.FullName != "System.String" )  
                            group method.ToString() by type.ToString();  
  
            foreach (var groupOfMethods in pubTypesQuery)  
            {  
                Console.WriteLine("Type: {0}", groupOfMethods.Key);  
                foreach (var method in groupOfMethods)  
                {  
                    Console.WriteLine("  {0}", method);  
                }  
            }  
  
            Console.WriteLine("Press any key to exit");  
            Console.ReadKey();  
        }  
    }    
}  
```  
  
 Nell'esempio viene usato il metodo <xref:System.Reflection.Assembly.GetTypes%2A> per restituire una matrice di tipi nell'assembly specificato. Il filtro [where](../../../../csharp/language-reference/keywords/where-clause.md) viene applicato in modo che vengano restituiti solo i tipi pubblici. Per ogni tipo pubblico, viene generata una sottoquery usando la matrice <xref:System.Reflection.MethodInfo> restituita dalla chiamata <xref:System.Type.GetMethods%2A>. Questi risultati vengono filtrati per restituire solo i metodi il cui tipo restituito è una matrice oppure un tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>. Infine, questi risultati vengono raggruppati usando il nome del tipo come chiave.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto che usi .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e alle direttive `using` per gli spazi dei nomi System.Linq e System.IO.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)
