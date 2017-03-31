---
title: "Procedura: Restituire sottoinsiemi di proprietà degli elementi in una query (Guida per programmatori C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- anonymous types [C#], for subsets of element properties
ms.assetid: fabdf349-f443-4e3f-8368-6c471be1dd7b
caps.latest.revision: 11
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3849d26506278fede6642530c60b6ec418f39464
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-return-subsets-of-element-properties-in-a-query-c-programming-guide"></a>Procedura: restituire sottoinsiemi di proprietà degli elementi in una query (Guida per programmatori C#)
Usare un tipo anonimo in un'espressione di query quando si verificano entrambe le condizioni seguenti:  
  
-   Si vogliono restituire solo alcune delle proprietà di ogni elemento di origine.  
  
-   Non è necessario archiviare la query all'esterno dell'ambito del metodo in cui è stata eseguita.  
  
 Se si vuole restituire solo una proprietà o un campo da ogni elemento di origine, è sufficiente usare l'operatore punto nella clausola `select`. Per restituire, ad esempio, solo l'`ID` di ogni `student`, scrivere la clausola `select` come segue:  
  
```  
select student.ID;  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come usare un tipo anonimo per restituire solo un sottoinsieme delle proprietà di ogni elemento di origine che corrisponde alla condizione specificata.  
  
 [!code-cs[csProgGuideLINQ#31](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-return-subsets-of-element-properties-in-a-query_1.cs)]  
  
 Si noti che se per le proprietà non è specificato alcun nome, il tipo anonimo usa i nomi dell'elemento di origine. Per assegnare nuovi nomi alle proprietà nel tipo anonimo, scrivere l'istruzione `select` come segue:  
  
```  
select new { First = student.FirstName, Last = student.LastName };  
```  
  
 Se si tenta questa operazione nell'esempio precedente, è necessario modificare anche l'istruzione `Console.WriteLine`:  
  
```  
Console.WriteLine(student.First + " " + student.Last);  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
-   Per eseguire questo codice, copiare e incollare la classe in un progetto di applicazione console di Visual C# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)]. Per impostazione predefinita, questo progetto usa la versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] e contiene un riferimento a System.Core.dll e una direttiva `using` per System.Linq. Se uno o più di questi requisiti non sono presenti nel progetto, è possibile aggiungerli manualmente.   
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)
