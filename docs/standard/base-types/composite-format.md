---
title: Formattazione composita
description: Formattazione composita
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: a01efc8f-c242-4535-bd32-acd0032d9590
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 15c549f5df0b6de8164e05f50855006996a47fac

---

# <a name="composite-formatting"></a>Formattazione composita

La funzionalità di formattazione composta di .NET consente di usare come input un elenco di oggetti e una stringa di formato composto. Una stringa di formato composto è costituita da testo fisso alternato a segnaposto indicizzati, denominati elementi di formato, che corrispondono agli oggetti dell'elenco. L'operazione di formattazione produce una stringa risultato costituita dal testo fisso originale alternato alla rappresentazione di stringa degli oggetti dell'elenco. 

La funzionalità di formattazione composita è supportata da metodi quali i seguenti: 

* [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)), che restituisce una stringa di risultato formattata. 

* [StringBuilder.AppendFormat] (xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider, System.String, System.Object), che aggiunge una stringa di risultato formattata a un oggetto [StringBuilder](xref:System.Text.StringBuilder).

* Alcuni overload del metodo [Console](xref:System.Console) `WriteLine`, che visualizza una stringa di risultato formattata nella console.  

* Alcuni overload del metodo [TextWriter](xref:System.IO.TextWriter) `WriteLine`, che scrive una stringa di risultato formattata in un flusso o in un file. Anche le classi derivate da [TextWriter](xref:System.IO.TextWriter), come ad esempio [StreamWriter](xref:System.IO.StreamWriter), condividono questa funzionalità.

* [Debug.WriteLine(String, Object[])](xref:System.Diagnostics.Debug.WriteLine(System.String,System.Object[])), che restituisce un messaggio formattato nei listener di traccia. 

* I metodi [Trace.TraceError(String, Object[])](xref:System.Diagnostics.Trace.TraceError(System.String,System.Object[])), [Trace.TraceInformation(String, Object[])](xref:System.Diagnostics.Trace.TraceInformation(System.String,System.Object[])), e [Trace.TraceWarning(String, Object[])](xref:System.Diagnostics.Trace.TraceWarning(System.String,System.Object[])) che restituiscono messaggi formattati nei listener di traccia. 

* Il metodo [TraceSource.TraceInformation(String,Object[])](xref:System.Diagnostics.TraceSource.TraceInformation(System.String,System.Object[])), che scrive un metodo informativo nei listener di traccia. 

## <a name="composite-format-string"></a>Stringa di formato composto

Una stringa di formato composto e un elenco di oggetti vengono usati come argomenti di metodi che supportano la funzionalità di formattazione composta. Una stringa di formato composto è costituita da zero o più esecuzioni di testo fisso alternate a uno o più elementi di formato. Il testo fisso corrisponde a una stringa di propria scelta e ogni elemento di formato corrisponde a un oggetto o una struttura boxed dell'elenco. La funzionalità di formattazione composta restituisce una nuova stringa risultato in cui ciascun elemento di formato viene sostituito dalla rappresentazione di stringa di origine dell'oggetto corrispondente dell'elenco.

