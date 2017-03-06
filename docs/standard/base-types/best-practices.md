---
title: Procedure consigliate per le espressioni regolari
description: Procedure consigliate per le espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 096fd614-91bf-4296-be24-12f62b062294
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: cf9c83de791fa4990a991689a26d4bbdd84cfe7d
ms.lasthandoff: 03/02/2017

---

# <a name="best-practices-for-regular-expressions"></a>Procedure consigliate per le espressioni regolari

Il motore delle espressioni regolari in .NET è uno strumento potente e completo che consente di elaborare il testo in base alle corrispondenze dei modelli anziché in base al confronto e alla corrispondenza con il testo letterale. Nella maggior parte dei casi, la corrispondenza dei modelli viene applicata in modo rapido ed efficiente. In alcuni casi, tuttavia, il motore delle espressioni regolari può risultare molto lento. In casi estremi, può anche sembrare che il motore non risponda durante l'elaborazione di un input relativamente piccolo per ore o perfino giorni. 

In questo argomento vengono illustrate alcune procedure consigliate che possono essere adottate dagli sviluppatori per ottenere prestazioni ottimali con le espressioni regolari. Include le sezioni seguenti:

* [Esaminare l'origine di input](#consider-the-input-source)

* [Gestire la creazione di istanze degli oggetti in modo appropriato](#handle-object-instantiation-appropriately)

* [Assumere il controllo del backtracking](#take-charge-of-backtracking)

* [Usare valori di timeout](#use-time-out-values)

* [Eseguire l'acquisizione solo quando necessario](#capture-only-when-necessary)

* [Argomenti correlati](#related-topics)

## <a name="consider-the-input-source"></a>Esaminare l'origine di input

In generale, le espressioni regolari possono accettare due tipi di input: vincolato o non vincolato. Per input vincolato si intende un testo che proviene da un'origine conosciuta o affidabile e segue un formato predefinito. Per input non vincolato si intende un testo che proviene da un'origine non inaffidabile, ad esempio un utente Web, e non può seguire un formato predefinito o previsto.

I modelli di espressione regolare vengono scritti in genere in modo da corrispondere all'input valido, ovvero gli sviluppatori esaminano il testo per il quale desiderano trovare una corrispondenza e scrivono quindi un modello di espressione regolare a esso corrispondente. Gli sviluppatori determinano infine se questo modello richiede una correzione o un'ulteriore elaborazione testandolo con più elementi di input validi. Se il modello corrisponde a tutti gli input considerati validi, viene dichiarato pronto per la produzione e può essere incluso in un'applicazione rilasciata. In tal modo, un modello di espressione regolare viene considerato appropriato per la corrispondenza con un input vincolato. Tuttavia, non verrà considerato appropriato per la corrispondenza con un input non vincolato.

Per corrispondere a un input non vincolato, un'espressione regolare deve potere gestire efficientemente tre tipi di testo:

• Testo che corrisponde al modello di espressione regolare.

• Testo che non corrisponde al modello di espressione regolare.

• Testo che quasi corrisponde al modello di espressione regolare.

L'ultimo tipo di testo è particolarmente problematico per un'espressione regolare scritta per gestire l'input vincolato. Se tale espressione regolare si basa anche sul [backtracking](backtracking.md) esteso, il motore delle espressioni regolari può richiedere una quantità eccessiva di tempo, in alcuni casi molte ore o giorni, per l'elaborazione di un testo apparentemente irrilevante. 

> [!WARNING]
> Nell'esempio seguente viene utilizzata un'espressione regolare soggetta a un backtracking eccessivo e che con tutta probabilità rifiuta indirizzi di posta elettronica validi. Non utilizzarla in una routine di convalida di posta elettronica. Per un'espressione regolare che convalida gli indirizzi di posta elettronica, vedere [Procedura: Verificare che le stringhe siano in formato di posta elettronica valido](verify-format.md). 


Si consideri, ad esempio, un'espressione regolare comunemente utilizzata ma estremamente problematica per la convalida dell'alias di un indirizzo di posta elettronica. L'espressione regolare `^[0-9A-Z]([-.\w]*[0-9A-Z])*$` viene scritta per elaborare gli indirizzi di posta elettronica ritenuti validi, composti da un carattere alfanumerico seguito da zero o più caratteri che possono essere alfanumerici, punti o trattini. L'espressione regolare deve terminare con un carattere alfanumerico. Tuttavia, come illustrato nell'esempio seguente, sebbene questa espressione regolare gestisca facilmente l'input valido, le prestazioni risulteranno molto inefficienti quando viene elaborato un input quasi valido.

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      Stopwatch sw;    
      string[] addresses = { "AAAAAAAAAAA@contoso.com", 
                             "AAAAAAAAAAaaaaaaaaaa!@contoso.com" };
      // The following regular expression should not actually be used to 
      // validate an email address.
      string pattern = @"^[0-9A-Z]([-.\w]*[0-9A-Z])*$";
      string input; 

      foreach (var address in addresses) {
         string mailBox = address.Substring(0, address.IndexOf("@"));       
         int index = 0;
         for (int ctr = mailBox.Length - 1; ctr >= 0; ctr--) {
            index++;

            input = mailBox.Substring(ctr, index); 
            sw = Stopwatch.StartNew();
            Match m = Regex.Match(input, pattern, RegexOptions.IgnoreCase);
            sw.Stop();
            if (m.Success)
               Console.WriteLine("{0,2}. Matched '{1,25}' in {2}", 
                                 index, m.Value, sw.Elapsed);
            else                     
               Console.WriteLine("{0,2}. Failed  '{1,25}' in {2}", 
                                 index, input, sw.Elapsed);
         }
         Console.WriteLine();
      }
   }
}

// The example displays output similar to the following:
//     1. Matched '                        A' in 00:00:00.0007122
//     2. Matched '                       AA' in 00:00:00.0000282
//     3. Matched '                      AAA' in 00:00:00.0000042
//     4. Matched '                     AAAA' in 00:00:00.0000038
//     5. Matched '                    AAAAA' in 00:00:00.0000042
//     6. Matched '                   AAAAAA' in 00:00:00.0000042
//     7. Matched '                  AAAAAAA' in 00:00:00.0000042
//     8. Matched '                 AAAAAAAA' in 00:00:00.0000087
//     9. Matched '                AAAAAAAAA' in 00:00:00.0000045
//    10. Matched '               AAAAAAAAAA' in 00:00:00.0000045
//    11. Matched '              AAAAAAAAAAA' in 00:00:00.0000045
//    
//     1. Failed  '                        !' in 00:00:00.0000447
//     2. Failed  '                       a!' in 00:00:00.0000071
//     3. Failed  '                      aa!' in 00:00:00.0000071
//     4. Failed  '                     aaa!' in 00:00:00.0000061
//     5. Failed  '                    aaaa!' in 00:00:00.0000081
//     6. Failed  '                   aaaaa!' in 00:00:00.0000126
//     7. Failed  '                  aaaaaa!' in 00:00:00.0000359
//     8. Failed  '                 aaaaaaa!' in 00:00:00.0000414
//     9. Failed  '                aaaaaaaa!' in 00:00:00.0000758
//    10. Failed  '               aaaaaaaaa!' in 00:00:00.0001462
//    11. Failed  '              aaaaaaaaaa!' in 00:00:00.0002885
//    12. Failed  '             Aaaaaaaaaaa!' in 00:00:00.0005780
//    13. Failed  '            AAaaaaaaaaaa!' in 00:00:00.0011628
//    14. Failed  '           AAAaaaaaaaaaa!' in 00:00:00.0022851
//    15. Failed  '          AAAAaaaaaaaaaa!' in 00:00:00.0045864
//    16. Failed  '         AAAAAaaaaaaaaaa!' in 00:00:00.0093168
//    17. Failed  '        AAAAAAaaaaaaaaaa!' in 00:00:00.0185993
//    18. Failed  '       AAAAAAAaaaaaaaaaa!' in 00:00:00.0366723
//    19. Failed  '      AAAAAAAAaaaaaaaaaa!' in 00:00:00.1370108
//    20. Failed  '     AAAAAAAAAaaaaaaaaaa!' in 00:00:00.1553966
//    21. Failed  '    AAAAAAAAAAaaaaaaaaaa!' in 00:00:00.3223372
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim sw As Stopwatch    
      Dim addresses() As String = { "AAAAAAAAAAA@contoso.com", 
                                 "AAAAAAAAAAaaaaaaaaaa!@contoso.com" }
      ' The following regular expression should not actually be used to 
      ' validate an email address.
      Dim pattern As String = "^[0-9A-Z]([-.\w]*[0-9A-Z])*$"
      Dim input As String 

      For Each address In addresses
         Dim mailBox As String = address.Substring(0, address.IndexOf("@"))       
         Dim index As Integer = 0
         For ctr As Integer = mailBox.Length - 1 To 0 Step -1
            index += 1
            input = mailBox.Substring(ctr, index) 
            sw = Stopwatch.StartNew()
            Dim m As Match = Regex.Match(input, pattern, RegexOptions.IgnoreCase)
            sw.Stop()
            if m.Success Then
               Console.WriteLine("{0,2}. Matched '{1,25}' in {2}", 
                                 index, m.Value, sw.Elapsed)
            Else                     
               Console.WriteLine("{0,2}. Failed  '{1,25}' in {2}", 
                                 index, input, sw.Elapsed)
            End If                  
         Next
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays output similar to the following:
'     1. Matched '                        A' in 00:00:00.0007122
'     2. Matched '                       AA' in 00:00:00.0000282
'     3. Matched '                      AAA' in 00:00:00.0000042
'     4. Matched '                     AAAA' in 00:00:00.0000038
'     5. Matched '                    AAAAA' in 00:00:00.0000042
'     6. Matched '                   AAAAAA' in 00:00:00.0000042
'     7. Matched '                  AAAAAAA' in 00:00:00.0000042
'     8. Matched '                 AAAAAAAA' in 00:00:00.0000087
'     9. Matched '                AAAAAAAAA' in 00:00:00.0000045
'    10. Matched '               AAAAAAAAAA' in 00:00:00.0000045
'    11. Matched '              AAAAAAAAAAA' in 00:00:00.0000045
'    
'     1. Failed  '                        !' in 00:00:00.0000447
'     2. Failed  '                       a!' in 00:00:00.0000071
'     3. Failed  '                      aa!' in 00:00:00.0000071
'     4. Failed  '                     aaa!' in 00:00:00.0000061
'     5. Failed  '                    aaaa!' in 00:00:00.0000081
'     6. Failed  '                   aaaaa!' in 00:00:00.0000126
'     7. Failed  '                  aaaaaa!' in 00:00:00.0000359
'     8. Failed  '                 aaaaaaa!' in 00:00:00.0000414
'     9. Failed  '                aaaaaaaa!' in 00:00:00.0000758
'    10. Failed  '               aaaaaaaaa!' in 00:00:00.0001462
'    11. Failed  '              aaaaaaaaaa!' in 00:00:00.0002885
'    12. Failed  '             Aaaaaaaaaaa!' in 00:00:00.0005780
'    13. Failed  '            AAaaaaaaaaaa!' in 00:00:00.0011628
'    14. Failed  '           AAAaaaaaaaaaa!' in 00:00:00.0022851
'    15. Failed  '          AAAAaaaaaaaaaa!' in 00:00:00.0045864
'    16. Failed  '         AAAAAaaaaaaaaaa!' in 00:00:00.0093168
'    17. Failed  '        AAAAAAaaaaaaaaaa!' in 00:00:00.0185993
'    18. Failed  '       AAAAAAAaaaaaaaaaa!' in 00:00:00.0366723
'    19. Failed  '      AAAAAAAAaaaaaaaaaa!' in 00:00:00.1370108
'    20. Failed  '     AAAAAAAAAaaaaaaaaaa!' in 00:00:00.1553966
'    21. Failed  '    AAAAAAAAAAaaaaaaaaaa!' in 00:00:00.3223372
```

Come illustrato nell'output dell'esempio, il motore delle espressioni regolari elabora l'alias di posta elettronica valido nello stesso intervallo di tempo indipendentemente dalla lunghezza. D'altra parte, quando l'indirizzo di posta elettronica quasi valido ha più di cinque caratteri, il tempo di elaborazione raddoppia approssimativamente per ogni carattere aggiuntivo nella stringa. Ciò significa che l'elaborazione di una stringa di 28 caratteri quasi valida richiederebbe più di un'ora e l'elaborazione di una stringa di 33 caratteri quasi valida richiederebbe quasi un giorno. 

Poiché questa espressione regolare è stata sviluppata considerando unicamente la corrispondenza con il formato di input, l'input che non corrisponde al modello non viene preso in considerazione. Di conseguenza, è possibile consentire a un input non vincolato che corrisponde quasi al modello di espressione regolare di ridurre significativamente le prestazioni.

Per risolvere tale problema, è possibile effettuare le operazioni seguenti:

* Durante lo sviluppo di un modello, è consigliabile considerare il modo in cui il backtracking potrebbe influire sulle prestazioni del motore delle espressioni regolari, soprattutto se l'espressione regolare è progettata per elaborare un input non vincolato. Per altre informazioni, vedere la sezione [Assumere il controllo del backtracking](#take-charge-of-backtracking).

* Testare in modo approfondito l'espressione regolare utilizzando un input non valido e quasi valido nonché un input valido. Per generare casualmente input per un'espressione regolare specifica, è possibile usare [Rex](http://research.microsoft.com/en-us/projects/rex/), uno strumento di analisi delle espressioni regolari di Microsoft Research.

## <a name="handle-object-instantiation-appropriately"></a>Gestire la creazione di istanze degli oggetti in modo appropriato

Il modello a oggetti delle espressioni regolari di .NET è basato sulla classe [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex), che rappresenta il motore delle espressioni regolari. Il fattore principale che spesso influisce sulle prestazioni delle espressioni regolari è il modo in cui viene usato il motore [Regex](xref:System.Text.RegularExpressions.Regex). Per definire un'espressione regolare è necessario associare il motore delle espressioni regolari a un modello di espressione regolare. Tale processo di associazione, indipendentemente dal fatto che comporti la creazione di un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) passando al relativo costruttore un modello di espressione regolare o la chiamata a un metodo statico passando il modello di espressione regolare con una stringa da analizzare, è necessariamente dispendioso.

È possibile associare il motore delle espressioni regolari a un modello di espressione regolare specifico e quindi usare il motore per trovare una corrispondenza con il testo in diversi modi:

* È possibile chiamare un metodo di corrispondenza dei modelli statico, ad esempio [Regex.Match(String, String)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String)). Non è richiesta la creazione di un'istanza di un oggetto di espressione regolare.

* È possibile creare un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) e chiamare un metodo di corrispondenza dei modelli dell'istanza di un'espressione regolare interpretata. È il metodo predefinito per associare il motore delle espressioni regolari a un modello di espressione regolare. Si verifica quando viene creata un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) senza un argomento options che include il flag [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled).

* È possibile creare un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) e chiamare un metodo di corrispondenza dei modelli dell'istanza di un'espressione regolare compilata. Gli oggetti di espressioni regolari rappresentano i modelli compilati quando l'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) viene creata con un argomento options che include il flag [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled).

> [!IMPORTANT]
> Il formato della chiamata al metodo (statico, interpretato, compilato) influisce sulle prestazioni se la stessa espressione regolare viene utilizzata più volte nelle chiamate al metodo oppure se in un'applicazione vengono utilizzati spesso gli oggetti di espressione regolare.
 
### <a name="static-regular-expressions"></a>Espressioni regolari statiche

I metodi con espressioni regolari statiche sono consigliati come alternativa alla creazione ripetuta di un'istanza di un oggetto di espressione regolare con la stessa espressione regolare. A differenza dei modelli di espressione regolare usati dagli oggetti di espressione regolare, i codici operativi o il linguaggio MSIL (Microsoft Intermediate Language) compilato dei modelli usati nelle chiamate al metodo di istanza vengono memorizzati nella cache interna dal motore delle espressioni regolari. 

È possibile ad esempio chiamare un metodo per convalidare l'input dell'utente. In questo esempio, un metodo denominato `IsValidCurrency` controlla se l'utente ha immesso un simbolo di valuta seguito da almeno una cifra decimale. Nell'esempio seguente viene illustrata un'implementazione molto inefficiente del metodo `IsValidCurrency`. Si noti che ogni chiamata al metodo crea una nuova istanza dell'oggetto [Regex](xref:System.Text.RegularExpressions.Regex) con lo stesso modello. Di conseguenza, il modello di espressione regolare deve essere ricompilato ogni volta che viene chiamato il metodo.

```csharp
using System;
using System.Text.RegularExpressions;

public class RegexLib
{
   public static bool IsValidCurrency(string currencyValue)
   {
      string pattern = @"\p{Sc}+\s*\d+";
      Regex currencyRegex = new Regex(pattern);
      return currencyRegex.IsMatch(currencyValue);
   }
}
```

```vb
Public Sub OKButton_Click(sender As Object, e As EventArgs) _ 
           Handles OKButton.Click

   If Not String.IsNullOrEmpty(sourceCurrency.Text) Then
      If RegexLib.IsValidCurrency(sourceCurrency.Text) Then
         PerformConversion()
      Else
         status.Text = "The source currency value is invalid."
      End If          
   End If
End Sub
```

È consigliabile sostituire questo codice inefficiente con una chiamata al metodo statico [Regex.IsMatch(String, String)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String)). In questo modo si evita di dover creare un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) ogni volta che si vuole chiamare un metodo di corrispondenza dei modelli e si consente al motore delle espressioni regolari di recuperare una versione compilata dell'espressione regolare dalla cache.

```csharp
using System;
using System.Text.RegularExpressions;

public class RegexLib
{
   public static bool IsValidCurrency(string currencyValue)
   {
      string pattern = @"\p{Sc}+\s*\d+";
      return Regex.IsMatch(currencyValue, pattern); 
   }
}
```

```vb
Imports System.Text.RegularExpressions

Public Module RegexLib
   Public Function IsValidCurrency(currencyValue As String) As Boolean
      Dim pattern As String = "\p{Sc}+\s*\d+"
      Return Regex.IsMatch(currencyValue, pattern)
   End Function
End Module
```

Per impostazione predefinita, nella cache vengono memorizzati gli ultimi 15 modelli di espressione regolare statica usati più di recente. Per le applicazioni che richiedono un numero maggiore di espressioni regolari statiche memorizzate nella cache, la dimensione della cache può essere modificata impostando la proprietà [Regex.CacheSize](xref:System.Text.RegularExpressions.Regex.CacheSize).

L'espressione regolare `\p{Sc}+\s*\d+` usata in questo esempio verifica che la stringa di input sia costituita da un simbolo di valuta e da almeno una cifra decimale. Il modello viene definito come illustrato nella tabella seguente.

Modello | Descrizione
------- | -----------
`\p{Sc}+` | Trova la corrispondenza di uno o più caratteri nella categoria Unicode Symbol, Currency.
`\s*` | Trovare la corrispondenza di zero o più spazi vuoti.
`\d+` | Trova la corrispondenza con una o più cifre decimali.
 
### <a name="interpreted-vs-compiled-regular-expressions"></a>Espressioni regolari interpretate ed espressioni regolari compilate

I modelli di espressione regolare che non sono associati al motore delle espressioni mediante l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) vengono interpretati. Quando viene creata un'istanza di un oggetto di espressione regolare, il motore delle espressioni regolari converte l'espressione regolare in un set di codici operativi. Quando viene chiamato un metodo di istanza, i codici operativi vengono convertiti in MSIL ed eseguiti dal compilatore JIT. Analogamente, quando viene chiamato un metodo con espressioni regolari statiche e l'espressione regolare non è presente nella cache, il motore delle espressioni regolari converte l'espressione regolare in un set di codici operativi che memorizza nella cache. Converte quindi i codici operativi in MSIL in modo tale che possano essere eseguiti dal compilatore JIT. Le espressioni regolari interpretate consentono di ridurre il tempo di avvio ma implicano tempi di esecuzione più lenti. Per questo motivo, risultano particolarmente adatte quando l'espressione regolare viene utilizzata in un numero limitato di chiamate al metodo o se il numero esatto di chiamate ai metodi delle espressioni regolari è sconosciuto ma si prevede che sia esiguo. Man mano che aumenta il numero di chiamate al metodo, il miglioramento delle prestazioni rispetto alla riduzione del tempo di avvio viene superato dalla minore velocità di esecuzione.

I modelli di espressione regolare che sono associati al motore delle espressioni mediante l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) vengono compilati. Ciò significa che quando viene creata un'istanza di un oggetto di espressione regolare o quando viene chiamato un metodo con espressioni regolari statiche e l'espressione regolare non è presente nella cache, il motore delle espressioni regolari converte l'espressione regolare in un set intermedio di codici operativi, il quale viene quindi convertito in MSIL. Il codice MSIL viene eseguito dal compilatore JIT non appena viene chiamato un metodo. A differenza delle espressioni regolari interpretate, le espressioni regolari compilate aumentano il tempo di avvio eseguendo i singoli metodi di corrispondenza dei modelli più velocemente. Di conseguenza, il vantaggio in termini di prestazioni che risulta dalla compilazione dell'espressione regolare aumenta proporzionalmente al numero di metodi dell'espressione regolare chiamati.

Riepilogando, è consigliabile utilizzare le espressioni regolari interpretate quando i metodi dell'espressione regolare vengono chiamati raramente con un'espressione regolare specifica e le espressioni regolari compilate quando i metodi dell'espressione regolare vengono chiamati frequentemente con un'espressione regolare specifica. È difficile determinare la soglia esatta oltre la quale la minore velocità di esecuzione delle espressioni regolari interpretate supera i vantaggi offerti dalla riduzione del tempo di avvio o la soglia oltre la quale la riduzione del tempo di avvio delle espressioni regolari compilate supera i vantaggi offerti dalla maggiore velocità di esecuzione. Dipende da vari fattori, tra cui la complessità dell'espressione regolare e i dati specifici che vengono elaborati. Per determinare se le espressioni regolari interpretate o compilate offrono le migliori prestazioni per lo scenario specifico dell'applicazione, è possibile usare la classe [Stopwatch](xref:System.Diagnostics.Stopwatch) per confrontare i rispettivi tempi di esecuzione.

Nell'esempio seguente vengono confrontate le prestazioni delle espressioni regolari compilate e interpretate durante la lettura delle prime dieci frasi e durante la lettura di tutte le frasi del testo di The Financier di Theodore Dreiser. Come illustrato nell'output dell'esempio, quando vengono effettuate solo dieci chiamate ai metodi di corrispondenza delle espressioni regolari, un'espressione regolare interpretata offre prestazioni migliori rispetto a un'espressione regolare compilata. Tuttavia, un'espressione regolare compilata offre prestazioni migliori quando viene effettuato un numero di chiamate maggiore, in questo caso oltre 13.000. 

```csharp
using System;
using System.Diagnostics;
using System.IO;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+((\r?\n)|,?\s))*\w+[.?:;!]";
      Stopwatch sw;
      Match match;
      int ctr;

      StreamReader inFile = new StreamReader(@".\Dreiser_TheFinancier.txt");
      string input = inFile.ReadToEnd();
      inFile.Close();

      // Read first ten sentences with interpreted regex.
      Console.WriteLine("10 Sentences with Interpreted Regex:");
      sw = Stopwatch.StartNew();
      Regex int10 = new Regex(pattern, RegexOptions.Singleline);
      match = int10.Match(input);
      for (ctr = 0; ctr <= 9; ctr++) {
         if (match.Success)
            // Do nothing with the match except get the next match.
            match = match.NextMatch();
         else
            break;
      }
      sw.Stop();
      Console.WriteLine("   {0} matches in {1}", ctr, sw.Elapsed);

      // Read first ten sentences with compiled regex.
      Console.WriteLine("10 Sentences with Compiled Regex:");
      sw = Stopwatch.StartNew();
      Regex comp10 = new Regex(pattern, 
                   RegexOptions.Singleline | RegexOptions.Compiled);
      match = comp10.Match(input);
      for (ctr = 0; ctr <= 9; ctr++) {
         if (match.Success)
            // Do nothing with the match except get the next match.
            match = match.NextMatch();
         else
            break;
      }
      sw.Stop();
      Console.WriteLine("   {0} matches in {1}", ctr, sw.Elapsed);

      // Read all sentences with interpreted regex.
      Console.WriteLine("All Sentences with Interpreted Regex:");
      sw = Stopwatch.StartNew();
      Regex intAll = new Regex(pattern, RegexOptions.Singleline);
      match = intAll.Match(input);
      int matches = 0;
      while (match.Success) {
         matches++;
         // Do nothing with the match except get the next match.
         match = match.NextMatch();
      }
      sw.Stop();
      Console.WriteLine("   {0:N0} matches in {1}", matches, sw.Elapsed);

      // Read all sentnces with compiled regex.
      Console.WriteLine("All Sentences with Compiled Regex:");
      sw = Stopwatch.StartNew();
      Regex compAll = new Regex(pattern, 
                      RegexOptions.Singleline | RegexOptions.Compiled);
      match = compAll.Match(input);
      matches = 0;
      while (match.Success) {
         matches++;
         // Do nothing with the match except get the next match.
         match = match.NextMatch();
      }
      sw.Stop();
      Console.WriteLine("   {0:N0} matches in {1}", matches, sw.Elapsed);      
   }
}
// The example displays the following output:
//       10 Sentences with Interpreted Regex:
//          10 matches in 00:00:00.0047491
//       10 Sentences with Compiled Regex:
//          10 matches in 00:00:00.0141872
//       All Sentences with Interpreted Regex:
//          13,443 matches in 00:00:01.1929928
//       All Sentences with Compiled Regex:
//          13,443 matches in 00:00:00.7635869
//       
//       >compare1
//       10 Sentences with Interpreted Regex:
//          10 matches in 00:00:00.0046914
//       10 Sentences with Compiled Regex:
//          10 matches in 00:00:00.0143727
//       All Sentences with Interpreted Regex:
//          13,443 matches in 00:00:01.1514100
//       All Sentences with Compiled Regex:
//          13,443 matches in 00:00:00.7432921
```

```vb
Imports System.Diagnostics
Imports System.IO
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+((\r?\n)|,?\s))*\w+[.?:;!]"
      Dim sw As Stopwatch
      Dim match As Match
      Dim ctr As Integer

      Dim inFile As New StreamReader(".\Dreiser_TheFinancier.txt")
      Dim input As String = inFile.ReadToEnd()
      inFile.Close()

      ' Read first ten sentences with interpreted regex.
      Console.WriteLine("10 Sentences with Interpreted Regex:")
      sw = Stopwatch.StartNew()
      Dim int10 As New Regex(pattern, RegexOptions.SingleLine)
      match = int10.Match(input)
      For ctr = 0 To 9
         If match.Success Then
            ' Do nothing with the match except get the next match.
            match = match.NextMatch()
         Else
            Exit For
         End If
      Next
      sw.Stop()
      Console.WriteLine("   {0} matches in {1}", ctr, sw.Elapsed)

      ' Read first ten sentences with compiled regex.
      Console.WriteLine("10 Sentences with Compiled Regex:")
      sw = Stopwatch.StartNew()
      Dim comp10 As New Regex(pattern, 
                   RegexOptions.SingleLine Or RegexOptions.Compiled)
      match = comp10.Match(input)
      For ctr = 0 To 9
         If match.Success Then
            ' Do nothing with the match except get the next match.
            match = match.NextMatch()
         Else
            Exit For
         End If
      Next
      sw.Stop()
      Console.WriteLine("   {0} matches in {1}", ctr, sw.Elapsed)

      ' Read all sentences with interpreted regex.
      Console.WriteLine("All Sentences with Interpreted Regex:")
      sw = Stopwatch.StartNew()
      Dim intAll As New Regex(pattern, RegexOptions.SingleLine)
      match = intAll.Match(input)
      Dim matches As Integer = 0
      Do While match.Success
         matches += 1
         ' Do nothing with the match except get the next match.
         match = match.NextMatch()
      Loop
      sw.Stop()
      Console.WriteLine("   {0:N0} matches in {1}", matches, sw.Elapsed)

      ' Read all sentnces with compiled regex.
      Console.WriteLine("All Sentences with Compiled Regex:")
      sw = Stopwatch.StartNew()
      Dim compAll As New Regex(pattern, 
                     RegexOptions.SingleLine Or RegexOptions.Compiled)
      match = compAll.Match(input)
      matches = 0
      Do While match.Success
         matches += 1
         ' Do nothing with the match except get the next match.
         match = match.NextMatch()
      Loop
      sw.Stop()
      Console.WriteLine("   {0:N0} matches in {1}", matches, sw.Elapsed)      
   End Sub
