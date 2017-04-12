---
title: Ordinamento dei dati (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 6f81065c-0c89-4bf3-a6d8-442273f8810e
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d6a009573f9ff3eba71875945128ee6cd37ac37b
ms.lasthandoff: 03/13/2017

---
# <a name="sorting-data-visual-basic"></a>Ordinamento dei dati (Visual Basic)
Un'operazione di ordinamento Ordina gli elementi di una sequenza in base a uno o più attributi. Il primo criterio di ordinamento consente di applicare un ordinamento principale agli elementi. Specificando un secondo criterio di ordinamento, è possibile ordinare gli elementi all'interno di ogni gruppo di ordinamento principale.  
  
 Nella figura seguente mostra i risultati di un'operazione di ordinamento alfabetico su una sequenza di caratteri.  
  
 ![Operazione di ordinamento LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq_ordering.png "LINQ_Ordering")  
  
 Nella sezione seguente sono elencati i metodi dell'operatore query standard che ordinano i dati.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|OrderBy|Ordina i valori in ordine crescente.|`Order By`|<xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=fullName></xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.OrderBy%2A?displayProperty=fullName></xref:System.Linq.Queryable.OrderBy%2A?displayProperty=fullName>|  
|OrderByDescending|Ordina i valori in ordine decrescente.|`Order By … Descending`|<xref:System.Linq.Enumerable.OrderByDescending%2A?displayProperty=fullName></xref:System.Linq.Enumerable.OrderByDescending%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.OrderByDescending%2A?displayProperty=fullName></xref:System.Linq.Queryable.OrderByDescending%2A?displayProperty=fullName>|  
|ThenBy|Esegue un ordinamento secondario in ordine crescente.|`Order By …, …`|<xref:System.Linq.Enumerable.ThenBy%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ThenBy%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.ThenBy%2A?displayProperty=fullName></xref:System.Linq.Queryable.ThenBy%2A?displayProperty=fullName>|  
|ThenByDescending|Esegue un ordinamento secondario in ordine decrescente.|`Order By …, … Descending`|<xref:System.Linq.Enumerable.ThenByDescending%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ThenByDescending%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.ThenByDescending%2A?displayProperty=fullName></xref:System.Linq.Queryable.ThenByDescending%2A?displayProperty=fullName>|  
|Reverse|Inverte l'ordine degli elementi in una raccolta.|Non applicabile.|<xref:System.Linq.Enumerable.Reverse%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Reverse%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Reverse%2A?displayProperty=fullName></xref:System.Linq.Queryable.Reverse%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>Esempi di sintassi delle espressioni di query  
  
### <a name="primary-sort-examples"></a>Esempi di ordinamento principale  
  
#### <a name="primary-ascending-sort"></a>Ordinamento crescente principale  
 Nell'esempio seguente viene illustrato come utilizzare il `Order By` clausola in una query LINQ per ordinare le stringhe in una matrice in base alla lunghezza di stringa, in ordine crescente.  
  
```vb  
Dim words = {"the", "quick", "brown", "fox", "jumps"}  
  
Dim sortQuery = From word In words   
                Order By word.Length   
                Select word  
  
Dim sb As New System.Text.StringBuilder()  
For Each str As String In sortQuery  
    sb.AppendLine(str)  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' the  
' fox  
' quick  
' brown  
' jumps  
```  
  
#### <a name="primary-descending-sort"></a>Ordinamento decrescente principale  
 Nell'esempio seguente viene illustrato come utilizzare il `Order By Descending` clausola in una query LINQ per ordinare le stringhe in base alla prima lettera, in ordine decrescente.  
  
```vb  
Dim words = {"the", "quick", "brown", "fox", "jumps"}  
  
Dim sortQuery = From word In words   
                Order By word.Substring(0, 1) Descending   
                Select word  
  
Dim sb As New System.Text.StringBuilder()  
For Each str As String In sortQuery  
    sb.AppendLine(str)  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' the  
' quick  
' jumps  
' fox  
' brown  
```  
  
### <a name="secondary-sort-examples"></a>Esempi di ordinamento secondaria  
  
#### <a name="secondary-ascending-sort"></a>Ordinamento crescente secondario  
 Nell'esempio seguente viene illustrato come utilizzare il `Order By` clausola in una query LINQ per eseguire un ordinamento primario e secondario delle stringhe in una matrice. Le stringhe vengono ordinate principalmente dalla lunghezza e poi in base alla prima lettera della stringa, in ordine crescente.  
  
```vb  
Dim words = {"the", "quick", "brown", "fox", "jumps"}  
  
Dim sortQuery = From word In words   
                Order By word.Length, word.Substring(0, 1)   
                Select word  
  
Dim sb As New System.Text.StringBuilder()  
For Each str As String In sortQuery  
    sb.AppendLine(str)  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' fox  
' the  
' brown  
' jumps  
' quick  
```  
  
#### <a name="secondary-descending-sort"></a>Ordinamento decrescente secondario  
 Nell'esempio seguente viene illustrato come utilizzare il `Order By Descending` clausola in una query LINQ per eseguire un ordinamento principale, in ordine crescente e un ordinamento secondario, in ordine decrescente. Le stringhe vengono ordinate principalmente dalla lunghezza e poi in base alla prima lettera della stringa.  
  
```vb  
Dim words = {"the", "quick", "brown", "fox", "jumps"}  
  
Dim sortQuery = From word In words   
                Order By word.Length, word.Substring(0, 1) Descending   
                Select word  
  
Dim sb As New System.Text.StringBuilder()  
For Each str As String In sortQuery  
    sb.AppendLine(str)  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' fox  
' the  
' quick  
' jumps  
' brown  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola Order By](../../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Procedura: ordinare i risultati della Query](../../../../visual-basic/programming-guide/language-features/linq/how-to-sort-query-results-by-using-linq.md)   
 [Procedura: ordinare o filtrare i dati di testo da qualsiasi parola o campo (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
