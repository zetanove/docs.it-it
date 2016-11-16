---
title: Codifica dei caratteri in .NET
description: Codifica dei caratteri in .NET
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bce54e41-e9dc-493a-8988-1cbadc340fe8
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 6080f5fa12a2391dd138828e0afc2219f1e3a11b

---

# <a name="character-encoding-in-net"></a>Codifica dei caratteri in .NET

I caratteri sono entità astratte rappresentabili in molti modi. La codifica dei caratteri è un sistema che abbina ogni carattere di un set di caratteri supportato a un valore che lo rappresenta. Il codice Morse, ad esempio, è una codifica dei caratteri che abbina ogni carattere dell'alfabeto romano a una serie di punti e linee utilizzabili per la trasmissione su linee telegrafiche. La codifica dei caratteri per i computer abbina ogni carattere di un set di caratteri supportato a un valore numerico che lo rappresenta. La codifica dei caratteri presenta due componenti distinti:

* Un codificatore, che converte una sequenza di caratteri in una sequenza di valori numerici (byte).

* Un decodificatore, che converte una sequenza di byte in una sequenza di caratteri.

La codifica dei caratteri descrive le regole in base alle quali operano un codificatore e un decodificatore. Ad esempio, la classe [UTF8Encoding](xref:System.Text.UTF8Encoding) descrive le regole per la codifica e la decodifica con UTF-8 (Unicode Transformation Format a 8 bit), che usa da uno a quattro byte per rappresentare un singolo carattere Unicode. La codifica e la decodifica possono includere anche la convalida. Ad esempio, la classe [UnicodeEncoding](xref:System.Text.UnicodeEncoding) controlla tutti i surrogati per assicurarsi che costituiscano coppie di surrogati valide. Una coppia di surrogati è costituita da un carattere con un punto di codice compreso tra U+D800 e U+DBFF seguito da un carattere con un punto di codice compreso tra U+DC00 e U+DFFF. Una strategia di fallback determina come un codificatore gestisce i caratteri non validi o come un decodificatore gestisce i byte non validi. 

> [!WARNING]
> Le classi di codifica in .NET consentono di archiviare e convertire i dati di tipo carattere. Non devono essere usate per archiviare i dati binari in formato stringa. In base alla codifica usata, la conversione dei dati binari in formato stringa con le classi Encoding può introdurre un comportamento imprevisto e generare dati non accurati o danneggiati. Per convertire i dati binari in un formato stringa, usare il metodo [Convert.ToBase64String](xref:System.Convert.ToBase64String(System.Byte[])). 
 
.NET usa la codifica UTF-16, rappresentata dalla classe [UnicodeEncoding](xref:System.Text.UnicodeEncoding), per rappresentare i caratteri e le stringhe. Le applicazioni destinate a Common Language Runtime usano codificatori per eseguire il mapping di rappresentazioni di caratteri Unicode supportate da Common Language Runtime ad altri schemi di codifica. Usano i decodificatori per eseguire il mapping di caratteri da codifiche non Unicode a Unicode.

Questo argomento include le sezioni seguenti:

