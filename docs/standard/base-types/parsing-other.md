---
title: Analisi di altre stringhe in .NET
description: Analisi di altre stringhe in .NET
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 67670b10-3df4-45ea-8908-5ba3f056887c
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: db80cc5f37e814f224ff76b14a906bb4d41064fb
ms.lasthandoff: 03/02/2017

---

# <a name="parsing-other-strings-in-net"></a>Analisi di altre stringhe in .NET

Oltre alle stringhe numeriche e [DateTime](xref:System.DateTime) è possibile analizzare le stringhe che rappresentano i tipi [Char](xref:System.Char), [Boolean](xref:System.Boolean) ed [Enum](xref:System.Enum) in tipi di dati.

## <a name="char"></a>Char

Il metodo di analisi statico associato al tipo di dati [Char](xref:System.Char) è utile per la conversione di una stringa contenente un solo carattere nel valore Unicode corrispondente. Nell'esempio seguente viene analizzata una stringa in un carattere Unicode.

```csharp
string MyString1 = "A";
char MyChar = Char.Parse(MyString1);
// MyChar now contains a Unicode "A" character.
```

```vb
Dim MyString1 As String = "A"
Dim MyChar As Char = Char.Parse(MyString1)
' MyChar now contains a Unicode "A" character.
```

## <a name="boolean"></a>Booleano

Il tipo di dati [Boolean](xref:System.Boolean) contiene un metodo [Parse](xref:System.Boolean.Parse(System.String)) che può essere usato per convertire una stringa che rappresenta un valore `Boolean` in un vero e proprio tipo `Boolean`. Questo metodo non fa distinzione tra maiuscole e minuscole e consente di analizzare correttamente una stringa contenente "True" o "False". Il metodo `Parse` associato al tipo `Boolean` consente anche di analizzare stringhe precedute e seguite da spazi vuoti. Se viene passata qualsiasi altra stringa, viene generata un'eccezione [FormatException](xref:System.FormatException).

Nell'esempio di codice seguente viene usato il metodo `Parse` per convertire una stringa in un valore `Boolean`.

```csharp
string MyString2 = "True";
bool MyBool = bool.Parse(MyString2);
// MyBool now contains a True Boolean value.
```

```vb
Dim MyString1 As String = "A"
Dim MyChar As Char = Char.Parse(MyString1)
' MyChar now contains a Unicode "A" character.
```

## <a name="enumeration"></a>Enumerazione

È possibile usare il metodo statico [Parse](xref:System.Enum.Parse(System.Type,System.String)) per inizializzare un tipo di enumerazione per il valore di una stringa. Questo metodo accetta il tipo di enumerazione che si sta analizzando, la stringa da analizzare un flag `Boolean` facoltativo che indica se l'analisi fa distinzione tra maiuscole e minuscole. La stringa da analizzare può contenere diversi valori separati da virgole, che possono essere preceduti o seguiti da uno o più spazi vuoti. Quando la stringa contiene più valori, il valore dell'oggetto restituito è il valore di tutti i valori specificati combinati con un'operazione OR bit per bit.

Nell'esempio seguente viene usato il metodo `Parse` per convertire una rappresentazione di stringa in un valore di enumerazione. L'enumerazione [DayOfWeek](xref:System.DayOfWeek) viene inizializzata su Thursday da una stringa.

```csharp
string MyString3 = "Thursday";
DayOfWeek MyDays = (DayOfWeek)Enum.Parse(typeof(DayOfWeek), MyString3);
Console.WriteLine(MyDays);
// The result is Thursday.
```

```vb
Dim MyString3 As String = "Thursday"
Dim MyDays As DayOfWeek = CType([Enum].Parse(GetType(DayOfWeek), MyString3), DayOfWeek)
Console.WriteLine("{0:G}", MyDays)
' The result is Thursday.
```

## <a name="see-also"></a>Vedere anche

[Analisi di stringhe in .NET](parsing-strings.md)

[Formattazione di tipi in .NET](formatting-types.md)

[Conversione di tipi in .NET](type-conversion.md)