Analizzare il frammento di codice [Format] (xref:System.String.Format(System.String.Format(System.IFormatProvider,System.String,System.Object)) seguente.

```csharp
string name = "Fred";
String.Format("Name = {0}, hours = {1:hh}", name, DateTime.Now);
```

```vb
Dim name As String = "Fred"
String.Format("Name = {0}, hours = {1:hh}", name, DateTime.Now)
```

Il testo fisso è `"Name = "` e `", hours = "`. Gli elementi di formato sono `"{0}"`, il cui indice è 0, che corrisponde all'elemento `name` dell'oggetto, e `"{1:hh}"`, il cui indice è 1, che corrisponde all'elemento `DateTime.Now` dell'oggetto.

## <a name="format-item-syntax"></a>Sintassi degli elementi di formato

Ogni elemento di formato usa il formato seguente ed è costituito dai componenti riportati di seguito:

__{__*index*[,*alignment*][:*formatString*]__}__

Le parentesi graffe corrispondenti "{" e "}" sono obbligatorie. 
 
### <a name="index-component"></a>Componente di indice

Il componente obbligatorio *index*, denominato anche identificatore di parametro, corrisponde a un numero a partire da 0 che identifica un elemento corrispondente nell'elenco di oggetti. Con l'elemento di formato con identificatore di parametro 0 viene formattato il primo oggetto dell'elenco, con l'elemento di formato con identificatore di parametro 1 viene formattato il secondo oggetto dell'elenco e così via. L'esempio seguente include quattro identificatori di parametro, numerati da zero a tre, per rappresentare i numeri primi inferiori a dieci: 

```csharp
string primes;
primes = String.Format("Prime numbers less than 10: {0}, {1}, {2}, {3}",
                       2, 3, 5, 7 );
Console.WriteLine(primes);
// The example displays the following output:
//      Prime numbers less than 10: 2, 3, 5, 7
```

```vb
Dim primes As String
primes = String.Format("Prime numbers less than 10: {0}, {1}, {2}, {3}",
                       2, 3, 5, 7 )
Console.WriteLine(primes)
' The example displays the following output:
'      Prime numbers less than 10: 2, 3, 5, 7
```

Più elementi di formato possono fare riferimento allo stesso elemento dell'elenco di oggetti specificando lo stesso identificatore di parametro. È ad esempio possibile formattare lo stesso valore numerico in formato esadecimale, scientifico e numerico specificando una stringa di formato composto "0x{0:X} {0:E} {0:N}", come nell'esempio seguente. 

```csharp
string multiple = String.Format("0x{0:X} {0:E} {0:N}",
                                Int64.MaxValue);
Console.WriteLine(multiple);
// The example displays the following output:
//      0x7FFFFFFFFFFFFFFF 9.223372E+018 9,223,372,036,854,775,807.00
```

```vb
Dim multiple As String = String.Format("0x{0:X} {0:E} {0:N}",
                                       Int64.MaxValue)
Console.WriteLine(multiple)
' The example displays the following output:
'      0x7FFFFFFFFFFFFFFF 9.223372E+018 9,223,372,036,854,775,807.00
```

Ogni elemento di formato può fare riferimento a un oggetto dell'elenco. Se ad esempio sono presenti tre oggetti, è possibile formattare il secondo, il primo e il terzo oggetto specificando una stringa di formato composto "{1} {0} {2}". Gli oggetti a cui non fa riferimento un elemento di formato vengono ignorati. Se un identificatore di parametro corrisponde a un elemento non incluso nei limiti dell'elenco di oggetti, in fase di esecuzione verrà generata un'eccezione [FormatException](xref:System.FormatException).

### <a name="alignment-component"></a>Componente di allineamento

Il componente facoltativo *alignment* corrisponde a un intero con segno che indica la larghezza preferita del campo formattato. Se il valore di *alignment* è inferiore alla lunghezza della stringa formattata, il componente *alignment* verrà ignorato e come larghezza del campo verrà usata la lunghezza della stringa. I dati formattati verranno allineati a destra se il valore di *alignment* è positivo e a sinistra se il valore di *alignment* è negativo. Per la spaziatura eventualmente necessaria verranno usati spazi vuoti. Se viene specificato il componente *alignment*, la virgola è obbligatoria.

L'esempio seguente definisce due matrici, una contenente i nomi dei dipendenti e l'altra contenente il numero di ore in cui hanno lavorato per un periodo di due settimane. La stringa di formato composto allinea a sinistra i nomi in un campo di 20 caratteri e allinea a destra le ore in un campo di 5 caratteri. Si noti che la stringa di formato standard "N1" viene usata anche per formattare le ore con una cifra frazionaria. 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string[] names = { "Adam", "Bridgette", "Carla", "Daniel",
                         "Ebenezer", "Francine", "George" };
      decimal[] hours = { 40, 6.667m, 40.39m, 82, 40.333m, 80,
                                 16.75m };

      Console.WriteLine("{0,-20} {1,5}\n", "Name", "Hours");
      for (int ctr = 0; ctr < names.Length; ctr++)
         Console.WriteLine("{0,-20} {1,5:N1}", names[ctr], hours[ctr]);

   }
}
// The example displays the following output:
//       Name                 Hours
//
//       Adam                  40.0
//       Bridgette              6.7
//       Carla                 40.4
//       Daniel                82.0
//       Ebenezer              40.3
//       Francine              80.0
//       George                16.8
```

```vb
Module Example
   Public Sub Main()
      Dim names() As String = { "Adam", "Bridgette", "Carla", "Daniel",
                                "Ebenezer", "Francine", "George" }
      Dim hours() As Decimal = { 40, 6.667d, 40.39d, 82, 40.333d, 80,
                                 16.75d }

      Console.WriteLine("{0,-20} {1,5}", "Name", "Hours")
      Console.WriteLine()
      For ctr As Integer = 0 To names.Length - 1
         Console.WriteLine("{0,-20} {1,5:N1}", names(ctr), hours(ctr))
      Next
   End Sub