* [Codifiche in .NET](#encodings-in-net)

* [Selezione di una classe di codifica](#selecting-an-encoding-class)

* [Uso di un oggetto di codifica](#using-an-encoding-object)

* [Scelta di una strategia di fallback](#choosing-a-fallback-strategy)

* [Implementazione di una strategia di fallback personalizzata](#implementing-a-custom-fallback-strategy)

## <a name="encodings-in-net"></a>Codifiche in .NET

Tutte le classi di codifica dei caratteri in .NET ereditano dalla classe [System.Text.Encoding](xref:System.Text.Encoding), una classe astratta che definisce le funzionalità comuni a tutte le codifiche dei caratteri. Per accedere ai singoli oggetti di codifica implementati in .NET, eseguire le operazioni seguenti:

* Usare le proprietà statiche della classe [Encoding](xref:System.Text.Encoding), che restituiscono oggetti che rappresentano le codifiche dei caratteri standard disponibili in .NET (ASCII, UTF-7, UTF-8, UTF-16 e UTF-32). Ad esempio, la proprietà [Encoding.Unicode](xref:System.Text.Encoding.Unicode) restituisce un oggetto [UnicodeEncoding](xref:System.Text.UnicodeEncoding). Ogni oggetto usa il fallback di sostituzione per gestire le stringhe che non può codificare e i byte che non può decodificare. Per altre informazioni, vedere la sezione [Fallback di sostituzione](#replacement-fallback).

* Chiamare il costruttore di classe della codifica. In questo modo è possibile creare istanze di oggetti per le codifiche ASCII, UTF-7, UTF-8, UTF-16 e UTF-32. Per impostazione predefinita, ogni oggetto usa il fallback di sostituzione per gestire le stringhe che non può codificare e i byte che non può decodificare, ma è possibile specificare che invece deve essere generata un'eccezione. Per altre informazioni, vedere le sezioni [Fallback di sostituzione](#replacement-fallback) e [Fallback di eccezione](#exception-fallback).

* Chiamare il costruttore [Encoding.Encoding(Int32)](xref:System.Text.Encoding.GetEncoding(System.Int32)) e passargli un Integer che rappresenta la codifica. Gli oggetti di codifica standard usano il fallback di sostituzione e gli oggetti di codifica della tabella codici e Double Byte Character Set (DBCS) usano il fallback con mapping più appropriato per gestire le stringhe che non possono codificare e i byte che non possono decodificare. Per altre informazioni, vedere la sezione [Fallback con mapping più appropriato](#best-fit-fallback).

* Chiamare il metodo [Encoding.GetEncoding](xref:System.Text.Encoding.GetEncoding(System.Int32)), che restituisce qualsiasi codifica standard, della tabella codici o DBCS disponibile in .NET. Gli overload consentono di specificare un oggetto di fallback sia per il codificatore che per il decodificatore.

> [!NOTE]
> Lo standard Unicode assegna un punto di codice (un numero) e un nome a ciascun carattere in ogni script supportato. Ad esempio, il carattere "A" è rappresentato dal punto di codice U+0041 e dal nome "LATIN CAPITAL LETTER A". Le codifiche Unicode Transformation Format (UTF) definiscono i modi per codificare quel punto di codice in una sequenza di uno o più byte. Uno schema di codifica Unicode semplifica lo sviluppo di applicazioni internazionali, perché consente di rappresentare in una sola codifica i caratteri di qualsiasi set di caratteri. Gli sviluppatori di applicazioni non devono più tenere traccia dello schema di codifica usato per produrre i caratteri per una lingua o un sistema di scrittura specifico e i dati possono essere condivisi tra i sistemi a livello internazionale senza essere danneggiati.
>
>  .NET supporta tre codifiche definite dallo standard Unicode: UTF-8, UTF-16 e UTF-32. Per altre informazioni, vedere lo standard Unicode nella [home page di Unicode](http://www.unicode.org/).
 
.NET supporta i sistemi di codifica dei caratteri elencati nella tabella seguente.

Codifica | Classe | Descrizione | Vantaggi/Svantaggi
-------- | ----- | ----------- | ------------------------ 
ASCII | [ASCIIEncoding](xref:System.Text.ASCIIEncoding) | Codifica un intervallo limitato di caratteri usando i sette bit più bassi di un byte. | Poiché questa codifica supporta solo i valori dei caratteri compresi tra U+0000 e U+007F, nella maggior parte dei casi non è adatta per le applicazioni internazionalizzate.
UTF-7 | [UTF7Encoding](xref:System.Text.UTF7Encoding) | Rappresenta i caratteri come sequenze di caratteri ASCII a 7 bit. I caratteri Unicode non ASCII sono rappresentati da una sequenza di escape di caratteri ASCII. | UTF-7 supporta protocolli di newsgroup e di posta elettronica. UTF-7 non è tuttavia particolarmente sicura o affidabile. In alcuni casi, la modifica di un bit può alterare radicalmente l'interpretazione di un'intera stringa UTF-7. In altri casi, stringhe UTF-7 diverse possono codificare lo stesso testo. Per le sequenze che includono caratteri non ASCII, UTF-7 richiede più spazio di UTF-8 e la codifica/decodifica è più lenta. Di conseguenza, è consigliabile usare UTF-8 anziché UTF-7, se possibile.
UTF-8 | [UTF8Encoding](xref:System.Text.UTF8Encoding) | Rappresenta ogni punto di codice Unicode come sequenza che include da uno a quattro byte. | UTF-8 supporta dimensioni dati a 8 bit e funziona bene con molti sistemi operativi esistenti. Per l'intervallo di caratteri ASCII, UTF-8 è identica alla codifica ASCII e consente un più ampio set di caratteri. Tuttavia, per gli script in cinese-giapponese-coreano (CJK), UTF-8 può richiedere tre byte per ogni carattere e potrebbe generare dimensioni dati maggiori di UTF-16. Si noti che a volte la quantità di dati ASCII, ad esempio di tag HTML, giustifica l'aumento delle dimensioni per la gamma CJK.
UTF-16 | [UnicodeEncoding](xref:System.Text.UnicodeEncoding) | Rappresenta ogni punto di codice Unicode come sequenza di uno o due Integer a 16 bit. I caratteri Unicode più comuni richiedono un solo punto di codice UTF-16, anche se i caratteri supplementari Unicode (U+10000 e successivi) richiedono due punti di codice surrogati UTF-16. Sono supportati sia ordini dei byte little-endian che big-endian. | La codifica UTF-16 viene usata da Common Language Runtime per rappresentare i valori Char e String e dal sistema operativo Windows per rappresentare i valori WCHAR.
UTF-32 | [UTF32Encoding](xref:System.Text.UTF32Encoding) | Rappresenta ogni punto di codice Unicode come Integer a 32 bit. Sono supportati sia ordini dei byte little-endian che big-endian. | La codifica UTF-32 viene usata quando le applicazioni vogliono evitare il comportamento dei punti di codice surrogati della codifica UTF-16 in sistemi operativi per cui lo spazio codificato è estremamente importante. I singoli glifi visualizzati su uno schermo possono comunque essere codificati con più di un carattere UTF-32.

Queste codifiche consentono di lavorare con i caratteri Unicode e con le codifiche più comunemente usate nelle applicazioni legacy. È anche possibile creare una codifica personalizzata definendo una classe che deriva da [Encoding](xref:System.Text.Encoding) ed eseguendo l'override dei relativi membri.

> [!NOTE]
> Per impostazione predefinita, .NET Core non rende disponibili le codifiche delle tabelle codici diverse dalla tabella codice 28591 e le codifiche Unicode, ad esempio UTF-8 e UTF-16. Tuttavia, è possibile aggiungere all'app le codifiche delle tabelle codici presenti nelle app di Windows standard destinate a .NET Framework. Per informazioni complete, vedere l'argomento [EncodingProvider](xref:System.Text.EncodingProvider). 

## <a name="selecting-an-encoding-class"></a>Selezione di una classe di codifica

Se è possibile scegliere la codifica che verrà usata dall'applicazione, è consigliabile usare una codifica Unicode, preferibilmente [UTF8Encoding](xref:System.Text.UTF8Encoding) o [UnicodeEncoding](xref:System.Text.UnicodeEncoding). .NET supporta anche una terza codifica Unicode, vale a dire [UTF32Encoding](xref:System.Text.UTF32Encoding). 

Se si prevede di usare una codifica ASCII ([ASCIIEncoding](xref:System.Text.ASCIIEncoding)), scegliere invece [UTF8Encoding](xref:System.Text.UTF8Encoding). Le due codifiche sono identiche per il set di caratteri ASCII, ma [UTF8Encoding](xref:System.Text.UTF8Encoding) offre i vantaggi seguenti: 

* Può rappresentare tutti i caratteri Unicode, mentre [ASCIIEncoding](xref:System.Text.ASCIIEncoding) supporta solo i valori di caratteri Unicode compresi tra U+0000 e U+007F.

* Fornisce il rilevamento errori e una migliore sicurezza.

* È stata ottimizzata per essere il più veloce possibile e dovrebbe essere più veloce di qualsiasi altra codifica. Anche per il contenuto interamente ASCII, le operazioni eseguite con [UTF8Encoding](xref:System.Text.UTF8Encoding) sono più veloci delle operazioni eseguite con [ASCIIEncoding](xref:System.Text.ASCIIEncoding).

È consigliabile usare [ASCIIEncoding](xref:System.Text.ASCIIEncoding) solo per le applicazioni legacy. Anche per le applicazioni legacy, [UTF8Encoding](xref:System.Text.UTF8Encoding) potrebbe essere tuttavia una scelta migliore per i motivi seguenti, presupponendo le impostazioni predefinite:

* Se l'applicazione include contenuto non esclusivamente ASCII e lo codifica con [ASCIIEncoding](xref:System.Text.ASCIIEncoding), ogni carattere non ASCII viene codificato come punto interrogativo (?). Se l'applicazione quindi decodifica questi dati, le informazioni vengono perse.


* Se l'applicazione include contenuto non esclusivamente ASCII e lo codifica con [UTF8Encoding](xref:System.Text.UTF8Encoding), il risultato appare incomprensibile se interpretato come ASCII. Tuttavia, se l'applicazione usa poi un decodificatore UTF-8 per decodificare questi dati, i dati eseguono correttamente un round trip.

In un'applicazione Web, i caratteri inviati al client in risposta a una richiesta Web dovrebbero rispecchiare la codifica usata nel client. Nella maggior parte dei casi, è consigliabile impostare la proprietà [HttpResponse.ContentEncoding](xref:System.Net.HttpResponseHeader.ContentEncoding) sul valore restituito dalla proprietà [HttpRequestHeader.ContentEncoding](xref:System.Net.HttpRequestHeader.ContentEncoding) per visualizzare il testo nella codifica prevista dall'utente.

## <a name="using-an-encoding-object"></a>Uso di un oggetto di codifica

Un codificatore converte una stringa di caratteri (per lo più caratteri Unicode) nell'equivalente numerico (byte). Ad esempio, è possibile usare un codificatore ASCII per convertire i caratteri Unicode in ASCII e poterli visualizzare nella console. Per eseguire la conversione, chiamare il metodo [Encoding.GetBytes](xref:System.Text.Encoding.GetBytes(System.Char[])). Per determinare il numero di byte necessari per archiviare i caratteri codificati prima di eseguire la codifica, è possibile chiamare il metodo [GetByteCount](xref:System.Text.Encoding.GetByteCount(System.Char[])).

L'esempio seguente usa una singola matrice di byte per codificare le stringhe in due operazioni distinte. Gestisce un indice che indica la posizione iniziale nella matrice di byte per il set successivo di byte con codifica ASCII. Chiama il metodo [ASCIIEncoding.GetByteCount(String)](xref:System.Text.ASCIIEncoding.GetByteCount(System.String)) per assicurarsi che la matrice di byte sia grande abbastanza da contenere la stringa codificata. Chiama poi il metodo [ASCIIEncoding.GetBytes(String, Int32, Int32, Byte[], Int32)](xref:System.Text.ASCIIEncoding.GetBytes(System.Char[],System.Int32,System.Int32,System.Byte[],System.Int32)) per codificare i caratteri nella stringa.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      string[] strings= { "This is the first sentence. ", 
                          "This is the second sentence. " };
      Encoding asciiEncoding = Encoding.ASCII;

      // Create array of adequate size.
      byte[] bytes = new byte[49];
      // Create index for current position of array.
      int index = 0;

      Console.WriteLine("Strings to encode:");
      foreach (var stringValue in strings) {
         Console.WriteLine("   {0}", stringValue);

         int count = asciiEncoding.GetByteCount(stringValue);
         if (count + index >=  bytes.Length)
            Array.Resize(ref bytes, bytes.Length + 50);

         int written = asciiEncoding.GetBytes(stringValue, 0, 
                                              stringValue.Length, 
                                              bytes, index);    

         index = index + written; 
      } 
      Console.WriteLine("\nEncoded bytes:");
      Console.WriteLine("{0}", ShowByteValues(bytes, index));
      Console.WriteLine();

      // Decode Unicode byte array to a string.
      string newString = asciiEncoding.GetString(bytes, 0, index);
      Console.WriteLine("Decoded: {0}", newString);
   }

   private static string ShowByteValues(byte[] bytes, int last ) 
   {
      string returnString = "   ";
      for (int ctr = 0; ctr <= last - 1; ctr++) {
         if (ctr % 20 == 0)
            returnString += "\n   ";
         returnString += String.Format("{0:X2} ", bytes[ctr]);
      }
      return returnString;
   }
}
// The example displays the following output:
//       Strings to encode:
//          This is the first sentence.
//          This is the second sentence.
//       
//       Encoded bytes:
//       
//          54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
//          6E 74 65 6E 63 65 2E 20 54 68 69 73 20 69 73 20 74 68 65 20
//          73 65 63 6F 6E 64 20 73 65 6E 74 65 6E 63 65 2E 20
//       
//       Decoded: This is the first sentence. This is the second sentence.
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim strings() As String = { "This is the first sentence. ", 
                                  "This is the second sentence. " }
      Dim asciiEncoding As Encoding = Encoding.ASCII

      ' Create array of adequate size.
      Dim bytes(50) As Byte
      ' Create index for current position of array.
      Dim index As Integer = 0

      Console.WriteLine("Strings to encode:")
      For Each stringValue In strings
         Console.WriteLine("   {0}", stringValue)

         Dim count As Integer = asciiEncoding.GetByteCount(stringValue)
         If count + index >=  bytes.Length Then
            Array.Resize(bytes, bytes.Length + 50)
         End If
         Dim written As Integer = asciiEncoding.GetBytes(stringValue, 0, 
                                                         stringValue.Length, 
                                                         bytes, index)    

         index = index + written 
      Next 
      Console.WriteLine()
      Console.WriteLine("Encoded bytes:")
      Console.WriteLine("{0}", ShowByteValues(bytes, index))
      Console.WriteLine()

      ' Decode Unicode byte array to a string.
      Dim newString As String = asciiEncoding.GetString(bytes, 0, index)
      Console.WriteLine("Decoded: {0}", newString)
   End Sub

   Private Function ShowByteValues(bytes As Byte(), last As Integer) As String
      Dim returnString As String = "   "
      For ctr As Integer = 0 To last - 1
         If ctr Mod 20 = 0 Then returnString += vbCrLf + "   "
         returnString += String.Format("{0:X2} ", bytes(ctr))
      Next
      Return returnString
   End Function
End Module
' The example displays the following output:
'       Strings to encode:
'          This is the first sentence.
'          This is the second sentence.
'       
'       Encoded bytes:
'       
'          54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
'          6E 74 65 6E 63 65 2E 20 54 68 69 73 20 69 73 20 74 68 65 20
'          73 65 63 6F 6E 64 20 73 65 6E 74 65 6E 63 65 2E 20
'       
'       Decoded: This is the first sentence. This is the second sentence.
```

Un decodificatore converte una matrice di byte che rispecchia una particolare codifica dei caratteri in un set di caratteri, in una matrice di caratteri o in una stringa. Per decodificare una matrice di byte in una matrice di caratteri, chiamare il metodo [Encoding.GetChars](xref:System.Text.Encoding.GetChars(System.Byte[])). Per decodificare una matrice di byte in una stringa, chiamare il metodo [GetString](xref:System.Text.Encoding.GetString(System.Byte[])). Per determinare il numero di caratteri necessari per archiviare i byte decodificati prima di eseguire la decodifica, è possibile chiamare il metodo [GetCharCount](xref:System.Text.Encoding.GetCharCount(System.Byte[])).

L'esempio seguente codifica tre stringhe e quindi le decodifica in una singola matrice di caratteri. Gestisce un indice che indica la posizione iniziale nella matrice di caratteri per il set successivo di caratteri decodificati. Chiama il metodo [GetCharCount](xref:System.Text.Encoding.GetCharCount(System.Byte[])) per assicurarsi che la matrice di caratteri sia grande abbastanza da contenere tutti i caratteri decodificati. Chiama poi il metodo [ASCIIEncoding.GetChars(Byte[], Int32, Int32, Char[], Int32)](xref:System.Text.ASCIIEncoding.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) per decodificare la matrice di byte.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      string[] strings = { "This is the first sentence. ", 
                           "This is the second sentence. ",
                           "This is the third sentence. " };
      Encoding asciiEncoding = Encoding.ASCII;
      // Array to hold encoded bytes.
      byte[] bytes;
      // Array to hold decoded characters.
      char[] chars = new char[50];
      // Create index for current position of character array.
      int index = 0;     

      foreach (var stringValue in strings) {
         Console.WriteLine("String to Encode: {0}", stringValue);
         // Encode the string to a byte array.
         bytes = asciiEncoding.GetBytes(stringValue);
         // Display the encoded bytes.
         Console.Write("Encoded bytes: ");
         for (int ctr = 0; ctr < bytes.Length; ctr++)
            Console.Write(" {0}{1:X2}", 
                          ctr % 20 == 0 ? Environment.NewLine : "", 
                          bytes[ctr]);
         Console.WriteLine();

         // Decode the bytes to a single character array.
         int count = asciiEncoding.GetCharCount(bytes);
         if (count + index >=  chars.Length)
            Array.Resize(ref chars, chars.Length + 50);

         int written = asciiEncoding.GetChars(bytes, 0, 
                                              bytes.Length, 
                                              chars, index);              
         index = index + written;
         Console.WriteLine();       
      }

      // Instantiate a single string containing the characters.
      string decodedString = new string(chars, 0, index - 1);
      Console.WriteLine("Decoded string: ");
      Console.WriteLine(decodedString);
   }
}
// The example displays the following output:
//    String to Encode: This is the first sentence.
//    Encoded bytes:
//    54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
//    6E 74 65 6E 63 65 2E 20
//    
//    String to Encode: This is the second sentence.
//    Encoded bytes:
//    54 68 69 73 20 69 73 20 74 68 65 20 73 65 63 6F 6E 64 20 73
//    65 6E 74 65 6E 63 65 2E 20
//    
//    String to Encode: This is the third sentence.
//    Encoded bytes:
//    54 68 69 73 20 69 73 20 74 68 65 20 74 68 69 72 64 20 73 65
//    6E 74 65 6E 63 65 2E 20
//    
//    Decoded string:
//    This is the first sentence. This is the second sentence. This is the third sentence.
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim strings() As String = { "This is the first sentence. ", 
                                  "This is the second sentence. ",
                                  "This is the third sentence. " }
      Dim asciiEncoding As Encoding = Encoding.ASCII
      ' Array to hold encoded bytes.
      Dim bytes() As Byte
      ' Array to hold decoded characters.
      Dim chars(50) As Char
      ' Create index for current position of character array.
      Dim index As Integer     

      For Each stringValue In strings
         Console.WriteLine("String to Encode: {0}", stringValue)
         ' Encode the string to a byte array.
         bytes = asciiEncoding.GetBytes(stringValue)
         ' Display the encoded bytes.
         Console.Write("Encoded bytes: ")
         For ctr As Integer = 0 To bytes.Length - 1
            Console.Write(" {0}{1:X2}", If(ctr Mod 20 = 0, vbCrLf, ""), 
                                        bytes(ctr))
         Next         
         Console.WriteLine()

         ' Decode the bytes to a single character array.
         Dim count As Integer = asciiEncoding.GetCharCount(bytes)
         If count + index >=  chars.Length Then
            Array.Resize(chars, chars.Length + 50)
         End If
         Dim written As Integer = asciiEncoding.GetChars(bytes, 0, 
                                                         bytes.Length, 
                                                         chars, index)              
         index = index + written
         Console.WriteLine()       
      Next

      ' Instantiate a single string containing the characters.
      Dim decodedString As New String(chars, 0, index - 1)
      Console.WriteLine("Decoded string: ")
      Console.WriteLine(decodedString)
   End Sub
End Module
' The example displays the following output:
'    String to Encode: This is the first sentence.
'    Encoded bytes:
'    54 68 69 73 20 69 73 20 74 68 65 20 66 69 72 73 74 20 73 65
'    6E 74 65 6E 63 65 2E 20
'    
'    String to Encode: This is the second sentence.
'    Encoded bytes:
'    54 68 69 73 20 69 73 20 74 68 65 20 73 65 63 6F 6E 64 20 73
'    65 6E 74 65 6E 63 65 2E 20
'    
'    String to Encode: This is the third sentence.
'    Encoded bytes:
'    54 68 69 73 20 69 73 20 74 68 65 20 74 68 69 72 64 20 73 65
'    6E 74 65 6E 63 65 2E 20
'    
'    Decoded string:
'    This is the first sentence. This is the second sentence. This is the third sentence.
```

I metodi di codifica e di decodifica di una classe derivata da [Encoding](xref:System.Text.Encoding) sono progettati per funzionare su un set completo di dati, ovvero tutti i dati da codificare o decodificare vengono specificati in una singola chiamata al metodo. In alcuni casi, tuttavia, i dati sono disponibili in un flusso e i dati da codificare o decodificare potrebbero essere disponibili solo in operazioni di lettura distinte. Ciò richiede che l'operazione di codifica o decodifica ricordi qualsiasi stato salvato dalla chiamata precedente. I metodi delle classi derivate da [Encoder](xref:System.Text.Encoder) e [Decoder](xref:System.Text.Decoder) possono gestire le operazioni di codifica e decodifica che comprendono più chiamate ai metodi.

Un oggetto [Encoder](xref:System.Text.Encoder) per una particolare codifica è disponibile nella proprietà [Encoding.GetEncoder](xref:System.Text.Encoding.GetEncoder) di tale codifica. Un oggetto [Decoder](xref:System.Text.Decoder) per una particolare codifica è disponibile nella proprietà [Encoding.GetDecoder](xref:System.Text.Encoding.GetDecoder) di tale codifica. Per le operazioni di decodifica, si noti che le classi derivate da [Decoder](xref:System.Text.Decoder) includono un metodo [Decoder.GetChars](xref:System.Text.Decoder.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)), ma non hanno uni un metodo corrispondente a [Encoding.GetString](xref:System.Text.Encoding.GetString(System.Byte[])).

L'esempio seguente illustra la differenza tra l'uso dei metodi [Encoding.GetChars](xref:System.Text.Encoding.GetChars(System.Byte[])) e [Decoder.GetChars](xref:System.Text.Decoder.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) per la decodifica di una matrice di byte Unicode. L'esempio codifica in un file una stringa che contiene alcuni caratteri Unicode e quindi usa i due metodi di decodifica per decodificarli dieci byte alla volta. Una coppia di surrogati presente nel decimo e nell'undicesimo byte viene decodificata in chiamate ai metodi distinte. Come specificato dall'output, il metodo [Encoding.GetChars](xref:System.Text.Encoding.GetChars(System.Byte[])) non può decodificare i byte e li sostituisce invece con +FFFD (REPLACEMENT CHARACTER). D'altra parte, il metodo [Decoder.GetChars](xref:System.Text.Decoder.GetChars(System.Byte[],System.Int32,System.Int32,System.Char[],System.Int32)) può decodificare la matrice di byte per ottenere la stringa originale.

```csharp
using System;
using System.IO;
using System.Text;

public class Example
{
   public static void Main()
   {
      // Use default replacement fallback for invalid encoding.
      UnicodeEncoding enc = new UnicodeEncoding(true, false, false);

      // Define a string with various Unicode characters.
      string str1 = "AB YZ 19 \uD800\udc05 \u00e4"; 
      str1 += "Unicode characters. \u00a9 \u010C s \u0062\u0308"; 
      Console.WriteLine("Created original string...\n");

      // Convert string to byte array.                     
      byte[] bytes = enc.GetBytes(str1);

      FileStream fs = File.Create(@".\characters.bin");
      BinaryWriter bw = new BinaryWriter(fs);
      bw.Write(bytes);
      bw.Close();

      // Read bytes from file.
      FileStream fsIn = File.OpenRead(@".\characters.bin");
      BinaryReader br = new BinaryReader(fsIn);

      const int count = 10;            // Number of bytes to read at a time. 
      byte[] bytesRead = new byte[10]; // Buffer (byte array).
      int read;                        // Number of bytes actually read. 
      string str2 = String.Empty;      // Decoded string.

      // Try using Encoding object for all operations.
      do { 
         read = br.Read(bytesRead, 0, count);
         str2 += enc.GetString(bytesRead, 0, read); 
      } while (read == count);
      br.Close();
      Console.WriteLine("Decoded string using UnicodeEncoding.GetString()...");
      CompareForEquality(str1, str2);
      Console.WriteLine();

      // Use Decoder for all operations.
      fsIn = File.OpenRead(@".\characters.bin");
      br = new BinaryReader(fsIn);
      Decoder decoder = enc.GetDecoder();
      char[] chars = new char[50];
      int index = 0;                   // Next character to write in array.
      int written = 0;                 // Number of chars written to array.
      do { 
         read = br.Read(bytesRead, 0, count);
         if (index + decoder.GetCharCount(bytesRead, 0, read) - 1 >= chars.Length) 
            Array.Resize(ref chars, chars.Length + 50);

         written = decoder.GetChars(bytesRead, 0, read, chars, index);
         index += written;                          
      } while (read == count);
      br.Close();            
      // Instantiate a string with the decoded characters.
      string str3 = new String(chars, 0, index); 
      Console.WriteLine("Decoded string using UnicodeEncoding.Decoder.GetString()...");
      CompareForEquality(str1, str3); 
   }

   private static void CompareForEquality(string original, string decoded)
   {
      bool result = original.Equals(decoded);
      Console.WriteLine("original = decoded: {0}", 
                        original.Equals(decoded, StringComparison.Ordinal));
      if (! result) {
         Console.WriteLine("Code points in original string:");
         foreach (var ch in original)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));
         Console.WriteLine();

         Console.WriteLine("Code points in decoded string:");
         foreach (var ch in decoded)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    Created original string...
//    
//    Decoded string using UnicodeEncoding.GetString()...
//    original = decoded: False
//    Code points in original string:
//    0041 0042 0020 0059 005A 0020 0031 0039 0020 D800 DC05 0020 00E4 0055 006E 0069 0063 006F
//    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
//    0020 0073 0020 0062 0308
//    Code points in decoded string:
//    0041 0042 0020 0059 005A 0020 0031 0039 0020 FFFD FFFD 0020 00E4 0055 006E 0069 0063 006F
//    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
//    0020 0073 0020 0062 0308
//    
//    Decoded string using UnicodeEncoding.Decoder.GetString()...
//    original = decoded: True
```

```vb
Imports System.IO
Imports System.Text

Module Example
   Public Sub Main()
      ' Use default replacement fallback for invalid encoding.
      Dim enc As New UnicodeEncoding(True, False, False)

      ' Define a string with various Unicode characters.
      Dim str1 As String = String.Format("AB YZ 19 {0}{1} {2}", 
                                         ChrW(&hD800), ChrW(&hDC05), ChrW(&h00e4))
      str1 += String.Format("Unicode characters. {0} {1} s {2}{3}", 
                            ChrW(&h00a9), ChrW(&h010C), ChrW(&h0062), ChrW(&h0308))
      Console.WriteLine("Created original string...")
      Console.WriteLine()

      ' Convert string to byte array.                     
      Dim bytes() As Byte = enc.GetBytes(str1)

      Dim fs As FileStream = File.Create(".\characters.bin")
      Dim bw As New BinaryWriter(fs)
      bw.Write(bytes)
      bw.Close()

      ' Read bytes from file.
      Dim fsIn As FileStream = File.OpenRead(".\characters.bin")
      Dim br As New BinaryReader(fsIn)

      Const count As Integer = 10      ' Number of bytes to read at a time. 
      Dim bytesRead(9) As Byte         ' Buffer (byte array).
      Dim read As Integer              ' Number of bytes actually read. 
      Dim str2 As String = ""          ' Decoded string.

      ' Try using Encoding object for all operations.
      Do 
         read = br.Read(bytesRead, 0, count)
         str2 += enc.GetString(bytesRead, 0, read) 
      Loop While read = count
      br.Close()
      Console.WriteLine("Decoded string using UnicodeEncoding.GetString()...")
      CompareForEquality(str1, str2)
      Console.WriteLine()

      ' Use Decoder for all operations.
      fsIn = File.OpenRead(".\characters.bin")
      br = New BinaryReader(fsIn)
      Dim decoder As Decoder = enc.GetDecoder()
      Dim chars(50) As Char
      Dim index As Integer = 0         ' Next character to write in array.
      Dim written As Integer = 0       ' Number of chars written to array.
      Do 
         read = br.Read(bytesRead, 0, count)
         If index + decoder.GetCharCount(bytesRead, 0, read) - 1 >= chars.Length Then 
            Array.Resize(chars, chars.Length + 50)
         End If   
         written = decoder.GetChars(bytesRead, 0, read, chars, index)
         index += written                          
      Loop While read = count
      br.Close()            
      ' Instantiate a string with the decoded characters.
      Dim str3 As New String(chars, 0, index) 
      Console.WriteLine("Decoded string using UnicodeEncoding.Decoder.GetString()...")
      CompareForEquality(str1, str3) 
   End Sub

   Private Sub CompareForEquality(original As String, decoded As String)
      Dim result As Boolean = original.Equals(decoded)
      Console.WriteLine("original = decoded: {0}", 
                        original.Equals(decoded, StringComparison.Ordinal))
      If Not result Then
         Console.WriteLine("Code points in original string:")
         For Each ch In original
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
         Console.WriteLine()

         Console.WriteLine("Code points in decoded string:")
         For Each ch In decoded
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
         Console.WriteLine()
      End If
   End Sub
End Module
' The example displays the following output:
'    Created original string...
'    
'    Decoded string using UnicodeEncoding.GetString()...
'    original = decoded: False
'    Code points in original string:
'    0041 0042 0020 0059 005A 0020 0031 0039 0020 D800 DC05 0020 00E4 0055 006E 0069 0063 006F
'    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
'    0020 0073 0020 0062 0308
'    Code points in decoded string:
'    0041 0042 0020 0059 005A 0020 0031 0039 0020 FFFD FFFD 0020 00E4 0055 006E 0069 0063 006F
'    0064 0065 0020 0063 0068 0061 0072 0061 0063 0074 0065 0072 0073 002E 0020 00A9 0020 010C
'    0020 0073 0020 0062 0308
'    
'    Decoded string using UnicodeEncoding.Decoder.GetString()...
'    original = decoded: True
```

## <a name="choosing-a-fallback-strategy"></a>Scelta di una strategia di fallback

Quando un metodo tenta di codificare o decodificare un carattere, ma non esiste alcun mapping, deve implementare una strategia di fallback che determina come gestire il mapping non riuscito. Esistono tre tipi di strategie di fallback: 

* Fallback con mapping più appropriato

* Fallback di sostituzione

* Fallback di eccezione

> [!IMPORTANT]
> I problemi più comuni nelle operazioni di codifica si verificano quando non è possibile eseguire il mapping di un carattere Unicode a una particolare codifica della tabella codici. I problemi più comuni nelle operazioni di decodifica si verificano quando sequenze di byte non valide non possono essere convertite in caratteri Unicode validi. Per questi motivi, è opportuno conoscere la strategia di fallback usata da un oggetto di codifica specifico. Quando è possibile, è consigliabile specificare la strategia di fallback usata da un oggetto di codifica quando si crea un'istanza dell'oggetto.
 
### <a name="bestfit-fallback"></a>Fallback con mapping più appropriato

Quando un carattere non ha una corrispondenza esatta nella codifica di destinazione, il codificatore può provare a eseguirne il mapping a un carattere simile. Il fallback con mapping più appropriato è principalmente un problema di codifica più che di decodifica. Esistono pochissime tabelle codici contenenti caratteri di cui non è possibile eseguire correttamente il mapping a Unicode. Il fallback con mapping più appropriato è quello predefinito per le codifiche della tabella codici e Double Byte Character Set recuperate dagli overload [Encoding.GetEncoding(Int32)](xref:System.Text.Encoding.GetEncoding(System.Int32)) e [Encoding.GetEncoding(String)](xref:System.Text.Encoding.GetEncoding(System.String)).

> [!NOTE]
> In teoria, le classi di codifica Unicode in .NET ([UTF8Encoding](xref:System.Text.UTF8Encoding), [UnicodeEncoding](xref:System.Text.UnicodeEncoding) e [UTF32Encoding](xref:System.Text.UTF32Encoding)) supportano ogni carattere di ogni set di caratteri e quindi possono essere usate per eliminare i problemi di fallback con mapping più appropriato. 
 

Le strategie di fallback con mapping più appropriato sono diverse a seconda delle tabelle codici e non sono documentate in dettaglio. Ad esempio, per alcune tabelle codici, dei caratteri latini a larghezza intera viene eseguito il mapping ai caratteri latini a metà larghezza più comuni. Per altre tabelle codici, questo mapping non viene eseguito. Anche se si adotta una strategia aggressiva basata sul mapping più appropriato, per alcuni caratteri in alcune codifiche non è concepibile un mapping appropriato. Ad esempio, per un ideogramma cinese non esistono mapping ragionevoli alla tabella codici 1252. In questo caso, viene usata una stringa di sostituzione. Per impostazione predefinita, questa stringa è semplicemente un punto interrogativo (QUESTION MARK, U+003F).

L'esempio seguente usa la tabella codici 1252 (la tabella codici di Windows per le lingue dell'Europa occidentale) per illustrare il mapping più appropriato e i relativi svantaggi. Viene usato il metodo [Encoding.GetEncoding(Int32](xref:System.Text.Encoding.GetEncoding(System.Int32)) per recuperare un oggetto di codifica per la tabella codici 1252. Per impostazione predefinita, usa il mapping più appropriato per i caratteri Unicode che non supporta. L'esempio crea un'istanza di una stringa che contiene tre caratteri non ASCII, CIRCLED LATIN CAPITAL LETTER S (U+24C8), SUPERSCRIPT FIVE (U+2075) e INFINITY (U+221E), separati da spazi. Come mostra l'output del seguente esempio, quando la stringa viene codificata, i tre caratteri originali diversi dallo spazio vengono sostituiti da QUESTION MARK (U+003F), DIGIT FIVE (U+0035) e DIGIT EIGHT (U+0038). DIGIT EIGHT è una sostituzione del tutto inadeguata per il carattere INFINITY non supportato e QUESTION MARK indica che non è disponibile alcun mapping per il carattere originale.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      // Get an encoding for code page 1252 (Western Europe character set).
      Encoding cp1252 = Encoding.GetEncoding(1252);

      // Define and display a string.
      string str = "\u24c8 \u2075 \u221e";
      Console.WriteLine("Original string: " + str);
      Console.Write("Code points in string: ");
      foreach (var ch in str)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine("\n");   

      // Encode a Unicode string.
      Byte[] bytes = cp1252.GetBytes(str);
      Console.Write("Encoded bytes: ");
      foreach (byte byt in bytes)
         Console.Write("{0:X2} ", byt);
      Console.WriteLine("\n");

      // Decode the string.
      string str2 = cp1252.GetString(bytes);
      Console.WriteLine("String round-tripped: {0}", str.Equals(str2));
      if (! str.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));
      }
   }
}
// The example displays the following output:
//       Original string: Ⓢ ⁵ ∞
//       Code points in string: 24C8 0020 2075 0020 221E
//       
//       Encoded bytes: 3F 20 35 20 38
//       
//       String round-tripped: False
//       ? 5 8
//       003F 0020 0035 0020 0038
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      ' Get an encoding for code page 1252 (Western Europe character set).
      Dim cp1252 As Encoding = Encoding.GetEncoding(1252)

      ' Define and display a string.
      Dim str As String = String.Format("{0} {1} {2}", ChrW(&h24c8), ChrW(&H2075), ChrW(&h221E))
      Console.WriteLine("Original string: " + str)
      Console.Write("Code points in string: ")
      For Each ch In str
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next
      Console.WriteLine()   
      Console.WriteLine()

      ' Encode a Unicode string.
      Dim bytes() As Byte = cp1252.GetBytes(str)
      Console.Write("Encoded bytes: ")
      For Each byt In bytes
         Console.Write("{0:X2} ", byt)
      Next
      Console.WriteLine()
      Console.WriteLine()

      ' Decode the string.
      Dim str2 As String = cp1252.GetString(bytes)
      Console.WriteLine("String round-tripped: {0}", str.Equals(str2))
      If Not str.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Original string: Ⓢ ⁵ ∞
