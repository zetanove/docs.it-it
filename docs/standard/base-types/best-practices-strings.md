---
title: Procedure consigliate per l&quot;uso delle stringhe
description: Procedure consigliate per l&quot;uso delle stringhe
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: b3cefaa4-0a3f-4a96-aba9-1de30fb07c29
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 3efd30bade564fe1b7dbf93237a9ff40c58c5f1e

---

# <a name="best-practices-for-using-strings"></a>Procedure consigliate per l'uso delle stringhe

.NET offre un ampio supporto per lo sviluppo di applicazioni localizzate e globalizzate e semplifica l'applicazione delle convenzioni relative alle impostazioni cultura correnti o alle impostazioni cultura specifiche quando si eseguono operazioni comuni come l'ordinamento e la visualizzazione delle stringhe. Tuttavia, l'ordinamento o il confronto delle stringhe non è sempre un'operazione con distinzione delle impostazioni cultura. Ad esempio, le stringhe usate internamente da un'applicazione in genere devono essere gestite in modo identico in tutte le impostazioni cultura. Quando i dati di stringa indipendenti dalle impostazioni cultura, ad esempio i tag XML, i tag HTML, i nomi utente, i percorsi di file e i nomi degli oggetti di sistema, vengono interpretati come dati con distinzione delle impostazioni cultura, nel codice dell'applicazione possono verificarsi bug complessi, riduzioni delle prestazioni e, in alcuni casi, problemi di sicurezza.

Questo articolo esamina i metodi di ordinamento, confronto e utilizzo di maiuscole e minuscole nelle stringhe in .NET, offre delle raccomandazioni per selezionare il metodo di gestione delle stringhe appropriato e fornisce informazioni aggiuntive sui metodi di gestione delle stringhe. Inoltre, esamina come vengono gestiti i file formattati, ad esempio i dati numerici e i dati relativi a data e ora, per la visualizzazione e l'archiviazione. 

In questo articolo sono contenute le sezioni seguenti:

