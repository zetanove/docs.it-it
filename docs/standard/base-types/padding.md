---
title: Aggiunta di spaziatura interna alle stringhe
description: Aggiunta di spaziatura interna alle stringhe
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 1c8b3b44-d370-49e1-90b5-64ac81c02ae91c8b3b44-d370-49e1-90b5-64ac81c02ae9
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: bc3cc9028b232cc2ba6ca3130c4bdb261c4a0a42
ms.lasthandoff: 03/02/2017

---

# <a name="padding-strings"></a>Aggiunta di spaziatura interna alle stringhe

Usare uno dei metodi [System.String](xref:System.String) riportati di seguito per creare una nuova stringa costituita da una stringa originale a cui vengono aggiunti caratteri iniziali o finali fino a una lunghezza totale specificata. Il carattere di riempimento può essere costituito da spazi o da un carattere specificato e di conseguenza viene visualizzato allineato a destra o sinistra.

Nome metodo | Uso
----------- | ---
[String.PadLeft](xref:System.String.PadLeft(System.Int32)) | Aggiunge caratteri iniziali a una stringa fino a ottenere una lunghezza totale specificata.
[String.PadRight](xref:System.String.PadRight(System.Int32)) | Aggiunge caratteri finali a una stringa fino a ottenere una lunghezza totale specificata.

## <a name="padleft"></a>PadLeft

Il metodo [String.PadLeft](xref:System.String.PadLeft(System.Int32)) crea una nuova stringa concatenando un numero sufficiente di caratteri di riempimento iniziali a una stringa originale per ottenere una lunghezza totale specificata. Il metodo [String.PadLeft(Int32)](xref:System.String.PadLeft(System.Int32)) usa spazi vuoti come carattere di riempimento e il metodo [String.PadLeft(Int32, Char)](xref:System.String.PadLeft(System.Int32,System.Char)) consente di specificare il proprio carattere di riempimento.

Nell'esempio di codice seguente viene usato il metodo [PadLeft(Int32, Char)](xref:System.String.PadLeft(System.Int32,System.Char)) per creare una nuova stringa di venti caratteri. L'esempio visualizza "`--------Hello World!`" nella console.

```csharp
string MyString = "Hello World!";
Console.WriteLine(MyString.PadLeft(20, '-'));
```

```vb
Dim MyString As String = "Hello World!"
Console.WriteLine(MyString.PadLeft(20, "-"c))
```

## <a name="padright"></a>PadRight

Il metodo [String.PadRight](xref:System.String.PadRight(System.Int32)) crea una nuova stringa concatenando un numero sufficiente di caratteri di riempimento finali a una stringa originale per ottenere una lunghezza totale specificata. Il metodo [String.PadRight(Int32)](xref:System.String.PadRight(System.Int32)) usa spazi vuoti come carattere di riempimento e il metodo [String.PadRight(Int32, Char)](xref:System.String.PadRight(System.Int32,System.Char)) consente di specificare il proprio carattere di riempimento.

Nell'esempio di codice seguente viene usato il metodo [PadRight(Int32, Char)](xref:System.String.PadRight(System.Int32,System.Char)) per creare una nuova stringa di venti caratteri. L'esempio visualizza "`Hello World!--------`" nella console.

```csharp
string MyString = "Hello World!";
Console.WriteLine(MyString.PadRight(20, '-'));
```

```vb
Dim MyString As String = "Hello World!"
Console.WriteLine(MyString.PadRight(20, "-"c))
```

## <a name="see-also"></a>Vedere anche

[Operazioni di base su stringhe](basic-string-operations.md)


