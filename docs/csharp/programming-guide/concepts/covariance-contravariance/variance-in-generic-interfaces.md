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
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 7acde09659624fd097471824e6407dc181d88893
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

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
  
```csharp  
IEnumerable<String> strings = new List<String>();  
IEnumerable<Object> objects = strings;  
```  
  
 Nelle versioni precedenti di .NET Framework, questo codice causa un errore di compilazione in C# con `Option Strict On`. Ora è invece possibile usare `strings` anziché `objects`, come illustrato nell'esempio precedente, poiché l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> è covariante.  
  
 La controvarianza consente a un metodo di avere tipi di argomenti meno derivati rispetto a quelli specificati dal parametro generico dell'interfaccia. Per illustrare la controvarianza, si supponga di aver creato una classe `BaseComparer` per confrontare le istanze della classe `BaseClass`. La classe `BaseComparer` implementa l'interfaccia `IEqualityComparer<BaseClass>`. Poiché l'interfaccia `BaseClass` è ora controvariante, è possibile usare <xref:System.Collections.Generic.IEqualityComparer%601> per confrontare le istanze delle classi che ereditano la classe `BaseComparer`. Queste operazioni sono illustrate nell'esempio di codice riportato di seguito.  
  
```csharp  
// Simple hierarchy of classes.  
class BaseClass { }  
class DerivedClass : BaseClass { }  
  
// Comparer class.  
class BaseComparer : IEqualityComparer<BaseClass>   
{  
    public int GetHashCode(BaseClass baseInstance)  
    {  
        return baseInstance.GetHashCode();  
    }  
    public bool Equals(BaseClass x, BaseClass y)  
    {  
        return x == y;  
    }  
}  
class Program  
{  
    static void Test()  
    {  
        IEqualityComparer<BaseClass> baseComparer = new BaseComparer();  
  
        // Implicit conversion of IEqualityComparer<BaseClass> to   
        // IEqualityComparer<DerivedClass>.  
        IEqualityComparer<DerivedClass> childComparer = baseComparer;  
    }  
}  
```  
  
 Per altri esempi, vedere [Uso della varianza nelle interfacce per le raccolte generiche (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md).  
  
 La varianza nelle interfacce generiche è supportata solo per i tipi di riferimento. I tipi di valore non supportano la varianza. Ad esempio, non è possibile convertire `IEnumerable<int>` in modo implicito in `IEnumerable<object>` perché i valori integer sono rappresentati da un tipo di valore.  
  
```csharp  
IEnumerable<int> integers = new List<int>();  
// The following statement generates a compiler errror,  
// because int is a value type.  
// IEnumerable<Object> objects = integers;  
```  
  
 È anche importante ricordare che le classi che implementano le interfacce varianti sono comunque invariabili. Ad esempio, sebbene <xref:System.Collections.Generic.List%601> implementi l'interfaccia covariante <xref:System.Collections.Generic.IEnumerable%601>, non è possibile convertire `List<Object>` in `List<String>` in modo implicito. come illustra l'esempio di codice riportato di seguito.  
  
```csharp  
// The following line generates a compiler error  
// because classes are invariant.  
// List<Object> list = new List<String>();  
  
// You can use the interface object instead.  
IEnumerable<Object> listObjects = new List<String>();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso della varianza nelle interfacce per le raccolte generiche (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)   
 [Creazione di interfacce generiche varianti (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)   
 [Interfacce generiche](../../../../standard/generics/interfaces.md)   
 [Varianza nei delegati (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
