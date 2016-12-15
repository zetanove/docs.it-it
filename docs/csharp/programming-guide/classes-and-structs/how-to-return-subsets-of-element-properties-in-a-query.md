---
title: "Procedura: restituire sottoinsiemi di propriet&#224; degli elementi in una query (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "tipi anonimi [C#], per sottoinsiemi di proprietà degli elementi"
ms.assetid: fabdf349-f443-4e3f-8368-6c471be1dd7b
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: restituire sottoinsiemi di propriet&#224; degli elementi in una query (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Utilizzare un tipo anonimo in un'espressione di query quando si verificano entrambe le condizioni seguenti:  
  
-   Si desidera restituire solo alcune delle proprietà di ogni elemento di origine.  
  
-   Non è necessario archiviare la query all'esterno dell'ambito del metodo in cui è stata eseguita la query.  
  
 Se si desidera restituire solo una proprietà o un campo da ogni elemento di origine, è sufficiente utilizzare l'operatore punto nella clausola `select`.  Per restituire, ad esempio, solo l'`ID` di ogni `student`, scrivere la clausola `select` come segue:  
  
```  
select student.ID;  
```  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un tipo anonimo per restituire solo un sottoinsieme delle proprietà di ogni elemento di origine che corrisponde alla condizione specificata.  
  
 [!code-cs[csProgGuideLINQ#31](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-return-subsets-of-element-properties-in-a-query_1.cs)]  
  
 Si noti che il tipo anonimo utilizza i nomi dell'elemento di origine per le proprietà se non è specificato alcun nome.  Per assegnare nomi nuovi alle proprietà nel tipo anonimo, scrivere l'istruzione `select` come segue:  
  
```  
select new { First = student.FirstName, Last = student.LastName };  
```  
  
 Se si tenta questa operazione nell'esempio precedente, è necessario modificare anche l'istruzione `Console.WriteLine`:  
  
```  
Console.WriteLine(student.First + " " + student.Last);  
```  
  
## Compilazione del codice  
  
-   Per eseguire questo codice, copiare e incollare la classe in un progetto di applicazione console di Visual C\# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)].  Per impostazione predefinita, questo progetto è destinato alla versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] e conterrà un riferimento a System.Core.dll e una direttiva `using` per System.Linq.  Se uno o più di questi requisiti non sono presenti nel progetto, è possibile aggiungerli manualmente.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)