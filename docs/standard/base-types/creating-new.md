---
title: Creazione di nuove stringhe
description: Creazione di nuove stringhe
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 639397c7-e694-43e0-845b-1681c62bd9fd
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 793b5bc4b26967104459fa2559c6127bb82f3a9d
ms.lasthandoff: 03/02/2017

---

# <a name="creating-new-strings"></a>Creazione di nuove stringhe

.NET consente di creare stringhe tramite una semplice assegnazione, oltre a eseguire l'overload del costruttore di classe per supportare la creazione di stringhe tramite una serie di parametri diversi. Nella classe [System.String](xref:System.String) .NET Framework fornisce anche diversi metodi per creare nuovi oggetti stringa tramite la combinazione di più stringhe, matrici di stringhe o oggetti. 

## <a name="creating-strings-using-assignment"></a>Creazione di stringhe tramite assegnazione

Il modo più semplice per creare un nuovo oggetto [String](xref:System.String) consiste nell'assegnare un valore letterale stringa a un oggetto [String](xref:System.String). 

## <a name="creating-strings-using-a-class-constructor"></a>Creazione di stringhe tramite un costruttore di classe

È possibile usare overload del costruttore della classe [String](xref:System.String) per creare stringhe da matrici di caratteri. È anche possibile creare una nuova stringa duplicando un determinato carattere per un numero specifico di volte. 

## <a name="methods-that-return-strings"></a>Metodi che restituiscono stringhe

Nella tabella seguente sono elencati diversi metodi utili che restituiscono nuovi oggetti stringa.

Nome metodo | Uso
----------- | ---
[String.Format](xref:System.String.Format(System.String,System.Object)) | Compila una stringa formattata da un insieme di oggetti di input.
[String.Concat](xref:System.String.Concat(System.String,System.String)) | Compila stringhe da due o più stringhe.
[String.Join](xref:System.String.Join(System.String,System.String[])) |Compila una nuova stringa combinando una matrice di stringhe.
[String.Insert](xref:System.String.Insert(System.Int32,System.String)) | Compila una nuova stringa inserendo una stringa in corrispondenza dell'indice specificato di una stringa esistente.
[String.CopyTo](xref:System.String.CopyTo(System.Int32,System.Char[],System.Int32,System.Int32)) | Copia i caratteri specificati di una stringa in una determinata posizione all'interno di una matrice di caratteri.

### <a name="format"></a>Formato

È possibile usare il metodo `String.Format` per creare stringhe formattate e concatenare stringhe che rappresentano più oggetti. Qualsiasi oggetto venga passato a questo metodo viene automaticamente convertito in una stringa. Se, ad esempio, l'applicazione deve visualizzare un valore [Int32](xref:System.Int32) e un valore [DateTime](xref:System.DateTime), è possibile costruire con facilità una stringa che rappresenti tali valori usando il metodo `Format`. Per altre informazioni sulle convenzioni di formattazione usate con questo metodo, vedere la sezione relativa alla [formattazione composita](composite-format.md).

Nell'esempio di codice che segue il metodo `Format` viene usato per creare una stringa che usa una variabile integer.

```csharp
int numberOfFleas = 12;
string miscInfo = String.Format("Your dog has {0} fleas. " +
                                "It is time to get a flea collar. " + 
                                "The current universal date is: {1:u}.", 
                                numberOfFleas, DateTime.Now);
Console.WriteLine(miscInfo);
// The example displays the following output:
//       Your dog has 12 fleas. It is time to get a flea collar. 
//       The current universal date is: 2008-03-28 13:31:40Z.
```

```vb
Dim numberOfFleas As Integer = 12
Dim miscInfo As String = String.Format("Your dog has {0} fleas. " & _
                                       "It is time to get a flea collar. " & _ 
                                       "The current universal date is: {1:u}.", _ 
                                       numberOfFleas, Date.Now)
Console.WriteLine(miscInfo)
' The example displays the following output:
'       Your dog has 12 fleas. It is time to get a flea collar. 
'       The current universal date is: 2008-03-28 13:31:40Z.
```