End Module
' The example displays output like the following:
'       10 Sentences with Interpreted Regex:
'          10 matches in 00:00:00.0047491
'       10 Sentences with Compiled Regex:
'          10 matches in 00:00:00.0141872
'       All Sentences with Interpreted Regex:
'          13,443 matches in 00:00:01.1929928
'       All Sentences with Compiled Regex:
'          13,443 matches in 00:00:00.7635869
'       
'       >compare1
'       10 Sentences with Interpreted Regex:
'          10 matches in 00:00:00.0046914
'       10 Sentences with Compiled Regex:
'          10 matches in 00:00:00.0143727
'       All Sentences with Interpreted Regex:
'          13,443 matches in 00:00:01.1514100
'       All Sentences with Compiled Regex:
'          13,443 matches in 00:00:00.7432921
```

Il criterio di espressione regolare usato nell'esempio, `\b(\w+((\r?\n)|,?\s))*\w+[.?:;!]`, è definito nel modo illustrato nella tabella seguente.

Modello | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`(\r?\n)|,?\s)` | Trova la corrispondenza di uno o nessun ritorno a capo seguito da un carattere di nuova riga o di una o nessuna virgola seguita da uno spazio vuoto.
`(\w+((\r?\n)|,?\s))*` | Trova la corrispondenza di zero o più occorrenze di uno o più caratteri alfanumerici seguiti da uno o nessun ritorno a capo e un carattere di nuova riga o da una o nessuna virgola seguita da uno spazio vuoto.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`[.?:;!]` | Trova la corrispondenza di un punto, un punto interrogativo, due punti, un punto e virgola o un punto esclamativo.
 
## <a name="take-charge-of-backtracking"></a>Assumere il controllo del backtracking

In genere, il motore delle espressioni regolari usa la progressione lineare per spostarsi in una stringa di input e confrontarla con un modello di espressione regolare. Tuttavia, quando in un modello di espressione regolare vengono usati quantificatori indeterminati come __*__, **+** e **?**, il motore delle espressioni regolari può tralasciare una parte delle corrispondenze parziali corrette e tornare a uno stato salvato in precedenza per cercare una corrispondenza corretta per l'intero modello. Questo processo è noto come backtracking.

> [!NOTE]
> Per altre informazioni sul backtracking, vedere [Dettagli sul comportamento delle espressioni regolari](regex-behavior.md) e [Backtracking nelle espressioni regolari](backtracking.md).
 
Il supporto del backtracking fornisce alle espressioni regolari potenza e flessibilità. Inoltre la responsabilità del controllo del funzionamento del motore delle espressioni regolari viene affidata agli sviluppatori delle espressioni regolari. Poiché spesso gli sviluppatori non sono consapevoli di questa responsabilità, un utilizzo improprio del backtracking o un utilizzo eccessivo del backtracking rappresenta spesso la causa principale della riduzione delle prestazioni delle espressioni regolari. Nello scenario peggiore, il tempo di esecuzione può raddoppiarsi per ogni carattere aggiuntivo nella stringa di input. Utilizzando infatti il backtracking in modo eccessivo, è facile creare l'equivalente a livello di codice di un ciclo infinito se l'input corrisponde quasi al modello di espressione regolare. Il motore delle espressioni regolari può richiedere ore o persino giorni per l'elaborazione di una stringa di input relativamente breve.

L'utilizzo del backtracking comporta spesso una riduzione delle prestazioni delle applicazioni sebbene il backtracking non sia essenziale per una corrispondenza. Ad esempio, l'espressione regolare `\b\p{Lu}\w*\b` cerca una corrispondenza di tutte le parole che iniziano con un carattere maiuscolo, come illustrato nella tabella seguente.

Modello | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\p{Lu}` | Trova la corrispondenza di un carattere maiuscolo.
`\w*` | Trova la corrispondenza di zero o più caratteri alfanumerici.
`\b` | Termina la corrispondenza sul confine di parola.
 