'       Code points in string: 24C8 0020 2075 0020 221E
'       
'       Encoded bytes: 3F 20 35 20 38
'       
'       String round-tripped: False
'       ? 5 8
'       003F 0020 0035 0020 0038
```

Il mapping più appropriato è il comportamento predefinito per un oggetto [Encoding](xref:System.Text.Encoding) che codifica i dati Unicode come dati della tabella codici. Esistono applicazioni legacy che si basano su questo comportamento. Tuttavia, per motivi di sicurezza, per la maggior parte delle nuove applicazioni si dovrebbe evitare il comportamento basato sul mapping più appropriato. Ad esempio, le applicazioni non dovrebbero inserire un nome di dominio tramite una codifica con mapping più appropriato.

> [!Note]
> Si può anche implementare un mapping basato sul fallback più appropriato personalizzato per una codifica. Per altre informazioni, vedere la sezione [Implementazione di una strategia di fallback personalizzata](#implementing-a-custom-fallback-strategy).
 
Se il fallback con mapping più appropriato è la scelta predefinita per un oggetto di codifica, è possibile scegliere un'altra strategia di fallback quando si recupera un oggetto [Encoding](xref:System.Text.Encoding) chiamando l'overload [Encoding.GetEncoding(Int32, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.Int32,System.Text.EncoderFallback,System.Text.DecoderFallback)) o [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)). La sezione seguente include un esempio che sostituisce con un asterisco (\*) ogni carattere di cui non è possibile eseguire il mapping alla tabella codici 1252.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding cp1252r = Encoding.GetEncoding(1252, 
                                  new EncoderReplacementFallback("*"),
                                  new DecoderReplacementFallback("*"));

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine();

      byte[] bytes = cp1252r.GetBytes(str1);
      string str2 = cp1252r.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      } 
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       Round-trip: False
//       * * *
//       002A 0020 002A 0020 002A
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim cp1252r As Encoding = Encoding.GetEncoding(1252, 
                                         New EncoderReplacementFallback("*"),
                                         New DecoderReplacementFallback("*"))

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()

      Dim bytes() As Byte = cp1252r.GetBytes(str1)
      Dim str2 As String = cp1252r.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next    
         Console.WriteLine()
      End If 
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       Round-trip: False
'       * * *
'       002A 0020 002A 0020 002A
```

