---
title: 'Procedura: Usare alberi delle espressioni per la compilazione di query dinamiche (C#) | Microsoft Docs'
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
ms.assetid: 52cd44dd-a3ec-441e-b93a-4eca388119c7
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 76dc6ebe2cc2489d83a2693a3143d36d46c8ef82
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="how-to-use-expression-trees-to-build-dynamic-queries-c"></a>Procedura: Usare alberi delle espressioni per la compilazione di query dinamiche (C#)
In LINQ gli alberi delle espressioni vengono usati per rappresentare query strutturate destinate alle origini dati che implementano <xref:System.Linq.IQueryable%601>. Il provider LINQ, ad esempio, implementa l'interfaccia <xref:System.Linq.IQueryable%601> per l'esecuzione di query su archivi dati relazionali. Il compilatore C# compila le query destinate a tali origini dati nel codice di un albero delle espressioni in runtime. Il provider di query può quindi percorrere la struttura dei dati dell'albero delle espressioni e convertirla in un linguaggio di query adatto all'origine dati.  
  
 In LINQ gli alberi delle espressioni sono usati anche per rappresentare espressioni lambda assegnate a variabili di tipo <xref:System.Linq.Expressions.Expression%601>.  
  
 Questo argomento descrive come usare gli alberi delle espressioni per creare query LINQ dinamiche. Le query dinamiche sono utili quando le specifiche di una query non sono note in fase di compilazione. Supponiamo ad esempio che un'applicazione offra un'interfaccia utente che consente all'utente finale di specificare uno o più predicati per filtrare i dati. Per usare LINQ per l'esecuzione di query e creare query LINQ in runtime, un'applicazione di questo tipo deve usare alberi delle espressioni.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come usare alberi delle espressioni per costruire una query su un'origine dati `IQueryable` e quindi eseguirla. Il codice compila un albero delle espressioni per rappresentare la query seguente:  
  
 `companies.Where(company => (company.ToLower() == "coho winery" || company.Length > 16)).OrderBy(company => company)`  
  
 I metodi factory nello spazio dei nomi <xref:System.Linq.Expressions> vengono usati per creare alberi delle espressioni che rappresentano le espressioni che costituiscono la query complessiva. Le espressioni che rappresentano le chiamate ai metodi operatore query standard fanno riferimento alle implementazioni di <xref:System.Linq.Queryable> di questi metodi. L'albero delle espressioni finale viene passato all'implementazione di <xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29> del provider dell'origine dati `IQueryable` per creare una query eseguibile di tipo `IQueryable`. I risultati si ottengono enumerando tale variabile di query.  
  
```csharp  
// Add a using directive for System.Linq.Expressions.  
  
string[] companies = { "Consolidated Messenger", "Alpine Ski House", "Southridge Video", "City Power & Light",  
                   "Coho Winery", "Wide World Importers", "Graphic Design Institute", "Adventure Works",  
                   "Humongous Insurance", "Woodgrove Bank", "Margie's Travel", "Northwind Traders",  
                   "Blue Yonder Airlines", "Trey Research", "The Phone Company",  
                   "Wingtip Toys", "Lucerne Publishing", "Fourth Coffee" };  
  
// The IQueryable data to query.  
IQueryable<String> queryableData = companies.AsQueryable<string>();  
  
// Compose the expression tree that represents the parameter to the predicate.  
ParameterExpression pe = Expression.Parameter(typeof(string), "company");  
  
// ***** Where(company => (company.ToLower() == "coho winery" || company.Length > 16)) *****  
// Create an expression tree that represents the expression 'company.ToLower() == "coho winery"'.  
Expression left = Expression.Call(pe, typeof(string).GetMethod("ToLower", System.Type.EmptyTypes));  
Expression right = Expression.Constant("coho winery");  
Expression e1 = Expression.Equal(left, right);  
  
// Create an expression tree that represents the expression 'company.Length > 16'.  
left = Expression.Property(pe, typeof(string).GetProperty("Length"));  
right = Expression.Constant(16, typeof(int));  
Expression e2 = Expression.GreaterThan(left, right);  
  
// Combine the expression trees to create an expression tree that represents the  
// expression '(company.ToLower() == "coho winery" || company.Length > 16)'.  
Expression predicateBody = Expression.OrElse(e1, e2);  
  
// Create an expression tree that represents the expression  
// 'queryableData.Where(company => (company.ToLower() == "coho winery" || company.Length > 16))'  
MethodCallExpression whereCallExpression = Expression.Call(  
    typeof(Queryable),  
    "Where",  
    new Type[] { queryableData.ElementType },  
    queryableData.Expression,  
    Expression.Lambda<Func<string, bool>>(predicateBody, new ParameterExpression[] { pe }));  
// ***** End Where *****  
  
// ***** OrderBy(company => company) *****  
// Create an expression tree that represents the expression  
// 'whereCallExpression.OrderBy(company => company)'  
MethodCallExpression orderByCallExpression = Expression.Call(  
    typeof(Queryable),  
    "OrderBy",  
    new Type[] { queryableData.ElementType, queryableData.ElementType },  
    whereCallExpression,  
    Expression.Lambda<Func<string, string>>(pe, new ParameterExpression[] { pe }));  
// ***** End OrderBy *****  
  
// Create an executable query from the expression tree.  
IQueryable<string> results = queryableData.Provider.CreateQuery<string>(orderByCallExpression);  
  
// Enumerate the results.  
foreach (string company in results)  
    Console.WriteLine(company);  
  
/*  This code produces the following output:  
  
    Blue Yonder Airlines  
    City Power & Light  
    Coho Winery  
    Consolidated Messenger  
    Graphic Design Institute  
    Humongous Insurance  
    Lucerne Publishing  
    Northwind Traders  
    The Phone Company  
    Wide World Importers  
*/  
```  
  
 Questo codice usa un numero fisso di espressioni nel predicato passato al metodo `Queryable.Where`. È tuttavia possibile scrivere un'applicazione che combini un numero variabile di espressioni di predicato a seconda dall'input dell'utente. È anche possibile variare gli operatori query standard chiamati nella query in base all'input dell'utente.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
-   Creare un nuovo progetto **Applicazione console**.  
  
-   Aggiungere un riferimento a System.Core.dll, se non è già presente.  
  
-   Includere lo spazio dei nomi System.Linq.Expressions.  
  
-   Copiare il codice dall'esempio e incollarlo nel metodo `Main`.  
  
## <a name="see-also"></a>Vedere anche  
 [Alberi delle espressioni (C#)](../../../../csharp/programming-guide/concepts/expression-trees/index.md)   
 [Procedura: Eseguire alberi delle espressioni (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [Procedura: Specificare dinamicamente i filtri dei predicati in fase di esecuzione](../../../../csharp/programming-guide/linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)