Poiché un confine di parola non è uguale a un carattere alfanumerico né è un subset di tali caratteri, non è possibile che il motore delle espressioni regolari attraversi un confine di parola quando viene trovata una corrispondenza con i caratteri alfanumerici. Ciò significa che per questa espressione regolare, il backtracking non potrà mai contribuire alla riuscita dell'operazione ma potrà solo ridurre le prestazioni poiché il motore delle espressioni regolari deve salvare lo stato per ogni corrispondenza preliminare corretta di un carattere alfanumerico.

Se si determina che il backtracking non è necessario, è possibile disabilitarlo usando l'elemento del linguaggio **(?>**_subexpression_**)**. Nell'esempio seguente viene analizzata una stringa di input utilizzando due espressioni regolari. La prima, `\b\p{Lu}\w*\b`, si basa sul backtracking. La seconda, `\b\p{Lu}(?>\w*)\b`, disabilita il backtracking. Come illustrato nell'output dell'esempio, entrambe producono lo stesso risultato.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This this word Sentence name Capital";
      string pattern = @"\b\p{Lu}\w*\b";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);

      Console.WriteLine();

      pattern = @"\b\p{Lu}(?>\w*)\b";   
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       This
//       Sentence
//       Capital
//       
//       This
//       Sentence
//       Capital
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This this word Sentence name Capital"
      Dim pattern As String = "\b\p{Lu}\w*\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
      Console.WriteLine()

      pattern = "\b\p{Lu}(?>\w*)\b"   
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       This
'       Sentence
'       Capital
'       
'       This
'       Sentence
'       Capital
```

In molti casi, il backtracking è essenziale per la corrispondenza di un modello di espressione regolare con il testo di input. Tuttavia, un utilizzo eccessivo del backtracking può ridurre notevolmente le prestazioni e dare l'impressione che un'applicazione non risponda. In particolare, tale situazione si verifica quando vengono annidati i quantificatori e il testo che corrisponde alla sottoespressione esterna è un subset del testo che corrisponde alla sottoespressione interna. 

> [!WARNING]
> Oltre a evitare un eccessivo utilizzo del backtracking, è necessario utilizzare la funzionalità di timeout per assicurarsi che l'eccessivo backtracking non comprometta troppo le prestazioni dell'espressione regolare. Per altre informazioni, vedere la sezione [Usare valori di timeout](#use-time-out-values).
 
Ad esempio, il criterio di espressione regolare `^[0-9A-Z]([-.\w]*[0-9A-Z])*\$$` viene usato per trovare la corrispondenza con un numero parte costituito da almeno un carattere alfanumerico. Tutti i caratteri aggiuntivi possono essere costituiti da un carattere alfanumerico, un trattino, un carattere di sottolineatura o un punto, sebbene l'ultimo carattere debba essere alfanumerico. Il numero parte termina con il simbolo del dollaro. In alcuni casi, il criterio di espressione regolare può presentare prestazioni estremamente insufficienti perché vengono annidati i quantificatori e perché la sottoespressione `[0-9A-Z]` è un subset della sottoespressione `[-.\w]*`.

In questi casi, è possibile ottimizzare le prestazioni dell'espressione regolare rimuovendo i quantificatori annidati e sostituendo la sottoespressione esterna con un'asserzione lookahead o lookbehind di larghezza zero. Le asserzioni lookahead e lookbehind sono ancoraggi; non spostano il puntatore nella stringa di input, ma eseguono il lookahead e lookbehind per verificare se è stata soddisfatta una condizione specificata. Ad esempio, l'espressione regolare del numero parte può essere riscritta come `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])\$$`. Tale modello di espressione regolare viene definito come illustrato nella tabella seguente.

Modello | Descrizione
------- | -----------
`^` | Inizia la corrispondenza all'inizio della stringa di input.
`[0-9A-Z]` | Trova la corrispondenza di un carattere alfanumerico. Il numero parte deve essere costituito da almeno uno di questi caratteri.
`[-.\w]*` | Trova la corrispondenza di zero o più occorrenze di un carattere alfanumerico, un trattino o un punto.
`\$] | Trova la corrispondenza di un simbolo del dollaro.
`(?<=[0-9A-Z])` | Esegue il lookahead del simbolo del dollaro finale per verificare che il carattere precedente sia alfanumerico.
`$` Termina la ricerca della corrispondenza alla fine della stringa di input.
 
