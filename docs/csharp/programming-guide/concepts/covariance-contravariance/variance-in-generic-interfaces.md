---
title: Varianza nelle interfacce generiche (C#) | Microsoft Docs
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
ms.assetid: 4828a8f9-48c0-4128-9749-7fcd6bf19a06
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
ms.openlocfilehash: 4c4f3ab00b4de2a6f38858dd5f332db3d47eb85b
ms.lasthandoff: 03/13/2017

---
# <a name="variance-in-generic-interfaces-c"></a>Varianza nelle interfacce generiche (C#)
In .NET framework 4 è stato introdotto il supporto della varianza per diverse interfacce generiche esistenti. Il supporto della varianza consente la conversione implicita delle classi che implementano tali interfacce. Le interfacce seguenti sono ora varianti:  
  
-   <xref:System.Collections.Generic.IEnumerable%601> (T è covariante)  
  
-   <xref:System.Collections.Generic.IEnumerator%601> (T è covariante)  
  
-   <xref:System.Linq.IQueryable%601> (T è covariante)  
  
-   <xref:System.Linq.IGrouping%602> (`TKey` e `TElement` sono covarianti)  
  
-   <xref:System.Collections.Generic.IComparer%601> (T è controvariante)  
  
-   <xref:System.Collections.Generic.IEqualityComparer%601> (T è controvariante)  
  
-   <xref:System.IComparable%601> (T è controvariante)  
  
 La covarianza consente a un metodo di avere un tipo restituito più derivato rispetto a quello definito dal parametro di tipo generico dell'interfaccia. Per illustrare la funzionalità di covarianza, considerare le seguenti interfacce generiche: `IEnumerable<Object>` e `IEnumerable<String>`. L'interfaccia `IEnumerable<String>` non eredita l'interfaccia`IEnumerable<Object>`. Tuttavia, il tipo `String` eredita il tipo `Object` e in alcuni casi è opportuno assegnare gli oggetti di ogni interfaccia all'altra. Queste operazioni sono illustrate nell'esempio di codice riportato di seguito.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Nelle versioni precedenti di .NET Framework, questo codice causa un errore di compilazione in C# con `Option Strict On`. Ma ora è possibile usare `strings` anziché `objects`, come illustrato nell'esempio precedente, perché l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> è covariante.  
  
 La controvarianza consente a un metodo di avere tipi di argomenti meno derivati rispetto a quelli specificati dal parametro generico dell'interfaccia. Per illustrare la controvarianza, si supponga di aver creato una classe `BaseComparer` per confrontare le istanze della classe `BaseClass`. La classe `BaseComparer` implementa l'interfaccia `IEqualityComparer<BaseClass>`. Poiché l'interfaccia <xref:System.Collections.Generic.IEqualityComparer%601> ora è controvariante, è possibile usare `BaseComparer` per confrontare le istanze delle classi che ereditano la classe `BaseClass`. Queste operazioni sono illustrate nell'esempio di codice riportato di seguito.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 Per altri esempi, vedere [Uso della varianza nelle interfacce per le raccolte generiche (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md).  
  
 La varianza nelle interfacce generiche è supportata solo per i tipi di riferimento. I tipi di valore non supportano la varianza. Ad esempio, non è possibile convertire `IEnumerable<int>` in modo implicito in `IEnumerable<object>` perché i valori integer sono rappresentati da un tipo di valore.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 È anche importante ricordare che le classi che implementano le interfacce varianti sono comunque invariabili. Ad esempio, sebbene <xref:System.Collections.Generic.List%601> implementi l'interfaccia covariante <xref:System.Collections.Generic.IEnumerable%601>, non è possibile convertire in modo implicito `List<Object>` in `List<String>`, come illustra l'esempio di codice riportato di seguito.  
  
```cs  
// The following line generates a compiler error  
// because classes are invariant.  
// List<Object> list = new List<String>();  
  
// You can use the interface object instead.  
IEnumerable<Object> listObjects = new List<String>();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso della varianza nelle interfacce per le raccolte generiche (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)   
 [Creazione di interfacce generiche varianti (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)   
 [Interfacce generiche](http://msdn.microsoft.com/library/88bf5b04-d371-4edb-ba38-01ec7cabaacf)   
 [Varianza nei delegati (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