### <a name="replacement-fallback"></a>Fallback di sostituzione

Quando un carattere non ha una corrispondenza esatta nello schema di destinazione e non esiste un carattere appropriato a cui eseguirne il mapping, l'applicazione può specificare una carattere o una stringa di sostituzione. È il comportamento predefinito del decodificatore Unicode, che sostituisce con REPLACEMENT_CHARACTER (U+FFFD) le sequenze a due byte che non può decodificare. È anche il comportamento predefinito della classe [ASCIIEncoding](xref:System.Text.ASCIIEncoding), che sostituisce ogni carattere che non può codificare o decodificare con un punto interrogativo. Il seguente esempio illustra la sostituzione dei caratteri della stringa Unicode dell'esempio precedente. Come mostra l'output, ogni carattere che non può essere decodificato con un byte ASCII viene sostituito da 0x3F, ovvero dal codice ASCII per il punto interrogativo.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding enc = Encoding.ASCII;

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine("\n");

      // Encode the original string using the ASCII encoder.
      byte[] bytes = enc.GetBytes(str1);
      Console.Write("Encoded bytes: ");
      foreach (var byt in bytes)
         Console.Write("{0:X2} ", byt);
      Console.WriteLine("\n");

      // Decode the ASCII bytes.
      string str2 = enc.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      } 
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       
//       Encoded bytes: 3F 20 3F 20 3F
//       
//       Round-trip: False
//       ? ? ?
//       003F 0020 003F 0020 003F
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim enc As Encoding = Encoding.Ascii

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()
      Console.WriteLine() 

      ' Encode the original string using the ASCII encoder.
      Dim bytes() As Byte = enc.GetBytes(str1)
      Console.Write("Encoded bytes: ")
      For Each byt In bytes
         Console.Write("{0:X2} ", byt)
      Next
      Console.WriteLine()
      Console.WriteLine()

      ' Decode the ASCII bytes.
      Dim str2 As String = enc.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next    
         Console.WriteLine()
      End If 
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       
'       Encoded bytes: 3F 20 3F 20 3F
'       
'       Round-trip: False
'       ? ? ?
'       003F 0020 003F 0020 003F
```

.NET include le classi [EncoderReplacementFallback](xref:System.Text.EncoderReplacementFallback) e [DecoderReplacementFallback](xref:System.Text.DecoderReplacementFallback), che usano una stringa sostitutiva se non è possibile eseguire il mapping esatto di un carattere in un'operazione di codifica o decodifica. Per impostazione predefinita, questa stringa di sostituzione è un punto interrogativo, ma è possibile chiamare un overload del costruttore di classe per scegliere un'altra stringa. In genere, la stringa di sostituzione è costituita da un solo carattere, anche se questo non è un requisito. L'esempio seguente modifica il comportamento del codificatore della tabella codici 1252 creando un'istanza dell'oggetto [EncoderReplacementFallback](xref:System.Text.EncoderReplacementFallback) che usa un asterisco (\*) come stringa di sostituzione.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding cp1252r = Encoding.GetEncoding(1252, 
                                  new EncoderReplacementFallback("*"),
                                  new DecoderReplacementFallback("*"));

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine();

      byte[] bytes = cp1252r.GetBytes(str1);
      string str2 = cp1252r.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      } 
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       Round-trip: False
//       * * *
//       002A 0020 002A 0020 002A
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim cp1252r As Encoding = Encoding.GetEncoding(1252, 
                                         New EncoderReplacementFallback("*"),
                                         New DecoderReplacementFallback("*"))

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()

      Dim bytes() As Byte = cp1252r.GetBytes(str1)
      Dim str2 As String = cp1252r.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next    
         Console.WriteLine()
      End If 
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       Round-trip: False
'       * * *
'       002A 0020 002A 0020 002A
```