End Module
' The example displays the following output:
'       Name                 Hours
'
'       Adam                  40.0
'       Bridgette              6.7
'       Carla                 40.4
'       Daniel                82.0
'       Ebenezer              40.3
'       Francine              80.0
'       George                16.8
```

### <a name="format-string-component"></a>Componente della stringa di formato

Il componente *formatString* facoltativo è una stringa di formato appropriata per il tipo di oggetto formattato. Specificare una stringa di formato numerico standard o personalizzata se l'oggetto corrispondente è un valore numerico, una stringa di formato di data e ora standard o personalizzata se l'oggetto corrispondente è un oggetto [DateTime](xref:System.DateTime) o una [stringa di formato di enumerazione](enumeration-format.md) se l'oggetto corrispondente è un valore di enumerazione. Se il componente *formatString* viene omesso, verrà usato l'identificatore di formato generale "G" per un tipo numerico, di data e ora o di enumerazione. Se viene specificato il componente *formatString*, i due punti sono obbligatori.

Nella tabella seguente sono elencati i tipi o le categorie di tipi della libreria di classi .NET Framework che supportano un set predefinito di stringhe di formato e vengono forniti collegamenti ad argomenti in cui vengono elencate le stringhe di formato supportate. Si noti che la formattazione delle stringhe è un meccanismo estendibile che consente di definire nuove stringhe di formato per tutti i tipi esistenti nonché definire un set di stringhe di formato supportate da un tipo definito dall'applicazione. Per altre informazioni, vedere gli argomenti [Interfaccia IFormattable](xref:System.IFormattable) e [Interfaccia ICustomFormatter](xref:System.ICustomFormatter). 

Tipo o categoria di tipo | Vedere
--------------------- | ---
Tipi di data e ora ([DateTime](xref:System.DateTime), [DateTimeOffset](xref:System.DateTimeOffset)) | [Stringhe di formato di data e ora standard](standard-datetime.md), [Stringhe di formato di data e ora personalizzato](custom-datetime.md)
Tipi di enumerazione (tutti i tipi derivati da [System.Enum](xref:System.Enum)) | [Stringhe di formato di enumerazione](enumeration-format.md)
Tipi numerici ([BigInteger](xref:System.Numerics.BigInteger), [Byte](xref:System.Byte), [Decimal](xref:System.Decimal), [Double](xref:System.Double), [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [SByte](xref:System.SByte), [Single](xref:System.Single), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), [UInt64](xref:System.UInt64)) | [Stringhe di formato numerico standard](standard-numeric.md), [Stringhe di formato numerico personalizzato](custom-numeric.md)
[Guid](xref:System.Guid) | [Guid.ToString(String)](xref:System.Guid.ToString(System.String))
[TimeSpan](xref:System.TimeSpan) | [Stringhe di formato TimeSpan standard](standard-timespan.md), [Stringhe di formato TimeSpan personalizzate](custom-timespan.md)

### <a name="escaping-braces"></a>Sequenze di escape delle parentesi graffe

Le parentesi graffe di apertura e di chiusura sono interpretate come l'inizio e la fine di un elemento di formato. Di conseguenza, è necessario usare una sequenza di escape per visualizzare una parentesi graffa di apertura o di chiusura letterale. Specificare due parentesi graffe di apertura ("{{") nel testo fisso per visualizzare una parentesi di apertura ("{") oppure due parentesi graffe di chiusura ("}}") per visualizzare una parentesi graffa di chiusura ("}"). Le parentesi graffe in un elemento di formato vengono interpretate sequenzialmente nell'ordine in cui sono rilevate. L'interpretazione delle parentesi graffe annidate non è supportata. 

Il tipo di interpretazione delle parentesi graffe in sequenza di escape può produrre risultati imprevisti. Si consideri, ad esempio, l'elemento di formato "{{{0:D}}}", destinato alla visualizzazione di una parentesi graffa di apertura, un valore numerico formattato come numero decimale e una parentesi graffa di chiusura. L'elemento di formato viene tuttavia interpretato nel modo seguente: 

1. Le prime due parentesi apertura ("{{") presentano una sequenza di escape e producono una parentesi graffa di apertura. 

2. I tre caratteri successivi ("{0:") sono interpretati come l'inizio di un elemento di formato.

3. Il carattere successivo ("D") verrebbe interpretato come identificatore del formato numerico standard Decimal, ma le due parentesi graffe successive con sequenza di escape ("}}") producono una parentesi graffa singola. Poiché la stringa risultante ("D}") non è un identificatore di un formato numerico standard, viene interpretata come una stringa di formato personalizzata che indica la visualizzazione della stringa letterale "D}". 

4. L'ultima parentesi graffa ("}") viene interpretata come la fine dell'elemento di formato. 

5. Il risultato finale visualizzato è la stringa letterale "{D}". Il valore numerico da formattare non viene visualizzato.

Per evitare di interpretare in modo errato gli elementi di formato e le parentesi graffe con sequenza di escape, è preferibile formattarli separatamente, ovvero nella prima operazione di formattazione visualizzare una parentesi graffa di apertura letterale, nella successiva operazione visualizzare il risultato dell'elemento di formato, quindi nell'ultima operazione visualizzare una parentesi graffa di chiusura letterale. Questo approccio viene illustrato nell'esempio seguente:

```csharp
int value = 6324;
string output = string.Format("{0}{1:D}{2}", 
                             "{", value, "}");