Nell'esempio seguente viene illustrato l'utilizzo dell'espressione regolare per trovare la corrispondenza con una matrice contenente i numeri parte possibili.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^[0-9A-Z][-.\w]*(?<=[0-9A-Z])\$$";
      string[] partNos = { "A1C$", "A4", "A4$", "A1603D$", "A1603D#" };

      foreach (var input in partNos) {
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine(match.Value);
         else
            Console.WriteLine("Match not found.");
      }      
   }
}
// The example displays the following output:
//       A1C$
//       Match not found.
//       A4$
//       A1603D$
//       Match not found.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^[0-9A-Z][-.\w]*(?<=[0-9A-Z])\$$"
      Dim partNos() As String = { "A1C$", "A4", "A4$", "A1603D$", 
                                  "A1603D#" }

      For Each input As String In partNos
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine(match.Value)
         Else
            Console.WriteLine("Match not found.")
         End If
      Next      
   End Sub
End Module
' The example displays the following output:
'       A1C$
'       Match not found.
'       A4$
'       A1603D$
'       Match not found.
```

Il linguaggio delle espressioni regolari in .NET include i seguenti elementi che è possibile usare per eliminare i quantificatori annidati. Per altre informazioni, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

Elemento di linguaggio | Descrizione
---------------- | ----------- 
**(?**=_subexpression_**)** | Asserzione lookahead positiva di larghezza zero. Lookahead della posizione corrente per determinare se *subexpression* corrisponde alla stringa di input.
**(?!**_subexpression_**)** | Asserzione lookahead negativa di larghezza zero. Lookahead della posizione corrente per determinare se *subexpression* non corrisponde alla stringa di input.
**(?<**=_subexpression_**)** | Lookbehind positivo di larghezza zero. Lookbehind della posizione corrente per determinare se *subexpression* corrisponde alla stringa di input.
**(?<!**_subexpression_**)** | Lookbehind negativo di larghezza zero. Lookbehind della posizione corrente per determinare se *subexpression* non corrisponde alla stringa di input.
 
## <a name="use-time-out-values"></a>Usare valori di timeout

Se le espressioni regolari elaborano l'input che corrisponde quasi al modello dell'espressione regolare, possono spesso basarsi su un backtracking eccessivo, con un impatto notevole sulle prestazioni. Oltre a considerare attentamente l'utilizzo del backtracking e a testare l'espressione regolare rispetto all'input maggiormente corrispondente, è necessario impostare sempre un valore di timeout per assicurarsi che l'impatto di un eventuale backtracking eccessivo sia contenuto.

L'intervallo di timeout dell'espressione regolare definisce il periodo di tempo durante il quale il motore delle espressioni regolari cercherà una singola corrispondenza prima del timeout. L'intervallo di timeout predefinito è [Regex.InfiniteMatchTimeout](xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout) che significa che l'espressione regolare non scadrà. È possibile eseguire l'override di questo valore e definire un intervallo di timeout come segue: 

* Specificando un valore di timeout quando si crea un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) chiamando il costruttore [Regex(String, RegexOptions, TimeSpan)](xref:System.Text.RegularExpressions.Regex.%23ctor(System.String,System.Text.RegularExpressions.RegexOptions,System.TimeSpan)).

* Chiamando un metodo di corrispondenza statico, ad esempio [Regex.Match(String, String, RegexOptions, TimeSpan)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions,System.TimeSpan)) o [Regex.Replace(String, String, String, RegexOptions, TimeSpan)](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions,System.TimeSpan)) che include un parametro *matchTimeout*.

Se è stato definito un intervallo di timeout e non viene trovata alcuna corrispondenza alla fine di questo intervallo, il metodo dell'espressione regolare genera un'eccezione [RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException). Nel gestore eccezioni, è possibile continuare a cercare la corrispondenza con un intervallo di timeout più lungo, abbandonare il tentativo di ricerca supponendo che non esista alcuna corrispondenza oppure abbandonare il tentativo di ricerca e registrare le informazioni sull'eccezione per un'analisi futura.

Nell'esempio seguente viene definito un metodo `GetWordData` che crea un'istanza di un'espressione regolare con un intervallo di timeout di 350 millisecondi per calcolare il numero di parole e il numero medio di caratteri di una parola in un documento di testo. Se l'operazione di ricerca della corrispondenza scade, l'intervallo di timeout viene aumentato di 350 millisecondi e viene nuovamente creata un'istanza dell'oggetto [Regex](xref:System.Text.RegularExpressions.Regex). Se il nuovo intervallo di timeout supera 1 secondo, il metodo genera nuovamente l'eccezione al chiamante.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      RegexUtilities util = new RegexUtilities();
      string title = "Doyle - The Hound of the Baskervilles.txt";
      try {
         var info = util.GetWordData(title);
         Console.WriteLine("Words:               {0:N0}", info.Item1);
         Console.WriteLine("Average Word Length: {0:N2} characters", info.Item2); 
      }
      catch (IOException e) {
         Console.WriteLine("IOException reading file '{0}'", title);
         Console.WriteLine(e.Message);
      }
      catch (RegexMatchTimeoutException e) {
         Console.WriteLine("The operation timed out after {0:N0} milliseconds", 
                           e.MatchTimeout.TotalMilliseconds);
      }
   }
}

public class RegexUtilities
{
   public Tuple<int, double> GetWordData(string filename)
   { 
      const int MAX_TIMEOUT = 1000;   // Maximum timeout interval in milliseconds.
      const int INCREMENT = 350;      // Milliseconds increment of timeout.

      List<string> exclusions = new List<string>( new string[] { "a", "an", "the" });
      int[] wordLengths = new int[29];        // Allocate an array of more than ample size.
      string input = null;
      StreamReader sr = null;
      try { 
         sr = new StreamReader(filename);
         input = sr.ReadToEnd();
      }
      catch (FileNotFoundException e) {
         string msg = String.Format("Unable to find the file '{0}'", filename);
         throw new IOException(msg, e);
      }
      catch (IOException e) {
         throw new IOException(e.Message, e);
      }
      finally {
         if (sr != null) sr.Close(); 
      }

      int timeoutInterval = INCREMENT;
      bool init = false;
      Regex rgx = null;
      Match m = null;
      int indexPos = 0;  
      do {
         try {
            if (! init) {
               rgx = new Regex(@"\b\w+\b", RegexOptions.None, 
                               TimeSpan.FromMilliseconds(timeoutInterval));
               m = rgx.Match(input, indexPos);
               init = true;
            }
            else { 
               m = m.NextMatch();
            }
            if (m.Success) {    
               if ( !exclusions.Contains(m.Value.ToLower()))
                  wordLengths[m.Value.Length]++;

               indexPos += m.Length + 1;   
            }
         }
         catch (RegexMatchTimeoutException e) {
            if (e.MatchTimeout.TotalMilliseconds < MAX_TIMEOUT) {
               timeoutInterval += INCREMENT;
               init = false;
            }
            else {
               // Rethrow the exception.
               throw; 
            }   
         }          
      } while (m.Success);

      // If regex completed successfully, calculate number of words and average length.
      int nWords = 0; 
      long totalLength = 0;

      for (int ctr = wordLengths.GetLowerBound(0); ctr <= wordLengths.GetUpperBound(0); ctr++) {
         nWords += wordLengths[ctr];
         totalLength += ctr * wordLengths[ctr];
      }
      return new Tuple<int, double>(nWords, totalLength/nWords);
   }
}
```