> [!NOTE]
> Si può anche implementare una classe di sostituzione per una codifica. Per altre informazioni, vedere la sezione [Implementazione di una strategia di fallback personalizzata](#implementing-a-custom-fallback-strategy).
 
Oltre a QUESTION MARK (U+003F), anche il carattere Unicode REPLACEMENT CHARACTER (U+FFFD) viene di solito usato come stringa di sostituzione, in particolare quando si decodificano sequenze di byte che non possono essere convertite in caratteri Unicode. Tuttavia è possibile scegliere qualsiasi stringa di sostituzione, che potrà contenere più caratteri.

### <a name="exception-fallback"></a>Fallback di eccezione

Invece di usare un fallback con mapping più appropriato o una stringa sostitutiva, un codificatore può generare un'eccezione [EncoderFallbackException](xref:System.Text.EncoderFallbackException) se non può codificare un set di caratteri, mentre un decodificatore può generare un'eccezione [DecoderFallbackException](xref:System.Text.DecoderFallbackException) se non può decodificare una matrice di byte. Per generare un'eccezione nelle operazioni di codifica e decodifica, usare un oggetto [EncoderFallbackException](xref:System.Text.EncoderFallbackException) e [DecoderFallbackException](xref:System.Text.DecoderFallbackException) rispettivamente con il metodo [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)). L'esempio seguente illustra il fallback di eccezione con la classe ASCIIEncoding.

```csharp
using System;
using System.Text;

public class Example
{
   public static void Main()
   {
      Encoding enc = Encoding.GetEncoding("us-ascii", 
                                          new EncoderExceptionFallback(), 
                                          new DecoderExceptionFallback());

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      foreach (var ch in str1)
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

      Console.WriteLine("\n");

      // Encode the original string using the ASCII encoder.
      byte[] bytes = {};
      try {
         bytes = enc.GetBytes(str1);
         Console.Write("Encoded bytes: ");
         foreach (var byt in bytes)
            Console.Write("{0:X2} ", byt);

         Console.WriteLine();
      }
      catch (EncoderFallbackException e) {
         Console.Write("Exception: ");
         if (e.IsUnknownSurrogate())
            Console.WriteLine("Unable to encode surrogate pair 0x{0:X4} 0x{1:X3} at index {2}.", 
                              Convert.ToUInt16(e.CharUnknownHigh), 
                              Convert.ToUInt16(e.CharUnknownLow), 
                              e.Index);
         else
            Console.WriteLine("Unable to encode 0x{0:X4} at index {1}.", 
                              Convert.ToUInt16(e.CharUnknown), 
                              e.Index);
         return;
      }
      Console.WriteLine();

      // Decode the ASCII bytes.
      try {
         string str2 = enc.GetString(bytes);
         Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
         if (! str1.Equals(str2)) {
            Console.WriteLine(str2);
            foreach (var ch in str2)
               Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

            Console.WriteLine();
         } 
      }
      catch (DecoderFallbackException e) {
         Console.Write("Unable to decode byte(s) ");
         foreach (byte unknown in e.BytesUnknown)
            Console.Write("0x{0:X2} ");

         Console.WriteLine("at index {0}", e.Index);
      }
   }
}
// The example displays the following output:
//       Ⓢ ⁵ ∞
//       24C8 0020 2075 0020 221E
//       
//       Exception: Unable to encode 0x24C8 at index 0.
```

```vb
Imports System.Text

Module Example
   Public Sub Main()
      Dim enc As Encoding = Encoding.GetEncoding("us-ascii", 
                                                 New EncoderExceptionFallback(), 
                                                 New DecoderExceptionFallback())

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&h24C8), ChrW(&h2075), ChrW(&h221E))
      Console.WriteLine(str1)
      For Each ch In str1
         Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
      Next    
      Console.WriteLine()
      Console.WriteLine() 

      ' Encode the original string using the ASCII encoder.
      Dim bytes() As Byte = {}
      Try
         bytes = enc.GetBytes(str1)
         Console.Write("Encoded bytes: ")
         For Each byt In bytes
            Console.Write("{0:X2} ", byt)
         Next
         Console.WriteLine()
      Catch e As EncoderFallbackException
         Console.Write("Exception: ")
         If e.IsUnknownSurrogate() Then
            Console.WriteLine("Unable to encode surrogate pair 0x{0:X4} 0x{1:X3} at index {2}.", 
                              Convert.ToUInt16(e.CharUnknownHigh), 
                              Convert.ToUInt16(e.CharUnknownLow), 
                              e.Index)
         Else
            Console.WriteLine("Unable to encode 0x{0:X4} at index {1}.", 
                              Convert.ToUInt16(e.CharUnknown), 
                              e.Index)
         End If                              
         Exit Sub
      End Try
      Console.WriteLine()

      ' Decode the ASCII bytes.
      Try
         Dim str2 As String = enc.GetString(bytes)
         Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
         If Not str1.Equals(str2) Then
            Console.WriteLine(str2)
            For Each ch In str2
               Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
            Next    
            Console.WriteLine()
         End If 
      Catch e As DecoderFallbackException
         Console.Write("Unable to decode byte(s) ")
         For Each unknown As Byte In e.BytesUnknown
            Console.Write("0x{0:X2} ")
         Next
         Console.WriteLine("at index {0}", e.Index)
      End Try
   End Sub
End Module
' The example displays the following output:
'       Ⓢ ⁵ ∞
'       24C8 0020 2075 0020 221E
'       
'       Exception: Unable to encode 0x24C8 at index 0.
```

> [!NOTE]
> Si può anche implementare un gestore di eccezioni personalizzato per un'operazione di codifica. Per altre informazioni, vedere la sezione [Implementazione di una strategia di fallback personalizzata](#implementing-a-custom-fallback-strategy).
 
Gli oggetti [EncoderFallbackException](xref:System.Text.EncoderFallbackException) e [DecoderFallbackException](xref:System.Text.DecoderFallbackException) contengono le informazioni seguenti sulla condizione che ha causato l'eccezione: 

* L'oggetto [EncoderFallbackException](xref:System.Text.EncoderFallbackException) include un metodo [IsUnknownSurrogate](xref:System.Text.EncoderFallbackException.IsUnknownSurrogate), indicante se il carattere o i caratteri che non possono essere codificati rappresentano una coppia di surrogati sconosciuti. In questo caso, il metodo restituisce `true`. Se invece rappresentano un singolo carattere sconosciuto, il metodo restituisce `false`. I caratteri della coppia di surrogati sono recuperati dalle proprietà [EncoderFallbackException.CharUnknownHigh](xref:System.Text.EncoderFallbackException.CharUnknownHigh) e [EncoderFallbackException.CharUnknownLow](xref:System.Text.EncoderFallbackException.CharUnknownLow). Il singolo carattere sconosciuto è invece recuperato dalla proprietà [EncoderFallbackException.CharUnknown](xref:System.Text.EncoderFallbackException.CharUnknown). La proprietà [EncoderFallbackException.Index](xref:System.Text.EncoderFallbackException.Index) indica la posizione nella stringa in cui è stato trovato il primo carattere che non è stato possibile codificare.

* L'oggetto [DecoderFallbackException](xref:System.Text.DecoderFallbackException) include una proprietà [BytesUnknown](xref:System.Text.DecoderFallbackException.BytesUnknown) che restituisce una matrice di byte che non è possibile decodificare. La proprietà [DecoderFallbackException.Index](xref:System.Text.DecoderFallbackException.Index) indica la posizione iniziale dei byte sconosciuti.

Anche se gli oggetti [EncoderFallbackException](xref:System.Text.EncoderFallbackException) e [DecoderFallbackException](xref:System.Text.DecoderFallbackException) contengono informazioni diagnostiche adeguate sull'eccezione, non consentono tuttavia l'accesso al buffer di codifica o di decodifica. Quindi non consentono di sostituire o correggere i dati non validi nel metodo di codifica o di decodifica.

## <a name="implementing-a-custom-fallback-strategy"></a>Implementazione di una strategia di fallback personalizzata

Oltre al mapping più appropriato che viene implementato internamente dalle tabelle codici, .NET include le classi seguenti per implementare una strategia di fallback:

* Usare [EncoderReplacementFallback](xref:System.Text.EncoderReplacementFallback) e [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) per sostituire i caratteri nelle operazioni di codifica.

* Usare [DecoderReplacementFallback](xref:System.Text.DecoderReplacementFallback) e [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) per sostituire i caratteri nelle operazioni di decodifica.

* Usare [EncoderExceptionFallback](xref:System.Text.EncoderExceptionFallback) e [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) per generare un'eccezione [EncoderFallbackException](xref:System.Text.EncoderFallbackException) quando un carattere non può essere codificato.

* Usare [DecoderExceptionFallback](xref:System.Text.DecoderExceptionFallback) e [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) per generare un'eccezione [DecoderFallbackException](xref:System.Text.DecoderFallbackException) quando un carattere non può essere decodificato.

Inoltre, è possibile implementare una soluzione personalizzata che usa il fallback con mapping più appropriato, il fallback di sostituzione o il fallback di eccezione, attenendosi alla procedura seguente: 

1. Derivare una classe da [EncoderFallback](xref:System.Text.EncoderFallback) per le operazioni di codifica e da [DecoderFallback](xref:System.Text.DecoderFallback) per le operazioni di decodifica.

2. Derivare una classe da [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) per le operazioni di codifica e da [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) per le operazioni di decodifica.

3. In caso di fallback di eccezione, se le classi [EncoderFallbackException](xref:System.Text.EncoderFallbackException) e [DecoderFallbackException](xref:System.Text.DecoderFallbackException) predefinite non sono soddisfacenti, derivare una classe da un oggetto eccezione, ad esempio [Exception](xref:System.Exception) o [ArgumentException](xref:System.ArgumentException).

### <a name="deriving-from-encoderfallback-or-decoderfallback"></a>Derivazione da EncoderFallback o DecoderFallback

Per implementare una soluzione di fallback personalizzata, è necessario creare una classe che eredita da [EncoderFallback](xref:System.Text.EncoderFallback) per le operazioni di codifica e da [DecoderFallback](xref:System.Text.DecoderFallback) per le operazioni di decodifica. Le istanze di queste classi vengono passate al metodo [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)) e fungono da intermediario tra la classe Encoding e l'implementazione del fallback.

