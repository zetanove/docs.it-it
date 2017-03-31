---
title: Sintassi di espressione di query per operatori di query standard (C#) | Documentazione Microsoft
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
ms.assetid: e1e17ef2-68ff-4c26-b6e2-015668227fa5
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
ms.openlocfilehash: 115f97eec99d5f22a659532ccf4ed7b20a089014
ms.lasthandoff: 03/13/2017

---
# <a name="query-expression-syntax-for-standard-query-operators-c"></a>Sintassi di espressione di query per operatori di query standard (C#)
Alcuni degli operatori di query standard usati più di frequente dispongono di una sintassi dedicata delle parole chiave per i linguaggi C# che consente di chiamare gli operatori come parte di un'espressione di *query*. Un'espressione di query rappresenta un modo diverso e più leggibile per esprimere una query rispetto alla sintassi equivalente *basata su metodo*. Le clausole di espressione di query vengono convertite in chiamate ai metodi di query in fase di compilazione.  
  
## <a name="query-expression-syntax-table"></a>Tabella della sintassi di espressione di query  
 La tabella seguente elenca gli operatori di query standard che hanno clausole di espressione di query equivalenti.  
  
|Metodo|Sintassi di espressione della query C#|  
|------------|---------------------------------|  
|<xref:System.Linq.Enumerable.Cast%2A>|Usare una variabile di intervallo tipizzata in modo esplicito, ad esempio:<br /><br /> `from int i in numbers`<br /><br /> Per altre informazioni, vedere [Clausola from](../../../../csharp/language-reference/keywords/from-clause.md).|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`group … by`<br /><br /> -oppure-<br /><br /> `group … by … into …`<br /><br /> Per altre informazioni, vedere [Clausola group](../../../../csharp/language-reference/keywords/group-clause.md).|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`join … in … on … equals … into …`<br /><br /> Per altre informazioni, vedere [Clausola join](../../../../csharp/language-reference/keywords/join-clause.md).|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`join … in … on … equals …`<br /><br /> Per altre informazioni, vedere [Clausola join](../../../../csharp/language-reference/keywords/join-clause.md).|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby`<br /><br /> Per altre informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).|  
<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby … descending`<br /><br /> Per altre informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).|  
|<xref:System.Linq.Enumerable.Select%2A>|`select`<br /><br /> Per altre informazioni, vedere [Clausola select](../../../../csharp/language-reference/keywords/select-clause.md).|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|Più clausole `from`.<br /><br /> Per altre informazioni, vedere [Clausola from](../../../../csharp/language-reference/keywords/from-clause.md).|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, …`<br /><br /> Per altre informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, … descending`<br /><br /> Per altre informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).|  
|<xref:System.Linq.Enumerable.Where%2A>|`where`<br /><br /> Per altre informazioni, vedere [Clausola where](../../../../csharp/language-reference/keywords/where-clause.md).|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable>   
 [Cenni preliminari sugli operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Classificazione degli operatori di query standard in base alla modalità di esecuzione (C#)](../../../../csharp/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)