```vb
Imports System.Collections.Generic
Imports System.IO
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim util As New RegexUtilities()
      Dim title As String = "Doyle - The Hound of the Baskervilles.txt"
      Try
         Dim info = util.GetWordData(title)
         Console.WriteLine("Words:               {0:N0}", info.Item1)
         Console.WriteLine("Average Word Length: {0:N2} characters", info.Item2) 
      Catch e As IOException
         Console.WriteLine("IOException reading file '{0}'", title)
         Console.WriteLine(e.Message)
      Catch e As RegexMatchTimeoutException
         Console.WriteLine("The operation timed out after {0:N0} milliseconds", 
                           e.MatchTimeout.TotalMilliseconds)
      End Try
   End Sub
End Module

Public Class RegexUtilities
   Public Function GetWordData(filename As String) As Tuple(Of Integer, Double) 
      Const MAX_TIMEOUT As Integer = 1000  ' Maximum timeout interval in milliseconds.
      Const INCREMENT As Integer = 350     ' Milliseconds increment of timeout.

      Dim exclusions As New List(Of String)({"a", "an", "the" })
      Dim wordLengths(30) As Integer        ' Allocate an array of more than ample size.
      Dim input As String = Nothing
      Dim sr As StreamReader = Nothing
      Try 
         sr = New StreamReader(filename)
         input = sr.ReadToEnd()
      Catch e As FileNotFoundException
         Dim msg As String = String.Format("Unable to find the file '{0}'", filename)
         Throw New IOException(msg, e)
      Catch e As IOException
         Throw New IOException(e.Message, e)
      Finally
         If sr IsNot Nothing Then sr.Close() 
      End Try

      Dim timeoutInterval As Integer = INCREMENT
      Dim init As Boolean = False
      Dim rgx As Regex = Nothing
      Dim m As Match = Nothing
      Dim indexPos As Integer = 0  
      Do
         Try
            If Not init Then
               rgx = New Regex("\b\w+\b", RegexOptions.None, 
                               TimeSpan.FromMilliseconds(timeoutInterval))
               m = rgx.Match(input, indexPos)
               init = True
            Else 
               m = m.NextMatch()
            End If
            If m.Success Then    
               If Not exclusions.Contains(m.Value.ToLower()) Then
                  wordLengths(m.Value.Length) += 1
               End If
               indexPos += m.Length + 1   
            End If
         Catch e As RegexMatchTimeoutException
            If e.MatchTimeout.TotalMilliseconds < MAX_TIMEOUT Then
               timeoutInterval += INCREMENT
               init = False
            Else
               ' Rethrow the exception.
               Throw 
            End If   
         End Try          
      Loop While m.Success

      ' If regex completed successfully, calculate number of words and average length.
      Dim nWords As Integer
      Dim totalLength As Long

      For ctr As Integer = wordLengths.GetLowerBound(0) To wordLengths.GetUpperBound(0)
         nWords += wordLengths(ctr)
         totalLength += ctr * wordLengths(ctr)
      Next
      Return New Tuple(Of Integer, Double)(nWords, totalLength/nWords)
   End Function
End Class
```