Quando si crea una soluzione di fallback personalizzata per un codificatore o un decodificatore, è necessario implementare i membri seguenti:

* La proprietà [EncoderFallback.MaxCharCount](xref:System.Text.EncoderFallback.MaxCharCount) o [DecoderFallback.MaxCharCount](xref:System.Text.DecoderFallback.MaxCharCount) che restituisce il numero massimo possibile di caratteri che il fallback con mapping più appropriato, di sostituzione o di eccezione può restituire per sostituire un singolo carattere. Per un fallback di eccezione personalizzata, il valore è zero. 

* Il metodo [EncoderFallback.CreateFallbackBuffer](xref:System.Text.EncoderFallback.CreateFallbackBuffer) o [DecoderFallback.CreateFallbackBuffer](xref:System.Text.DecoderFallback.CreateFallbackBuffer), che restituisce l'implementazione di [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) o [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) personalizzata. Il metodo viene chiamato dal codificatore quando rileva il primo carattere che non può codificare correttamente oppure dal decodificatore quando rileva il primo byte che non può decodificare correttamente.

### <a name="deriving-from-encoderfallbackbuffer-or-decoderfallbackbuffer"></a>Derivazione da EncoderFallbackBuffer o DecoderFallbackBuffer

Per implementare una soluzione di fallback personalizzata, è necessario creare anche una classe che eredita da [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) per le operazioni di codifica e da [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) per le operazioni di decodifica. Le istanze di queste classi vengono restituite dal metodo `CreateFallbackBuffer` delle classi [EncoderFallback](xref:System.Text.EncoderFallback) e [DecoderFallback](xref:System.Text.DecoderFallback). Il metodo [EncoderFallback.CreateFallbackBuffer](xref:System.Text.EncoderFallback.CreateFallbackBuffer) viene chiamato dal codificatore quando rileva il primo carattere che non può codificare, mentre il metodo [DecoderFallback.CreateFallbackBuffer](xref:System.Text.DecoderFallback.CreateFallbackBuffer) viene chiamato dal decodificatore quando rileva uno o più byte che non può decodificare. Le classi [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) e [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) consentono l'implementazione del fallback. Ogni istanza rappresenta un buffer contenente i caratteri di fallback che sostituiranno il carattere che non può essere codificato o la sequenza di byte che non può essere decodificata.

