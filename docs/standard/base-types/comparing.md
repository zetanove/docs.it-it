---
title: Confronto di stringhe
description: Confronto di stringhe
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 920ee5e8-3d61-4941-b5af-fc50eaee427c
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 2ad585bd5475cf39aeae5dadc9ce3864c501a205

---

# <a name="comparing-strings"></a>Confronto di stringhe

.NET offre diversi metodi per confrontare i valori delle stringhe. La tabella seguente elenca e descrive i metodi di confronto di valori.

Nome metodo | Uso
----------- | ---
[String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) | Confronta i valori di due stringhe. Restituisce un valore intero.
[String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) | Confronta due stringhe senza tenere in considerazione le impostazioni cultura locali. Restituisce un valore intero.
[String.CompareTo](xref:System.String.CompareTo(System.String)) | Confronta l'oggetto stringa corrente con un'altra stringa. Restituisce un valore intero.
[String.StartsWith](xref:System.String.StartsWith(System.String)) | Determina se una stringa inizia con la stringa passata. Restituisce un valore booleano.
[String.EndsWith](xref:System.String.CompareTo(System.String)) | Determina se una stringa finisce con la stringa passata. Restituisce un valore booleano.
[String.Equals](xref:System.String.CompareTo(System.String)) | Determina se due stringhe sono uguali. Restituisce un valore booleano.
[String.IndexOf](xref:System.String.IndexOf(System.Char)) | Restituisce la posizione di indice di un carattere o una stringa, a partire dall'inizio della stringa esaminata. Restituisce un valore intero.
[String.LastIndexOf](xref:System.String.LastIndexOf(System.Char)) | Restituisce la posizione di indice di un carattere o una stringa, a partire dalla fine della stringa esaminata. Restituisce un valore intero.

## <a name="compare"></a>Compare

Il metodo statico [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) consente di confrontare due stringhe in modo accurato. Questo metodo fa distinzione tra le impostazioni cultura. È possibile usare questa funzione per confrontare due stringhe o le sottostringhe di due stringhe. Sono inoltre disponibili overload che consentono o meno di fare distinzione tra maiuscole e minuscole e di tenere o meno in considerazione le differenze nelle impostazioni cultura. La tabella seguente illustra i tre valori interi che questo metodo può restituire. 

Valore restituito | Condizione
------------ | ---------
Intero negativo | La prima stringa precede la seconda stringa nella sequenza di ordinamento, oppure la prima stringa è `null`.
0 | La prima stringa e la seconda stringa sono uguali, oppure sono entrambe `null`.
Un intero positivo, o 1 | La prima stringa segue la seconda stringa nella sequenza di ordinamento, oppure la seconda stringa è Null.
 
> [!IMPORTANT]
> Il metodo [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) è destinato principalmente a essere usato quando si ordinano le stringhe. Non usare il metodo [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) per verificare l'uguaglianza, ovvero, per cercare in modo esplicito un valore restituito pari a 0 senza considerare se una stringa è minore o maggiore dell'altra. Per determinare se due stringhe sono uguali, usare invece il metodo [String.Equals(String, String, StringComparison)](xref:System.String.Equals(System.String,System.String,System.StringComparison)).

L'esempio seguente usa il metodo [String.Compare](xref:System.String.Compare(System.String,System.Int32,System.String,System.Int32,System.Int32)) per determinare i valori relativi di due stringhe.

```csharp
string string1 = "Hello World!";
Console.WriteLine(String.Compare(string1, "Hello World?"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(String.Compare(string1, "Hello World?"))
```

L'esempio visualizza `-1` nella console.

## <a name="compareordinal"></a>CompareOrdinal

Il metodo [String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) confronta due oggetti stringa senza considerare le impostazioni cultura locali. I valori restituiti da questo metodo sono identici a quelli restituiti dal metodo `Compare` nella tabella precedente.

> [!IMPORTANT]
> Il metodo [String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) è destinato principalmente a essere usato quando si ordinano le stringhe. Non usare il metodo [String.CompareOrdinal](xref:System.String.CompareOrdinal(System.String,System.Int32,System.String,System.Int32,System.Int32)) per verificare l'uguaglianza, ovvero per cercare in modo esplicito un valore restituito pari a 0 senza considerare se una stringa è minore o maggiore dell'altra. Per determinare se due stringhe sono uguali, usare invece il metodo [String.Equals(String, String, StringComparison)](xref:System.String.Equals(System.String,System.String,System.StringComparison)).

L'esempio seguente usa il metodo `CompareOrdinal` per confrontare i valori di due stringhe.

```csharp
string string1 = "Hello World!";
Console.WriteLine(String.CompareOrdinal(string1, "hello world!"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(String.CompareOrdinal(string1, "hello world!"))
```

L'esempio visualizza `-32` nella console.

## <a name="compareto"></a>CompareTo

Il metodo [String.CompareTo](xref:System.String.CompareTo(System.String)) confronta la stringa incapsulata dall'oggetto stringa corrente con un altro oggetto o stringa. I valori restituiti da questo metodo sono identici a quelli restituiti dal metodo `String.Compare` nella tabella precedente.