## <a name="capture-only-when-necessary"></a>Eseguire l'acquisizione solo quando necessario

Le espressioni regolari in .NET supportano diversi costrutti di raggruppamento, che consentono di raggruppare un modello di espressione regolare in una o più sottoespressioni. I costrutti di raggruppamento più comunemente usati nel linguaggio delle espressioni regolari di .NET sono **(**_subexpression_**)** che definisce un gruppo di acquisizione numerato, e **(?<*_name_**>**_subexpression_**)**che definisce un gruppo di acquisizione denominato. I costrutti di raggruppamento sono indispensabili per la creazione di backreference e per la definizione di una sottoespressione a cui viene applicato un quantificatore. 

Tuttavia, l'utilizzo di questi elementi del linguaggio ha un costo. Comportano il popolamento dell'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) con le acquisizioni non denominate o denominate più recenti e se un singolo costrutto di raggruppamento ha acquisito più sottostringhe nella stringa di input comportano anche il popolamento dell'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) restituito dalla proprietà [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) di un gruppo di acquisizione specifico con più oggetti [Capture](xref:System.Text.RegularExpressions.Capture).

I costrutti di raggruppamento spesso vengono utilizzati solo in un'espressione regolare in modo tale che sia possibile applicarvi i quantificatori e che i gruppi acquisiti da queste sottoespressioni non vengano utilizzati successivamente. Ad esempio, l'espressione regolare `\b(\w+[;,]?\s?)+[.?!]` è progettata per acquisire un'intera frase. Nella tabella seguente sono descritti gli elementi del linguaggio del modello di espressione regolare e il relativo effetto sulle raccolte [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) e [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) dell'oggetto [Match](xref:System.Text.RegularExpressions.Match).

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`[;,]?` | Trova la corrispondenza di una o nessuna virgola oppure di uno o nessun punto e virgola.
`\s?` | Trova la corrispondenza di uno o nessuno spazio vuoto.
`(\w+[;,]?\s?)+` | Trova la corrispondenza di una o più occorrenze di uno o più caratteri alfanumerici seguiti da una virgola o un punto e virgola facoltativo seguito da uno spazio vuoto facoltativo. Questo modello definisce il primo gruppo di acquisizione, necessario affinché la combinazione di più caratteri alfanumerici, ovvero una parola, seguiti da un simbolo di punteggiatura facoltativo venga ripetuta finché il motore delle espressioni regolari non raggiunge la fine di una frase.
`[.?!]` | Trova la corrispondenza di un punto, un punto interrogativo o un punto esclamativo.
 
