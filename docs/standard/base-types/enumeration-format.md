---
title: Stringhe di formato di enumerazione
description: Stringhe di formato di enumerazione
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 4d581898-99bc-42c3-816c-d8238f45096f
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 804884f75eb30764c0b8aaf2c8cd115029811157
ms.lasthandoff: 03/02/2017

---

# <a name="enumeration-format-strings"></a>Stringhe di formato di enumerazione

È possibile usare il metodo [Enum.ToString](xref:System.Enum.ToString) per creare un nuovo oggetto stringa che rappresenti il valore numerico, esadecimale o stringa di un membro di enumerazione. Questo metodo accetta una delle stringhe di formattazione di enumerazione per specificare il valore che si vuole venga restituito.

Nella tabella che segue sono elencate le stringhe di formattazione di enumerazione e i valori da esse restituiti. In questi identificatori di formato non viene fatta distinzione tra maiuscole e minuscole.

## <a name="the-g-or-g-format-strings"></a>Stringhe di formato G o g

Le stringhe di formato G o g visualizzano la voce di enumerazione come valore di stringa, se possibile. In caso contrario, visualizzano il valore intero dell'istanza corrente. Se l'enumerazione viene definita con l'attributo `Flags` impostato, i valori di stringa di ciascuna voce valida saranno concatenati tra loro, separati da virgole. Se l'attributo `Flags` non è impostato, un valore non valido verrà visualizzato sotto forma di voce numerica. L'esempio seguente illustra l'identificatore di formato G.

```csharp
Console.WriteLine(ConsoleColor.Red.ToString("G"));         // Displays Red
FileAttributes attributes = FileAttributes.Hidden |
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("G"));   // Displays Hidden, Archive
```

```vb
Console.WriteLine(ConsoleColor.Red.ToString("G"))           ' Displays Red
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("G"))     ' Displays Hidden, Archive
```

## <a name="the-f-or-f-format-strings"></a>Stringhe di formato F o f

Le stringhe di formato F o f visualizzano la voce di enumerazione come valore di stringa, se possibile. Se è possibile visualizzare interamente il valore come una sommatoria delle voci dell'enumerazione (anche se l'attributo `Flags` non è presente), i valori di stringa di ciascuna voce valida verranno concatenati tra loro, separati da virgole. Se non è possibile determinare completamente il valore sulla base delle voci di enumerazione, il valore verrà formattato sotto forma di valore intero. L'esempio seguente illustra l'identificatore di formato F.

```csharp
Console.WriteLine(ConsoleColor.Blue.ToString("F"));       // Displays Blue
FileAttributes attributes = FileAttributes.Hidden | 
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("F"));   // Displays Hidden, Archive
```

```vb
Console.WriteLine(ConsoleColor.Blue.ToString("F"))         ' Displays Blue
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("F"))     ' Displays Hidden, Archive
```

## <a name="the-d-or-d-format-strings"></a>Stringhe di formato D o d

Le stringhe di formato D o d visualizzano la voce di enumerazione come valore intero nella rappresentazione più breve possibile. L'esempio seguente illustra l'identificatore di formato D.

```csharp
Console.WriteLine(ConsoleColor.Cyan.ToString("D"));         // Displays 11
FileAttributes attributes = FileAttributes.Hidden |
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("D"));                // Displays 34
````

```vb
Console.WriteLine(ConsoleColor.Cyan.ToString("D"))           ' Displays 11
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("D"))                  ' Displays 34 
```

## <a name="the-x-or-x-format-strings"></a>Stringhe di formato X o x

Le stringhe di formato X o x visualizzano la voce di enumerazione come valore esadecimale. Il valore viene rappresentato con l'aggiunta di un numero di zeri iniziali sufficiente a raggiungere la lunghezza minima di otto cifre. L'esempio seguente illustra l'identificatore di formato X.

```csharp
Console.WriteLine(ConsoleColor.Cyan.ToString("X"));   // Displays 0000000B
FileAttributes attributes = FileAttributes.Hidden |
                            FileAttributes.Archive;
Console.WriteLine(attributes.ToString("X"));          // Displays 00000022
```

```vb
Console.WriteLine(ConsoleColor.Cyan.ToString("X"))     ' Displays 0000000B
Dim attributes As FileAttributes = FileAttributes.Hidden Or _
                                   FileAttributes.Archive
Console.WriteLine(attributes.ToString("X"))            ' Displays 00000022 
```

## <a name="example"></a>Esempio

L'esempio seguente definisce un'enumerazione denominata `Colors` costituita dalle tre voci `Red`, `Blue` e `Green`.

 ```csharp
 public enum Color {Red = 1, Blue = 2, Green = 3}
```

```vb
Public Enum Color
   Red = 1
   Blue = 2
   Green = 3
End Enum
```

Dopo aver definito l'enumerazione è possibile dichiararne un'istanza nel modo seguente.

```csharp
Color myColor = Color.Green;
```

```vb
Dim myColor As Color = Color.Green
```

Sarà quindi possibile usare il metodo `Color.ToString(System.String)` per visualizzare il valore di enumerazione in modi diversi, a seconda dell'identificatore di formato passato.

```csharp
Console.WriteLine("The value of myColor is {0}.", 
                  myColor.ToString("G"));
Console.WriteLine("The value of myColor is {0}.", 
                  myColor.ToString("F"));
Console.WriteLine("The value of myColor is {0}.", 
                  myColor.ToString("D"));
Console.WriteLine("The value of myColor is 0x{0}.", 
                  myColor.ToString("X"));
// The example displays the following output to the console:
//       The value of myColor is Green.
//       The value of myColor is Green.
//       The value of myColor is 3.
//       The value of myColor is 0x00000003.
```

```vb
Console.WriteLine("The value of myColor is {0}.", _
                  myColor.ToString("G"))
Console.WriteLine("The value of myColor is {0}.", _
                  myColor.ToString("F"))
Console.WriteLine("The value of myColor is {0}.", _
                  myColor.ToString("D"))
Console.WriteLine("The value of myColor is 0x{0}.", _
                  myColor.ToString("X"))
' The example displays the following output to the console:
'       The value of myColor is Green.
'       The value of myColor is Green.
'       The value of myColor is 3.
'       The value of myColor is 0x00000003. 
```

## <a name="see-also"></a>Vedere anche

[Formattazione di tipi](formatting-types.md)