> [!IMPORTANT]
> Il metodo [String.CompareTo](xref:System.String.CompareTo(System.String)) è destinato principalmente a essere usato quando si ordinano le stringhe. Non usare il metodo [String.CompareTo](xref:System.String.CompareTo(System.String)) per verificare l'uguaglianza, ovvero per cercare in modo esplicito un valore restituito pari a 0 senza considerare se una stringa è minore o maggiore dell'altra. Per determinare se due stringhe sono uguali, usare invece il metodo [String.Equals(String, String, StringComparison)](xref:System.String.Equals(System.String,System.String,System.StringComparison)).

L'esempio seguente usa il metodo `String.CompareTo` per confrontare l'oggetto `string1` con l'oggetto `string2`.

```csharp
string string1 = "Hello World";
string string2 = "Hello World!";
int MyInt = string1.CompareTo(string2);
Console.WriteLine( MyInt );
```

```vb
Dim string1 As String = "Hello World"
Dim string2 As String = "Hello World!"
Dim MyInt As Integer = string1.CompareTo(string2)
Console.WriteLine(MyInt)
```

L'esempio visualizza `-1` nella console.

## <a name="equals"></a>Equals

Il metodo [String.Equals](xref:System.String.CompareTo(System.String)) consente di determinare in modo semplice se due stringhe sono uguali. Questo metodo, che fa distinzione tra maiuscole e minuscole, restituisce un valore booleano `true` o `false`. Può essere usato da una classe esistente, come illustrato nell'esempio seguente. L'esempio seguente usa il metodo `Equals` per determinare se un oggetto stringa contiene la frase "Hello World".

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.Equals("Hello World"));
```

```vb
Dim string1 As String = "Hello World"
Console.WriteLine(string1.Equals("Hello World"))
```

L'esempio visualizza `true` nella console.

Questo metodo può anche essere usato come metodo statico. L'esempio seguente confronta due oggetti stringa tramite un metodo statico.

```csharp
string string1 = "Hello World";
string string2 = "Hello World";
Console.WriteLine(String.Equals(string1, string2));
```

```vb
Dim string1 As String = "Hello World"
Dim string2 As String = "Hello World"
Console.WriteLine(String.Equals(string1, string2))
```

L'esempio visualizza `true` nella console.

## <a name="startswith-and-endswith"></a>StartsWith ed EndsWith

È possibile usare il metodo [String.StartsWith](xref:System.String.StartsWith(System.String)) per determinare se un oggetto stringa inizia con gli stessi caratteri inclusi in un'altra stringa. Questo metodo, che fa distinzione tra maiuscole e minuscole, restituisce `true` se l'oggetto stringa corrente inizia con la stringa passata e `false` in caso contrario. L'esempio seguente usa questo metodo per determinare se un oggetto stringa inizia con "Hello".

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.StartsWith("Hello"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.StartsWith("Hello"))
```

L'esempio visualizza `true` nella console.

Il metodo [String.EndsWith](xref:System.String.CompareTo(System.String)) confronta una stringa passata con i caratteri presenti alla fine dell'oggetto stringa corrente. Anch'esso restituisce un valore booleano. L'esempio seguente verifica la fine di una stringa usando il metodo `EndsWith`.

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.EndsWith("Hello"));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.EndsWith("Hello"))
```

L'esempio visualizza `false` nella console.

## <a name="indexof-and-lastindexof"></a>IndexOf e LastIndexOf

È possibile usare il metodo [String.IndexOf](xref:System.String.IndexOf(System.Char)) per determinare la posizione della prima occorrenza di un carattere specifico all'interno di una stringa. Questo metodo, che fa distinzione tra maiuscole e minuscole, inizia il conteggio dall'inizio di una stringa e restituisce la posizione di un carattere passato usando un indice in base zero. Se il carattere non viene trovato, viene restituito un valore -1.

L'esempio seguente usa il metodo `IndexOf` per cercare la prima occorrenza del carattere "`l`" in una stringa.

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.IndexOf('l'));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.IndexOf("l"))
```

L'esempio visualizza `2` nella console.

Il metodo [String.LastIndexOf](xref:System.String.LastIndexOf(System.Char)) è simile al metodo `String.IndexOf`, con la differenza che restituisce la posizione dell'ultima occorrenza di un carattere specifico all'interno di una stringa. Anch'esso fa distinzione tra maiuscole e minuscole e usa un indice in base zero. 

L'esempio seguente usa il metodo `LastIndexOf` per cercare l'ultima occorrenza del carattere "`l`" in una stringa.

```csharp
string string1 = "Hello World";
Console.WriteLine(string1.LastIndexOf('l'));
```

```vb
Dim string1 As String = "Hello World!"
Console.WriteLine(string1.LastIndexOf("l"))
```

L'esempio visualizza `9` nella console.

Entrambi i metodi sono utili quando vengono usati in combinazione con il metodo [String.Remove](xref:System.String.Remove(System.Int32)). È possibile usare il metodo `IndexOf` o `LastIndexOf` per recuperare la posizione di un carattere e quindi specificare tale posizione nel metodo `Remove method` per rimuovere un carattere o una parola che inizia con tale carattere.

## <a name="see-also"></a>Vedere anche

[Operazioni di base su stringhe](basic-string-operations.md)















<!--HONumber=Nov16_HO3-->


