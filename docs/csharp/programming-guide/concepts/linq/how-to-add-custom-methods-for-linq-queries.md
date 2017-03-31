---
title: 'Procedura: Aggiungere metodi personalizzati per query LINQ (C#) | Microsoft Docs'
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
ms.assetid: 1a500f60-2e10-49fb-8b2a-d8d08e4817cb
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
ms.openlocfilehash: 7843620518dd7965724f0108a8fa008c95bd4793
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-add-custom-methods-for-linq-queries-c"></a>Procedura: Aggiungere metodi personalizzati per query LINQ (C#)
È possibile estendere il set di metodi da usare per le query LINQ aggiungendo metodi di estensione per l'interfaccia <xref:System.Collections.Generic.IEnumerable%601>. Oltre alla media standard o a un numero massimo di operazioni, ad esempio, è possibile creare un metodo di aggregazione personalizzato per calcolare un singolo valore da una sequenza di valori. È anche possibile creare un metodo che funzioni come un filtro personalizzato o una trasformazione di dati specifica per una sequenza di valori che restituisca una nuova sequenza. Esempi di tali metodi sono <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Skip%2A> e <xref:System.Linq.Enumerable.Reverse%2A>.  
  
 Quando si estende l'interfaccia <xref:System.Collections.Generic.IEnumerable%601>, è possibile applicare i metodi personalizzati per qualsiasi raccolta enumerabile. Per altre informazioni, vedere [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  
  
## <a name="adding-an-aggregate-method"></a>Aggiunta di un metodo di aggregazione  
 Un metodo di aggregazione calcola un singolo valore da un set di valori. LINQ offre diversi metodi di aggregazione, tra cui <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Min%2A> e <xref:System.Linq.Enumerable.Max%2A>. È possibile creare il proprio metodo di aggregazione aggiungendo un metodo di estensione all'interfaccia <xref:System.Collections.Generic.IEnumerable%601>.  
  
 L'esempio di codice seguente illustra come creare un metodo di estensione denominato `Median` per calcolare un valore mediano per una sequenza di numeri di tipo `double`.  
  
```cs  
public static class LINQExtension  
{  
    public static double Median(this IEnumerable<double> source)  
    {  
        if (source.Count() == 0)  
        {  
            throw new InvalidOperationException("Cannot compute median for an empty set.");  
        }  
  
        var sortedList = from number in source  
                         orderby number  
                         select number;  
  
        int itemIndex = (int)sortedList.Count() / 2;  
  
        if (sortedList.Count() % 2 == 0)  
        {  
            // Even number of items.  
            return (sortedList.ElementAt(itemIndex) + sortedList.ElementAt(itemIndex - 1)) / 2;  
        }  
        else  
        {  
            // Odd number of items.  
            return sortedList.ElementAt(itemIndex);  
        }  
    }  
}  
```  
  
 Chiamare questo metodo di estensione per qualsiasi raccolta enumerabile nello stesso modo in cui si chiamano altri metodi di aggregazione dall'interfaccia <xref:System.Collections.Generic.IEnumerable%601>.  
  
 L'esempio di codice seguente illustra come usare il metodo `Median` di una matrice di tipo `double`.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
### <a name="overloading-an-aggregate-method-to-accept-various-types"></a>Overload di un metodo di aggregazione per accettare tipi diversi  
 È possibile eseguire l'overload del metodo di aggregazione in modo che accetti sequenze di tipi diversi. L'approccio standard consiste nel creare un overload per ogni tipo. Un altro approccio consiste nel creare un overload che accetti un tipo generico e lo converta in un tipo specifico tramite un delegato. È anche possibile combinare entrambi gli approcci.  
  
#### <a name="to-create-an-overload-for-each-type"></a>Per creare un overload per ogni tipo  
 È possibile creare un overload specifico per ogni tipo che si vuole supportare. Nell'esempio di codice seguente viene illustrato l'overload del metodo `Median` per il tipo `integer`.  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
 È ora possibile chiamare gli overload `Median` per entrambi i tipi `integer` e `double`, come illustrato nel codice seguente:  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
#### <a name="to-create-a-generic-overload"></a>Per creare un overload generico  
 È anche possibile creare un overload che accetti una sequenza di oggetti generici. Questo overload accetta un delegato come parametro e lo usa per convertire una sequenza di oggetti di un tipo generico in un tipo specifico.  
  
 Nel codice seguente viene illustrato l'overload del metodo `Median` che accetta il delegato <xref:System.Func%602> come parametro. Questo delegato accetta un oggetto di tipo generico T e restituisce un oggetto di tipo `double`.  
  
```cs  
// Generic overload.  
  
public static double Median<T>(this IEnumerable<T> numbers,  
                       Func<T, double> selector)  
{  
    return (from num in numbers select selector(num)).Median();  
}  
```  
  
 È ora possibile chiamare il metodo `Median` per una sequenza di oggetti di qualsiasi tipo. Se il tipo non ha un proprio overload del metodo, è necessario passare un parametro del delegato. In C# è possibile usare un'espressione lambda a questo scopo. Solo in Visual Basic, se si usa la clausola `Aggregate` o `Group By` anziché la chiamata al metodo, è possibile passare qualsiasi valore o espressione che si trovi nell'ambito della clausola.  
  
 L'esempio di codice seguente illustra come chiamare il metodo `Median` per una matrice di numeri interi e una matrice di stringhe. Per le stringhe, viene calcolato il valore mediano della lunghezza delle stringhe nella matrice. Nell'esempio viene illustrato come passare il parametro del delegato <xref:System.Func%602> al metodo `Median` per ogni caso.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
## <a name="adding-a-method-that-returns-a-collection"></a>Aggiunta di un metodo che restituisce una raccolta  
 È possibile estendere l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> con un metodo di query personalizzato che restituisce una sequenza di valori. In questo caso il metodo deve restituire una raccolta di tipo <xref:System.Collections.Generic.IEnumerable%601>. Tali metodi possono essere usati per applicare filtri o trasformazioni di dati in una sequenza di valori.  
  
 Nell'esempio seguente viene illustrato come creare un metodo di estensione denominato `AlternateElements` che restituisce tutti gli altri elementi in una raccolta, a partire dal primo elemento.  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 È possibile chiamare questo metodo di estensione per qualsiasi raccolta enumerabile nello stesso modo in cui si chiamano altri metodi dall'interfaccia <xref:System.Collections.Generic.IEnumerable%601>, come illustrato nel codice seguente:  
  
```cs  
string[] strings = { "a", "b", "c", "d", "e" };  
  
var query = strings.AlternateElements();  
  
foreach (var element in query)  
{  
    Console.WriteLine(element);  
}  
/*  
 This code produces the following output:  
  
 a  
 c  
 e  
*/  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Generic.IEnumerable%601>   
 [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)