In questo esempio [DateTime.Now](xref:System.DateTime.Now) visualizza l'ora e la data correnti nel modo specificato dalle impostazioni cultura associate al thread corrente.

### <a name="concat"></a>Concat

Il metodo `String.Concat` può essere usato per creare facilmente un nuovo oggetto stringa da due o più oggetti esistenti. Questo metodo rappresenta una modalità di concatenamento delle stringhe indipendente dal linguaggio. Il metodo accetta qualsiasi classe che derivi da `System.Object`. Nell'esempio di codice che segue viene creata una stringa da due oggetti stringa esistenti e da un carattere di separazione.

```csharp
string helloString1 = "Hello";
string helloString2 = "World!";
Console.WriteLine(String.Concat(helloString1, ' ', helloString2));
// The example displays the following output:
//      Hello World!
```

```vb
Dim helloString1 As String = "Hello"
Dim helloString2 As String = "World!"
Console.WriteLine(String.Concat(helloString1, " "c, helloString2))
' The example displays the following output:
'      Hello World!
```

### <a name="join"></a>Join

Il metodo `String.Join` consente di creare una nuova stringa da una matrice di stringhe e da una stringa di separazione. Questo metodo è utile per concatenare più stringhe, creando un elenco, eventualmente separato da virgole.

Nell'esempio di codice seguente viene usato uno spazio per eseguire l'associazione di una matrice di stringhe.

```csharp
string[] words = {"Hello", "and", "welcome", "to", "my" , "world!"};
Console.WriteLine(String.Join(" ", words));
// The example displays the following output:
//      Hello and welcome to my world!
```

```vb
Dim words() As String = {"Hello", "and", "welcome", "to", "my" , "world!"}
Console.WriteLine(String.Join(" ", words))
' The example displays the following output:
'      Hello and welcome to my world!
```

### <a name="insert"></a>INS

Il metodo `String.Insert` consente di creare una nuova stringa inserendo una stringa in una posizione specificata all'interno di un'altra stringa. Questo metodo usa un indice a base zero. Nell'esempio di codice che segue viene inserita una stringa in corrispondenza della quinta posizione di indice di `MyString` e viene creata una nuova stringa con tale valore.

```csharp
string sentence = "Once a time.";   
 Console.WriteLine(sentence.Insert(4, " upon"));
 // The example displays the following output:
 //      Once upon a time.
```

```vb
Dim sentence As String = "Once a time."   
 Console.WriteLine(sentence.Insert(4, " upon"))
 ' The example displays the 
```

### <a name="copyto"></a>CopyTo

Il metodo `String.CopyTo` consente di copiare parti di una stringa in una matrice di caratteri. È possibile specificare sia l'indice iniziale della stringa sia il numero dei caratteri da copiare. Il metodo contiene l'indice di origine, una matrice di caratteri, l'indice di destinazione e il numero dei caratteri da copiare. Tutti gli indici sono a base zero.

Nell'esempio di codice riportato di seguito il metodo `CopyTo` viene usato per copiare nella prima posizione di indice di una matrice di caratteri i caratteri della parola "Hello" di un oggetto stringa.

```csharp
string greeting = "Hello World!";
char[] charArray = {'W','h','e','r','e'};
Console.WriteLine("The original character array: {0}", new string(charArray));
greeting.CopyTo(0, charArray,0 ,5);
Console.WriteLine("The new character array: {0}", new string(charArray));
// The example displays the following output:
//       The original character array: Where
//       The new character array: Hello
```

```vb
Dim greeting As String = "Hello World!"
Dim charArray() As Char = {"W"c, "h"c, "e"c, "r"c, "e"c}
Console.WriteLine("The original character array: {0}", New String(charArray))
greeting.CopyTo(0, charArray,0 ,5)
Console.WriteLine("The new character array: {0}", New String(charArray))
' The example displays the following output:
'       The original character array: Where
'       The new character array: Hello
```

## <a name="see-also"></a>Vedere anche

[Operazioni di base su stringhe](basic-string-operations.md)

[Formattazione composita](composite-format.md)


