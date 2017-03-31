---
title: Clausola where (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- whereclause_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- where keyword [C#]
- where clause [C#]
ms.assetid: 7f9bf952-7744-4f91-b676-cddb55d107c3
caps.latest.revision: 16
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
ms.openlocfilehash: 1094f68293dd05fdfe69a39016689cbaa3fd6290
ms.lasthandoff: 03/13/2017

---
# <a name="where-clause-c-reference"></a>Clausola where (Riferimento C#)
La clausola `where` viene usata in un'espressione di query per specificare quali elementi dell'origine dati verranno restituiti nell'espressione di query. Viene applicata una condizione booleana (*predicato*) a ogni elemento di origine (a cui fa riferimento la variabile di intervallo) e viene restituita quella per cui la condizione specificata è vera. Una singola espressione di query può contenere più clausole `where` e una singola clausola può contenere più sottoespressioni di predicato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente la clausola `where` esclude tutti i numeri tranne quelli minori di cinque. Se si rimuove la clausola `where`, vengono restituiti tutti i numeri dell'origine dati. L'espressione `num < 5` è il predicato che viene applicato a ogni elemento.  
  
 [!code-cs[cscsrefQueryKeywords#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-clause_1.cs)]  
  
## <a name="example"></a>Esempio  
 In una singola clausola `where` è possibile specificare tutti i predicati necessari usando gli operatori [ && ](../../../csharp/language-reference/operators/conditional-and-operator.md) e [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md). Nell'esempio seguente la query specifica due predicati per selezionare solo i numeri pari minori di cinque.  
  
 [!code-cs[cscsrefQueryKeywords#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-clause_2.cs)]  
  
## <a name="example"></a>Esempio  
 Una clausola `where` può contenere uno o più metodi che restituiscono valori booleani. Nell'esempio seguente la clausola `where` usa un metodo per determinare se il valore corrente della variabile di intervallo è pari o dispari.  
  
 [!code-cs[cscsrefQueryKeywords#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-clause_3.cs)]  
  
## <a name="remarks"></a>Note  
 La clausola `where` è un meccanismo di filtro. Può essere posizionata praticamente ovunque in un'espressione di query, ma non può essere la prima o l'ultima clausola. Una clausola `where` la può apparire prima o dopo una clausola [group](../../../csharp/language-reference/keywords/group-clause.md) a seconda se gli elementi di origine devono essere filtrati prima o dopo essere stati raggruppati.  
  
 Se un predicato specificato non è valido per gli elementi nell'origine dati, si verificherà un errore in fase di compilazione. Questo è uno dei vantaggi del controllo efficace del tipo offerto da [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].  
  
 In fase di compilazione la parola chiave `where` viene convertita in una chiamata al metodo <xref:System.Linq.Enumerable.Where%2A> dell'operatore query standard.  
  
## <a name="see-also"></a>Vedere anche  
 [Parole chiave di query (LINQ)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Clausola from](../../../csharp/language-reference/keywords/from-clause.md)   
 [Clausola select](../../../csharp/language-reference/keywords/select-clause.md)   
 [Filtraggio dei dati](http://msdn.microsoft.com/library/cee88d0f-31aa-4c60-9452-cc122ed0057d)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Nozioni di base su LINQ in C#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)
