---
title: Confronti e ordinamenti all&quot;interno delle raccolte
description: Confronti e ordinamenti all&quot;interno delle raccolte
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c7b7c005-628d-427a-91ad-af0c3958c00e
translationtype: Human Translation
ms.sourcegitcommit: e07788926a995b41571be276379ad9285747951d
ms.openlocfilehash: bad7fd4e9cda1976a31f287d7c95d81d113a30fa

---

# <a name="comparisons-and-sorts-within-collections"></a>Confronti e ordinamenti all'interno delle raccolte

Le classi [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) eseguono confronti in quasi tutti i processi di gestione delle raccolte, che si tratti di cercare l'elemento da rimuovere o di restituire il valore di una coppia chiave-valore.

Le raccolte in genere usano un operatore di uguaglianza e/o un confronto di ordinamento. Vengono usati due costrutti per i confronti. 

## <a name="checking-for-equality"></a>Verifica dell'uguaglianza

I metodi come `Contains`, `IndexOf`, `LastIndexOf` e `Remove` usano un confronto di uguaglianza per gli elementi della raccolta. Se la raccolta è generica, viene verificata l'uguaglianza degli elementi secondo le linee guida seguenti:

*   Se il tipo T implementa l'interfaccia generica [IEquatable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IEquatable-1), l'operatore di confronto di uguaglianza è il metodo `Equals` di tale interfaccia.

*   Se il tipo T non implementa `IEquatable<T>`, viene usato `Object.Equals`.

Alcuni overload del costruttore per le raccolte dizionario accettano un'implementazione di [IEqualityComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEqualityComparer-1), che viene usata per confrontare l'uguaglianza delle chiavi.

## <a name="determining-sort-order"></a>Determinare il tipo di ordinamento

I metodi come `BinarySearch` e `Sort` usano un confronto di ordinamento per gli elementi della raccolta. È possibile eseguire il confronto tra gli elementi della raccolta o tra un elemento e un valore specificato. Per confrontare gli oggetti, esistono un operatore di confronto predefinito e un operatore di confronto esplicito. 

L'operatore di confronto predefinito si basa su almeno uno degli oggetti confrontati per implementare l'interfaccia `IComparable`. È consigliabile implementare `IComparable` in tutte le classi che vengono usate come valori in una raccolta di elenchi o come chiavi in una raccolta di dizionari. Per una raccolta generica, il confronto di uguaglianza è determinato come segue:

*   Se il tipo T implementa l'interfaccia generica [System.IComparable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IComparable-1), l'operatore di confronto predefinito è il metodo `CompareTo(T)` di tale interfaccia.

*   Se il tipo T implementa l'interfaccia non generica [System.IComparable](https://docs.microsoft.com/dotnet/core/api/System.IComparable), l'operatore di confronto predefinito è il metodo `CompareTo`(Object) di tale interfaccia.

*   Se il tipo T non implementa alcuna interfaccia, non sarà presente nessun operatore di confronto predefinito e sarà necessario fornire in modo esplicito un delegato di confronto un o operatore di confronto.

Per specificare i confronti espliciti, alcuni metodi accettano un'implementazione `IComparer` come parametro. Ad esempio, il metodo `List<T>.Sort` accetta un'implementazione [System.Collections.Generic.IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1). 

## <a name="equality-and-sort-example"></a>Esempio di uguaglianza e ordinamento

Nel codice seguente viene illustrata un'implementazione di [IEquatable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IEquatable-1) e di [IComparable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IComparable-1) su un semplice oggetto business. Quando l'oggetto viene memorizzato in un elenco e ordinato, la chiamata al metodo `Sort()` risulta nell'uso dell'operatore di confronto predefinito per il tipo "Part" e il metodo `Sort(Comparison<T>)` viene implementato tramite l'uso di un metodo anonimo.

C#