Quando si crea una soluzione di fallback personalizzata per un codificatore o un decodificatore, è necessario implementare i membri seguenti:

* Il metodo [EncoderFallbackBuffer.Fallback](xref:System.Text.EncoderFallbackBuffer.%23ctor) o [DecoderFallbackBuffer.Fallback](xref:System.Text.DecoderFallbackBuffer.Fallback(System.Byte[],System.Int32)). Il metodo [EncoderFallbackBuffer.Fallback](xref:System.Text.EncoderFallbackBuffer.Fallback(System.Char,System.Char,System.Int32)) viene chiamato dal codificatore per comunicare al buffer di fallback informazioni sul carattere che non può codificare. Poiché il carattere da codificare può essere una coppia di surrogati, questo metodo viene sottoposto a overload. A un overload vengono passati il carattere da codificare e l'indice nella stringa. Al secondo overload vengono passati il surrogato alto e quello basso insieme all'indice nella stringa. Il metodo [DecoderFallbackBuffer.Fallback](xref:System.Text.DecoderFallbackBuffer.Fallback(System.Byte[],System.Int32)) viene chiamato dal decodificatore per comunicare al buffer di fallback informazioni sul carattere che non può decodificare. A questo metodo viene passata una matrice di byte che non può decodificare, insieme all'indice del primo byte. Il metodo di fallback dovrebbe restituire `true` se il buffer di fallback può fornire uno o più caratteri di sostituzione o con mapping più appropriato. In caso contrario, dovrebbe restituire `false`. Per un fallback di eccezione, il metodo di fallback dovrebbe generare un'eccezione.

* Il metodo [EncoderFallbackBuffer.GetNextChar](xref:System.Text.EncoderFallbackBuffer.GetNextChar) o [DecoderFallbackBuffer.GetNextChar](xref:System.Text.DecoderFallbackBuffer.GetNextChar), che viene chiamato ripetutamente dal codificatore o dal decodificatore per ottenere il carattere successivo dal buffer di fallback. Quando sono stati restituiti tutti i caratteri di fallback, il metodo dovrebbe restituire U+0000. 

* La proprietà [EncoderFallbackBuffer.Remaining](xref:System.Text.EncoderFallbackBuffer.Remaining) o [DecoderFallbackBuffer.Remaining](xref:System.Text.DecoderFallbackBuffer.Remaining) che restituisce il numero di caratteri rimanenti nel buffer di fallback.

* Il metodo [EncoderFallbackBuffer.MovePrevious](xref:System.Text.EncoderFallbackBuffer.MovePrevious) o [DecoderFallbackBuffer.MovePrevious](xref:System.Text.DecoderFallbackBuffer.MovePrevious), che sposta la posizione corrente nel buffer di fallback al carattere precedente.

* Il metodo [EncoderFallbackBuffer.Reset](xref:System.Text.EncoderFallbackBuffer.Reset) o [DecoderFallbackBuffer.Reset](xref:System.Text.DecoderFallbackBuffer.Reset), che reinizializza il buffer di fallback.

Se l'implementazione del fallback è un fallback con mapping più appropriato o un fallback di sostituzione, le classi derivate da [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer) e [DecoderFallbackBuffer](xref:System.Text.DecoderFallbackBuffer) gestiscono anche due campi di istanza privata, vale a dire il numero esatto di caratteri nel buffer e l'indice del carattere successivo nel buffer da restituire.

### <a name="an-encoderfallback-example"></a>Esempio di EncoderFallback

In un esempio precedente è stato usato il fallback di sostituzione per sostituire con un asterisco (\*) i caratteri Unicode non corrispondenti a caratteri ASCII. L'esempio seguente usa un'implementazione del fallback con mapping più appropriato personalizzato invece di fornire un mapping migliore dei caratteri non ASCII.

Il codice seguente definisce una classe denominata `CustomMapper` derivata da [EncoderFallback](xref:System.Text.EncoderFallback) per gestire il mapping più appropriato di caratteri non ASCII. Il metodo `CreateFallbackBuffer` restituisce un oggetto `CustomMapperFallbackBuffer`, che consente l'implementazione di [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer). La classe `CustomMapper` usa un oggetto [Dictionary&lt;TKey, TValue&gt;](xref:System.Collections.Generic.Dictionary%602) per archiviare i mapping di caratteri Unicode non supportati (valore chiave) e i relativi caratteri a 8 bit, che vengono archiviati in due byte consecutivi in un Integer a 64 bit. Per rendere questo mapping disponibile al buffer di fallback, l'istanza di `CustomMapper` viene passata come parametro al costruttore di classe `CustomMapperFallbackBuffer`. Poiché il mapping di più lungo è la stringa "INF" per il carattere Unicode U+221E, la proprietà `MaxCharCount` restituisce 3. 

```csharp
public class CustomMapper : EncoderFallback
{
   public string DefaultString;
   internal Dictionary<ushort, ulong> mapping;

   public CustomMapper() : this("*")
   {   
   }

   public CustomMapper(string defaultString)
   {
      this.DefaultString = defaultString;

      // Create table of mappings
      mapping = new Dictionary<ushort, ulong>();
      mapping.Add(0x24C8, 0x53);
      mapping.Add(0x2075, 0x35);
      mapping.Add(0x221E, 0x49004E0046);
   }

   public override EncoderFallbackBuffer CreateFallbackBuffer()
   {
      return new CustomMapperFallbackBuffer(this);
   }

   public override int MaxCharCount
   {
      get { return 3; }
   } 
}
```

