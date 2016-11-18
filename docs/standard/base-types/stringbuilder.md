---
title: Uso della classe StringBuilder
description: Uso della classe StringBuilder
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: f4f5d1c7-d84d-4867-810f-2708cd6de0da
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 2c42a4ac5fcd889eedea27b54b249f48c4848c88

---

# <a name="using-the-stringbuilder-class"></a>Uso della classe StringBuilder

L'oggetto [String](xref:System.String) non è modificabile. Ogni volta che si usa uno dei metodi nella classe [System.String](xref:System.String), si crea un nuovo oggetto stringa in memoria che richiede una nuova allocazione di spazio. In situazioni in cui è necessario modificare ripetutamente una stringa, il sovraccarico associato alla creazione di un nuovo oggetto [String](xref:System.String) può essere dispendioso. La classe [System.Text.StringBuilder](xref:System.Text.StringBuilder) può essere usata per modificare una stringa senza creare un nuovo oggetto. Ad esempio, l'uso della classe [StringBuilder](xref:System.Text.StringBuilder) può migliorare le prestazioni quando si concatenano più stringhe in un ciclo.

## <a name="importing-the-systemtext-namespace"></a>Importazione dello spazio dei nomi System.Type

La classe [StringBuilder](xref:System.Text.StringBuilder) si trova nello spazio dei nomi [System.Text](xref:System.Text). Per evitare di specificare il nome di tipo completo nel codice, è possibile importare lo spazio dei nomi [System.Text](xref:System.Text): 

```csharp
using System;
using System.Text;
```

```vb
Imports System.Text
```

## <a name="instantiating-a-stringbuilder-object"></a>Creazione di un'istanza di un oggetto StringBuilder

È possibile creare una nuova istanza della classe [StringBuilder](xref:System.Text.StringBuilder) inizializzando la variabile con uno dei metodi del costruttore di overload, come illustrato nell'esempio seguente.

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
```

## <a name="setting-the-capacity-and-length"></a>Impostazione di capacità e lunghezza

Anche se [StringBuilder](xref:System.Text.StringBuilder) è un oggetto dinamico che consente di espandere il numero di caratteri nella stringa incapsulata, è possibile specificare un valore per il numero massimo di caratteri che può contenere. Questo valore rappresenta la capacità dell'oggetto e non deve essere confuso con la lunghezza della stringa contenuta dall'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente. Ad esempio, è possibile creare una nuova istanza della classe [StringBuilder](xref:System.Text.StringBuilder) con la stringa "Hello", che ha una lunghezza pari a 5 caratteri, e specificare che l'oggetto ha una capacità massima di 25 caratteri. Quando si modifica la classe [StringBuilder](xref:System.Text.StringBuilder), le dimensioni non vengono riallocate automaticamente fino a quando non viene raggiunta la capacità specificata. In questo caso, il nuovo spazio viene allocato automaticamente e la capacità viene raddoppiata. È possibile specificare la capacità della classe [StringBuilder](xref:System.Text.StringBuilder) usando uno dei costruttori di overload. L'esempio seguente specifica che l'oggetto `MyStringBuilder` può essere espanso fino a un massimo di 25 spazi.

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!", 25);
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!", 25) 
```

È anche possibile usare la proprietà [Capacity](xref:System.Text.StringBuilder.Capacity) di lettura/scrittura per impostare la lunghezza massima dell'oggetto. L'esempio seguente usa la proprietà [Capacity](xref:System.Text.StringBuilder.Capacity) per definire la lunghezza massima dell'oggetto.

```csharp
MyStringBuilder.Capacity = 25;
```

```vb
MyStringBuilder.Capacity = 25
```

Il metodo [EnsureCapacity](xref:System.Text.StringBuilder.EnsureCapacity(System.Int32)) può essere usato per verificare la capacità dell'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente. Se la capacità è maggiore del valore passato, non vengono apportate modifiche. Invece, se la capacità è minore del valore passato, la capacità corrente viene modificata in modo che corrisponda al valore passato.

