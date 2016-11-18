---
title: 'Esempio di espressione regolare: ricerca di HREF'
description: 'Esempio di espressione regolare: ricerca di HREF'
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d6484880-bdac-47cd-b5e5-9419c9ed14cd
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 494ceeb2cc3bbf77098d2b6145690e7229ed3b9f

---

# <a name="regular-expression-example-scanning-for-hrefs"></a>Esempio di espressione regolare: ricerca di HREF

Nell'esempio riportato di seguito viene cercata una stringa di input e vengono visualizzati tutti i valori href="…" e le relative posizioni nella stringa. 

## <a name="the-regex-object"></a>L'oggetto Regex

Poiché il metodo `DumpHRefs` può essere chiamato più volte dal codice utente, viene usato il metodo `static` [Regex.Match(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)). In questo modo il motore delle espressioni regolari memorizza nella cache l'espressione regolare ed evita il sovraccarico di un'istanza di un nuovo oggetto [Regex](xref:System.Text.RegularExpressions.Regex) ogni volta che viene chiamato il metodo. Viene quindi usato un oggetto [Match](xref:System.Text.RegularExpressions.Match) per eseguire un'iterazione in tutte le corrispondenze nella stringa. 

```csharp
private static void DumpHRefs(string inputString) 
{
   Match m;
   string HRefPattern = "href\\s*=\\s*(?:[\"'](?<1>[^\"']*)[\"']|(?<1>\\S+))";

   try {
      m = Regex.Match(inputString, HRefPattern, 
                      RegexOptions.IgnoreCase | RegexOptions.Compiled, 
                      TimeSpan.FromSeconds(1));
      while (m.Success)
      {
         Console.WriteLine("Found href " + m.Groups[1] + " at " 
            + m.Groups[1].Index);
         m = m.NextMatch();
      }   
   }
   catch (RegexMatchTimeoutException) {
      Console.WriteLine("The matching operation timed out.");
   }
}
```

```vb
Private Sub DumpHRefs(inputString As String) 
   Dim m As Match
   Dim HRefPattern As String = "href\s*=\s*(?:[""'](?<1>[^""']*)[""']|(?<1>\S+))"

   Try
      m = Regex.Match(inputString, HRefPattern, _ 
                      RegexOptions.IgnoreCase Or RegexOptions.Compiled,
                      TimeSpan.FromSeconds(1))
      Do While m.Success
         Console.WriteLine("Found href {0} at {1}.", _
                           m.Groups(1), m.Groups(1).Index)
         m = m.NextMatch()
      Loop   
   Catch e As RegexMatchTimeoutException
      Console.WriteLine("The matching operation timed out.")
   End Try
End Sub
```

Nell'esempio seguente viene illustrata una chiamata al metodo `DumpHRefs`.

```csharp
public static void Main()
{
   string inputString = "My favorite web sites include:</P>" +
                        "<A HREF=\"http://msdn2.microsoft.com\">" +
                        "MSDN Home Page</A></P>" +
                        "<A HREF=\"http://www.microsoft.com\">" +
                        "Microsoft Corporation Home Page</A></P>" +
                        "<A HREF=\"http://blogs.msdn.com/bclteam\">" +
                        ".NET Base Class Library blog</A></P>";
   DumpHRefs(inputString);                     

}
// The example displays the following output:
//       Found href http://msdn2.microsoft.com at 43
//       Found href http://www.microsoft.com at 102
//       Found href http://blogs.msdn.com/bclteam at 176
```

```vb
Public Sub Main()
   Dim inputString As String = "My favorite web sites include:</P>" & _
                               "<A HREF=""http://msdn2.microsoft.com"">" & _
                               "MSDN Home Page</A></P>" & _
                               "<A HREF=""http://www.microsoft.com"">" & _
                               "Microsoft Corporation Home Page</A></P>" & _
                               "<A HREF=""http://blogs.msdn.com/bclteam"">" & _
                               ".NET Base Class Library blog</A></P>"
   DumpHRefs(inputString)                     
End Sub
' The example displays the following output:
'       Found href http://msdn2.microsoft.com at 43
'       Found href http://www.microsoft.com at 102
'       Found href http://blogs.msdn.com/bclteam/) at 176
```

Il criterio di ricerca di espressioni regolari `href\s*=\s*(?:["']&#40;?<1>[^"']*)["']|(?<1>\S+))` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`href` | Corrisponde alla stringa letterale "href". La corrispondenza non fa distinzione tra maiuscole e minuscole.
`\s*` | Trovare la corrispondenza di zero o più spazi vuoti.
`=` |Corrisponde al segno di uguale.
`\s*` | Trovare la corrispondenza di zero o più spazi vuoti.
`(?:["']&#40;?<1>[^"']*)"&#124;(?<1>\S+))` | Corrisponde a uno dei seguenti elementi senza assegnazione del risultato a un gruppo acquisito: Una virgoletta o un apostrofo, seguito da zero o più occorrenze di qualsiasi carattere diverso dai primi, seguito da una virgoletta o un apostrofo. Il gruppo denominato `1` è incluso in questo modello. -or- Uno o più caratteri diversi dallo spazio vuoto. Il gruppo denominato `1` è incluso in questo modello.
`(?<1>[^"']*)` | Assegnare zero o più occorrenze di qualsiasi carattere diverso da una virgoletta o un apostrofo al gruppo di acquisizione denominato `1`.
`"(?<1>\S+)` | Assegnare uno o più caratteri diversi da spazi vuoti al gruppo di acquisizione denominato `1`.
 
## <a name="match-result-class"></a>Classe di risultati di corrispondenza

I risultati della ricerca vengono archiviati nella classe [Match](xref:System.Text.RegularExpressions.Match), che offre l'accesso a tutte le sottostringhe estratte dalla ricerca. Tale classe memorizza anche la stringa cercata e l'espressione regolare usata, pertanto è possibile chiamare il metodo [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) per eseguire un'altra ricerca a partire dal punto in cui è terminata quella più recente.

## <a name="explicitly-named-captures"></a>Acquisizioni denominate in modo esplicito

Nelle espressioni regolari tradizionali, le parentesi di cattura vengono automaticamente numerate in sequenza. Ciò comporta due problemi. In primo luogo, se un'espressione regolare viene modificata dall'inserimento o rimozione di un set di parentesi, tutto il codice che fa riferimento alle catture numerate deve essere riscritto per riflettere la nuova numerazione. In secondo luogo, poiché diversi set di parentesi spesso vengono usati per specificare due espressioni alternative per una corrispondenza accettabile, potrebbe essere difficile determinare quale delle due espressioni ha effettivamente restituito un risultato.

Per risolvere questi problemi, la classe [Regex](xref:System.Text.RegularExpressions.Regex) supporta la sintassi `(?<name>…)` per l'acquisizione di una corrispondenza in uno slot specificato (che è possibile denominare tramite una stringa o un numero intero, che può essere chiamato più rapidamente). Le corrispondenze alternative per la stessa stringa possono perciò essere tutte indirizzate verso la stessa posizione. In caso di conflitto, l'ultima corrispondenza rilasciata in uno slot è quella corretta. (È tuttavia disponibile un elenco completo di più corrispondenze per un unico slot. Per informazioni dettagliate, vedere la raccolta [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures).)

## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)

[Esempi di espressioni regolari](regex-examples.md)




<!--HONumber=Nov16_HO3-->