Come illustrato nell'esempio seguente, quando viene trovata una corrispondenza, entrambi gli oggetti [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) e [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) vengono popolati con le acquisizioni della corrispondenza. In questo caso, è presente il gruppo di acquisizione `(\w+[;,]?\s?)` in modo tale che sia possibile applicarvi il quantificatore **+** consentendo al criterio di espressione regolare di trovare la corrispondenza con ogni parola di una frase. In caso contrario, verrebbe trovata la corrispondenza con l'ultima parola di una frase.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is one sentence. This is another.";
      string pattern = @"\b(\w+[;,]?\s?)+[.?!]";

      foreach (Match match in Regex.Matches(input, pattern)) {
         Console.WriteLine("Match: '{0}' at index {1}.", 
                           match.Value, match.Index);
         int grpCtr = 0;
         foreach (Group grp in match.Groups) {
            Console.WriteLine("   Group {0}: '{1}' at index {2}.",
                              grpCtr, grp.Value, grp.Index);
            int capCtr = 0;
            foreach (Capture cap in grp.Captures) {
               Console.WriteLine("      Capture {0}: '{1}' at {2}.",
                                 capCtr, cap.Value, cap.Index);
               capCtr++;
            }
            grpCtr++;
         }          
         Console.WriteLine();        
      }
   }
}
// The example displays the following output:
//       Match: 'This is one sentence.' at index 0.
//          Group 0: 'This is one sentence.' at index 0.
//             Capture 0: 'This is one sentence.' at 0.
//          Group 1: 'sentence' at index 12.
//             Capture 0: 'This ' at 0.
//             Capture 1: 'is ' at 5.
//             Capture 2: 'one ' at 8.
//             Capture 3: 'sentence' at 12.
//       
//       Match: 'This is another.' at index 22.
//          Group 0: 'This is another.' at index 22.
//             Capture 0: 'This is another.' at 22.
//          Group 1: 'another' at index 30.
//             Capture 0: 'This ' at 22.
//             Capture 1: 'is ' at 27.
//             Capture 2: 'another' at 30.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is one sentence. This is another."
      Dim pattern As String = "\b(\w+[;,]?\s?)+[.?!]"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Match: '{0}' at index {1}.", 
                           match.Value, match.Index)
         Dim grpCtr As Integer = 0
         For Each grp As Group In match.Groups
            Console.WriteLine("   Group {0}: '{1}' at index {2}.",
                              grpCtr, grp.Value, grp.Index)
            Dim capCtr As Integer = 0
            For Each cap As Capture In grp.Captures
               Console.WriteLine("      Capture {0}: '{1}' at {2}.",
                                 capCtr, cap.Value, cap.Index)
               capCtr += 1
            Next
            grpCtr += 1
         Next          
         Console.WriteLine()        
      Next    
   End Sub