La proprietà [Length](xref:System.Text.StringBuilder.Length) può essere anche visualizzata o impostata. Se si imposta la proprietà [Length](xref:System.Text.StringBuilder.Length) su un valore maggiore della proprietà [Capacity](xref:System.Text.StringBuilder.Capacity), la proprietà [Capacity](xref:System.Text.StringBuilder.Capacity) viene impostata automaticamente sullo stesso valore della proprietà [Length](xref:System.Text.StringBuilder.Length). L'impostazione della proprietà [Length](xref:System.Text.StringBuilder.Length) su un valore minore della lunghezza della stringa all'interno dell'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente consente di abbreviare la stringa.

## <a name="modifying-the-stringbuilder-string"></a>Modifica della stringa StringBuilder

La tabella seguente elenca i metodi che è possibile usare per modificare il contenuto di [StringBuilder](xref:System.Text.StringBuilder).

Nome metodo | Uso
----------- | ---
[StringBuilder.Append](xref:System.Text.StringBuilder.Append(System.Char)) | Aggiunge informazioni alla fine dell'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente.
[StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) | Sostituisce un identificatore di formato passato in una stringa con il testo formattato.
[StringBuilder.Insert](xref:System.Text.StringBuilder.Insert(System.Int32,System.Char)) | Inserisce una stringa o un oggetto nell'indice specificato dell'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente.
[StringBuilder.Remove](xref:System.Text.StringBuilder.Remove(System.Int32,System.Int32)) | Rimuove un numero specificato di caratteri dall'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente.
[StringBuilder.Replace](xref:System.Text.StringBuilder.Replace(System.Char,System.Char)) | Sostituisce un determinato carattere nell'indice specificato.

### <a name="append"></a>Aggiungi

Il metodo [StringBuilder.Append](xref:System.Text.StringBuilder.Append(System.Char)) può essere usato per aggiungere testo o una rappresentazione di stringa di un oggetto alla fine di una stringa rappresentata dall'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente. Nell'esempio seguente viene inizializzato un oggetto [StringBuilder](xref:System.Text.StringBuilder) su "Hello World" e quindi viene aggiunto il testo alla fine dell'oggetto. Lo spazio viene allocato automaticamente in base alle esigenze.

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Append(" What a beautiful day.");
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello World! What a beautiful day.
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Append(" What a beautiful day.")
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'       Hello World! What a beautiful day.
```

### <a name="appendformat"></a>AppendFormat

Il metodo [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) aggiunge del testo alla fine dell'oggetto [StringBuilder](xref:System.Text.StringBuilder). Supporta la funzionalità di formattazione composita (per altre informazioni, vedere [Formattazione composita](composite-format.md)) chiamando l'implementazione [IFormattable](xref:System.IFormattable) dell'oggetto o gli oggetti da formattare. Pertanto, accetta le stringhe di formato standard per i valori numerici, di data e ora e di enumerazione, le stringhe di formato personalizzato per i valori numerici e di data e ora e le stringhe di formato definite per i tipi personalizzati. Per informazioni sulla formattazione, vedere [Formattazione di tipi](formatting-types.md)). È possibile usare questo metodo per personalizzare il formato delle variabili e aggiungere tali valori a un oggetto [StringBuilder](xref:System.Text.StringBuilder). L'esempio seguente usa il metodo AppendFormat per inserire un valore intero formattato come valore di valuta alla fine di un oggetto [StringBuilder](xref:System.Text.StringBuilder).

```csharp
int MyInt = 25; 
StringBuilder MyStringBuilder = new StringBuilder("Your total is ");
MyStringBuilder.AppendFormat("{0:C} ", MyInt);
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Your total is $25.00
```

```vb
Dim MyInt As Integer = 25
Dim MyStringBuilder As New StringBuilder("Your total is ")
MyStringBuilder.AppendFormat("{0:C} ", MyInt)
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'     Your total is $25.00 
```

### <a name="insert"></a>INS

Il metodo [StringBuilder.Insert](xref:System.Text.StringBuilder.Insert(System.Int32,System.Char)) aggiunge una stringa o un oggetto in una posizione specificata nell'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente. L'esempio seguente usa questo metodo per inserire una parola nella sesta posizione di un oggetto [StringBuilder](xref:System.Text.StringBuilder).

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Insert(6,"Beautiful ");
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello Beautiful World!
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Insert(6, "Beautiful ")
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'      Hello Beautiful World!
```

### <a name="remove"></a>Rimuovi

