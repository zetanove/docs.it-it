---
title: 'Procedura: Rimuovere caratteri non validi da una stringa'
description: Come rimuovere caratteri non validi da una stringa
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: f1df4967-7887-41d2-b60f-0da9be67c8fa
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 2d5b0756ab8c34cca0c4ca7c1eb73f81a7a10b70

---

# <a name="how-to-strip-invalid-characters-from-a-string"></a>Procedura: Rimuovere caratteri non validi da una stringa

Nell'esempio seguente viene usato il metodo statico [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions,System.TimeSpan)) per rimuovere i caratteri non validi da una stringa. 

## <a name="example"></a>Esempio

È possibile usare il metodo `CleanInput` definito in questo esempio per rimuovere i caratteri potenzialmente dannosi che sono stati inseriti in un campo di testo che accetta l'input dell'utente. In questo caso, `CleanInput` rimuove tutti i caratteri non alfanumerici tranne punto (.), chiocciole ((@),) e trattini (-) e restituisce la stringa restante. È tuttavia possibile modificare l'espressione regolare in modo che rimuova i caratteri che non devono essere inclusi in una stringa di input.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
    static string CleanInput(string strIn)
    {
        // Replace invalid characters with empty strings.
        try {
           return Regex.Replace(strIn, @"[^\w\.@-]", "", 
                                RegexOptions.None, TimeSpan.FromSeconds(1.5)); 
        }
        // If we timeout when replacing invalid characters, 
        // we should return Empty.
        catch (RegexMatchTimeoutException) {
           return String.Empty;   
        }
    }
}
```

```vb
Imports System.Text.RegularExpressions

Module Example
    Function CleanInput(strIn As String) As String
        ' Replace invalid characters with empty strings.
        Try
           Return Regex.Replace(strIn, "[^\w\.@-]", "")
        ' If we timeout when replacing invalid characters, 
        ' we should return String.Empty.
        Catch e As RegexMatchTimeoutException
           Return String.Empty         
        End Try
    End Function
End Module
```

Il criterio di espressione regolare `[^\w\.@-]` corrisponde a qualsiasi carattere che non è un carattere alfanumerico, un punto, un simbolo @ o un trattino. Un carattere alfanumerico è qualsiasi lettera, numero decimale o connettore di punteggiatura, ad esempio un carattere di sottolineatura. Qualsiasi carattere che corrisponde a questo criterio viene sostituito da [String.Empty](xref:System.String.Empty), ovvero la stringa definita dal criterio di sostituzione. Per consentire ulteriori caratteri nell'input dell'utente, aggiungere tali caratteri alla classe di caratteri nel criterio di espressione regolare. Ad esempio, il criterio di espressione regolare `[^\w\.@-\\%]` consente anche un simbolo di percentuale e una barra rovesciata in una stringa di input.

## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)

[Esempi di espressioni regolari](regex-examples.md)



<!--HONumber=Nov16_HO3-->