```vb
Public Class CustomMapper : Inherits EncoderFallback
   Public DefaultString As String
   Friend mapping As Dictionary(Of UShort, ULong)

   Public Sub New()
      Me.New("?")
   End Sub

   Public Sub New(ByVal defaultString As String)
      Me.DefaultString = defaultString

      ' Create table of mappings
      mapping = New Dictionary(Of UShort, ULong)
      mapping.Add(&H24C8, &H53)
      mapping.Add(&H2075, &H35)
      mapping.Add(&H221E, &H49004E0046)
   End Sub

   Public Overrides Function CreateFallbackBuffer() As System.Text.EncoderFallbackBuffer
      Return New CustomMapperFallbackBuffer(Me)
   End Function

   Public Overrides ReadOnly Property MaxCharCount As Integer
      Get
         Return 3
      End Get
   End Property
End Class
```

Il codice seguente definisce la classe `CustomMapperFallbackBuffer`, derivata da [EncoderFallbackBuffer](xref:System.Text.EncoderFallbackBuffer). Il dizionario contenente i mapping più appropriati e definito nell'istanza di `CustomMapper` è disponibile nel costruttore di classe. Il metodo `Fallback` restituisce `true` se uno dei caratteri Unicode che il codificatore ASCII non può codificare è definito nel dizionario dei mapping. In caso contrario, restituisce `false`. Per ogni fallback, la variabile privata `count` indica il numero di caratteri ancora da restituire e la variabile privata `index` indica la posizione nel buffer della stringa, `charsToReturn`, del carattere successivo da restituire. 

```csharp
public class CustomMapperFallbackBuffer : EncoderFallbackBuffer
{
   int count = -1;                   // Number of characters to return
   int index = -1;                   // Index of character to return
   CustomMapper fb; 
   string charsToReturn; 

   public CustomMapperFallbackBuffer(CustomMapper fallback)
   {
      this.fb = fallback;
   }

   public override bool Fallback(char charUnknownHigh, char charUnknownLow, int index)
   {
      // Do not try to map surrogates to ASCII.
      return false;
   }

   public override bool Fallback(char charUnknown, int index)
   {
      // Return false if there are already characters to map.
      if (count >= 1) return false;

      // Determine number of characters to return.
      charsToReturn = String.Empty;

      ushort key = Convert.ToUInt16(charUnknown);
      if (fb.mapping.ContainsKey(key)) {
         byte[] bytes = BitConverter.GetBytes(fb.mapping[key]);
         int ctr = 0;
         foreach (var byt in bytes) {
            if (byt > 0) {
               ctr++;
               charsToReturn += (char) byt;
            }
         }
         count = ctr;
      }
      else {
         // Return default.
         charsToReturn = fb.DefaultString;
         count = 1;
      }
      this.index = charsToReturn.Length - 1;

      return true;
   }

   public override char GetNextChar()
   {
      // We'll return a character if possible, so subtract from the count of chars to return.
      count--;
      // If count is less than zero, we've returned all characters.
      if (count < 0) 
         return '\u0000';

      this.index--;
      return charsToReturn[this.index + 1];
   }

   public override bool MovePrevious()
   {
      // Original: if count >= -1 and pos >= 0
      if (count >= -1) {
         count++;
         return true;
      }
      else {
         return false;
      }
   }

   public override int Remaining 
   {
      get { return count < 0 ? 0 : count; }
   }

   public override void Reset()
   {
      count = -1;
      index = -1;
   }
}
```

```vb
Public Class CustomMapperFallbackBuffer : Inherits EncoderFallbackBuffer

   Dim count As Integer = -1        ' Number of characters to return
   Dim index As Integer = -1        ' Index of character to return
   Dim fb As CustomMapper
   Dim charsToReturn As String

   Public Sub New(ByVal fallback As CustomMapper)
      MyBase.New()
      Me.fb = fallback
   End Sub

   Public Overloads Overrides Function Fallback(ByVal charUnknownHigh As Char, ByVal charUnknownLow As Char, ByVal index As Integer) As Boolean
      ' Do not try to map surrogates to ASCII.
      Return False
   End Function

   Public Overloads Overrides Function Fallback(ByVal charUnknown As Char, ByVal index As Integer) As Boolean
      ' Return false if there are already characters to map.
      If count >= 1 Then Return False

      ' Determine number of characters to return.
      charsToReturn = String.Empty

      Dim key As UShort = Convert.ToUInt16(charUnknown)
      If fb.mapping.ContainsKey(key) Then
         Dim bytes() As Byte = BitConverter.GetBytes(fb.mapping.Item(key))
         Dim ctr As Integer
         For Each byt In bytes
            If byt > 0 Then
               ctr += 1
               charsToReturn += Chr(byt)
            End If
         Next
         count = ctr
      Else
         ' Return default.
         charsToReturn = fb.DefaultString
         count = 1
      End If
      Me.index = charsToReturn.Length - 1

      Return True
   End Function

   Public Overrides Function GetNextChar() As Char
      ' We'll return a character if possible, so subtract from the count of chars to return.
      count -= 1
      ' If count is less than zero, we've returned all characters.
      If count < 0 Then Return ChrW(0)

      Me.index -= 1
      Return charsToReturn(Me.index + 1)
   End Function

   Public Overrides Function MovePrevious() As Boolean
      ' Original: if count >= -1 and pos >= 0
      If count >= -1 Then
         count += 1
         Return True
      Else
         Return False
      End If
   End Function

   Public Overrides ReadOnly Property Remaining As Integer
      Get
         Return If(count < 0, 0, count)
      End Get
   End Property

   Public Overrides Sub Reset()
      count = -1
      index = -1
   End Sub
End Class
```

Il codice seguente crea poi un'istanza dell'oggetto `CustomMapper` e la passa al metodo [Encoding.GetEncoding(String, EncoderFallback, DecoderFallback)](xref:System.Text.Encoding.GetEncoding(System.String,System.Text.EncoderFallback,System.Text.DecoderFallback)). L'output indica che l'implementazione del fallback con mapping più appropriato gestisce correttamente i tre caratteri non ASCII nella stringa originale.

```csharp
using System;
using System.Collections.Generic;
using System.Text;

class Program
{
   static void Main()
   {
      Encoding enc = Encoding.GetEncoding("us-ascii", new CustomMapper(), new DecoderExceptionFallback());

      string str1 = "\u24C8 \u2075 \u221E";
      Console.WriteLine(str1);
      for (int ctr = 0; ctr <= str1.Length - 1; ctr++) {
         Console.Write("{0} ", Convert.ToUInt16(str1[ctr]).ToString("X4"));
         if (ctr == str1.Length - 1) 
            Console.WriteLine();
      }
      Console.WriteLine();

      // Encode the original string using the ASCII encoder.
      byte[] bytes = enc.GetBytes(str1);
      Console.Write("Encoded bytes: ");
      foreach (var byt in bytes)
         Console.Write("{0:X2} ", byt);

      Console.WriteLine("\n");

      // Decode the ASCII bytes.
      string str2 = enc.GetString(bytes);
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2));
      if (! str1.Equals(str2)) {
         Console.WriteLine(str2);
         foreach (var ch in str2)
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"));

         Console.WriteLine();
      }
   }
}
```

```vb
Imports System.Text
Imports System.Collections.Generic

Module Module1

   Sub Main()
      Dim enc As Encoding = Encoding.GetEncoding("us-ascii", New CustomMapper(), New DecoderExceptionFallback())

      Dim str1 As String = String.Format("{0} {1} {2}", ChrW(&H24C8), ChrW(&H2075), ChrW(&H221E))
      Console.WriteLine(str1)
      For ctr As Integer = 0 To str1.Length - 1
         Console.Write("{0} ", Convert.ToUInt16(str1(ctr)).ToString("X4"))
         If ctr = str1.Length - 1 Then Console.WriteLine()
      Next
      Console.WriteLine()

      ' Encode the original string using the ASCII encoder.
      Dim bytes() As Byte = enc.GetBytes(str1)
      Console.Write("Encoded bytes: ")
      For Each byt In bytes
         Console.Write("{0:X2} ", byt)
      Next
      Console.WriteLine()
      Console.WriteLine()

      ' Decode the ASCII bytes.
      Dim str2 As String = enc.GetString(bytes)
      Console.WriteLine("Round-trip: {0}", str1.Equals(str2))
      If Not str1.Equals(str2) Then
         Console.WriteLine(str2)
         For Each ch In str2
            Console.Write("{0} ", Convert.ToUInt16(ch).ToString("X4"))
         Next
         Console.WriteLine()
      End If
   End Sub
End Module
```

## <a name="see-also"></a>Vedere anche

[System.Text.Encoder](xref:System.Text.Encoder)

[System.Text.EncoderFallback](xref:System.Text.EncoderFallback)

[System.Text.Decoder](xref:System.Text.Decoder)

[System.Text.DecoderFallback](xref:System.Text.DecoderFallback)

[System.Text.Encoding](xref:System.Text.Encoding)







<!--HONumber=Nov16_HO1-->


