---
title: 'Procedura: Verificare che le stringhe siano in formato di posta elettronica valido'
description: Come verificare che le stringhe siano in formato di posta elettronica valido
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 6d735520-4059-4754-b34c-d117299d36f1
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: bedd1d281256545776c874a38ccb71ad594467c2

---

# <a name="how-to-verify-that-strings-are-in-valid-email-format"></a>Procedura: Verificare che le stringhe siano in formato di posta elettronica valido

L'esempio seguente usa un'espressione regolare per verificare la validità del formato di posta elettronica di una stringa.

## <a name="example"></a>Esempio

Nell'esempio viene definito un metodo `IsValidEmail` che restituisce `true` se nella stringa è presente un indirizzo di posta elettronica valido e `false` in caso contrario, ma non esegue alcuna altra azione. 

Per verificare che l'indirizzo di posta elettronica sia valido, il metodo `IsValidEmail` chiama il metodo [Regex.Replace(String, String, MatchEvaluator)](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.Text.RegularExpressions.MatchEvaluator)) con il criterio di espressione regolare `(@)(.+)$` per separare il nome di dominio dall'indirizzo di posta elettronica. Il terzo parametro è un delegato [MatchEvaluator](xref:System.Text.RegularExpressions.MatchEvaluator) che rappresenta il metodo che elabora e sostituisce il testo corrispondente. Il criterio di espressione regolare viene interpretato nel modo seguente. 

Criterio | Descrizione
------- | ----------- 
`(@)` | Trova la corrispondenza con il carattere @. Equivale al primo gruppo di acquisizione.
`(.+)` | Trova la corrispondenza con una o più occorrenze di qualsiasi carattere. Equivale al secondo gruppo di acquisizione.
`$` | Terminare la corrispondenza alla fine della stringa.
 
Il nome di dominio con il carattere @ viene passato al metodo `DomainMapper`, che usa la classe [IdnMapping](xref:System.Globalization.IdnMapping) per convertire i caratteri Unicode non compresi nell'intervallo di caratteri US-ASCII a Punycode. Il metodo imposta anche il flag `invalid` su `true` se il metodo [IdnMapping.GetAscii](xref:System.Globalization.IdnMapping.GetAscii(System.String)) rileva caratteri non validi nel nome di dominio. Il metodo restituisce il nome di dominio Punycode preceduto dal simbolo @ al metodo `IsValidEmail`. 

Il metodo `IsValidEmail` chiama quindi il metodo [Regex.IsMatch(String, String)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String)) per verificare che l'indirizzo sia conforme a un criterio di espressione regolare. 

