---
title: 'Esempio di espressione regolare: modifica dei formati di data'
description: 'Esempio di espressione regolare: modifica dei formati di data'
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3e196697-981c-4c1d-93dd-c3b236ef36dd
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 65cdec2c8bc8caf44329ee44bd574e612723be11

---

# <a name="regular-expression-example-changing-date-formats"></a>Esempio di espressione regolare: modifica dei formati di data

Nell'esempio di codice seguente viene usato il metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) per sostituire le date nel formato *mm/gg/aa* con date nel formato *gg-mm-aa*.

## <a name="example"></a>Esempio

```csharp
static string MDYToDMY(string input) 
{
   try {
      return Regex.Replace(input, 
            "\\b(?<month>\\d{1,2})/(?<day>\\d{1,2})/(?<year>\\d{2,4})\\b",
            "${day}-${month}-${year}", RegexOptions.None,
            TimeSpan.FromMilliseconds(150));
   }         
   catch (RegexMatchTimeoutException) {
      return input;
   }
}
```

```vb
Function MDYToDMY(input As String) As String
   Try
      Return Regex.Replace(input, _
             "\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b", _
             "${day}-${month}-${year}", RegexOptions.None,
             TimeSpan.FromMilliseconds(150))
    Catch e As RegexMatchTimeoutException
       Return input
    End Try         
End Function
```

Il codice seguente illustra come il metodo `MDYToDMY` può essere chiamato in un'applicazione. 

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class Class1
{
   public static void Main()
   {
      string dateString = DateTime.Today.ToString("d", 
                                        DateTimeFormatInfo.InvariantInfo);
      string resultString = MDYToDMY(dateString);
      Console.WriteLine("Converted {0} to {1}.", dateString, resultString);
   }

   static string MDYToDMY(string input) 
   {
      try {
         return Regex.Replace(input, 
               "\\b(?<month>\\d{1,2})/(?<day>\\d{1,2})/(?<year>\\d{2,4})\\b",
               "${day}-${month}-${year}", RegexOptions.None,
               TimeSpan.FromMilliseconds(150));
      }         
      catch (RegexMatchTimeoutException) {
         return input;
      }
   }

}
// The example displays the following output to the console if run on 8/21/2007:
//      Converted 08/21/2007 to 21-08-2007.
```

```vb
Imports System.Globalization
Imports System.Text.RegularExpressions

Module DateFormatReplacement
   Public Sub Main()
      Dim dateString As String = Date.Today.ToString("d", _
                                           DateTimeFormatInfo.InvariantInfo)
      Dim resultString As String = MDYToDMY(dateString)
      Console.WriteLine("Converted {0} to {1}.", dateString, resultString)
   End Sub

    Function MDYToDMY(input As String) As String
       Try
          Return Regex.Replace(input, _
                 "\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b", _
                 "${day}-${month}-${year}", RegexOptions.None,
                 TimeSpan.FromMilliseconds(150))
        Catch e As RegexMatchTimeoutException
           Return input
        End Try         
    End Function
End Module
' The example displays the following output to the console if run on 8/21/2007:
'      Converted 08/21/2007 to 21-08-2007.
```

## <a name="comments"></a>Commenti

Il criterio di ricerca di espressioni regolari `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia la corrispondenza sul confine di parola.
`(?<month>\d{1,2})` | Trova la corrispondenza con una o due cifre decimali. Equivale al gruppo acquisito `month`.
`/` | Corrisponde alla barra.
`(?<day>\d{1,2})` | Trova la corrispondenza con una o due cifre decimali. Equivale al gruppo acquisito `day`.
`/` | Corrisponde alla barra.
`(?<year>\d{2,4})` | Corrisponde a due - quattro cifre decimali. Equivale al gruppo acquisito `year`.
`\b` | Termina la corrispondenza sul confine di parola.
 
Il modello `${day}-${month}-${year}` definisce la stringa di sostituzione come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`$(day)` | Aggiunge la stringa acquisita dal gruppo di acquisizione `day`.
`-` | Aggiunge un trattino.
`$(month)` | Aggiunge la stringa acquisita dal gruppo di acquisizione `month`.
`-` | Aggiunge un trattino.
`$(year)` | Aggiunge la stringa acquisita dal gruppo di acquisizione `year`.
 
## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)

[Esempi di espressioni regolari](regex-examples.md)



<!--HONumber=Nov16_HO3-->