È possibile usare il metodo [StringBuilder.Remove](xref:System.Text.StringBuilder.Remove(System.Int32,System.Int32)) per rimuovere un numero specificato di caratteri dall'oggetto [StringBuilder](xref:System.Text.StringBuilder) corrente, a partire dall'indice in base zero specificato. L'esempio seguente usa il metodo [Remove](xref:System.Text.StringBuilder.Remove(System.Int32,System.Int32)) per abbreviare un oggetto [StringBuilder](xref:System.Text.StringBuilder).

```csharp
StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Remove(5,7);
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Remove(5, 7)
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'       Hello
```

### <a name="replace"></a>Sostituisci

Il metodo [StringBuilder.Replace](xref:System.Text.StringBuilder.Replace(System.Char,System.Char)) |Sostituisce un determinato carattere nell'indice specificato.
può essere usato per sostituire i caratteri all'interno dell'oggetto [StringBuilder](xref:System.Text.StringBuilder) con un altro carattere specificato. Nell'esempio seguente viene usato il metodo [Replace](xref:System.Text.StringBuilder.Replace(System.Char,System.Char)) |Sostituisce un determinato carattere nell'indice specificato.
per cercare un oggetto [StringBuilder](xref:System.Text.StringBuilder) per tutte le istanze del carattere punto esclamativo (!) e sostituirle con il carattere punto interrogativo (?).
 
 ```csharp
 StringBuilder MyStringBuilder = new StringBuilder("Hello World!");
MyStringBuilder.Replace('!', '?');
Console.WriteLine(MyStringBuilder);
// The example displays the following output:
//       Hello World?
```

```vb
Dim MyStringBuilder As New StringBuilder("Hello World!")
MyStringBuilder.Replace("!"c, "?"c)
Console.WriteLine(MyStringBuilder)
' The example displays the following output:
'       Hello World?
```

## <a name="converting-a-stringbuilder-object-to-a-string"></a>Conversione di un oggetto StringBuilder in una stringa

È necessario convertire l'oggetto [StringBuilder](xref:System.Text.StringBuilder) in un oggetto [String](xref:System.String) prima di poter passare la stringa rappresentata dall'oggetto [StringBuilder](xref:System.Text.StringBuilder) a un metodo che contiene un parametro [String](xref:System.String) o per visualizzarlo nell'interfaccia utente. Eseguire questa conversione chiamando il metodo [StringBuilder.ToString](xref:System.Text.StringBuilder.ToString). Nell'esempio seguente vengono chiamati diversi metodi [StringBuilder](xref:System.Text.StringBuilder) e quindi viene chiamato il metodo [StringBuilder.ToString](xref:System.Text.StringBuilder.ToString) per visualizzare la stringa.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      StringBuilder sb = new StringBuilder();
      bool flag = true;
      string[] spellings = { "recieve", "receeve", "receive" };
      sb.AppendFormat("Which of the following spellings is {0}:", flag);
      sb.AppendLine();
      for (int ctr = 0; ctr <= spellings.GetUpperBound(0); ctr++) {
         sb.AppendFormat("   {0}. {1}", ctr, spellings[ctr]);
         sb.AppendLine();
      }
      sb.AppendLine();
      Console.WriteLine(sb.ToString());
   }
}
// The example displays the following output:
//       Which of the following spellings is True:
//          0. recieve
//          1. receeve
//          2. receive
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim sb As New StringBuilder()
      Dim flag As Boolean = True
      Dim spellings() As String = { "recieve", "receeve", "receive" }
      sb.AppendFormat("Which of the following spellings is {0}:", flag)
      sb.AppendLine()
      For ctr As Integer = 0 To spellings.GetUpperBound(0)
         sb.AppendFormat("   {0}. {1}", ctr, spellings(ctr))
         sb.AppendLine()
      Next
      sb.AppendLine()
      Console.WriteLine(sb.ToString())
   End Sub
End Module
' The example displays the following output:
'       Which of the following spellings is True:
'          0. recieve
'          1. receeve
'          2. receive
```

## <a name="see-also"></a>Vedere anche

[System.Text.StringBuilder](xref:System.Text.StringBuilder)

[Operazioni di base su stringhe](basic-string-operations.md)

[Formattazione di tipi](formatting-types.md)



<!--HONumber=Nov16_HO3-->


