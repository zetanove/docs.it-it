---
title: Modifica della combinazione di maiuscole e minuscole
description: Modifica della combinazione di maiuscole e minuscole
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 646c5afd-8aec-4393-9c00-f68ad2580c68
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: a6f6f21daae79f752cfac0a70558778ae98d1a5d

---

# <a name="changing-case"></a>Modifica della combinazione di maiuscole e minuscole

Quando si scrive un'applicazione che accetta input dall'utente non si può conoscere la combinazione di maiuscole e minuscole che verrà usata durante l'immissione dei dati. Spesso è desiderabile che le la combinazione di maiuscole e minuscole nelle stringhe sia coerente, in particolare se le stringhe vengono visualizzate nell'interfaccia utente. La tabella seguente descrive due metodi per la modifica della combinazione di maiuscole e minuscole.

Nome metodo | Uso
----------- | ---
[String.ToUpper](xref:System.String.ToUpper) | Converte tutti i caratteri di una stringa in lettere maiuscole.
[String.ToLower](xref:System.String.ToLower) | Converte tutti i caratteri di una stringa in lettere minuscole.

> [!WARNING]  
> Si noti che i metodi `String.ToUpper` e `String.ToLower` non vanno usati per convertire le stringhe a scopo di confronto o verifica dell'uguaglianza. 

## <a name="comparing-strings-of-mixed-case"></a>Confronto di stringhe con una combinazione mista di maiuscole e minuscole

Per confrontare stringhe di caratteri maiuscoli e minuscoli per determinare se sono uguali, chiamare uno degli overload del metodo [String](xref:System) `Equals` con un parametro *comparisonType* parametro e specificare un valore di [StringComparison.CurrentCultureIgnoreCase](xref:System.StringComparison.CurrentCultureIgnoreCase) o [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) per l'argomento *comparisonType*. 

Per altre informazioni, vedere [Best Practices for Using Strings](best-practices.md) (Procedure consigliate per l'uso di stringhe). 

## <a name="toupper"></a>ToUpper

Il metodo [String.ToUpper](xref:System.String.ToUpper) converte tutti i caratteri di una stringa in lettere maiuscole. L'esempio seguente converte la stringa "Hello World!" da caratteri maiuscoli e minuscoli in caratteri maiuscoli.

```csharp
string properString = "Hello World!";
Console.WriteLine(properString.ToUpper());
// This example displays the following output:
//       HELLO WORLD!
```

```vb
Dim MyString As String = "Hello World!"
Console.WriteLine(MyString.ToUpper())
' This example displays the following output:
'       HELLO WORLD!
```

## <a name="tolower"></a>ToLower

Il metodo [String.ToLower](xref:System.String.ToLower) è simile al precedente, ma converte tutti i caratteri di una stringa in lettere minuscole. L'esempio seguente converte la stringa "Hello World!" in caratteri minuscoli.

```csharp
string properString = "Hello World!";
Console.WriteLine(properString.ToLower());
// This example displays the following output:
//       hello world!
```

```vb
Dim MyString As String = "Hello World!"
Console.WriteLine(MyString.ToLower())
' This example displays the following output:
'       hello world!
```

## <a name="see-also"></a>Vedere anche

[Operazioni di base su stringhe](basic-string-operations.md)



<!--HONumber=Nov16_HO1-->