Si noti che il metodo `IsValidEmail` non esegue l'autenticazione per convalidare l'indirizzo di posta elettronica e si limita a stabilire se il formato è valido per un indirizzo di posta elettronica. Inoltre il metodo `IsValidEmail` non verifica che il nome di dominio di primo livello sia un nome di dominio valido elencato nella pagina del [Database delle aree radice sul sito IANA](https://www.iana.org/domains/root/db), cosa che richiederebbe un'operazione di ricerca. L'espressione regolare verifica invece solo che il nome di dominio di primo livello sia costituito da un numero di caratteri ASCII compreso tra due e 24. Il nome deve iniziare e finire con caratteri alfanumerici e i caratteri rimanenti possono essere alfanumerici o un trattino (-). 

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class RegexUtilities
{
   bool invalid = false;

   public bool IsValidEmail(string strIn)
   {
       invalid = false;
       if (String.IsNullOrEmpty(strIn))
          return false;

       // Use IdnMapping class to convert Unicode domain names.
       try {
          strIn = Regex.Replace(strIn, @"(@)(.+)$", this.DomainMapper,
                                RegexOptions.None, TimeSpan.FromMilliseconds(200));
       }
       catch (RegexMatchTimeoutException) {
         return false;
       }

        if (invalid)
           return false;

       // Return true if strIn is in valid e-mail format.
       try {
          return Regex.IsMatch(strIn,
                @"^(?("")("".+?(?<!\\)""@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))" +
                @"(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$",
                RegexOptions.IgnoreCase, TimeSpan.FromMilliseconds(250));
       }
       catch (RegexMatchTimeoutException) {
          return false;
       }
   }

   private string DomainMapper(Match match)
   {
      // IdnMapping class with default property values.
      IdnMapping idn = new IdnMapping();

      string domainName = match.Groups[2].Value;
      try {
         domainName = idn.GetAscii(domainName);
      }
      catch (ArgumentException) {
         invalid = true;
      }
      return match.Groups[1].Value + domainName;
   }
}
```

```vb
Imports System.Globalization
Imports System.Text.RegularExpressions

Public Class RegexUtilities
   Dim invalid As Boolean = False

   public Function IsValidEmail(strIn As String) As Boolean
       invalid = False
       If String.IsNullOrEmpty(strIn) Then Return False

       ' Use IdnMapping class to convert Unicode domain names.
       Try
          strIn = Regex.Replace(strIn, "(@)(.+)$", AddressOf Me.DomainMapper, 
                                RegexOptions.None, TimeSpan.FromMilliseconds(200))
       Catch e As RegexMatchTimeoutException
          Return False
       End Try

       If invalid Then Return False

       ' Return true if strIn is in valid e-mail format.
       Try
          Return Regex.IsMatch(strIn,
                 "^(?("")("".+?(?<!\\)""@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))" +
                 "(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$",
                 RegexOptions.IgnoreCase, TimeSpan.FromMilliseconds(250))
       Catch e As RegexMatchTimeoutException
          Return False
       End Try  
   End Function

   Private Function DomainMapper(match As Match) As String
      ' IdnMapping class with default property values.
      Dim idn As New IdnMapping()

      Dim domainName As String = match.Groups(2).Value
      Try
         domainName = idn.GetAscii(domainName)
      Catch e As ArgumentException
         invalid = True      
      End Try      
      Return match.Groups(1).Value + domainName
   End Function
End Class
```

In questo esempio il modello di espressione regolare `^(?(")(".+?(?<!\\)"@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$` viene interpretato come illustrato nella tabella seguente. Si noti che l'espressione regolare viene compilata usando il flag [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase).

Criterio | Descrizione
------- | ----------- 
`^` | Iniziare la ricerca della corrispondenza all'inizio della stringa.
`(?(")` | Determinare se il primo carattere corrisponde a una virgoletta. `(?(")` è l'inizio di un costrutto di alternanza.
`(?("")("".+?(?<!\\)""@)` | Se il primo carattere è una virgoletta, cercare la corrispondenza con una virgoletta iniziale seguita da almeno un'occorrenza di qualsiasi carattere, seguita da una virgoletta finale. La virgoletta finale non deve essere preceduta da un carattere barra rovesciata `(\). (?<!`. è l'inizio di un'asserzione lookbehind negativa di larghezza zero. La stringa dovrebbe terminare con la chiocciola (@).
`&#124;(([0-9a-z] | Se il primo carattere non è una virgoletta, cercare la corrispondenza di qualsiasi carattere alfabetico da a a z o da A a Z (nel confronto è applicata la distinzione tra maiuscole e minuscole) oppure di qualsiasi carattere numerico da 0 a 9.
`(\.(?!\.))` | Se il carattere successivo è un punto, cercare la corrispondenza del punto. Se non è un punto, eseguire il look ahead del carattere successivo e continuare la ricerca della corrispondenza. `(?!\.)` è un'asserzione lookahead negativa di larghezza zero che impedisce la comparsa di due punti consecutivi nella parte locale di un indirizzo di posta elettronica.
`&#124;[-!#\$%&'\*\+/=\?\^`\{\}\&#124;~\w] | Se il carattere successivo non è un punto, cercare la corrispondenza con qualsiasi carattere alfanumerico o con uno dei caratteri seguenti: -!#$%'*+=?^`{}&#124;~. 
`((\.(?!\.))&#124;[-!#\$%'\*\+/=\?\^`\{\}\&#124;~\w])* | Cercare la corrispondenza del modello di alternanza (un punto seguito da un carattere diverso dal punto o da uno dei numerosi caratteri) zero o più volte.
`@` | Trova la corrispondenza con il carattere @.
`(?<=[0-9a-z])` | Continuare la ricerca della corrispondenza se il carattere che precede il carattere @ è compreso tra A e Z, tra a e z oppure tra 0 e 9. Il costrutto `(?<=[0-9a-z])` definisce un'asserzione lookbehind positiva di larghezza zero.
`(?(\[)` | Controllare se il carattere che segue @ è una parentesi di apertura.
`(\[(\d{1,3}\.){3}\d{1,3}\])` | Se è una parentesi di apertura, cercare la corrispondenza della parentesi di apertura seguita da un indirizzo IP (quattro set da una a tre cifre, con ogni set separato da un punto) e una parentesi di chiusura.
`&#124;(([0-9a-z][-\w]*[0-9a-z]*\.)+` | Se il carattere che segue @ non è una parentesi di apertura, cercare la corrispondenza con un carattere alfanumerico avente un valore compreso tra A e Z, a e z oppure 0 e 9, seguito da zero o più occorrenze di un carattere alfanumerico o di un trattino, seguite da zero o un carattere alfanumerico con un valore compreso tra A e Z, a e z oppure 0 e 9 seguito da un punto. Questo modello può essere ripetuto una o più volte e deve essere seguito dal nome di dominio di primo livello. 
`[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))` | Il nome di dominio di primo livello deve iniziare e finire con un carattere alfanumerico (a-z, A-Z e 0-9). Può anche includere da zero a 22 caratteri ASCII, che possono essere caratteri alfanumerici o trattini. 
`$` | Terminare la corrispondenza alla fine della stringa.
 
È possibile chiamare i metodi `IsValidEmail` e `DomainMapper` usando codice simile al seguente:

```csharp
public class Application
{
   public static void Main()
   {
      RegexUtilities util = new RegexUtilities();
      string[] emailAddresses = { "david.jones@proseware.com", "d.j@server1.proseware.com",
                                  "jones@ms1.proseware.com", "j.@server1.proseware.com",
                                  "j@proseware.com9", "js#internal@proseware.com",
                                  "j_9@[129.126.118.1]", "j..s@proseware.com",
                                  "js*@proseware.com", "js@proseware..com",
                                  "js@proseware.com9", "j.s@server1.proseware.com",
                                   "\"j\\\"s\\\"\"@proseware.com", "js@contoso.中国" };

      foreach (var emailAddress in emailAddresses) {
         if (util.IsValidEmail(emailAddress))
            Console.WriteLine("Valid: {0}", emailAddress);
         else
            Console.WriteLine("Invalid: {0}", emailAddress);
      }                                            
   }
}
// The example displays the following output:
//       Valid: david.jones@proseware.com
//       Valid: d.j@server1.proseware.com
//       Valid: jones@ms1.proseware.com
//       Invalid: j.@server1.proseware.com
//       Valid: j@proseware.com9
//       Valid: js#internal@proseware.com
//       Valid: j_9@[129.126.118.1]
//       Invalid: j..s@proseware.com
//       Invalid: js*@proseware.com
//       Invalid: js@proseware..com
//       Valid: js@proseware.com9
//       Valid: j.s@server1.proseware.com
//       Valid: "j\"s\""@proseware.com
//       Valid: js@contoso.ä¸­å›½
```

```vb
Public Class Application
   Public Shared Sub Main()
      Dim util As New RegexUtilities()
      Dim emailAddresses() As String = { "david.jones@proseware.com", "d.j@server1.proseware.com", _
                                         "jones@ms1.proseware.com", "j.@server1.proseware.com", _
                                         "j@proseware.com9", "js#internal@proseware.com", _
                                         "j_9@[129.126.118.1]", "j..s@proseware.com", _
                                         "js*@proseware.com", "js@proseware..com", _
                                         "js@proseware.com9", "j.s@server1.proseware.com",
                                         """j\""s\""""@proseware.com", "js@contoso.中国" }

      For Each emailAddress As String In emailAddresses
         If util.IsValidEmail(emailAddress) Then
            Console.WriteLine("Valid: {0}", emailAddress)
         Else
            Console.WriteLine("Invalid: {0}", emailAddress)
         End If      
      Next                                            
   End Sub
End Class
' The example displays the following output:
'       Valid: david.jones@proseware.com
'       Valid: d.j@server1.proseware.com
'       Valid: jones@ms1.proseware.com
'       Invalid: j.@server1.proseware.com
'       Valid: j@proseware.com9
'       Valid: js#internal@proseware.com
'       Valid: j_9@[129.126.118.1]
'       Invalid: j..s@proseware.com
'       Invalid: js*@proseware.com
'       Invalid: js@proseware..com
'       Valid: js@proseware.com9
'       Valid: j.s@server1.proseware.com
'       Valid: "j\"s\""@proseware.com
'       Valid: js@contoso.ä¸­å›½
```

## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)

[Esempi di espressioni regolari](regex-examples.md)



<!--HONumber=Nov16_HO3-->