* [Suggerimenti per l'uso delle stringhe](#recommendations-for-string-usage)

* [Specifica esplicita per il confronto tra stringhe](#specifying-string-comparisons-explicitly)

* [Dettagli sul confronto tra stringhe](#the-details-of-string-comparison)

* [Scelta di un membro StringComparison per la chiamata al metodo](#choosing-a-stringcomparison-member-for-your-method-call)

* [Metodi comuni per il confronto tra stringhe](#common-string-comparison-methods)

* [Metodi che eseguono indirettamente il confronto tra stringhe](#methods-that-perform-string-comparison-indirectly)

* [Visualizzazione e conservazione dei dati formattati](#displaying-and-persisting-formatted-data)

## <a name="recommendations-for-string-usage"></a>Suggerimenti per l'uso delle stringhe

Quando si sviluppa con .NET, seguire queste semplici raccomandazione quando si usano le stringhe: 

* Usare gli overload che specificano esplicitamente le regole di confronto tra stringhe per le operazioni di stringa. In genere, questo implica chiamare un overload del metodo con un parametro di tipo [StringComparison](xref:System.StringComparison).

* Usare [StringComparison.Ordinal](xref:System.StringComparison.Ordinal) o [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) per i confronti come valore predefinito sicuro per una corrispondenza tra stringhe indipendente dalla cultura.

* Usare i confronti con [StringComparison.Ordinal](xref:System.StringComparison.Ordinal) o [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) per ottenere prestazioni migliori.

* Usare operazioni di stringa basate su [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture) quando si visualizza l'output all'utente.

* Usare i valori non linguistici [StringComparison.Ordinal](xref:System.StringComparison.Ordinal) o [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) anziché le operazioni di stringa basate su [CultureInfo.InvariantCulture](xref:System.Globalization.CultureInfo.InvariantCulture) quando il confronto non è rilevante linguisticamente, ad esempio è simbolico.

* Usare il metodo [String.ToUpperInvariant](xref:System.String.ToUpperInvariant) anziché il metodo [String.ToLowerInvariant](xref:System.String.ToLowerInvariant) quando si normalizzano le stringhe per il confronto.

* Usare un overload del metodo [String](xref:System.String) `Equals` per controllare se due stringhe sono uguali.

* Usare un overload dei metodi [String](xref:System.String) `Compare` e [String.CompareTo](xref:System.String.CompareTo(System.String)) per ordinare le stringhe senza controllare se sono uguali.

* Usare la formattazione con distinzione delle impostazioni cultura per visualizzare i dati non di tipo stringa, ad esempio numeri e dati, in un'interfaccia utente. Usare la formattazione con la lingua inglese per conservare i dati non di tipo stringa in formato stringa.

Evitare le operazioni seguenti quando si usano le stringhe:

* Non usare overload che non specificano in modo esplicito o implicito le regole di confronto tra stringhe per le operazioni di stringa. 

* Non usare un overload del metodo [String](xref:System.String) `Compare` o [String.CompareTo](xref:System.String.CompareTo(System.String)) ed eseguire un test per il valore restituito zero per determinare se due stringhe sono uguali.

* Non usare la formattazione con distinzione delle impostazioni cultura per conservare i dati numerici o di data e ora in formato stringa.

## <a name="specifying-string-comparisons-explicitly"></a>Specifica esplicita per il confronto tra stringhe

Molti dei metodi di modifica delle stringhe in .NET sono di tipo overload. In genere, uno o più overload accettano le impostazioni predefinite, mentre altri accettano le impostazioni non predefinite, specificando invece una determinata procedura di confronto o modifica delle stringhe. La maggior parte dei metodi che non si basano sulle impostazioni predefinite include un parametro di tipo [StringComparison](xref:System.StringComparison), che corrisponde a un'enumerazione che specifica in modo esplicito le regole per il confronto tra stringhe in base alle impostazioni cultura e alle maiuscole e minuscole. La tabella seguente descrive i membri dell'enumerazione [StringComparison](xref:System.StringComparison). 

Membro StringComparison | Descrizione
----------------------- | -----------
[StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture) | Esegue un confronto con distinzione tra maiuscole e minuscole usando le impostazioni cultura correnti.
[CurrentCultureIgnoreCase](xref:System.StringComparison.CurrentCultureIgnoreCase) | Esegue un confronto senza distinzione tra maiuscole e minuscole usando le impostazioni cultura correnti.
[StringComparison.Ordinal](xref:System.StringComparison.Ordinal) | Esegue un confronto ordinale.
[StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) | Esegue un confronto ordinale senza distinzione tra maiuscole e minuscole.

Ad esempio, il metodo [String](xref:System.String) `IndexOf`, che restituisce l'indice di una sottostringa in un oggetto [String](xref:System.String) che corrisponde a un carattere o a una stringa, ha nove overload:

* [IndexOf(Char)](xref:System.String.IndexOf(System.Char)), [IndexOf(Char, Int32)](xref:System.String.IndexOf(System.Char,System.Int32)) e [IndexOf(Char, Int32, Int32)](xref:System.String.IndexOf(System.Char,System.Int32,System.Int32)), che per impostazione predefinita eseguono una ricerca ordinale (con distinzione tra maiuscole e minuscole e senza distinzione delle impostazioni cultura) per un carattere nella stringa.

* [IndexOf(String)](xref:System.String.IndexOf(System.String)), [IndexOf(String, Int32)](xref:System.String.IndexOf(System.String,System.Int32)) e [IndexOf(String, Int32, Int32)](xref:System.String.IndexOf(System.String,System.Int32,System.Int32)), che per impostazione predefinita eseguono una ricerca con distinzione tra maiuscole e minuscole e con distinzione delle impostazioni cultura per una sottostringa nella stringa.

* [IndexOf(String, StringComparison)](xref:System.String.IndexOf(System.String,System.StringComparison)), [IndexOf(String, Int32, StringComparison)](xref:System.String.IndexOf(System.String,System.Int32,System.StringComparison)) e [IndexOf(String, Int32, Int32, StringComparison)](xref:System.String.IndexOf(System.String,System.Int32,System.Int32,System.StringComparison)), che includono un parametro di tipo StringComparison che consente di specificare il tipo di confronto.

Si consiglia di selezione un overload che non uso i valori predefiniti, per i seguenti motivi:

* Alcuni overload con parametri predefiniti (quelli che cercano [Char](xref:System.Char) nell'istanza della stringa) eseguono un confronto ordinale, mentre altri (quelli che cercano una stringa nell'istanza della stringa) applicano la distinzione delle impostazioni cultura. È difficile ricordare quale valore predefinito viene usato dai diversi metodi ed è facile confondere gli overload.

* Lo scopo del codice basato sui valori predefiniti per le chiamate al metodo non è chiaro. Nell'esempio seguente, che si basa su impostazioni predefinite, è difficile capire se lo sviluppatore intendeva eseguire un confronto ordinale o linguistico tra due stringhe o se la differenza tra maiuscole e minuscole tra `protocol` e "http" può causare la restituzione di `false` nel test di uguaglianza.

  ```csharp
  string protocol = GetProtocol(url);       
  if (String.Equals(protocol, "http", StringComparison.OrdinalIgnoreCase)) {
     // ...Code to handle HTTP protocol.
  }
  else {
     throw new InvalidOperationException();
  }
  ```

  ```vb
  Dim protocol As String = GetProtocol(url)       
  If String.Equals(protocol, "http") Then
    ' ...Code to handle HTTP protocol.
  Else
     Throw New InvalidOperationException()
  End If
  ```

In generale, si consiglia di chiamare un metodo non basato sulle impostazioni predefinite perché disambigua lo scopo del codice. In questo modo, anche il codice diventa più leggibile ed è più facile eseguirne il debug e la manutenzione. L'esempio seguente riguarda le domande relative all'esempio precedente. Viene specificato che viene utilizzato il confronto ordinale e che le differenze tra maiuscole e minuscole vengono ignorate. 

```csharp
string protocol = GetProtocol(url);       
if (String.Equals(protocol, "http", StringComparison.OrdinalIgnoreCase)) {
   // ...Code to handle HTTP protocol.
}
else {
   throw new InvalidOperationException();
}
```

```vb
Dim protocol As String = GetProtocol(url)       
If String.Equals(protocol, "http", StringComparison.OrdinalIgnoreCase) Then
   ' ...Code to handle HTTP protocol.
Else
   Throw New InvalidOperationException()
End If
```

## <a name="the-details-of-string-comparison"></a>Dettagli sul confronto tra stringhe

Il confronto tra stringhe è la base di molte operazioni relative alle stringhe, in particolare l'ordinamento e il test di uguaglianza. L'ordinamento delle stringhe viene eseguito in un modo specifico: se "my" compare prima di "string" in un elenco ordinato di stringhe, nel confronto "my" deve essere minore o uguale a "string". Inoltre, il confronto definisce implicitamente l'uguaglianza. L'operazione di confronto restituisce zero per le stringhe che considera uguali. In altre parole, nessuna stringa viene considerata minore delle altre. Le operazioni più significative relative alle stringhe includono una o più delle seguenti procedure: confronto con un'altra stringa ed esecuzione di un'operazione di ordinamento definita correttamente.

Tuttavia, la valutazione di due stringhe per l'uguaglianza e l'ordinamento non produce un unico risultato corretto; l'esito dipende dai criteri usati per il confronto delle stringhe. In particolare, i confronti tra stringhe ordinali o basati sulle convenzioni di utilizzo di maiuscole e minuscole e di ordinamento delle impostazioni cultura correnti o della lingua inglese (impostazioni indipendenti dalle impostazioni cultura basate sulla lingua inglese) possono produrre risultati diversi.

### <a name="string-comparisons-that-use-the-current-culture"></a>Confronti tra stringhe che usano le impostazioni cultura correnti

Un criterio prevede l'uso delle convenzioni delle impostazioni cultura correnti quando si confrontano le stringhe. I confronti basati sulle impostazioni cultura correnti usano le impostazioni cultura o le impostazioni locali correnti del thread. È necessario usare sempre i confronti basati sulle impostazioni cultura correnti quando i dati sono linguisticamente rilevanti e quando riflettono un'interazione utente con distinzione delle impostazioni cultura. 

Tuttavia, il comportamento di confronto e di utilizzo di maiuscole e minuscole in .NET cambia quando vengono modificate le impostazioni cultura. Ciò accade quando un'applicazione viene eseguita in un computer con impostazioni cultura diverse da quelle del computer in cui è stata sviluppata oppure quando il thread di esecuzione modifica le proprie impostazioni cultura. Questo comportamento è intenzionale, tuttavia resta poco chiaro per molti sviluppatori. L'esempio seguente illustra le differenze nell'ordinamento tra le impostazioni cultura della lingua inglese per gli Stati Uniti ("en-US") e di quella svedese ("sv-SE"). Si noti che le parole "ångström", "Windows" e "Visual Studio" vengono visualizzate in posizioni diverse nelle matrici di stringhe ordinate.

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string[] values= { "able", "ångström", "apple", "Æble", 
                         "Windows", "Visual Studio" };
      Array.Sort(values);
      DisplayArray(values);

      // Change culture to Swedish (Sweden).
      string originalCulture = CultureInfo.CurrentCulture.Name;
      Thread.CurrentThread.CurrentCulture = new CultureInfo("sv-SE");
      Array.Sort(values);
      DisplayArray(values);

      // Restore the original culture.
      Thread.CurrentThread.CurrentCulture = new CultureInfo(originalCulture);
    }

    private static void DisplayArray(string[] values)
    {
      Console.WriteLine("Sorting using the {0} culture:",  
                        CultureInfo.CurrentCulture.Name);
      foreach (string value in values)
         Console.WriteLine("   {0}", value);

      Console.WriteLine();
    }
}
// The example displays the following output:
//       Sorting using the en-US culture:
//          able
//          Æble
//          ångström
//          apple
//          Visual Studio
//          Windows
//       
//       Sorting using the sv-SE culture:
//          able
//          Æble
//          apple
//          Windows
//          Visual Studio
//          ångström
```

```vb
Imports System.Globalization
Imports System.Threading

Module Example
   Public Sub Main()
      Dim values() As String = { "able", "ångström", "apple", _
                                 "Æble", "Windows", "Visual Studio" }
      Array.Sort(values)
      DisplayArray(values)

      ' Change culture to Swedish (Sweden).
      Dim originalCulture As String = CultureInfo.CurrentCulture.Name
      Thread.CurrentThread.CurrentCulture = New CultureInfo("sv-SE")
      Array.Sort(values)
      DisplayArray(values)

      ' Restore the original culture.
      Thread.CurrentThread.CurrentCulture = New CultureInfo(originalCulture)
    End Sub

    Private Sub DisplayArray(values() As String)
      Console.WRiteLine("Sorting using the {0} culture:", _ 
                        CultureInfo.CurrentCulture.Name)
      For Each value As String In values
         Console.WriteLine("   {0}", value)
      Next
      Console.WriteLine()   
    End Sub
End Module
' The example displays the following output:
'       Sorting using the en-US culture:
'          able
'          Æble
'          ångström
'          apple
'          Visual Studio
'          Windows
'       
'       Sorting using the sv-SE culture:
'          able
'          Æble
'          apple
'          Windows
'          Visual Studio
'          ångström
```

I confronti senza distinzione tra maiuscole e minuscole che usano le impostazioni cultura correnti sono uguali a quelli con distinzione delle impostazioni cultura, ma ignorano la distinzione tra maiuscole e minuscole come indicato dalle impostazioni cultura correnti del thread. Questo comportamento può manifestarsi anche negli ordinamenti. 

I confronti che usano la semantica delle impostazioni cultura correnti sono i confronti predefiniti per i seguenti metodi:

* Overload di [String](xref:System.String) `Compare` che non includono un parametro [StringComparison](xref:System.StringComparison).

* Overload di [String.CompareTo](xref:System.String.CompareTo(System.String)).

* Metodo [String.StartsWith(String)](xref:System.String.StartsWith(System.String)) predefinito. 

* Metodo [String.EndsWith(String)](xref:System.String.EndsWith(System.String)) predefinito.

* Overload di [String](xref:System.String) `IndexOf` che accettano [String](xref:System.String) come parametro di ricerca e non includono un parametro [StringComparison](xref:System.StringComparison).

* Overload di [String](xref:System.String) `LastIndexOf` che accettano [String](xref:System.String) come parametro di ricerca e non includono un parametro [StringComparison](xref:System.StringComparison).

In ogni caso, si consiglia di chiamare un overload con il parametro [StringComparison](xref:System.StringComparison) per rendere chiaro lo scopo della chiamata al metodo. 

È possibile che vengano generati bug complessi e meno complessi quando i dati non linguistici della stringa vengono interpretati linguisticamente oppure quando i dati della stringa di specifiche impostazioni cultura vengono interpretati usando le convenzioni di altre impostazioni cultura. L'esempio canonico è il problema della I turca.

Per quasi tutti gli alfabeti latini, incluso l'inglese (Stati Uniti), il carattere "i" (\u0069) corrisponde alla versione minuscola del carattere "I" (\u0049). Questa regola di utilizzo di maiuscole e minuscole diventa rapidamente l'impostazione predefinita per chi programma queste impostazioni cultura. Tuttavia, l'alfabeto turco ("tr-TR") include una "I con punto", "İ" (\u0130), che è la versione maiuscola di "i". L'alfabeto turco include anche una "i senza punto" minuscola, "ı" (\u0131), la cui versione maiuscola è "I". Questo comportamento si verifica anche con le impostazioni cultura azera ("az").

Pertanto, i presupposti relativi all'uso della maiuscola per "i" o della minuscola per "I" non sono validi in tutte le impostazioni cultura. Se si usano gli overload predefiniti per le routine di confronto tra stringhe, questi saranno soggetti a variazioni tra le diverse impostazioni cultura. Se i dati da confrontare sono di tipo non linguistico, l'uso degli overload predefiniti può produrre risultati indesiderati, come illustrato in questo tentativo di eseguire un confronto senza distinzione tra maiuscole e minuscole delle stringhe "file" e "FILE".

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string fileUrl = "file";
      Thread.CurrentThread.CurrentCulture = new CultureInfo("en-US");
      Console.WriteLine("Culture = {0}",
                        Thread.CurrentThread.CurrentCulture.DisplayName);
      Console.WriteLine("(file == FILE) = {0}", 
                       fileUrl.StartsWith("FILE", true, null));
      Console.WriteLine();

      Thread.CurrentThread.CurrentCulture = new CultureInfo("tr-TR");
      Console.WriteLine("Culture = {0}",
                        Thread.CurrentThread.CurrentCulture.DisplayName);
      Console.WriteLine("(file == FILE) = {0}", 
                        fileUrl.StartsWith("FILE", true, null));
   }
}
// The example displays the following output:
//       Culture = English (United States)
//       (file == FILE) = True
//       
//       Culture = Turkish (Turkey)
//       (file == FILE) = False
```

```vb
Imports System.Globalization
Imports System.Threading

Module Example
   Public Sub Main()
      Dim fileUrl = "file"
      Thread.CurrentThread.CurrentCulture = New CultureInfo("en-US")
      Console.WriteLine("Culture = {0}", _
                        Thread.CurrentThread.CurrentCulture.DisplayName)
      Console.WriteLine("(file == FILE) = {0}", _ 
                       fileUrl.StartsWith("FILE", True, Nothing))
      Console.WriteLine()

      Thread.CurrentThread.CurrentCulture = New CultureInfo("tr-TR")
      Console.WriteLine("Culture = {0}", _
                        Thread.CurrentThread.CurrentCulture.DisplayName)
      Console.WriteLine("(file == FILE) = {0}", _ 
                        fileUrl.StartsWith("FILE", True, Nothing))
   End Sub
End Module
' The example displays the following output:
'       Culture = English (United States)
'       (file == FILE) = True
'       
'       Culture = Turkish (Turkey)
'       (file == FILE) = False
```

Questo confronto può causare problemi significativi se le impostazioni cultura vengono usate inavvertitamente in impostazioni relative alla sicurezza, come nel seguente esempio. Una chiamata al metodo come `IsFileURI("file:")` restituisce `true`, se le impostazioni cultura correnti sono per la lingua inglese (Stati Uniti) oppure `false` se le impostazioni cultura correnti sono per la lingua turca. Quindi, nei sistemi turchi, qualcuno potrebbe aggirare le misure di sicurezza che bloccano l'accesso agli URI senza distinzione tra maiuscole e minuscole che iniziano con "FILE:".

```csharp
public static bool IsFileURI(String path) 
{
   return path.StartsWith("FILE:", true, null);
}
```

```vb
Public Shared Function IsFileURI(path As String) As Boolean 
   Return path.StartsWith("FILE:", True, Nothing)
End Function
```

In questo caso, poiché "file:" deve essere interpretato come un identificatore non linguistico e senza distinzione delle impostazioni cultura, il codice deve essere scritto come mostrato nell'esempio seguente.

```csharp
public static bool IsFileURI(string path) 
{
   return path.StartsWith("FILE:", StringComparison.OrdinalIgnoreCase);
}
```

```vb
Public Shared Function IsFileURI(path As String) As Boolean 
    Return path.StartsWith("FILE:", StringComparison.OrdinalIgnoreCase)
End Function
```

## <a name="ordinal-string-operations"></a>Operazioni di stringa ordinali

La specifica del valore [StringComparison.Ordinal](xref:System.StringComparison.Ordinal) o [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) in una chiamata al metodo indica un confronto non linguistico in cui le funzionalità dei linguaggi naturali vengono ignorate. I metodi richiamati con questi valori [StringComparison](xref:System.StringComparison) basano le decisioni relative alle operazioni di stringa su confronti di byte semplici invece che sull'utilizzo di maiuscole e minuscole o di tabelle di equivalenza parametrizzate dalle impostazioni cultura. In molti casi, questo approccio risulta più adatto per l'interpretazione desiderata delle stringhe e rende il codice più veloce e affidabile. 

I confronti ordinali sono confronti tra stringhe in cui ogni byte di ogni stringa viene confrontato senza interpretazione linguistica, ad esempio "windows" non corrisponde a "Windows". Usare questo confronto quando il contesto impone l'esatta corrispondenza delle stringhe o richiede un criterio di corrispondenza conservativo. Inoltre, il confronto ordinale è l'operazione di confronto più rapida perché non applica regole linguistiche quando determina un risultato.

Le stringhe in .NET possono contenere caratteri null incorporati. Una delle differenze più evidenti tra il confronto ordinale e quello con distinzione delle impostazioni cultura (inclusi i confronti che usano la lingua inglese) riguarda la gestione dei caratteri null incorporati in una stringa. Questi caratteri vengono ignorati quando si usano i metodi [String](xref:System.String) `Compare` e [String](xref:System.String) `Equals` per eseguire confronti con distinzione delle impostazioni cultura, inclusi i confronti che usano le impostazioni cultura per la lingua inglese. Di conseguenza, nei confronti con distinzione delle impostazioni cultura, le stringhe che contengono caratteri null incorporati e quelle che non li contengono possono essere considerate uguali. 

> [!IMPORTANT]
> Sebbene i metodi di confronto tra stringhe ignorino i caratteri null incorporati, i metodi di ricerca delle stringhe, ad esempio [String.Contains](xref:System.String.Contains(System.String)), [String.EndsWith](xref:System.String.EndsWith(System.String)), [String.IndexOf](xref:System.String.IndexOf(System.Char)), [String.LastIndexOf](xref:System.String.LastIndexOf(System.String)) e [String.StartsWith](xref:System.String.StartsWith(System.String)) non li ignorano. 

L'esempio successivo esegue un confronto con distinzione delle impostazioni cultura della stringa "Aa" con una stringa simile che contiene diversi caratteri null incorporati tra "A" e "a" e mostra in che modo le due stringhe vengono considerate uguali.. 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string str1 = "Aa";
      string str2 = "A" + new String('\u0000', 3) + "a";
      Console.WriteLine("Comparing '{0}' ({1}) and '{2}' ({3}):", 
                        str1, ShowBytes(str1), str2, ShowBytes(str2));
      Console.WriteLine("   With String.Compare:");
      Console.WriteLine("      Current Culture: {0}", 
                        String.Compare(str1, str2, StringComparison.CurrentCulture));
      Console.WriteLine("      Invariant Culture: {0}", 
                        String.Compare(str1, str2, StringComparison.InvariantCulture));

      Console.WriteLine("   With String.Equals:");
      Console.WriteLine("      Current Culture: {0}", 
                        String.Equals(str1, str2, StringComparison.CurrentCulture));
      Console.WriteLine("      Invariant Culture: {0}", 
                        String.Equals(str1, str2, StringComparison.InvariantCulture));
   }

   private static string ShowBytes(string str)
   {
      string hexString = String.Empty;
      for (int ctr = 0; ctr < str.Length; ctr++)
      {
         string result = String.Empty;
         result = Convert.ToInt32(str[ctr]).ToString("X4");
         result = " " + result.Substring(0,2) + " " + result.Substring(2, 2);
         hexString += result;
      }
      return hexString.Trim();
   }
}
// The example displays the following output:
//    Comparing 'Aa' (00 41 00 61) and 'A   a' (00 41 00 00 00 00 00 00 00 61):
//       With String.Compare:
//          Current Culture: 0
//          Invariant Culture: 0
//       With String.Equals:
//          Current Culture: True
//          Invariant Culture: True
```

```vb
Module Example
   Public Sub Main()
      Dim str1 As String = "Aa"
      Dim str2 As String = "A" + New String(Convert.ToChar(0), 3) + "a"
      Console.WriteLine("Comparing '{0}' ({1}) and '{2}' ({3}):", _
                        str1, ShowBytes(str1), str2, ShowBytes(str2))
      Console.WriteLine("   With String.Compare:")
      Console.WriteLine("      Current Culture: {0}", _
                        String.Compare(str1, str2, StringComparison.CurrentCulture))
      Console.WriteLine("      Invariant Culture: {0}", _
                        String.Compare(str1, str2, StringComparison.InvariantCulture))

      Console.WriteLine("   With String.Equals:")
      Console.WriteLine("      Current Culture: {0}", _
                        String.Equals(str1, str2, StringComparison.CurrentCulture))
      Console.WriteLine("      Invariant Culture: {0}", _
                        String.Equals(str1, str2, StringComparison.InvariantCulture))
   End Sub

   Private Function ShowBytes(str As String) As String
      Dim hexString As String = String.Empty
      For ctr As Integer = 0 To str.Length - 1
         Dim result As String = String.Empty
         result = Convert.ToInt32(str.Chars(ctr)).ToString("X4")
         result = " " + result.Substring(0,2) + " " + result.Substring(2, 2)
         hexString += result
      Next
      Return hexString.Trim()
   End Function
End Module
```

Tuttavia, le stringhe non sono considerate uguali quando si usa il confronto ordinale, come mostrato nell'esempio seguente.

```csharp
Console.WriteLine("Comparing '{0}' ({1}) and '{2}' ({3}):", 
                  str1, ShowBytes(str1), str2, ShowBytes(str2));
Console.WriteLine("   With String.Compare:");
Console.WriteLine("      Ordinal: {0}", 
                  String.Compare(str1, str2, StringComparison.Ordinal));

Console.WriteLine("   With String.Equals:");
Console.WriteLine("      Ordinal: {0}", 
                  String.Equals(str1, str2, StringComparison.Ordinal));
// The example displays the following output:
//    Comparing 'Aa' (00 41 00 61) and 'A   a' (00 41 00 00 00 00 00 00 00 61):
//       With String.Compare:
//          Ordinal: 97
//       With String.Equals:
//          Ordinal: False
```

```vb
Console.WriteLine("Comparing '{0}' ({1}) and '{2}' ({3}):", _
                  str1, ShowBytes(str1), str2, ShowBytes(str2))
Console.WriteLine("   With String.Compare:")
Console.WriteLine("      Ordinal: {0}", _
                  String.Compare(str1, str2, StringComparison.Ordinal))

Console.WriteLine("   With String.Equals:")
Console.WriteLine("      Ordinal: {0}", _
                  String.Equals(str1, str2, StringComparison.Ordinal))
' The example displays the following output:
'    Comparing 'Aa' (00 41 00 61) and 'A   a' (00 41 00 00 00 00 00 00 00 61):
'       With String.Compare:
'          Ordinal: 97
'       With String.Equals:
'          Ordinal: False
```

I confronti ordinali senza distinzione tra maiuscole e minuscole rappresentano il secondo approccio più conservativo. Questi confronti ignorano quasi del tutto l'utilizzo di maiuscole e minuscole, ad esempio "windows" corrisponde a "Windows". Quando si usano i caratteri ASCII, questo criterio è equivalente a [StringComparison.Ordinal](xref:System.StringComparison.Ordinal), ma ignora il normale utilizzo di maiuscole e minuscole ASCII. Quindi, qualsiasi carattere in [A, Z] (\u0041-\u005A) corrisponde al carattere corrispondente in [a,z] (\u0061-\007A). L'utilizzo di maiuscole e minuscole al di fuori dell'intervallo ASCII usa le tabelle in lingua inglese. Pertanto, il confronto seguente:

```csharp
String.Compare(strA, strB, StringComparison.OrdinalIgnoreCase);
```

```vb
String.Compare(strA, strB, StringComparison.OrdinalIgnoreCase)
```

è equivalente (ma più rapido) rispetto al confronto: 

```csharp
String.Compare(strA.ToUpperInvariant(), strB.ToUpperInvariant(), 
               StringComparison.Ordinal);
```

```vb
String.Compare(strA.ToUpperInvariant(), strB.ToUpperInvariant(), 
               StringComparison.Ordinal)
```

Questi confronti sono comunque molto rapidi.

[StringComparison.Ordinal](xref:System.StringComparison.Ordinal) e [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) usano entrambi direttamente i valori binari e sono più adatti per la corrispondenza. Se non si è sicuri delle impostazioni di confronto, usare uno di questi due valori. Tuttavia, poiché eseguono un confronto byte per byte, l'ordinamento non viene eseguito linguisticamente (come in un dizionario inglese), ma in modo binario. Se visualizzati dagli utenti, i risultati possono sembrare strani in molti contesti.

La semantica ordinale è l'impostazione predefinita per gli overload [String](xref:System.String) `Equals` che non includono un argomento [StringComparison](xref:System.StringComparison) (incluso l'operatore di uguaglianza). In ogni caso, si consiglia di chiamare un overload con un parametro [StringComparison](xref:System.StringComparison).

### <a name="string-operations-that-use-the-invariant-culture"></a>Operazioni di stringa che usano impostazioni cultura non dipendenti da paese/area geografica

I confronti con le impostazioni cultura per la lingua inglese usano la proprietà [CompareInfo](xref:System.Globalization.CompareInfo) restituita dalla proprietà statica [CultureInfo.InvariantCulture](xref:System.Globalization.CultureInfo.InvariantCulture). Questo comportamento è uguale in tutti i sistemi. Converte i caratteri al di fuori dell'intervallo in quelli che considera caratteri equivalenti in lingua inglese. Questo criterio può essere utile per gestire il comportamento di un set di stringhe nelle impostazioni cultura, ma spesso produce risultati imprevisti.

I confronti senza distinzione tra maiuscole e minuscole con le impostazioni cultura per la lingua inglese usano la proprietà statica [CompareInfo](xref:System.Globalization.CompareInfo) restituita dalla proprietà statica [CultureInfo.InvariantCulture](xref:System.Globalization.CultureInfo.InvariantCulture) anche per le informazioni sul confronto. Le differenze tra maiuscole e minuscole in questi caratteri convertiti vengono ignorate.

L'oggetto [CultureInfo.InvariantCulture](xref:System.Globalization.CultureInfo.InvariantCulture) fa sì che il metodo [String](xref:System.String) `Compare` interpreti alcuni set di caratteri come equivalenti. Ad esempio, la seguente equivalenza è valida in lingua inglese:

InvariantCulture: a + ̊ = å

La lettera A minuscola latina "a" (\u0061) quando si trova accanto al carattere cerchio in alto "+ " ̊" (\u030a) viene interpretata come lettera A minuscola latina con il carattere cerchio in alto "å" (\u00e5). Come mostrato nell'esempio seguente, questo comportamento è diverso dal confronto ordinale.

```csharp
string separated = "\u0061\u030a";
string combined = "\u00e5";

Console.WriteLine("Equal sort weight of {0} and {1} using InvariantCulture: {2}",
                  separated, combined, 
                  String.Compare(separated, combined, 
                                 StringComparison.InvariantCulture) == 0);

Console.WriteLine("Equal sort weight of {0} and {1} using Ordinal: {2}",
                  separated, combined,
                  String.Compare(separated, combined, 
                                 StringComparison.Ordinal) == 0);
// The example displays the following output:
//    Equal sort weight of a° and å using InvariantCulture: True
//    Equal sort weight of a° and å using Ordinal: False 
```

```vb
Dim separated As String = ChrW(&h61) + ChrW(&h30a)
Dim combined As String = ChrW(&he5)

Console.WriteLine("Equal sort weight of {0} and {1} using InvariantCulture: {2}", _
                  separated, combined, _
                  String.Compare(separated, combined, _ 
                                 StringComparison.InvariantCulture) = 0)

Console.WriteLine("Equal sort weight of {0} and {1} using Ordinal: {2}", _
                  separated, combined, _
                  String.Compare(separated, combined, _
                                 StringComparison.Ordinal) = 0)
' The example displays the following output:
'    Equal sort weight of a° and å using InvariantCulture: True
'    Equal sort weight of a° and å using Ordinal: False
```

Quando si interpretano i nomi di file, i cookie o qualsiasi altro elemento che può contenere un carattere come "å", i confronti ordinali offrono il comportamento più trasparente e appropriato.

In realtà la lingua inglese ha poche proprietà che la rendono utile per il confronto. Esegue il confronto in un modo linguisticamente rilevante, che non assicura un'equivalenza simbolica completa, ma non rappresenta la scelta ottimale per la visualizzazione nelle impostazioni cultura. Ad esempio, se un file di dati di grandi dimensioni che contiene un elenco di identificatori ordinati per la visualizzazione viene associato a un'applicazione, per aggiungere elementi all'elenco è necessario l'inserimento con un ordinamento in lingua inglese.

## <a name="choosing-a-stringcomparison-member-for-your-method-call"></a>Scelta di un membro StringComparison per la chiamata al metodo

La tabella seguente mostra il mapping da un contesto di stringhe semantico a un membro dell'enumerazione [StringComparison](xref:System.StringComparison).

Dati | Comportamento | Valore System.StringComparison corrispondente
---- | -------- | -------------------------------------------
Identificatori interni con distinzione tra maiuscole e minuscole, identificatori con distinzione tra maiuscole e minuscole in standard come XML e HTTP o impostazioni di sicurezza con distinzione tra maiuscole e minuscole. | Identificatore non linguistico, con una corrispondenza esatta dei byte. | [StringComparison.Ordinal](xref:System.StringComparison.Ordinal)
Identificatori interni senza distinzione tra maiuscole e minuscole, identificatori senza distinzione tra maiuscole e minuscole in standard come XML e HTTP, percorsi di file, chiavi e valori del Registro di sistema, variabili di ambiente, identificatori di risorse, ad esempio nomi di handle o impostazioni di sicurezza senza distinzione tra maiuscole e minuscole. | Identificatore non linguistico, indipendente dalla distinzione tra maiuscole e minuscole. | [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase)
Dati visualizzati all'utente o maggior parte dell'input utente. | Dati che richiedono personalizzazioni linguistiche locali. | [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture) o [CurrentCultureIgnoreCase](xref:System.StringComparison.CurrentCultureIgnoreCase)

## <a name="common-string-comparison-methods"></a>Metodi comuni per il confronto tra stringhe

Le sezioni seguenti descrivono i metodi più comuni per il confronto tra stringhe.

### <a name="stringcompare"></a>String.Compare

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

Poiché si tratta dell'operazione più importante per l'interpretazione della stringa, tutte le istanze di queste chiamate al metodo devono essere esaminate per determinare se le stringhe devono essere interpretate in base alle impostazioni cultura correnti o devono essere dissociate dalle impostazioni cultura (simbolicamente). In genere, si tratta del secondo caso e deve pertanto essere usato un confronto [StringComparison.Ordinal](xref:System.StringComparison.Ordinal).

La classe [System.Globalization.CompareInfo](xref:System.Globalization.CompareInfo), restituita dalla proprietà [CultureInfo.CompareInfo](xref:System.Globalization.CultureInfo.CompareInfo), include anche un metodo [Compare](xref:System.Globalization.CompareInfo.Compare(System.String,System.Int32,System.String,System.Int32,System.Globalization.CompareOptions)) che offre numerose opzioni di corrispondenza (ordinale, con esclusione degli spazi vuoti, con esclusione del tipo Kana e così via) mediante l'enumerazione flag [CompareOptions](xref:System.Globalization.CompareOptions). 

### <a name="stringcompareto"></a>String.CompareTo

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

Questo metodo attualmente non offre un overload che specifica un tipo [StringComparison](xref:System.StringComparison). In genere è possibile convertire questo metodo nel tipo consigliato [String.Compare(String, String, StringComparison)](xref:System.String.Compare(System.String,System.String,System.StringComparison)).

I tipi che implementano le interfacce [IComparable](xref:System.IComparable) e [IComparable&lt;T&gt;](xref:System.IComparable%601) implementano questo metodo. Poiché non offre l'opzione di un parametro [StringComparison](xref:System.StringComparison), l'implementazione dei tipi spesso lascia specificare all'utente [StringComparer](xref:System.StringComparer) nel proprio costruttore. L'esempio seguente definisce una classe `FileName` il cui costruttore include un parametro [StringComparer](xref:System.StringComparer). L'oggetto [StringComparer](xref:System.StringComparer) viene quindi usato nel metodo `FileName.CompareTo`.

```csharp
using System;

public class FileName : IComparable
{
   string fname;
   StringComparer comparer; 

   public FileName(string name, StringComparer comparer)
   {
      if (String.IsNullOrEmpty(name))
         throw new ArgumentNullException("name");

      this.fname = name;

      if (comparer != null)
         this.comparer = comparer;
      else
         this.comparer = StringComparer.OrdinalIgnoreCase;
   }

   public string Name
   {
      get { return fname; }
   }

   public int CompareTo(object obj)
   {
      if (obj == null) return 1;

      if (! (obj is FileName))
         return comparer.Compare(this.fname, obj.ToString());
      else
         return comparer.Compare(this.fname, ((FileName) obj).Name);
   }
}
```

```vb
Public Class FileName : Implements IComparable
   Dim fname As String
   Dim comparer As StringComparer 

   Public Sub New(name As String, comparer As StringComparer)
      If String.IsNullOrEmpty(name) Then
         Throw New ArgumentNullException("name")
      End If

      Me.fname = name

      If comparer IsNot Nothing Then
         Me.comparer = comparer
      Else
         Me.comparer = StringComparer.OrdinalIgnoreCase
      End If      
   End Sub

   Public ReadOnly Property Name As String
      Get
         Return fname
      End Get   
   End Property

   Public Function CompareTo(obj As Object) As Integer _
          Implements IComparable.CompareTo
      If obj Is Nothing Then Return 1

      If Not TypeOf obj Is FileName Then
         obj = obj.ToString()
      Else
         obj = CType(obj, FileName).Name
      End If         
      Return comparer.Compare(Me.fname, obj)
   End Function
End Class
```

### <a name="stringequals"></a>String.Equals

Interpretazione predefinita: [StringComparison.Ordinal](xref:System.StringComparison.Ordinal).

La classe [String](xref:System.String) consente di eseguire un test di uguaglianza chiamando gli overload del metodo `Equals` dell'istanza o statici oppure usando l'operatore di uguaglianza statico. Gli overload e l'operatore usano il confronto ordinale per impostazione predefinita. Tuttavia, si consiglia di chiamare comunque un overload che specifichi esplicitamente il tipo [StringComparison](xref:System.StringComparison) anche se si vuole eseguire un confronto ordinale; questo semplifica la ricerca di codice per una determinata interpretazione della stringa. 

### <a name="stringtoupper-and-stringtolower"></a>String.ToUpper e String.ToLower

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

Prestare attenzione quando si usano questi metodi perché l'utilizzo forzato di maiuscole o minuscole in una stringa è una procedura usata spesso come normalizzazione minore per confrontare stringhe indipendentemente dalla distinzione tra maiuscole e minuscole. In questo caso, valutare l'uso di un confronto senza distinzione tra maiuscole e minuscole. 

Sono anche disponibili i metodi [String.ToUpperInvariant](xref:System.String.ToUpperInvariant) e [String.ToLowerInvariant](xref:System.String.ToLowerInvariant). [ToUpperInvariant](xref:System.String.ToUpperInvariant) è la modalità standard di normalizzazione dei caratteri maiuscoli e minuscoli. A livello di comportamento, i confronti eseguiti usando [StringComparison.OrdinalIgnoreCase](xref:System.StringComparison.OrdinalIgnoreCase) corrispondono alla composizione di due chiamate: la chiamata a [ToUpperInvariant](xref:System.String.ToUpperInvariant) in entrambi gli argomenti di stringa e l'esecuzione di un confronto con [StringComparison.Ordinal](xref:System.StringComparison.Ordinal).

Sono disponibili anche overload per la conversione in maiuscole e minuscole in determinate impostazioni cultura, passando un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le specifiche impostazioni cultura al metodo.

### <a name="chartoupper-and-chartolower"></a>Char.ToUpper e Char.ToLower

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

Questi metodi funzionano in modo simile ai metodi [String.ToUpper](xref:System.String.ToUpper) e [String.ToLower](xref:System.String.ToLower) descritti nella sezione precedente.

### <a name="stringstartswith-and-stringendswith"></a>String.StartsWith e String.EndsWith

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

Per impostazione predefinita, entrambi i metodi eseguono un confronto con distinzione delle impostazioni cultura.

### <a name="stringindexof-and-stringlastindexof"></a>String.IndexOf e String.LastIndexOf

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

La modalità di esecuzione dei confronti con gli overload predefiniti di questi metodi manca di coerenza. Tutti i metodi [String](xref:System.String) `IndexOf` e [String](xref:System.String) `LastIndexOf` che includono un parametro [Char](xref:System.Char) eseguono un confronto ordinale, ma i metodi predefiniti [String](xref:System.String) `IndexOf` e [String`](xref:System.String) `LastIndexOf` che includono un parametro [String](xref:System.String) eseguono un confronto con distinzione delle impostazioni cultura. 

Se si chiama il metodo ` `IndexOf` or `LastIndexOf` e si passa una stringa da individuare nell'istanza corrente, si consiglia di chiamare un overload che specifichi esplicitamente il tipo [StringComparison](xref:System.StringComparison). Gli overload che includono un argomento [Char](xref:System.Char) non consentono di specificare un tipo [StringComparison](xref:System.StringComparison).

## <a name="methods-that-perform-string-comparison-indirectly"></a>Metodi che eseguono indirettamente il confronto tra stringhe

Alcuni metodi non di tipo stringa in cui il confronto tra stringhe rappresenta l'operazione più importante usano il tipo [StringComparer](xref:System.StringComparer). La classe [StringComparer](xref:System.StringComparer) include quattro proprietà statiche che restituiscono istanze [StringComparer](xref:System.StringComparer) i cui metodi `Compare` eseguono i tipi di confronto tra stringhe seguenti:

* Confronti tra stringhe con distinzione delle impostazioni cultura usando le impostazioni cultura correnti. Questo oggetto [StringComparer](xref:System.StringComparer) è restituito dalla proprietà [StringComparer.CurrentCulture](xref:System.StringComparer.CurrentCulture).

* Confronti senza distinzione tra maiuscole e minuscole usando le impostazioni cultura correnti. Questo oggetto [StringComparer](xref:System.StringComparer) è restituito dalla proprietà [StringComparer.CurrentCultureIgnoreCase](xref:System.StringComparer.CurrentCultureIgnoreCase).

* Confronto ordinale. Questo oggetto [StringComparer](xref:System.StringComparer) è restituito dalla proprietà [StringComparer.Ordinal](xref:System.StringComparer.Ordinal). 

* Confronto ordinale senza distinzione tra maiuscole e minuscole. Questo oggetto [StringComparer](xref:System.StringComparer) è restituito dalla proprietà [StringComparer.OrdinalIgnoreCase](xref:System.StringComparer.OrdinalIgnoreCase).

### <a name="arraysort-and-arraybinarysearch"></a>Array.Sort e Array.BinarySearch

Interpretazione predefinita: [StringComparison.CurrentCulture](xref:System.StringComparison.CurrentCulture).

Quando si archiviano dati in una raccolta o si leggono dati persistenti da un file o da un database nella raccolta, la modifica delle impostazioni cultura correnti può invalidare le invarianti nella raccolta. Il metodo [Array.BinarySearch](xref:System.Array.BinarySearch(System.Array,System.Object)) presuppone che gli elementi nella matrice da cercare siano già ordinati. Per ordinare qualsiasi elemento di tipo stringa nella matrice, il metodo [Array.Sort](xref:System.Array.Sort(System.Array)) chiama il metodo [String] `Compare` per ordinare i singoli elementi. L'uso di un operatore di confronto con distinzione delle impostazioni cultura può essere pericoloso se le impostazioni cultura vengono modificate tra l'ordinamento della matrice e la ricerca dei contenuti. Nel codice seguente, ad esempio, le operazioni di archiviazione e recupero vengono eseguite nell'operatore di confronto fornito in modo implicito dalla proprietà `Thread.CurrentThread.CurrentCulture`. Se le impostazioni cultura possono cambiare tra le chiamate a `StoreNames` e `DoesNameExist` e, in particolare, se il contenuto della matrice viene conservato tra le due chiamate al metodo, è possibile che la ricerca binaria non riesca. 

```csharp
// Incorrect.
string []storedNames;

public void StoreNames(string [] names)
{
   int index = 0;
   storedNames = new string[names.Length];

   foreach (string name in names)
   {
      this.storedNames[index++] = name;
   }

   Array.Sort(names); // Line A.
}

public bool DoesNameExist(string name)
{
   return (Array.BinarySearch(this.storedNames, name) >= 0);  // Line B.
}
```

```vb
' Incorrect.
Dim storedNames() As String

Public Sub StoreNames(names() As String)
   Dim index As Integer = 0
   ReDim storedNames(names.Length - 1)

   For Each name As String In names
      Me.storedNames(index) = name
      index+= 1
   Next

   Array.Sort(names)          ' Line A.
End Sub

Public Function DoesNameExist(name As String) As Boolean
   Return Array.BinarySearch(Me.storedNames, name) >= 0      ' Line B.
End Function
```

L'esempio seguente mostra una variazione consigliata che usa lo stesso metodo di confronto ordinale (senza distinzione delle impostazioni cultura) sia per l'ordinamento che per la ricerca nella matrice. Il codice modificato si riflette nelle righe identificate con `Line A` e `Line B` nei due esempi.

```csharp
// Correct.
string []storedNames;

public void StoreNames(string [] names)
{
   int index = 0;
   storedNames = new string[names.Length];

   foreach (string name in names)
   {
      this.storedNames[index++] = name;
   }

   Array.Sort(names, StringComparer.Ordinal);  // Line A.
}

public bool DoesNameExist(string name)
{
   return (Array.BinarySearch(this.storedNames, name, StringComparer.Ordinal) >= 0);  // Line B.
}
```

```vb
' Correct.
Dim storedNames() As String

Public Sub StoreNames(names() As String)
   Dim index As Integer = 0
   ReDim storedNames(names.Length - 1)

   For Each name As String In names
      Me.storedNames(index) = name
      index+= 1
   Next

   Array.Sort(names, StringComparer.Ordinal)           ' Line A.
End Sub

Public Function DoesNameExist(name As String) As Boolean
   Return Array.BinarySearch(Me.storedNames, name, StringComparer.Ordinal) >= 0      ' Line B.
End Function
```

Se i dati vengono conservati e spostati nelle impostazioni cultura e l'ordinamento viene usato per presentare i dati all'utente, potrebbe esser opportuno usare `StringComparison.InvariantCulture`, che garantisce un output utente migliore dal punto di vista linguistico ma non viene interessato dalle modifiche nelle impostazioni cultura. L'esempio seguente modifica i due esempi precedenti per usare la lingua inglese per l'ordinamento e la ricerca della matrice.

```csharp
// Correct.
string []storedNames;

public void StoreNames(string [] names)
{
   int index = 0;
   storedNames = new string[names.Length];

   foreach (string name in names)
   {
      this.storedNames[index++] = name;
   }

   Array.Sort(names, StringComparer.InvariantCulture);  // Line A.
}

public bool DoesNameExist(string name)
{
   return (Array.BinarySearch(this.storedNames, name, StringComparer.InvariantCulture) >= 0);  // Line B.
}
```

```vb
' Correct.
Dim storedNames() As String

Public Sub StoreNames(names() As String)
   Dim index As Integer = 0
   ReDim storedNames(names.Length - 1)

   For Each name As String In names
      Me.storedNames(index) = name
      index+= 1
   Next

   Array.Sort(names, StringComparer.InvariantCulture)           ' Line A.
End Sub

Public Function DoesNameExist(name As String) As Boolean
   Return Array.BinarySearch(Me.storedNames, name, StringComparer.InvariantCulture) >= 0      ' Line B.
End Function
```

### <a name="collections-example-hashtable-constructor"></a>Esempio di raccolte: costruttore Hashtable

L'esecuzione dell'hashing nelle stringhe fornisce un secondo esempio di operazione interessata dal modo in cui vengono confrontate le stringhe. 

L'esempio seguente crea un'istanza dell'oggetto [Hashtable](xref:System.Collections.Hashtable) passando l'oggetto [StringComparer](xref:System.StringComparer) restituito dalla proprietà [StringComparer.OrdinalIgnoreCase](xref:System.StringComparer.OrdinalIgnoreCase). Poiché una classe [StringComparer](xref:System.StringComparer) derivata da [StringComparer](xref:System.StringComparer) implementa l'interfaccia [IEqualityComparer](xref:System.Collections.IEqualityComparer), il metodo [GetHashCode](xref:System.Collections.IEqualityComparer) viene usato per calcolare il codice hash delle stringhe nella tabella hash.

```csharp
const int initialTableCapacity = 100;
Hashtable h;

public void PopulateFileTable(string directory)
{
   h = new Hashtable(initialTableCapacity, 
                     StringComparer.OrdinalIgnoreCase);

   foreach (string file in Directory.GetFiles(directory))
         h.Add(file, File.GetCreationTime(file));
}

public void PrintCreationTime(string targetFile)
{
   Object dt = h[targetFile];
   if (dt != null)
   {
      Console.WriteLine("File {0} was created at time {1}.",
         targetFile, 
         (DateTime) dt);
   }
   else
   {
      Console.WriteLine("File {0} does not exist.", targetFile);
   }
}
```

```vb
Const initialTableCapacity As Integer = 100
Dim h As Hashtable

Public Sub PopulateFileTable(dir As String)
   h = New Hashtable(initialTableCapacity, _
                     StringComparer.OrdinalIgnoreCase)

   For Each filename As String In Directory.GetFiles(dir)
      h.Add(filename, File.GetCreationTime(filename))
   Next                        
End Sub

Public Sub PrintCreationTime(targetFile As String)
   Dim dt As Object = h(targetFile)
   If dt IsNot Nothing Then
      Console.WriteLine("File {0} was created at {1}.", _
         targetFile, _
         CDate(dt))
   Else
      Console.WriteLine("File {0} does not exist.", targetFile)
   End If
End Sub  
```

## <a name="displaying-and-persisting-formatted-data"></a>Visualizzazione e conservazione dei dati formattati

Quando si consente agli utenti di visualizzare dati non di tipo stringa, come numeri e date e ore, formattarli usando le impostazioni cultura dell'utente. Per impostazione predefinita, il metodo [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) e i metodi `ToString` dei tipi numerici e dei tipi data e ora usano le impostazioni cultura del thread corrente per le operazioni di formattazione. Per specificare esplicitamente che il metodo di formattazione deve usare le impostazioni cultura correnti, è possibile chiamare un overload di un metodo di formattazione con un parametro provider, ad esempio [String.Format(IFormatProvider, String, Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) o [DateTime.ToString(IFormatProvider)](xref:System.DateTime.ToString(System.IFormatProvider)) e passare la proprietà [CultureInfo.CurrentCulture](xref:System.Globalization.CultureInfo.CurrentCulture). 

È possibile conservare i dati non di tipo stringa come dati binari o formattati. Se si sceglie di salvarli come dati formattati, è necessario chiamare un overload del metodo di formattazione che include un parametro *provider* e passare la proprietà [CultureInfo.InvariantCulture](xref:System.Globalization.CultureInfo.InvariantCulture). La lingua inglese fornisce un formato coerente per i dati formattati, indipendente dalle impostazioni cultura e dal computer. Al contrario, conservare i dati formattati con impostazioni cultura diverse dalla lingua inglese presenta diverse limitazioni: 

* È probabile che i dati non saranno utilizzabili se vengono recuperati in un sistema con impostazioni cultura diverse oppure se l'utente del sistema corrente modifica le impostazioni cultura correnti e prova a recuperare i dati. 

* Le proprietà delle impostazioni cultura in uno specifico computer possono essere diverse rispetto ai valori standard. Un utente può personalizzare in qualsiasi momento le impostazioni di visualizzazione con distinzione delle impostazioni cultura. Per questo motivo, i dati formattati salvati in un sistema potrebbero non essere leggibili dopo che un utente personalizza le impostazioni cultura. La portabilità dei dati formattati tra i vari computer potrebbe risultare ancora più limitata. 

* Gli standard internazionali, regionali o nazionali che regolano la formattazione dei numeri o delle date e delle ore cambiano nel tempo e queste modifiche vengono incorporate negli aggiornamenti del sistema operativo. Quando le convenzioni di formattazione vengono modificate, i dati formattati con le convenzioni precedenti possono diventare illeggibili. 

L'esempio seguente illustra la limitazione della portabilità causata dall'uso della formattazione con distinzione delle impostazioni cultura per la persistenza dei dati. L'esempio salva una matrice di valori di data e ora in un file. Questi vengono formattati usando le convenzioni delle impostazioni cultura per la lingua inglese (Stati Uniti) . Quando l'applicazione modifica le impostazioni cultura del thread corrente in francese (Svizzera), tenta di leggere i valori salvati usando le convenzioni di formattazione delle impostazioni cultura correnti. Il tentativo di lettura di due elementi di dati genera un'eccezione [FormatException](xref:System.FormatException), quindi la matrice di date conterrà due elementi non corretti uguali a [MinValue](xref:System.DateTime.MinValue). 

```csharp
using System;
using System.Globalization;
using System.IO;
using System.Text;
using System.Threading;

public class Example
{
   private static string filename = @".\dates.dat";

   public static void Main()
   {
      DateTime[] dates = { new DateTime(1758, 5, 6, 21, 26, 0), 
                           new DateTime(1818, 5, 5, 7, 19, 0), 
                           new DateTime(1870, 4, 22, 23, 54, 0),  
                           new DateTime(1890, 9, 8, 6, 47, 0), 
                           new DateTime(1905, 2, 18, 15, 12, 0) }; 
      // Write the data to a file using the current culture.
      WriteData(dates);
      // Change the current culture.
      Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture("fr-CH");
      // Read the data using the current culture.
      DateTime[] newDates = ReadData();
      foreach (var newDate in newDates)
         Console.WriteLine(newDate.ToString("g"));
   }

   private static void WriteData(DateTime[] dates) 
   {
      StreamWriter sw = new StreamWriter(filename, false, Encoding.UTF8);    
      for (int ctr = 0; ctr < dates.Length; ctr++) {
         sw.Write("{0}", dates[ctr].ToString("g", CultureInfo.CurrentCulture));
         if (ctr < dates.Length - 1) sw.Write("|");   
      }      
      sw.Close();
   }

   private static DateTime[] ReadData() 
   {
      bool exceptionOccurred = false;

      // Read file contents as a single string, then split it.
      StreamReader sr = new StreamReader(filename, Encoding.UTF8);
      string output = sr.ReadToEnd();
      sr.Close();   

      string[] values = output.Split( new char[] { '|' } );
      DateTime[] newDates = new DateTime[values.Length]; 
      for (int ctr = 0; ctr < values.Length; ctr++) {
         try {
            newDates[ctr] = DateTime.Parse(values[ctr], CultureInfo.CurrentCulture);
         }
         catch (FormatException) {
            Console.WriteLine("Failed to parse {0}", values[ctr]);
            exceptionOccurred = true;
         }
      }      
      if (exceptionOccurred) Console.WriteLine();
      return newDates;
   }
}
// The example displays the following output:
//       Failed to parse 4/22/1870 11:54 PM
//       Failed to parse 2/18/1905 3:12 PM
//       
//       05.06.1758 21:26
//       05.05.1818 07:19
//       01.01.0001 00:00
//       09.08.1890 06:47
//       01.01.0001 00:00
//       01.01.0001 00:00
```

```vb
Imports System.Globalization
Imports System.IO
Imports System.Text
Imports System.Threading

Module Example
   Private filename As String = ".\dates.dat"

   Public Sub Main()
      Dim dates() As Date = { #5/6/1758 9:26PM#, #5/5/1818 7:19AM#, _ 
                              #4/22/1870 11:54PM#, #9/8/1890 6:47AM#, _ 
                              #2/18/1905 3:12PM# }
      ' Write the data to a file using the current culture.
      WriteData(dates)
      ' Change the current culture.
      Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture("fr-CH")
      ' Read the data using the current culture.
      Dim newDates() As Date = ReadData()
      For Each newDate In newDates
         Console.WriteLine(newDate.ToString("g"))
      Next
   End Sub

   Private Sub WriteData(dates() As Date)
      Dim sw As New StreamWriter(filename, False, Encoding.Utf8)    
      For ctr As Integer = 0 To dates.Length - 1
         sw.Write("{0}", dates(ctr).ToString("g", CultureInfo.CurrentCulture))
         If ctr < dates.Length - 1 Then sw.Write("|")   
      Next      
      sw.Close()
   End Sub

   Private Function ReadData() As Date()
      Dim exceptionOccurred As Boolean = False

      ' Read file contents as a single string, then split it.
      Dim sr As New StreamReader(filename, Encoding.Utf8)
      Dim output As String = sr.ReadToEnd()
      sr.Close()   

      Dim values() As String = output.Split( {"|"c } )
      Dim newDates(values.Length - 1) As Date 
      For ctr As Integer = 0 To values.Length - 1
         Try
            newDates(ctr) = DateTime.Parse(values(ctr), CultureInfo.CurrentCulture)
         Catch e As FormatException
            Console.WriteLine("Failed to parse {0}", values(ctr))
            exceptionOccurred = True
         End Try
      Next      
      If exceptionOccurred Then Console.WriteLine()
      Return newDates
   End Function
End Module
' The example displays the following output:
'       Failed to parse 4/22/1870 11:54 PM
'       Failed to parse 2/18/1905 3:12 PM
'       
'       05.06.1758 21:26
'       05.05.1818 07:19
'       01.01.0001 00:00
'       09.08.1890 06:47
'       01.01.0001 00:00
'       01.01.0001 00:00
'
```

Tuttavia, se si sostituisce la proprietà [CultureInfo.CurrentCulture](xref:System.Globalization.CultureInfo.CurrentCulture) con [CultureInfo.InvariantCulture](xref:System.Globalization.CultureInfo.InvariantCulture) nelle chiamate a [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) e [DateTime.Parse(String, IFormatProvider)](xref:System.DateTime.Parse(System.String,System.IFormatProvider)), i dati di data e ora persistenti vengono ripristinati come illustrato nell'output seguente.

```
// 06.05.1758 21:26
// 05.05.1818 07:19
// 22.04.1870 23:54
// 08.09.1890 06:47
// 18.02.1905 15:12
```

## <a name="see-also"></a>Vedere anche

[Modifica di stringhe](manipulating-strings.md)



<!--HONumber=Nov16_HO1-->