Console.WriteLine(output);
// The example displays the following output:
//       {6324} 
```

```vb
Dim value As Integer = 6324
Dim output As String = String.Format("{0}{1:D}{2}", _
                                     "{", value, "}")
Console.WriteLine(output)   
' The example displays the following output:
'       {6324}
```

### <a name="processing-order"></a>Ordine di elaborazione

Se la chiamata al metodo di formattazione composita include un argomento [IFormatProvider](xref:System.IFormatProvider) il cui valore non è Null, il runtime chiama il metodo [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) per richiedere un'implementazione di [ICustomFormatter](xref:System.ICustomFormatter). Se il metodo può restituire un'implementazione di [ICustomFormatter](xref:System.ICustomFormatter), viene memorizzato nella cache per un uso successivo. 

Ogni valore nell'elenco di parametri che corrisponde a un elemento di formato viene convertito in una stringa, attenendosi alla procedura seguente. Se una condizione qualsiasi nei primi tre passaggi è true, la rappresentazione in formato stringa del valore viene restituita in tale passaggio e i passaggi successivi non vengono eseguiti.

1. Se il valore da formattare è `null`, viene restituita una stringa vuota (""). 

2. Se l'implementazione di [ICustomFormatter](xref:System.ICustomFormatter) è disponibile, il runtime chiama il metodo [Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)). Passa al metodo il valore *formatString* dell'elemento di formato, se disponibile, o `null` in caso contrario, insieme con l'implementazione di [IFormatProvider](xref:System.IFormatProvider). 

3. Se il valore implementa l'interfaccia [IFormattable](xref:System.IFormattable), viene chiamato il metodo dell'interfaccia [ToString(String,IFormatProvider)](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)). Al metodo viene passato il valore *formatString*, se disponibile nell'elemento di formato, o `null` in caso contrario. L'argomento [IFormatProvider](xref:System.IFormatProvider) è determinato come segue:

    *   Per un valore numerico, se viene chiamato un metodo di formattazione composita con un argomento [IFormatProvider](xref:System.IFormatProvider) non Null, il runtime richiede un oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) dal relativo metodo [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)). Se non è in grado di specificarne uno, se il valore dell'argomento è `null` o se il metodo di formattazione composita non ha un parametro [IFormatProvider](xref:System.IFormatProvider), viene usato l'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo per le impostazioni cultura del thread corrente. 
    
    * Per un valore di data e ora, se viene chiamato un metodo di formattazione composita con un argomento [IFormatProvider](xref:System.IFormatProvider) non Null, il runtime richiede un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo)[NumberFormatInfo]dal metodo [IFormatProvider.GetFormat](xref:System.IFormatProvider._GetFormat(System.Type). Se non è in grado di specificarne uno, se il valore dell'argomento è `null` o se il metodo di formattazione composita non ha un parametro [IFormatProvider](xref:System.IFormatProvider), viene usato l'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) per le impostazioni cultura del thread corrente. 
    
    * Per gli oggetti di altri tipi, se una formattazione composita viene chiamata con un argomento [IFormatProvider](xref:System.IFormatProvider), il relativo valore (incluso `null`, se non viene specificato alcun oggetto [IFormatProvider](xref:System.IFormatProvider)) viene passato direttamente all'implementazione di [IFormattable.ToString](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)). In caso contrario un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le impostazioni cultura del thread corrente viene passato all'implementazione di [IFormattable.ToString](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)). 
    
4. Viene chiamato il metodo senza parametri `ToString` del tipo, che esegue l'override di [Object.ToString()](xref:System.Object.ToString) o eredita il comportamento della relativa classe di base. In questo caso la stringa di formato specificata dal componente *formatString* nell'elemento di formato, se presente, viene ignorata.

L'allineamento viene applicato al termine dei precedenti passaggi. 

## <a name="code-examples"></a>Esempi di codice

Nell'esempio seguente vengono illustrate una stringa creata con la formattazione composita e un'altra creata mediante il metodo `ToString` di un oggetto. Entrambi i tipi di formattazione producono risultati equivalenti. 

```csharp
string FormatString1 = String.Format("{0:dddd MMMM}", DateTime.Now);
string FormatString2 = DateTime.Now.ToString("dddd MMMM");
```

```vb
Dim FormatString1 As String = String.Format("{0:dddd MMMM}", DateTime.Now)
Dim FormatString2 As String = DateTime.Now.ToString("dddd MMMM")
```

Presupponendo che il giorno corrente sia un giovedì di maggio, il valore di entrambe le stringhe dell'esempio precedente sarà `Thursday May` se sono specificate le impostazioni cultura inglesi.

[Console.WriteLine](xref:System.Console.WriteLine) espone la stessa funzionalità di [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)). L'unica differenza tra i due metodi è che [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) restituisce il risultato come stringa, mentre [Console.WriteLine](xref:System.Console.WriteLine) scrive il risultato nel flusso di output associato all'oggetto [Console](xref:System.Console). Nell'esempio seguente viene usato il metodo [Console.WriteLine](xref:System.Console.WriteLine) per formattare il valore di `MyInt` come valore di valuta.

```csharp
int MyInt = 100;
Console.WriteLine("{0:C}", MyInt);
// The example displays the following output 
// if en-US is the current culture:
//        $100.00
```

```vb
Dim MyInt As Integer = 100
Console.WriteLine("{0:C}", MyInt)
' The example displays the following output
' if en-US is the current culture:
'        $100.00
```

Nell'esempio riportato di seguito vengono illustrate la formattazione di più oggetti e la formattazione di un oggetto in due diversi modi.

```csharp
string myName = "Fred";
Console.WriteLine(String.Format("Name = {0}, hours = {1:hh}, minutes = {1:mm}",
      myName, DateTime.Now));