End Module
' The example displays the following output:
'       Match: 'This is one sentence.' at index 0.
'          Group 0: 'This is one sentence.' at index 0.
'             Capture 0: 'This is one sentence.' at 0.
'          Group 1: 'sentence' at index 12.
'             Capture 0: 'This ' at 0.
'             Capture 1: 'is ' at 5.
'             Capture 2: 'one ' at 8.
'             Capture 3: 'sentence' at 12.
'       
'       Match: 'This is another.' at index 22.
'          Group 0: 'This is another.' at index 22.
'             Capture 0: 'This is another.' at 22.
'          Group 1: 'another' at index 30.
'             Capture 0: 'This ' at 22.
'             Capture 1: 'is ' at 27.
'             Capture 2: 'another' at 30.
```

Quando le sottoespressioni vengono utilizzate solo per applicarvi i quantificatori e non è necessario il testo acquisito, è consigliabile disabilitare le acquisizioni del gruppo. Ad esempio, l'elemento del linguaggio **(?:**_subexpression_**)** impedisce al gruppo al quale viene applicato di acquisire le sottostringhe corrispondenti. Nell'esempio seguente il criterio di espressione regolare dell'esempio precedente viene modificato in `\b(?:\w+[;,]?\s?)+[.?!]`. Come illustrato nell'output, il motore delle espressioni regolari non popolerà le raccolte [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) e [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection).

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is one sentence. This is another.";
      string pattern = @"\b(?:\w+[;,]?\s?)+[.?!]";

      foreach (Match match in Regex.Matches(input, pattern)) {
         Console.WriteLine("Match: '{0}' at index {1}.", 
                           match.Value, match.Index);
         int grpCtr = 0;
         foreach (Group grp in match.Groups) {
            Console.WriteLine("   Group {0}: '{1}' at index {2}.",
                              grpCtr, grp.Value, grp.Index);
            int capCtr = 0;
            foreach (Capture cap in grp.Captures) {
               Console.WriteLine("      Capture {0}: '{1}' at {2}.",
                                 capCtr, cap.Value, cap.Index);
               capCtr++;
            }
            grpCtr++;
         }          
         Console.WriteLine();        
      }
   }
}
// The example displays the following output:
//       Match: 'This is one sentence.' at index 0.
//          Group 0: 'This is one sentence.' at index 0.
//             Capture 0: 'This is one sentence.' at 0.
//       
//       Match: 'This is another.' at index 22.
//          Group 0: 'This is another.' at index 22.
//             Capture 0: 'This is another.' at 22.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is one sentence. This is another."
      Dim pattern As String = "\b(?:\w+[;,]?\s?)+[.?!]"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Match: '{0}' at index {1}.", 
                           match.Value, match.Index)
         Dim grpCtr As Integer = 0
         For Each grp As Group In match.Groups
            Console.WriteLine("   Group {0}: '{1}' at index {2}.",
                              grpCtr, grp.Value, grp.Index)
            Dim capCtr As Integer = 0
            For Each cap As Capture In grp.Captures
               Console.WriteLine("      Capture {0}: '{1}' at {2}.",
                                 capCtr, cap.Value, cap.Index)
               capCtr += 1
            Next
            grpCtr += 1
         Next          
         Console.WriteLine()        
      Next    
   End Sub
End Module
' The example displays the following output:
'       Match: 'This is one sentence.' at index 0.
'          Group 0: 'This is one sentence.' at index 0.
'             Capture 0: 'This is one sentence.' at 0.
'       
'       Match: 'This is another.' at index 22.
'          Group 0: 'This is another.' at index 22.
'             Capture 0: 'This is another.' at 22.
```

È possibile disabilitare le acquisizioni in uno dei modi seguenti:

* Usare l'elemento del linguaggio **(?:**_subexpression_**)**. Questo elemento impedisce l'acquisizione delle sottostringhe corrispondenti nel gruppo a cui viene applicato. Non disabilita le acquisizioni delle sottostringhe in tutti i gruppi annidati.

* Usare l'opzione [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture). Disabilita tutte le acquisizioni non denominate o implicite nel modello di espressione regolare. Quando si usa questa opzione, è possibile acquisire solo le sottostringhe che corrispondono ai gruppi denominati definiti con l'elemento del linguaggio **(?<**_name_**>**_subexpression_**)**. Il flag [ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) può essere passato al parametro options di un costruttore di classe [Regex](xref:System.Text.RegularExpressions.Regex) o al parametro options di un metodo di corrispondenza statico [Regex](xref:System.Text.RegularExpressions.Regex).

* Usare l'opzione **n** nell'elemento del linguaggio **(?imnsx)**. Questa opzione disabilita tutte le acquisizioni non denominate o implicite dal punto nel modello di espressione regolare in corrispondenza del quale viene visualizzato l'elemento. Le acquisizioni vengono disabilitate fino alla fine del modello o finché l'opzione **(-n)** non abilita le acquisizioni non denominate o implicite. Per altre informazioni, vedere [Costrutti vari nelle espressioni regolari](miscellaneous.md).

* Usare l'opzione **n** nell'elemento del linguaggio **(?imnsx:**_subexpression_**)**. Questa opzione disabilita tutte le acquisizioni non denominate o implicite in *subexpression*. Vengono inoltre disabilitate tutte le acquisizioni dai gruppi di acquisizione annidati non denominati o impliciti.

## <a name="related-topics"></a>Argomenti correlati

Titolo | Descrizione
----- | ----------- 
[Dettagli sul comportamento delle espressioni regolari](regex-behavior.md) | Viene esaminata l'implementazione del motore delle espressioni regolari in .NET. L'argomento è incentrato sulla flessibilità delle espressioni regolari e sulla responsabilità dello sviluppatore al fine di garantire un funzionamento efficace e affidabile del motore delle espressioni regolari.
[Backtracking nelle espressioni regolari](backtracking.md) | Viene illustrato il backtracking e il modo in cui influisce sulle prestazioni delle espressioni regolari e vengono esaminati gli elementi del linguaggio che forniscono le alternative al backtracking.
[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md) | Vengono illustrati gli elementi del linguaggio delle espressioni regolari in .NET e vengono forniti i collegamenti alla documentazione dettagliata per ogni elemento del linguaggio.
 


