---
title: 'Procedura: Estrarre un protocollo e un numero di porta da un URL'
description: Come estrarre un protocollo e un numero di porta da un URL
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: d2462fb4-6d61-44ab-8466-73f1f06c3058
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 578b70412e876001f4462e2409739acf3609097b
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-extract-a-protocol-and-port-number-from-a-url"></a>Procedura: Estrarre un protocollo e un numero di porta da un URL

L'esempio seguente estrae un protocollo e un numero di porta da un URL. 

## <a name="example"></a>Esempio

L'esempio usa il metodo [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) per restituire il protocollo seguito da due punti e dal numero di porta. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string url = "http://www.contoso.com:8080/letters/readme";

      Regex r = new Regex(@"^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/",
                          RegexOptions.None, TimeSpan.FromMilliseconds(150));
      Match m = r.Match(url);
      if (m.Success)
         Console.WriteLine(r.Match(url).Result("${proto}${port}")); 
   }
}
// The example displays the following output:
//       http:8080
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim url As String = "http://www.contoso.com:8080/letters/readme.html" 
      Dim r As New Regex("^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/",
                         RegexOptions.None, TimeSpan.FromMilliseconds(150))

      Dim m As Match = r.Match(url)
      If m.Success Then
         Console.WriteLine(r.Match(url).Result("${proto}${port}"))
      End If   
   End Sub
End Module
' The example displays the following output:
'       http:8080
```

Il modello di espressione regolare `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` può essere interpretato come indicato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Iniziare la ricerca della corrispondenza all'inizio della stringa.
`(?<proto>\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Assegnare al gruppo il nome proto.
`://` | Trovare la corrispondenza di due punti seguiti da due barre.
`[^/]+?` | Trovare la corrispondenza di una o più occorrenze (ma il minor numero possibile) di qualsiasi carattere diverso da una barra.
`(?<port>:\d+)?` | Trovare la corrispondenza di zero o una occorrenza di due punti seguiti da una o più cifre. Assegnare al gruppo il nome port.
`/` | Trovare la corrispondenza di una barra.
 
Il metodo [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) espande la sequenza di sostituzione `${proto}${port}` che concatena il valore dei due gruppi denominati acquisiti nel modello di espressione regolare. Si tratta di una comoda alternativa alla concatenazione esplicita delle stringhe recuperate dall'oggetto Collection restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups).

L'esempio usa il metodo [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)) con due sostituzioni, `${proto}` e `${port}`, per includere i gruppi acquisiti nella stringa di output. È possibile invece recuperare i gruppi acquisiti dall'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) della corrispondenza, come viene illustrato dal codice seguente.

```csharp
Console.WriteLine(m.Groups["proto"].Value + m.Groups["port"].Value); 
```

```vb
Console.WriteLine(m.Groups("proto").Value + m.Groups("port").Value)
```

## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)

[Esempi di espressioni regolari](regex-examples.md)

