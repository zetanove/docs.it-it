---
title: Varianza nelle interfacce generiche (Visual Basic) | Documenti di Microsoft
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
ms.assetid: cf4096d0-4bb3-45a9-9a6b-f01e29a60333
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c53c27bdb085213046553fc4b08f11336880a7c2
ms.lasthandoff: 03/13/2017

---
# <a name="variance-in-generic-interfaces-visual-basic"></a>Varianza nelle interfacce generiche (Visual Basic)
.NET framework 4 introdotto il supporto della varianza per diverse interfacce generiche esistenti. Il supporto della varianza consente la conversione implicita di classi che implementano tali interfacce. Le interfacce seguenti sono ora variant:  
  
-   <xref:System.Collections.Generic.IEnumerable%601>(T è covariante)</xref:System.Collections.Generic.IEnumerable%601>  
  
-   <xref:System.Collections.Generic.IEnumerator%601>(T è covariante)</xref:System.Collections.Generic.IEnumerator%601>  
  
-   <xref:System.Linq.IQueryable%601>(T è covariante)</xref:System.Linq.IQueryable%601>  
  
-   <xref:System.Linq.IGrouping%602>(`TKey` e `TElement` sono covarianti)</xref:System.Linq.IGrouping%602>  
  
-   <xref:System.Collections.Generic.IComparer%601>(T è controvariante)</xref:System.Collections.Generic.IComparer%601>  
  
-   <xref:System.Collections.Generic.IEqualityComparer%601>(T è controvariante)</xref:System.Collections.Generic.IEqualityComparer%601>  
  
-   <xref:System.IComparable%601>(T è controvariante)</xref:System.IComparable%601>  
  
 La covarianza consente a un metodo per restituire un tipo più derivato da quello definito dal parametro di tipo generico dell'interfaccia. Per illustrare la funzionalità di covarianza, considerare le seguenti interfacce generiche: `IEnumerable(Of Object)` e `IEnumerable(Of String)`. Il `IEnumerable(Of String)` interfaccia non eredita il `IEnumerable(Of Object)` interfaccia. Tuttavia, il `String` tipo ereditare il `Object` tipo e in alcuni casi è consigliabile assegnare gli oggetti di queste interfacce tra loro. Come illustrato nell'esempio di codice seguente.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Nelle versioni precedenti di .NET Framework, questo codice causa un errore di compilazione in Visual Basic con `Option Strict On`. Ma ora è possibile utilizzare `strings` invece di `objects`, come illustrato nell'esempio precedente, in quanto il <xref:System.Collections.Generic.IEnumerable%601>interfaccia è covariante.</xref:System.Collections.Generic.IEnumerable%601>  
  
 La controvarianza consente a un metodo di tipi di argomenti che sono meno derivati rispetto a quello specificato dal parametro generico dell'interfaccia. Per illustrare la controvarianza, si supponga di aver creato un `BaseComparer` per confrontare le istanze della classe di `BaseClass` (classe). La classe `BaseComparer` implementa l'interfaccia `IEqualityComparer(Of BaseClass)`. Poiché il <xref:System.Collections.Generic.IEqualityComparer%601>interfaccia è controvariante, è possibile utilizzare `BaseComparer` per confrontare le istanze di classi che ereditano la `BaseClass` classe</xref:System.Collections.Generic.IEqualityComparer%601> Come illustrato nell'esempio di codice seguente.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 Per ulteriori esempi, vedere [utilizzando varianza nelle interfacce per le raccolte generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md).  
  
 Varianza nelle interfacce generiche è supportata per i tipi di riferimento solo. Tipi di valore non supportano la varianza. Ad esempio, `IEnumerable(Of Integer)` non può essere convertita implicitamente in `IEnumerable(Of Object)`, in quanto i valori integer sono rappresentati da un tipo di valore.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 È inoltre importante ricordare che le classi che implementano interfacce variant sono ancora invariate. Ad esempio, sebbene <xref:System.Collections.Generic.List%601>implementa l'interfaccia covariante <xref:System.Collections.Generic.IEnumerable%601>, non è possibile convertire in modo implicito `List(Of Object)` a `List(Of String)`.</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.Generic.List%601> Come illustrato nell'esempio di codice seguente.  
  
```vb  
' The following statement generates a compiler error  
' because classes are invariant.  
' Dim list As List(Of Object) = New List(Of String)  
  
' You can use the interface object instead.  
Dim listObjects As IEnumerable(Of Object) = New List(Of String)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo della varianza nelle interfacce per le raccolte generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)   
 [Creazione di interfacce generiche Variant (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)   
 [Interfacce generiche](http://msdn.microsoft.com/library/88bf5b04-d371-4edb-ba38-01ec7cabaacf)   
 [Varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
