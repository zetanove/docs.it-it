---
title: Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe
description: Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 95d818bc-2661-43f6-adb8-13b53abf9682
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 6105861882c3bfd525a2d902fd2600f5da10417d

---

# <a name="trimming-and-removing-characters-from-strings"></a>Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe

Se si sta analizzando una frase in singole parole, è possibile che si ottengano parole con spazi vuoti alle estremità. In questo caso è possibile usare uno dei metodi trim della classe [System.String](https://docs.microsoft.com/dotnet/core/api/System.String) per rimuovere un numero qualsiasi di spazi o altri caratteri da una posizione specificata nella stringa. La tabella seguente illustra i metodi trim disponibili.

Nome metodo | Uso
----------- | ---
[String.Trim](https://docs.microsoft.com/dotnet/core/api/System.String.Trim) | Rimuove gli spazi vuoti o i caratteri specificati in una matrice di caratteri all'inizio e alla fine di una stringa.
[String.TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) | Rimuove i caratteri specificati in una matrice di caratteri alla fine di una stringa.
[String.TrimStart](https://docs.microsoft.com/dotnet/core/api/System.String.TrimStart(System.Char[])) | Rimuove i caratteri specificati in una matrice di caratteri all'inizio di una stringa.
[String.Remove](https://docs.microsoft.com/dotnet/core/api/System.String.Remove(System.Int32)) | Rimuove un numero specificato di caratteri da una posizione di indice specificata in una stringa.


## <a name="trim"></a>Trim

È possibile rimuovere facilmente gli spazi vuoti da entrambe le estremità di una stringa usando il metodo [String.Trim](https://docs.microsoft.com/dotnet/core/api/System.String.Trim), come visualizzato nell'esempio seguente.

```csharp
string MyString = " Big   ";
Console.WriteLine("Hello{0}World!", MyString);
string TrimString = MyString.Trim();
Console.WriteLine("Hello{0}World!", TrimString);
//       The example displays the following output:
//             Hello Big   World!
//             HelloBigWorld!
```

```vb
Dim MyString As String = " Big   "
Console.WriteLine("Hello{0}World!", MyString)
Dim TrimString As String = MyString.Trim()
Console.WriteLine("Hello{0}World!", TrimString)
' The example displays the following output:
'       Hello Big   World!
'       HelloBigWorld!
```

È anche possibile rimuovere i caratteri specificati in una matrice di caratteri all'inizio e alla fine di una stringa. Nell'esempio seguente vengono rimossi gli spazi vuoti, i punti e gli asterischi.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      String header = "* A Short String. *";
      Console.WriteLine(header);
      Console.WriteLine(header.Trim( new Char[] { ' ', '*', '.' } ));
   }
}
// The example displays the following output:
//       * A Short String. *
//       A Short String
```

```vb
Module Example
   Public Sub Main()
      Dim header As String = "* A Short String. *"
      Console.WriteLine(header)
      Console.WriteLine(header.Trim( { " "c, "*"c, "."c } ))
   End Sub
End Module
' The example displays the following output:
'       * A Short String. *
'       A Short String
```

## <a name="trimend"></a>TrimEnd

Il metodo [TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) rimuove caratteri alla fine di una stringa, creando un nuovo oggetto stringa. Una matrice di caratteri viene passata a questo metodo per specificare i caratteri da rimuovere. L'ordine degli elementi nella matrice di caratteri non influenza l'operazione di rimozione. La rimozione si interrompe quando viene trovato un carattere non specificato nella matrice.

L'esempio seguente rimuove le ultime lettere di una stringa con il metodo TrimEnd. In questo esempio la posizione dei caratteri `'r'` e `'W'` viene invertita per indicare che l'ordine dei caratteri nella matrice non è importante. Si noti che questo codice rimuove l'ultima parola di `MyString` e una parte della prima parola.

```csharp
string MyString = "Hello World!";
char[] MyChar = {'r','o','W','l','d','!',' '};
string NewString = MyString.TrimEnd(MyChar);
Console.WriteLine(NewString);
```

```vb
Dim MyString As String = "Hello World!"
Dim MyChar() As Char = {"r","o","W","l","d","!"," "}
Dim NewString As String = MyString.TrimEnd(MyChar)
Console.WriteLine(NewString)
```

Il codice visualizza `He` nella console.

L'esempio seguente rimuove l'ultima parola di una stringa con il metodo [TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])). In questo codice la parola `Hello` è seguita da una virgola: dato che la virgola non è specificata nella matrice di caratteri da tagliare, l'operazione di taglio termina in corrispondenza della virgola.

```csharp
string MyString = "Hello, World!";
char[] MyChar = {'r','o','W','l','d','!',' '};
string NewString = MyString.TrimEnd(MyChar);
Console.WriteLine(NewString);
```

```vb
Dim MyString As String = "Hello, World!"
Dim MyChar() As Char = {"r","o","W","l","d","!"," "}
Dim NewString As String = MyString.TrimEnd(MyChar)
Console.WriteLine(NewString)
```

Il codice visualizza `Hello,` nella console.

## <a name="trimstart"></a>TrimStart

Il metodo [String.TrimStart](https://docs.microsoft.com/dotnet/core/api/System.String.TrimStart(System.Char[])) è simile al metodo [String.TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])) ma crea una nuova stringa rimuovendo caratteri dall'inizio di un oggetto stringa esistente. Una matrice di caratteri viene passata al metodo [TrimStart](https://docs.microsoft.com/dotnet/core/api/System.String.TrimStart(System.Char[])) per specificare i caratteri da rimuovere. Come per il metodo [TrimEnd](https://docs.microsoft.com/dotnet/core/api/System.String.TrimEnd(System.Char[])), l'ordine degli elementi nella matrice di caratteri non è importante per l'operazione di rimozione. La rimozione si interrompe quando viene trovato un carattere non specificato nella matrice.

L'esempio seguente rimuove la prima parola di una stringa. In questo esempio la posizione dei caratteri `'l'` e `'H'` viene invertita per indicare che l'ordine dei caratteri nella matrice non è importante.

```csharp
string MyString = "Hello World!";
char[] MyChar = {'e', 'H','l','o',' ' };
string NewString = MyString.TrimStart(MyChar);
Console.WriteLine(NewString);
```

```vb
Dim MyString As String = "Hello World!"
Dim MyChar() As Char = {"e","H","l","o"," " }
Dim NewString As String = MyString.TrimStart(MyChar)
Console.WriteLine(NewString)
```

Il codice visualizza `World!` nella console.

## <a name="remove"></a>Rimuovi

Il metodo [String.Remove](https://docs.microsoft.com/dotnet/core/api/System.String.Remove(System.Int32)) rimuove un numero specificato di caratteri a partire da una posizione specificata in una stringa esistente. Questo metodo presuppone un indice a base zero.

L'esempio seguente rimuove dieci caratteri da una stringa a partire dalla posizione cinque di un indice a base zero della stringa.

```csharp
string MyString = "Hello Beautiful World!";
Console.WriteLine(MyString.Remove(5,10));
// The example displays the following output:
//         Hello World!  
```

```vb
Dim MyString As String = "Hello Beautiful World!"
Console.WriteLine(MyString.Remove(5,10))
' The example displays the following output:
'         Hello World!
```

È anche possibile rimuovere da una stringa una sottostringa o un carattere specificato chiamando il metodo [String.Replace(String, String)](https://docs.microsoft.com/dotnet/core/api/System.String.Replace(System.String,System.String)) e specificando in sostituzione una stringa vuota ([String.Empty](https://docs.microsoft.com/dotnet/core/api/System.String.Empty)). Nell'esempio seguente vengono rimosse tutte le virgole da una stringa.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      String phrase = "a cold, dark night";
      Console.WriteLine("Before: {0}", phrase);
      phrase = phrase.Replace(",", "");
      Console.WriteLine("After: {0}", phrase);
   }
}
// The example displays the following output:
//       Before: a cold, dark night
//       After: a cold dark night
```

```vb
Module Example
   Public Sub Main()
      Dim phrase As String = "a cold, dark night"
      Console.WriteLine("Before: {0}", phrase)
      phrase = phrase.Replace(",", "")
      Console.WriteLine("After: {0}", phrase)
   End Sub
End Module
' The example displays the following output:
'       Before: a cold, dark night
'       After: a cold dark night
```

## <a name="see-also"></a>Vedere anche

[Operazioni di base su stringhe](basic-string-operations.md)




<!--HONumber=Nov16_HO3-->


