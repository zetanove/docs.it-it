---
title: Caratteri di escape nelle espressioni regolari
description: Caratteri di escape nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 41d35531-2af9-47d4-9780-fbc1e682fbc2
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 08a781be74120d26b8408ee8e9b12051b005ad54

---

# <a name="character-escapes-in-regular-expressions"></a>Caratteri di escape nelle espressioni regolari

La barra rovesciata (\) in un'espressione regolare fornisce una delle indicazioni seguenti: 

* Il carattere che segue è un carattere speciale, come illustrato nella tabella nella sezione seguente. Ad esempio, **\b** è un ancoraggio che indica che una corrispondenza di un'espressione regolare deve iniziare sul confine di una parola, **\t** rappresenta un carattere di tabulazione e **\x020** rappresenta uno spazio.

* Un carattere che altrimenti verrebbe interpretato come un costrutto di linguaggio non di escape deve essere interpretato letteralmente. Ad esempio, una parentesi graffa (**{**) segna l'inizio della definizione di un quantificatore, ma una barra rovesciata seguita da una parentesi graffa (**\{**) indica che il motore delle espressioni regolari deve trovare la corrispondenza con la parentesi graffa. Analogamente, una singola barra rovesciata segna l'inizio di un costrutto di linguaggio di escape, ma due barre rovesciate (**\\**) indicano che il motore delle espressioni regolari deve trovare la corrispondenza con la barra rovesciata.

> [!NOTE]
> Le sequenze di caratteri di escape vengono riconosciute nei modelli di espressioni regolari, ma non nei modelli di sostituzione. 
 
## <a name="character-escapes-in-net"></a>Caratteri di escape in .NET

La tabella seguente elenca i caratteri di escape supportati dalle espressioni regolari in .NET.

Carattere o sequenza | Descrizione
--------------------- | ----------- 
Tutti i caratteri eccetto i seguenti: **. $ ^ { [ ( &#124; ) * + ? \** | I caratteri diversi da quelli elencati nella colonna **Carattere o sequenza** non hanno un significato speciale nelle espressioni regolari, ma corrispondono a se stessi. I caratteri inclusi nella colonna **Carattere o sequenza** sono elementi speciali del linguaggio di espressioni regolari. Per trovare una corrispondenza con essi in un'espressione regolare, è necessario aggiungere un carattere di escape o includerli in un gruppo di caratteri positivi. Ad esempio, l'espressione regolare `\$\d+ or [$]\d+` trova la corrispondenza con "$1200". 
**\a** | Corrisponde a un carattere di controllo del segnale acustico di avviso, **\u0007**.
**\b** | In una classe di caratteri __[__*character*_*group*__]__ corrisponde a un carattere backspace, **\u0008**. Vedere [Classi di caratteri nelle espressioni regolari](classes.md). Al di fuori di una classe di caratteri, **\b** è un ancoraggio che corrisponde a un confine di parola. Vedere [Ancoraggi nelle espressioni regolari](anchors.md).
**\t** | Trova la corrispondenza di un carattere di tabulazione, **\u0009**.
**\r** | Trova la corrispondenza di un carattere di ritorno a capo, **\u000D**. Si noti che **\r** non equivale al carattere di nuova riga **\n**.
**\v** | Trova la corrispondenza di un carattere di tabulazione verticale, **\u000B**.
**\f** | Trova la corrispondenza di un carattere di avanzamento carta, **\u000C**.
**\n** | Trova la corrispondenza di una nuova riga, **\u000A**.
**\e** | Trova la corrispondenza di un carattere di escape, **\u001B**.
**\**_nnn_ | Corrisponde a un carattere ASCII dove nnn è costituito da due o tre cifre che rappresentano il codice carattere ottale. Ad esempio, `\040` rappresenta un carattere di spazio. Questo costrutto viene interpretato come un backreference se è costituito solo da una cifra, ad esempio `\2` o se corrisponde al numero di un gruppo di acquisizione. Vedere [Costrutti di backreference nelle espressioni regolari](backreference.md). 
**\x**_nn_ | Corrisponde a un carattere ASCII dove *nn* è un codice carattere esadecimale a due cifre.
**\c**_X_ | Corrisponde a un carattere di controllo ASCII, dove *X* è la lettera del carattere di controllo. Ad esempio, `\cC` corrisponde a CTRL-C.
**\u**_nnnn_ | Corrisponde a un'unità di codice UTF-16 il cui valore è l'esadecimale *nnnn*. **Nota** La sequenza di caratteri di escape Perl 5 usata per specificare Unicode non è supportata da .NET. Il carattere di escape Perl 5 ha il formato **\x{####…}**, dove **####…** è una serie di cifre esadecimali. Usare invece **\u**_nnnn_. 
**\** | Quando è seguito da un carattere non riconosciuto come carattere di escape, corrisponde a tale carattere. Ad esempio, `\*` corrisponde a un asterisco (*) ed equivale a `\x2A`.
 
## <a name="example"></a>Esempio

L'esempio seguente illustra l'uso di una sequenza di caratteri di escape in un'espressione regolare. Viene analizzata una stringa contenente i nomi delle più grandi città del mondo e la relativa popolazione nel 2009. Ogni nome di città è separato dalla relativa popolazione da un carattere di tabulazione (**\t**) o una barra verticale (| o `\u007c`). Le singole città e la relativa popolazione sono separate tra loro da un ritorno a capo e un avanzamento riga. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string delimited = @"\G(.+)[\t\u007c](.+)\r?\n";
      string input = "Mumbai, India|13,922,125\t\n" + 
                            "Shanghai, China\t13,831,900\n" + 
                            "Karachi, Pakistan|12,991,000\n" + 
                            "Delhi, India\t12,259,230\n" + 
                            "Istanbul, Turkey|11,372,613\n";
      Console.WriteLine("Population of the World's Largest Cities, 2009");
      Console.WriteLine();
      Console.WriteLine("{0,-20} {1,10}", "City", "Population");
      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, delimited))
         Console.WriteLine("{0,-20} {1,10}", match.Groups[1].Value, 
                                            match.Groups[2].Value);
   }
}
// The example displyas the following output:
//       Population of the World's Largest Cities, 2009
//       
//       City                 Population
//       
//       Mumbai, India        13,922,125
//       Shanghai, China      13,831,900
//       Karachi, Pakistan    12,991,000
//       Delhi, India         12,259,230
//       Istanbul, Turkey     11,372,613
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim delimited As String = "\G(.+)[\t\u007c](.+)\r?\n"
      Dim input As String = "Mumbai, India|13,922,125" + vbCrLf + _
                            "Shanghai, China" + vbTab + "13,831,900" + vbCrLf + _
                            "Karachi, Pakistan|12,991,000" + vbCrLf + _
                            "Delhi, India" + vbTab + "12,259,230" + vbCrLf + _
                            "Istanbul, Turkey|11,372,613" + vbCrLf
      Console.WriteLine("Population of the World's Largest Cities, 2009")
      Console.WriteLine()
      Console.WriteLine("{0,-20} {1,10}", "City", "Population")
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, delimited)
         Console.WriteLine("{0,-20} {1,10}", match.Groups(1).Value, _
                                            match.Groups(2).Value)
      Next                         
   End Sub
End Module
' The example displays the following output:
'       Population of the World's Largest Cities, 2009
'       
'       City                 Population
'       
'       Mumbai, India        13,922,125
'       Shanghai, China      13,831,900
'       Karachi, Pakistan    12,991,000
'       Delhi, India         12,259,230
'       Istanbul, Turkey     11,372,613
```

L'espressione regolare `\G(.+)[\t|\u007c](.+)\r?\n` viene interpretata come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\G` | Inizia la corrispondenza dove termina l'ultima corrispondenza.
`(.+)` | Trova la corrispondenza con qualsiasi carattere uno o più volte. Equivale al primo gruppo di acquisizione.
`[\t\u007c]` | Trova la corrispondenza con un carattere di tabulazione (**\t**) o una barra verticale (&#124;).
`(.+)` | Trova la corrispondenza con qualsiasi carattere uno o più volte. Equivale al secondo gruppo di acquisizione.
`\r?\n` | Trova la corrispondenza con zero o una occorrenza di un ritorno a capo seguito da una nuova riga.
 
## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)




<!--HONumber=Nov16_HO1-->