```csharp
using System;
using System.Collections.Generic;
// Simple business object. A PartId is used to identify the type of part 
// but the part name can change. 
public class Part : IEquatable<Part> , IComparable<Part>
{
    public string PartName { get; set; }

    public int PartId { get; set; }

    public override string ToString()
    {
        return "ID: " + PartId + "   Name: " + PartName;
    }
    public override bool Equals(object obj)
    {
        if (obj == null) return false;
        Part objAsPart = obj as Part;
        if (objAsPart == null) return false;
        else return Equals(objAsPart);
    }
    public int SortByNameAscending(string name1, string name2)
    {

        return name1.CompareTo(name2);
    }

    // Default comparer for Part type.
    public int CompareTo(Part comparePart)
    {
          // A null value means that this object is greater.
        if (comparePart == null)
            return 1;

        else
            return this.PartId.CompareTo(comparePart.PartId);
    }
    public override int GetHashCode()
    {
        return PartId;
    }
    public bool Equals(Part other)
    {
        if (other == null) return false;
        return (this.PartId.Equals(other.PartId));
    }
    // Should also override == and != operators.

}
public class Example
{
    public static void Main()
    {
        // Create a list of parts.
        List<Part> parts = new List<Part>();

        // Add parts to the list.
        parts.Add(new Part() { PartName = "regular seat", PartId = 1434 });
        parts.Add(new Part() { PartName= "crank arm", PartId = 1234 });
        parts.Add(new Part() { PartName = "shift lever", PartId = 1634 }); ;
        // Name intentionally left null.
        parts.Add(new Part() {  PartId = 1334 });
        parts.Add(new Part() { PartName = "banana seat", PartId = 1444 });
        parts.Add(new Part() { PartName = "cassette", PartId = 1534 });


        // Write out the parts in the list. This will call the overridden 
        // ToString method in the Part class.
        Console.WriteLine("\nBefore sort:");
        foreach (Part aPart in parts)
        {
            Console.WriteLine(aPart);
        }


        // Call Sort on the list. This will use the 
        // default comparer, which is the Compare method 
        // implemented on Part.
        parts.Sort();


        Console.WriteLine("\nAfter sort by part number:");
        foreach (Part aPart in parts)
        {
            Console.WriteLine(aPart);
        }

        // This shows calling the Sort(Comparison(T) overload using 
        // an anonymous method for the Comparison delegate. 
        // This method treats null as the lesser of two values.
        parts.Sort(delegate(Part x, Part y)
        {
            if (x.PartName == null && y.PartName == null) return 0;
            else if (x.PartName == null) return -1;
            else if (y.PartName == null) return 1;
            else return x.PartName.CompareTo(y.PartName);
        });

        Console.WriteLine("\nAfter sort by name:");
        foreach (Part aPart in parts)
        {
            Console.WriteLine(aPart);
        }

        /*

            Before sort:
        ID: 1434   Name: regular seat
        ID: 1234   Name: crank arm
        ID: 1634   Name: shift lever
        ID: 1334   Name:
        ID: 1444   Name: banana seat
        ID: 1534   Name: cassette

        After sort by part number:
        ID: 1234   Name: crank arm
        ID: 1334   Name:
        ID: 1434   Name: regular seat
        ID: 1444   Name: banana seat
        ID: 1534   Name: cassette
        ID: 1634   Name: shift lever

        After sort by name:
        ID: 1334   Name:
        ID: 1444   Name: banana seat
        ID: 1534   Name: cassette
        ID: 1234   Name: crank arm
        ID: 1434   Name: regular seat
        ID: 1634   Name: shift lever

         */

    }
}
```

## <a name="see-also"></a>Vedere anche

[IComparer](https://docs.microsoft.com/dotnet/core/api/System.Collections.IComparer)

[IEquatable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IEquatable-1)

[IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1)

[IComparable](https://docs.microsoft.com/dotnet/core/api/System.IComparable)

[IComparable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.IComparable-1)



<!--HONumber=Nov16_HO3-->