// Depending on the current time, the example displays output like the following:
//    Name = Fred, hours = 11, minutes = 30                 
```

```vb
Dim myName As String = "Fred"
Console.WriteLine(String.Format("Name = {0}, hours = {1:hh}, minutes = {1:mm}", _
                  myName, DateTime.Now))
' Depending on the current time, the example displays output like the following:
'    Name = Fred, hours = 11, minutes = 30
```

Nell'esempio seguente viene illustrato l'utilizzo dell'allineamento nella formattazione. Gli argomenti formattati sono inseriti tra barre verticali (|) per evidenziare l'allineamento ottenuto.

```csharp
string myFName = "Fred";
string myLName = "Opals";
int myInt = 100;
string FormatFName = String.Format("First Name = |{0,10}|", myFName);
string FormatLName = String.Format("Last Name = |{0,10}|", myLName);
string FormatPrice = String.Format("Price = |{0,10:C}|", myInt); 
Console.WriteLine(FormatFName);
Console.WriteLine(FormatLName);
Console.WriteLine(FormatPrice);
Console.WriteLine();

FormatFName = String.Format("First Name = |{0,-10}|", myFName);
FormatLName = String.Format("Last Name = |{0,-10}|", myLName);
FormatPrice = String.Format("Price = |{0,-10:C}|", myInt);
Console.WriteLine(FormatFName);
Console.WriteLine(FormatLName);
Console.WriteLine(FormatPrice);
// The example displays the following output on a system whose current
// culture is en-US:
//          First Name = |      Fred|
//          Last Name = |     Opals|
//          Price = |   $100.00|
//
//          First Name = |Fred      |
//          Last Name = |Opals     |
//          Price = |$100.00   |
```

```vb
Dim myFName As String = "Fred"
Dim myLName As String = "Opals"

Dim myInt As Integer = 100
Dim FormatFName As String = String.Format("First Name = |{0,10}|", myFName)
Dim FormatLName As String = String.Format("Last Name = |{0,10}|", myLName)
Dim FormatPrice As String = String.Format("Price = |{0,10:C}|", myInt)
Console.WriteLine(FormatFName)
Console.WriteLine(FormatLName)
Console.WriteLine(FormatPrice)
Console.WriteLine()

FormatFName = String.Format("First Name = |{0,-10}|", myFName)
FormatLName = String.Format("Last Name = |{0,-10}|", myLName)
FormatPrice = String.Format("Price = |{0,-10:C}|", myInt)
Console.WriteLine(FormatFName)
Console.WriteLine(FormatLName)
Console.WriteLine(FormatPrice)
' The example displays the following output on a system whose current
' culture is en-US:
'          First Name = |      Fred|
'          Last Name = |     Opals|
'          Price = |   $100.00|
'
'          First Name = |Fred      |
'          Last Name = |Opals     |
'          Price = |$100.00   |
```

## <a name="see-also"></a>Vedere anche

[Console.WriteLine](xref:System.Console.WriteLine)

[String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))

[Formattazione di tipi](formatting-types.md)

[Stringhe di formato di data e ora standard](standard-datetime.md)

[Stringhe di formato di data e ora personalizzato](custom-datetime.md)

[Stringhe di formato di enumerazione](enumeration-format.md)

[Stringhe di formato numerico standard](standard-numeric.md)

[Stringhe di formato numerico personalizzato](custom-numeric.md)

[Stringhe di formato TimeSpan standard](standard-timespan.md)

[Stringhe di formato TimeSpan personalizzate](custom-timespan.md)



<!--HONumber=Nov16_HO3-->


