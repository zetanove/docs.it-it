---
title: Formattazione di tipi
description: Formattazione di tipi
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: cf497639-9f91-45cb-836f-998d1cea2f43
translationtype: Human Translation
ms.sourcegitcommit: b967d8e55347f44a012e4ad8e916440ae228c8ec
ms.openlocfilehash: e9b8ad13a48dd43236769b130d6f8a75b7b023ca
ms.lasthandoff: 03/10/2017

---

# <a name="formatting-types"></a>Formattazione di tipi

La formattazione è il processo di conversione di un'istanza di una classe, una struttura o un valore di enumerazione nella relativa rappresentazione di stringa, eseguito spesso in modo che la stringa risultante possa essere visualizzata dagli utenti o deserializzata per ripristinare il tipo di dati originale. Questa conversione può comportare le difficoltà seguenti:

* Il modo in cui i valori vengono archiviati internamente non riflette necessariamente il modo in cui gli utenti desiderano visualizzarli. Un numero di telefono potrebbe ad esempio venire archiviato nel formato **8009999999**, che non è di immediata comprensione. Potrebbe invece essere preferibile visualizzarlo come **800-999-9999**. Per un esempio relativo all'applicazione di questo formato a un numero, vedere la sezione [Stringhe di formato personalizzate](#custom-format-strings). 

* La conversione di un oggetto nella relativa rappresentazione di stringa non è sempre intuitiva. Non è ad esempio chiaro come dovrebbe venire visualizzata la rappresentazione di stringa di un oggetto **Temperature** o di un oggetto **Person**. Per un esempio in cui un oggetto **Temperature** viene formattato in modi diversi, vedere la sezione [Stringhe di formato standard](#standard-format-strings).

* I valori richiedono spesso una formattazione dipendente dalle impostazioni cultura. In un'applicazione in cui vengono usati i numeri per riflettere valori monetari, ad esempio, le stringhe numeriche devono includere il simbolo di valuta, il separatore di gruppi, che nella maggior parte delle impostazioni cultura corrisponde al separatore delle migliaia, e il separatore decimale delle impostazioni cultura correnti. Per un esempio, vedere la sezione [Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider](#culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface). 

* È possibile che in un'applicazione lo stesso valore debba essere visualizzato in diversi modi. È ad esempio possibile che un membro di enumerazione venga rappresentato visualizzando una rappresentazione di stringa del relativo nome oppure visualizzando il relativo valore sottostante. Per un esempio in cui un membro dell'enumerazione [DayOfWeek](xref:System.DayOfWeek) viene formattato in modi diversi, vedere la sezione [Stringhe di formato standard](#standard-format-strings).

In .NET è disponibile un supporto avanzato della formattazione che consente agli sviluppatori di soddisfare questi requisiti. 

> [!NOTE]
> La formattazione consente di convertire il valore di un tipo in una rappresentazione di stringa, mentre l'analisi è l'operazione inversa. Un'operazione di analisi consente di creare un'istanza di un tipo di dati dalla relativa rappresentazione di stringa. Per informazioni sulla conversione di stringhe in altri tipi di dati, vedere [Analisi di stringhe](parsing-strings.md).

In questa panoramica sono incluse le sezioni seguenti:

* [Formattazione in .NET](#formatting-in-net)

* [Formattazione predefinita tramite il metodo ToString](#default-formatting-using-the-tostring-method)

* [Override del metodo ToString](#overriding-the-tostring-method)

* [Metodo ToString e stringhe di formato](#the-tostring-method-and-format-strings)

    * [Stringhe di formato standard](#standard-format-strings)
    
    * [Stringhe di formato personalizzate](#custom-format-strings)
    
    * [Stringhe di formato e tipi .NET](#format-strings-and-net-types)
    
* [Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider](#culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface)

    * [Formattazione dipendente dalle impostazioni cultura di valori numerici](#culture-sensitive-formatting-of-numeric-values)
    
    * [Formattazione dipendente dalle impostazioni cultura di valori data e ora](#culture-sensitive-formatting-of-date-and-time-values)
    
* [Interfaccia IFormattable](#the-iformattable-interface)

* [Formattazione composita](#composite-formatting)

* [Formattazione personalizzata con ICustomFormatter](#custom-formatting-with-icustomformatter)

* [Argomenti correlati](#related-topics)

* [Riferimento](#reference)

## <a name="formatting-in-net"></a>Formattazione in .NET

Il meccanismo di base per la formattazione è costituito dall'implementazione predefinita del metodo [Object.ToString](xref:System.Object.ToString), illustrato nella sezione [Formattazione predefinita tramite il metodo ToString](#default-formatting-using-the-tostring-method) più avanti in questo argomento. In .NET sono tuttavia disponibili diversi metodi per modificare ed estendere il supporto predefinito della formattazione, tra cui:

* Override del metodo [Object.ToString](xref:System.Object.ToString) per definire una rappresentazione di stringa personalizzata del valore di un oggetto. Per altre informazioni, vedere la sezione [Override del metodo ToString](#overriding-the-tostring-method) più avanti in questo argomento.

* Definizione di identificatori di formato che consentono l'assunzione di più forme da parte della rappresentazione di stringa del valore di un oggetto. L'identificatore di formato "X" nell'istruzione seguente consente, ad esempio, di convertire un valore intero nella rappresentazione di stringa di un valore esadecimale.

  ```csharp
  int integerValue = 60312;
  Console.WriteLine(integerValue.ToString("X"));   // Displays EB98.
  ```

  ```vb
  Dim integerValue As Integer = 60312
  Console.WriteLine(integerValue.ToString("X"))   ' Displays EB98.
  ```
  
  Per altre informazioni sugli identificatori di formato, vedere la sezione [Metodo ToString e stringhe di formato](#the-tostring-method-and-format-strings).
  
* Uso di provider di formato per sfruttare le convenzioni di formattazione di impostazioni cultura specifiche. Nell'istruzione seguente, ad esempio, viene visualizzato un valore di valuta usando le convenzioni di formattazione delle impostazioni cultura en-US. 

  ```csharp
  double cost = 1632.54; 
  Console.WriteLine(cost.ToString("C", 
                  new System.Globalization.CultureInfo("en-US")));   
  // The example displays the following output:
  //       $1,632.54
  ```

  ```vb
  Dim cost As Double = 1632.54
  Console.WriteLine(cost.ToString("C", New System.Globalization.CultureInfo("en-US")))
  ' The example displays the following output:
  '       $1,632.54
  ```
  
  Per altre informazioni sulla formattazione con i provider di formato, vedere la sezione [Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider](#culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface).  
  
* Implementazione dell'interfaccia [IFormattable](xref:System.IFormattable) per supportare sia la conversione di stringa con la classe [Convert](xref:System.Convert) che la formattazione composita. Per altre informazioni, vedere la sezione [Interfaccia IFormattable](#the-iformattable-interface).

* Uso della formattazione composita per incorporare la rappresentazione di stringa di un valore in una stringa di dimensioni maggiori. Per altre informazioni, vedere la sezione [Formattazione composita](#composite-formatting).

* Implementazione di [ICustomFormatter](xref:System.ICustomFormatter) e [IFormatProvider](xref:System.IFormatProvider) per offrire una soluzione di formattazione personalizzata completa. Per altre informazioni, vedere la sezione [Formattazione personalizzata con ICustomFormatter](#custom-formatting-with-icustomformatter).

Nelle sezioni seguenti vengono esaminati questi metodi per la conversione di un oggetto nella relativa rappresentazione di stringa.

## <a name="default-formatting-using-the-tostring-method"></a>Formattazione predefinita tramite il metodo ToString

Ogni tipo derivato da [System.Object](xref:System.Object) eredita automaticamente un metodo [ToString](xref:System.Object.ToString) senza parametri che, per impostazione predefinita, restituisce il nome del tipo. Nell'esempio seguente viene illustrato il metodo [ToString](xref:System.Object.ToString) predefinito. Viene definita una classe denominata `Automobile` che non dispone di implementazione. Quando viene creata un'istanza della classe e viene chiamato il relativo metodo [ToString](xref:System.Object.ToString), viene visualizzato il nome del tipo relativo. Si noti che il metodo [ToString](xref:System.Object.ToString) non viene chiamato in modo esplicito nell'esempio. Il metodo [Console.WriteLine(Object)](xref:System.Console.WriteLine(System.Object)) chiama in modo implicito il metodo [ToString](xref:System.Object.ToString) dell'oggetto passato come argomento. 

```csharp
using System;

public class Automobile
{
   // No implementation. All members are inherited from Object.
}

public class Example
{
   public static void Main()
   {
      Automobile firstAuto = new Automobile();
      Console.WriteLine(firstAuto);
   }
}
// The example displays the following output:
//       Automobile
```

```vb 
Public Class Automobile
   ' No implementation. All members are inherited from Object.
End Class

Module Example
   Public Sub Main()
      Dim firstAuto As New Automobile()
      Console.WriteLine(firstAuto)
   End Sub
End Module
' The example displays the following output:
'       Automobile
```

Poiché tutti i tipi diversi dalle interfacce sono derivati da [Object](xref:System.Object), questa funzionalità viene fornita automaticamente alle classi o alle strutture personalizzate. La funzionalità offerta dal metodo [ToString](xref:System.Object.ToString) predefinito è tuttavia limitata poiché non fornisce informazioni su un'istanza del tipo sebbene consenta di identificarlo. Per fornire una rappresentazione di stringa di un oggetto che offra informazioni sull'oggetto, è necessario eseguire l'override del metodo [ToString](xref:System.Object.ToString).

> [!NOTE]
> Le strutture ereditano dall'oggetto [ValueType](xref:System.ValueType), che a sua volta viene derivato da [Object](xref:System.Object). Sebbene [ValueType](xref:System.ValueType) esegua l'override di [Object.ToString](xref:System.Object.ToString), l'implementazione è identica.

## <a name="overriding-the-tostring-method"></a>Override del metodo ToString

La visualizzazione del nome di un tipo ha spesso un uso limitato e non consente agli utenti dei tipi di distinguere tra le istanze. È tuttavia possibile eseguire l'override del metodo [ToString](xref:System.Object.ToString) per offrire una rappresentazione più utile del valore di un oggetto. Nell'esempio seguente viene definito un oggetto `Temperature` e viene eseguito l'override del relativo metodo [ToString](xref:System.Object.ToString) per visualizzare la temperatura in gradi Celsius.

```csharp
using System;

public class Temperature
{
   private decimal temp;

   public Temperature(decimal temperature)
   {
      this.temp = temperature;   
   }

   public override string ToString()
   {
      return this.temp.ToString("N1") + "°C";
   }
}

public class Example
{
   public static void Main()
   {
      Temperature currentTemperature = new Temperature(23.6m);
      Console.WriteLine("The current temperature is " +
                        currentTemperature.ToString());
   }
}
// The example displays the following output:
//       The current temperature is 23.6°C.
```

```vb
Public Class Temperature
   Private temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.temp = temperature
   End Sub

   Public Overrides Function ToString() As String
      Return Me.temp.ToString("N1") + "°C"   
   End Function
End Class

Module Example
   Public Sub Main()
      Dim currentTemperature As New Temperature(23.6d)
      Console.WriteLine("The current temperature is " +
                        currentTemperature.ToString())
   End Sub
End Module
' The example displays the following output:
'       The current temperature is 23.6°C.
```

In .NET è stato eseguito l'override del metodo [ToString](xref:System.Object.ToString) di ogni tipo di valore primitivo per visualizzare il valore dell'oggetto anziché il relativo nome. Nella tabella seguente viene illustrato l'override per ogni tipo primitivo. Si noti che la maggior parte dei metodi sottoposti a override chiama un altro overload del metodo [ToString](xref:System.Object.ToString) e passa a esso l'identificatore di formato "G", che definisce il formato generale per il tipo, e un oggetto [IFormatProvider](xref:System.IFormatProvider), che rappresenta le impostazioni cultura correnti.

Tipo | Override di ToString
---- | -----------------
[Boolean](xref:System.Boolean) | Restituisce [Boolean.TrueString](xref:System.Boolean.TrueString) o [Boolean.FalseString](xref:System.Boolean.FalseString).
[Byte](xref:System.Byte) | Chiama `Byte.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Byte](xref:System.Byte) per le impostazioni cultura correnti.
[Char](xref:System.Char) | Restituisce il carattere come stringa.
[DateTime](xref:System.DateTime) | Chiama `DateTime.ToString("G", DatetimeFormatInfo.CurrentInfo)` per formattare il valore di data e ora per le impostazioni cultura correnti. 
[Decimal](xref:System.Decimal) | Chiama `Decimal.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Decimal](xref:System.Decimal) per le impostazioni cultura correnti.
[Double](xref:System.Double) | Chiama `Double.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Double](xref:System.Double) per le impostazioni cultura correnti.
[Int16](xref:System.Int16) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Int16](xref:System.Int16) per le impostazioni cultura correnti.
[Int32](xref:System.Int32) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Int32](xref:System.Int32) per le impostazioni cultura correnti.
[Int64](xref:System.Int64) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Int64](xref:System.Int64) per le impostazioni cultura correnti.
[SByte](xref:System.SByte) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [SByte](xref:System.SByte) | per le impostazioni cultura correnti.
[Single](xref:System.Single) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [Single](xref:System.Single) per le impostazioni cultura correnti.
[UInt32](xref:System.UInt32) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [UInt32](xref:System.UInt32) per le impostazioni cultura correnti.
[UInt32](xref:System.UInt32) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [UInt32](xref:System.UInt32) per le impostazioni cultura correnti.
[UInt64](xref:System.UInt64) | Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore [UInt64](xref:System.UInt64) per le impostazioni cultura correnti.

## <a name="the-tostring-method-and-format-strings"></a>Metodo ToString e stringhe di formato

L'utilizzo del metodo [ToString](xref:System.Object.ToString) predefinito o l'esecuzione dell'override di [ToString](xref:System.Object.ToString) è un'operazione appropriata quando un oggetto dispone di una singola rappresentazione di stringa. Spesso, tuttavia, il valore di un oggetto dispone di più rappresentazioni. È ad esempio possibile esprimere una temperatura in gradi Fahrenheit, gradi Celsius o gradi Kelvin. Analogamente, il valore intero 10 può essere rappresentato in diversi modi, tra cui 10, 10,0, 1.0e01 o €10,00.

Per consentire a un singolo valore di disporre di più rappresentazioni di stringa, in .NET vengono usate le stringhe di formato. Una stringa di formato è una stringa che contiene uno o più identificatori di formato predefiniti costituiti da singoli caratteri o gruppi di caratteri che definiscono il modo in cui deve essere formattato l'output del metodo [ToString](xref:System.Object.ToString). La stringa di formato viene quindi passata come parametro al metodo [ToString](xref:System.Object.ToString) dell'oggetto per determinare come deve venire visualizzata la rappresentazione di stringa del valore di tale oggetto.

Tutti i tipi numerici, di data e ora e di enumerazione in .NET supportano un set predefinito di identificatori di formato. È anche possibile usare le stringhe di formato per definire più rappresentazioni di stringa dei tipi di dati definiti dall'applicazione.

### <a name="standard-format-strings"></a>Stringhe di formato standard

Una stringa di formato standard contiene un singolo identificatore di formato, che è un carattere alfabetico che definisce la rappresentazione di stringa dell'oggetto a cui viene applicata, insieme a un identificatore di precisione facoltativo, che influisce sul numero di cifre visualizzate nella stringa di risultato. Se l'identificatore di precisione viene omesso o non è supportato, un identificatore di formato standard è equivalente a una stringa di formato standard. 

In .NET viene definito un set di identificatori di formato standard per tutti i tipi numerici, di data e ora e di enumerazione. Ognuna di queste categorie supporta, ad esempio, un identificatore di formato standard "G", che definisce una rappresentazione di stringa generale di un valore di tale tipo.

Le stringhe di formato standard per i tipi di enumerazione controllano direttamente la rappresentazione di stringa di un valore. Le stringhe di formato passate al metodo [ToString](xref:System.Object.ToString) del valore di un'enumerazione determinano se il valore viene visualizzato tramite il relativo nome di stringa (identificatori di formato "G" e "F"), il relativo valore integrale sottostante (identificatore di formato "D") oppure il relativo valore esadecimale (identificatore di formato "X"). Nell'esempio seguente viene illustrato l'uso delle stringhe di formato standard per formattare un valore dell'enumerazione [DayOfWeek](xref:System.DayOfWeek). 

```csharp
DayOfWeek thisDay = DayOfWeek.Monday;
string[] formatStrings = {"G", "F", "D", "X"};

foreach (string formatString in formatStrings)
   Console.WriteLine(thisDay.ToString(formatString));
// The example displays the following output:
//       Monday
//       Monday
//       1
//       00000001
```

```vb
Dim thisDay As DayOfWeek = DayOfWeek.Monday
Dim formatStrings() As String = {"G", "F", "D", "X"}

For Each formatString As String In formatStrings
   Console.WriteLine(thisDay.ToString(formatString))
Next
' The example displays the following output:
'       Monday
'       Monday
'       1
'       00000001
```

Per informazioni sulle stringhe di formato di enumerazione, vedere [Stringhe di formato di enumerazione](enumeration-format.md).

Le stringhe di formato standard per i tipi numerici definiscono in genere una stringa di risultato il cui aspetto preciso viene controllato da uno o più valori delle proprietà. L'identificatore di formato "C", ad esempio, consente di formattare un numero come valore di valuta. Quando si chiama il metodo [ToString](xref:System.Object.ToString) con l'identificatore di formato "C" come unico parametro, vengono usati i valori delle proprietà seguenti dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) delle impostazioni cultura correnti per definire la rappresentazione di stringa del valore numerico:

* Proprietà [CurrencySymbol](xref:System.Globalization.NumberFormatInfo.CurrencySymbol), che specifica il simbolo di valuta delle impostazioni cultura correnti.

* Proprietà [CurrencyNegativePattern](xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern) o [CurrencyPositivePattern](xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern) , che restituisce un intero che determina quanto segue: 

    * Posizione del simbolo di valuta.
    
    * Utilizzo di un segno negativo iniziale, di un segno negativo finale o di parentesi per indicare i valori negativi.
    
    * Inserimento di uno spazio tra il valore numerico e il simbolo di valuta.
    
* Proprietà [CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits), che definisce il numero di cifre frazionarie nella stringa di risultato.

* Proprietà [CurrencyDecimalSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator), che definisce il simbolo del separatore decimale nella stringa di risultato.

* Proprietà [CurrencyGroupSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator), che definisce il simbolo del separatore di gruppi.

* Proprietà [CurrencyGroupSizes](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes), che definisce il numero di cifre in ogni gruppo a sinistra del separatore decimale.

* Proprietà [NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign), che determina il segno negativo usato nella stringa di risultato se non vengono usate parentesi per indicare i valori negativi.

Le stringhe di formato numerico possono inoltre includere un identificatore di precisione. Il significato di questo identificatore dipende dalla stringa di formato con la quale viene usato, ma in genere esso indica il numero totale di cifre o il numero di cifre frazionarie che devono essere presenti nella stringa di risultato. Nell'esempio seguente vengono usati, ad esempio, la stringa numerica standard "X4"e un identificatore di precisione per creare un valore stringa con quattro cifre esadecimali.

```csharp
byte[] byteValues = { 12, 163, 255 };
foreach (byte byteValue in byteValues)
   Console.WriteLine(byteValue.ToString("X4"));
// The example displays the following output:
//       000C
//       00A3
//       00FF
```

```vb
Dim byteValues() As Byte = { 12, 163, 255 }
For Each byteValue As Byte In byteValues
   Console.WriteLine(byteValue.ToString("X4"))
Next
' The example displays the following output:
'       000C
'       00A3
'       00FF
```

Per altre informazioni sulle stringhe di formato numerico standard, vedere [Stringhe di formato numerico standard](standard-numeric.md). 

Le stringhe di formato standard per i valori di data e ora sono alias per stringhe di formato personalizzate archiviate da una proprietà [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) specifica. Se viene chiamato, ad esempio, il metodo [ToString](xref:System.Object.ToString) di un valore di data e ora con l'identificatore di formato "D", la data e l'ora vengono visualizzate usando la stringa di formato personalizzata archiviata nella proprietà [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) delle impostazioni cultura correnti. Per altre informazioni sulle stringhe di formato personalizzate, vedere la sezione [Stringhe di formato personalizzate](#custom-format-strings). Nell'esempio seguente viene illustrata questa relazione.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      DateTime date1 = new DateTime(2017, 6, 30);
      Console.WriteLine("D Format Specifier:     {0:D}", date1);
      string longPattern = CultureInfo.CurrentCulture.DateTimeFormat.LongDatePattern;
      Console.WriteLine("'{0}' custom format string:     {1}", 
                        longPattern, date1.ToString(longPattern));
   }
}
// The example displays the following output when run on a system whose
// current culture is en-US:
//    D Format Specifier:     Tuesday, June 30, 2017
//    'dddd, MMMM dd, yyyy' custom format string:     Tuesday, June 30, 2017
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim date1 As Date = #6/30/2009#
      Console.WriteLine("D Format Specifier:     {0:D}", date1)
      Dim longPattern As String = CultureInfo.CurrentCulture.DateTimeFormat.LongDatePattern
      Console.WriteLine("'{0}' custom format string:     {1}", _
                        longPattern, date1.ToString(longPattern))
   End Sub
End Module
' The example displays the following output when run on a system whose
' current culture is en-US:
'    D Format Specifier:     Tuesday, June 30, 2009
'    'dddd, MMMM dd, yyyy' custom format string:     Tuesday, June 30, 2009
```

Per altre informazioni sulle stringhe di formato di data e ora standard, vedere [Stringhe di formato di data e ora standard](standard-datetime.md).

È anche possibile usare le stringhe di formato standard per definire la rappresentazione di stringa di un oggetto definito dall'applicazione, prodotta dal metodo `ToString(String)` dell'oggetto. È possibile definire gli identificatori di formato standard specifici supportati dall'oggetto, nonché determinare se per essi viene fatta o meno distinzione tra maiuscole e minuscole. L'implementazione del metodo `ToString(String)` deve supportare gli elementi seguenti:

* Un identificatore di formato "G" che rappresenta un formato abituale o comune dell'oggetto. L'overload senza parametri del metodo `ToString` dell'oggetto deve chiamare il relativo overload di `ToString(String)` e passare a esso la stringa di formato standard "G".

* Supporto per un identificatore di formato equivalente a un riferimento Null. Un identificatore di formato equivalente a un riferimento Null deve essere considerato equivalente all'identificatore di formato "G".

Una classe `Temperature` può, ad esempio, archiviare internamente la temperatura in gradi Celsius e usare gli identificatori di formato per rappresentare il valore dell'oggetto `Temperature` in gradi Celsius, gradi Fahrenheit e gradi Kelvin. Nell'esempio seguente viene illustrato questo concetto.

```csharp
using System;

public class Temperature
{
   private decimal m_Temp;

   public Temperature(decimal temperature)
   {
      this.m_Temp = temperature;
   }

   public decimal Celsius
   {
      get { return this.m_Temp; }
   }

   public decimal Kelvin
   {
      get { return this.m_Temp + 273.15m; }   
   }

   public decimal Fahrenheit
   {
      get { return Math.Round(((decimal) (this.m_Temp * 9 / 5 + 32)), 2); }
   }

   public override string ToString()
   {
      return this.ToString("C");
   }

   public string ToString(string format)
   {  
      // Handle null or empty string.
      if (String.IsNullOrEmpty(format)) format = "C";
      // Remove spaces and convert to uppercase.
      format = format.Trim().ToUpperInvariant();      

      // Convert temperature to Fahrenheit and return string.
      switch (format)
      {
         // Convert temperature to Fahrenheit and return string.
         case "F":
            return this.Fahrenheit.ToString("N2") + " °F";
         // Convert temperature to Kelvin and return string.
         case "K":
            return this.Kelvin.ToString("N2") + " K";
         // return temperature in Celsius.
         case "G":
         case "C":
            return this.Celsius.ToString("N2") + " °C";
         default:
            throw new FormatException(String.Format("The '{0}' format string is not supported.", format));
      }      
   }
}

public class Example
{
   public static void Main()
   {
      Temperature temp1 = new Temperature(0m);
      Console.WriteLine(temp1.ToString());
      Console.WriteLine(temp1.ToString("G"));
      Console.WriteLine(temp1.ToString("C"));
      Console.WriteLine(temp1.ToString("F"));
      Console.WriteLine(temp1.ToString("K"));

      Temperature temp2 = new Temperature(-40m);
      Console.WriteLine(temp2.ToString());
      Console.WriteLine(temp2.ToString("G"));
      Console.WriteLine(temp2.ToString("C"));
      Console.WriteLine(temp2.ToString("F"));
      Console.WriteLine(temp2.ToString("K"));

      Temperature temp3 = new Temperature(16m);
      Console.WriteLine(temp3.ToString());
      Console.WriteLine(temp3.ToString("G"));
      Console.WriteLine(temp3.ToString("C"));
      Console.WriteLine(temp3.ToString("F"));
      Console.WriteLine(temp3.ToString("K"));

      Console.WriteLine(String.Format("The temperature is now {0:F}.", temp3));
   }
}
// The example displays the following output:
//       0.00 °C
//       0.00 °C
//       0.00 °C
//       32.00 °F
//       273.15 K
//       -40.00 °C
//       -40.00 °C
//       -40.00 °C
//       -40.00 °F
//       233.15 K
//       16.00 °C
//       16.00 °C
//       16.00 °C
//       60.80 °F
//       289.15 K
//       The temperature is now 16.00 °C.
```

```vb
Public Class Temperature
   Private m_Temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.m_Temp = temperature
   End Sub

   Public ReadOnly Property Celsius() As Decimal
      Get
         Return Me.m_Temp
      End Get   
   End Property

   Public ReadOnly Property Kelvin() As Decimal
      Get
         Return Me.m_Temp + 273.15d   
      End Get
   End Property

   Public ReadOnly Property Fahrenheit() As Decimal
      Get
         Return Math.Round(CDec(Me.m_Temp * 9 / 5 + 32), 2)
      End Get      
   End Property

   Public Overrides Function ToString() As String
      Return Me.ToString("C")
   End Function

   Public Overloads Function ToString(format As String) As String  
      ' Handle null or empty string.
      If String.IsNullOrEmpty(format) Then format = "C"
      ' Remove spaces and convert to uppercase.
      format = format.Trim().ToUpperInvariant()      

      Select Case format
         Case "F"
           ' Convert temperature to Fahrenheit and return string.
            Return Me.Fahrenheit.ToString("N2") & " °F"
         Case "K"
            ' Convert temperature to Kelvin and return string.
            Return Me.Kelvin.ToString("N2") & " K"
         Case "C", "G"
            ' Return temperature in Celsius.
            Return Me.Celsius.ToString("N2") & " °C"
         Case Else
            Throw New FormatException(String.Format("The '{0}' format string is not supported.", format))
      End Select      
   End Function
End Class

Public Module Example
   Public Sub Main()
      Dim temp1 As New Temperature(0d)
      Console.WriteLine(temp1.ToString())
      Console.WriteLine(temp1.ToString("G"))
      Console.WriteLine(temp1.ToString("C"))
      Console.WriteLine(temp1.ToString("F"))
      Console.WriteLine(temp1.ToString("K"))

      Dim temp2 As New Temperature(-40d)
      Console.WriteLine(temp2.ToString())
      Console.WriteLine(temp2.ToString("G"))
      Console.WriteLine(temp2.ToString("C"))
      Console.WriteLine(temp2.ToString("F"))
      Console.WriteLine(temp2.ToString("K"))

      Dim temp3 As New Temperature(16d)
      Console.WriteLine(temp3.ToString())
      Console.WriteLine(temp3.ToString("G"))
      Console.WriteLine(temp3.ToString("C"))
      Console.WriteLine(temp3.ToString("F"))
      Console.WriteLine(temp3.ToString("K"))

      Console.WriteLine(String.Format("The temperature is now {0:F}.", temp3))
   End Sub
End Module
' The example displays the following output:
'       0.00 °C
'       0.00 °C
'       0.00 °C
'       32.00 °F
'       273.15 K
'       -40.00 °C
'       -40.00 °C
'       -40.00 °C
'       -40.00 °F
'       233.15 K
'       16.00 °C
'       16.00 °C
'       16.00 °C
'       60.80 °F
'       289.15 K
'       The temperature is now 16.00 °C.
```

### <a name="custom-format-strings"></a>Stringhe di formato personalizzate

Oltre alle stringhe di formato standard, in .NET sono definite stringhe di formato personalizzate sia per valori numerici che per valori di data e ora. Una stringa di formato personalizzata è costituita da uno o più identificatori di formato personalizzati che definiscono la rappresentazione di stringa di un valore. La stringa di formato di data e ora personalizzata "yyyy/mm/dd hh:mm:ss.ffff t zzz" consente, ad esempio, di convertire una data nella relativa rappresentazione di stringa nel formato "2008/11/15 07:45:00.0000 P -08:00" per le impostazioni cultura en-US. Analogamente, la stringa di formato personalizzata "0000" consente di convertire il valore intero 12 in "0012". Per un elenco completo di stringhe di formato personalizzate, vedere [Stringhe di formato di data e ora personalizzate](custom-datetime.md) e [Stringhe di formato numerico personalizzate](custom-numeric.md).

Se una stringa di formato è costituita da un solo identificatore di formato personalizzato, l'identificatore di formato deve essere preceduto dal simbolo di percentuale (%) per evitare confusione con un identificatore di formato standard. Nell'esempio seguente viene usato l'identificatore di formato personalizzato "M" per visualizzare un numero a una cifra o a due cifre del mese di una data specifica.

```csharp
DateTime date1 = new DateTime(2009, 9, 8);
Console.WriteLine(date1.ToString("%M"));       
// Displays 9
```

```vb
Dim date1 As Date = #09/08/2009#
Console.WriteLine(date1.ToString("%M"))      ' Displays 9
```

Numerose stringhe di formato standard per i valori di data e ora sono alias per stringhe di formato personalizzate definite dalle proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo). Le stringhe di formato personalizzate offrono inoltre una notevole flessibilità in quanto consentono una formattazione definita dall'applicazione per valori numerici o di data e ora. È possibile definire stringhe di risultato personalizzate sia per valori numerici che per valori di data e ora combinando più identificatori di formato personalizzati in una singola stringa di formato personalizzata. Nell'esempio seguente viene definita una stringa di formato personalizzata che consente di visualizzare il giorno della settimana tra parentesi dopo il nome del mese, il giorno e l'anno.

```csharp
string customFormat = "MMMM dd, yyyy (dddd)";
DateTime date1 = new DateTime(2009, 8, 28);
Console.WriteLine(date1.ToString(customFormat));   
// The example displays the following output if run on a system
// whose language is English:
//       August 28, 2009 (Friday) 
```

```vb
Dim customFormat As String = "MMMM dd, yyyy (dddd)"
Dim date1 As Date = #8/28/2009#
Console.WriteLine(date1.ToString(customFormat))   
' The example displays the following output if run on a system
' whose language is English:
'       August 28, 2009 (Friday) 
```

L'esempio seguente definisce una stringa di formato personalizzata che visualizza un valore [Int64](xref:System.Int64) come numero di telefono degli Stati Uniti standard di sette cifre con il relativo prefisso. 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      long number = 8009999999;
      string fmt = "000-000-0000";
      Console.WriteLine(number.ToString(fmt));
   }
}
// The example displays the following output:
//        800-999-9999
```

```vb
Module Example
   Public Sub Main()
      Dim number As Long = 8009999999
      Dim fmt As String = "000-000-0000"
      Console.WriteLine(number.ToString(fmt))
   End Sub
End Module
' The example displays the following output:

' The example displays the following output:
'       800-999-9999
```

Sebbene le stringhe di formato standard consentano in genere di gestire la maggior parte delle necessità relative alla formattazione per i tipi definiti dall'applicazione, è anche possibile definire identificatori di formato personalizzati per formattare i tipi. 

### <a name="format-strings-and-net-types"></a>Stringhe di formato e tipi .NET

Tutti i tipi numerici, ovvero[Byte](xref:System.Byte), [Decimal](xref:System.Decimal), [Double](xref:System.Double), [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [SByte](xref:System.SByte), [Single](xref:System.Single), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), [UInt64](xref:System.UInt64) e [BigInteger](xref:System.Numerics.BigInteger), e i tipi [DateTime](xref:System.DateTime), [DateTimeOffset](xref:System.DateTimeOffset), [TimeSpan](xref:System.TimeSpan), [Guid](xref:System.Guid) e tutti i tipi di enumerazione supportano la formattazione con stringhe di formato. Per informazioni sulle stringhe di formato specifiche supportate da ogni tipo, vedere gli argomenti seguenti: 

Titolo | Definizione
----- | ----------
[Stringhe di formato numerico standard](standard-numeric.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori numerici. 
[Stringhe di formato numerico personalizzato](custom-numeric.md) | Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori numerici.
[Stringhe di formato di data e ora standard](standard-datetime.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori [DateTime](xref:System.DateTime).
[Stringhe di formato di data e ora personalizzato](custom-datetime.md) | Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori [DateTime](xref:System.DateTime).
[Stringhe di formato TimeSpan standard](standard-timespan.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di intervalli di tempo.
[Stringhe di formato TimeSpan personalizzate](custom-timespan.md) | Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per intervalli di tempo.
[Stringhe di formato di enumerazione](enumeration-format.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa di valori di enumerazione.
[Guid.ToString(String)](xref:System.Guid.ToString(System.String)) | Descrive le stringhe di formato standard per i valori [Guid](xref:System.Guid).

## <a name="culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface"></a>Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider

Sebbene gli identificatori di formato consentano di personalizzare la formattazione degli oggetti, la creazione di una rappresentazione di stringa significativa degli oggetti richiede spesso informazioni aggiuntive sulla formattazione. La formattazione, ad esempio, di un numero come valore di valuta tramite la stringa di formato standard "C" o una stringa di formato personalizzata, come ad esempio "$ #,#.00", richiede almeno la possibilità di includere nella stringa formattata le informazioni relative al simbolo di valuta, al separatore di gruppi e al separatore decimale corretti. In .NET queste informazioni aggiuntive sulla formattazione vengono rese disponibili tramite l'interfaccia [IFormatProvider](xref:System.IFormatProvider), fornita come parametro di uno o più overload del metodo `ToString` di tipi numerici e di data e ora. Le implementazioni di [IFormatProvider](xref:System.IFormatProvider) vengono usate in .NET per supportare la formattazione specifica delle impostazioni cultura. Nell'esempio seguente viene illustrato come cambia la rappresentazione di stringa di un oggetto quando viene formattata con tre oggetti [IFormatProvider](xref:System.IFormatProvider) che rappresentano impostazioni cultura diverse.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      decimal value = 1603.42m;
      Console.WriteLine(value.ToString("C3", new CultureInfo("en-US")));
      Console.WriteLine(value.ToString("C3", new CultureInfo("fr-FR")));
      Console.WriteLine(value.ToString("C3", new CultureInfo("de-DE")));
   }
}
// The example displays the following output:
//       $1,603.420
//       1 603,420 €
//       1.603,420 €
```

```vb
Imports System.Globalization

Public Module Example
   Public Sub Main()
      Dim value As Decimal = 1603.42d
      Console.WriteLine(value.ToString("C3", New CultureInfo("en-US")))
      Console.WriteLine(value.ToString("C3", New CultureInfo("fr-FR")))
      Console.WriteLine(value.ToString("C3", New CultureInfo("de-DE")))
   End Sub
End Module
' The example displays the following output:
'       $1,603.420
'       1 603,420 €
'       1.603,420 €
```

L'interfaccia [IFormatProvider](xref:System.IFormatProvider) include un solo metodo, ovvero [GetFormat(Type)](xref:System.IFormatProvider.GetFormat(System.Type)), che dispone di un singolo parametro che specifica il tipo di oggetto che fornisce informazioni sulla formattazione. Se il metodo può fornire un oggetto di tale tipo, lo restituisce. In caso contrario, restituisce un riferimento Null.

[IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) è un metodo di callback. Quando si chiama un overload del metodo `ToString` che include un parametro [IFormatProvider](xref:System.IFormatProvider), viene chiamato il metodo [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) dell'oggetto [IFormatProvider](xref:System.IFormatProvider). Il metodo [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) è responsabile della restituzione di un oggetto che fornisce le informazioni sulla formattazione necessarie, specificate dal relativo parametro *formatType*, al metodo `ToString`. 

Diversi metodi di conversione di stringhe o di formattazione includono un parametro di tipo [IFormatProvider](xref:System.IFormatProvider), ma in molti casi il valore del parametro viene ignorato quando il metodo viene chiamato. Nella tabella seguente sono elencati alcuni dei metodi di formattazione che usano il parametro e il tipo dell'oggetto [Type](xref:System.Type) che passano al metodo [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)). 

Metodo | Tipo di parametro *formatType*
------ | ------------------------------
Metodo `ToString` di tipi numerici | [System.Globalization.NumberFormatInfo](xref:System.Globalization.NumberFormatInfo)
Metodo `ToString` di tipi di data e ora | [System.Globalization.DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo)
[String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) | [System.ICustomFormatter](xref:System.ICustomFormatter)
[StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)) | [System.ICustomFormatter](xref:System.ICustomFormatter)

In .NET sono disponibili tre classi che implementano [IFormatProvider](xref:System.IFormatProvider): 

* [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo), una classe che offre informazioni sulla formattazione per i valori di data e ora per impostazioni cultura specifiche. L'implementazione [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) relativa restituisce un'istanza di se stessa.

* [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo), una classe che offre informazioni sulla formattazione numerica per impostazioni cultura specifiche. L'implementazione [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) relativa restituisce un'istanza di se stessa.

* [CultureInfo](xref:System.Globalization.CultureInfo). L'implementazione [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) può restituire un oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) per offrire informazioni sulla formattazione numerica o un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) per offrire informazioni sulla formattazione per i valori di data e ora. 

È anche possibile implementare un provider di formato personalizzato per sostituire una di queste classi. Il metodo `GetFormat` dell'implementazione, tuttavia, deve restituire un oggetto del tipo elencato nella tabella precedente, se deve fornire informazioni sulla formattazione al metodo `ToString`.

### <a name="culture-sensitive-formatting-of-numeric-values"></a>Formattazione dipendente dalle impostazioni cultura di valori numerici

Per impostazione predefinita, la formattazione di valori numerici è dipendente dalle impostazioni cultura. Se non si specificano impostazioni cultura quando si chiama un metodo di formattazione, vengono usate le convenzioni di formattazione delle impostazioni cultura del thread corrente. Questa situazione viene illustrata nell'esempio seguente in cui le impostazioni cultura del thread corrente vengono modificate quattro volte e viene chiamato il metodo [Decimal.ToString(String)](xref:System.Decimal.ToString(System.String)). In ogni caso, la stringa risultante riflette le convenzioni di formattazione delle impostazioni cultura correnti. Questo accade perché i metodi `ToString` e `ToString(String)` eseguono il wrapping di chiamate al metodo `ToString(String, IFormatProvider)` di ogni tipo numerico. 

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string[] cultureNames = { "en-US", "fr-FR", "es-MX", "de-DE" };
      Decimal value = 1043.17m;

      foreach (var cultureName in cultureNames) {
         // Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName);
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name);
         Console.WriteLine(value.ToString("C2"));
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//       The current culture is en-US
//       $1,043.17
//       
//       The current culture is fr-FR
//       1 043,17 €
//       
//       The current culture is es-MX
//       $1,043.17
//       
//       The current culture is de-DE
//       1.043,17 €
```

```vb
Imports System.Globalization
Imports System.Threading 

Module Example
   Public Sub Main()
      Dim cultureNames() As String = { "en-US", "fr-FR", "es-MX", "de-DE" }
      Dim value As Decimal = 1043.17d 

      For Each cultureName In cultureNames
         ' Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName)
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name)
         Console.WriteLine(value.ToString("C2"))
         Console.WriteLine()
      Next                  
   End Sub
End Module
' The example displays the following output:
'       The current culture is en-US
'       $1,043.17
'       
'       The current culture is fr-FR
'       1 043,17 €
'       
'       The current culture is es-MX
'       $1,043.17
'       
'       The current culture is de-DE
'       1.043,17 €
```

È anche possibile formattare un valore numerico per impostazioni cultura specifiche chiamando un overload di `ToString` con un parametro *provider* e passando uno degli elementi seguenti: 

* Oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le impostazioni cultura, di cui verranno usate le convenzioni di formattazione. Il metodo [CultureInfo.GetFormat](xref:System.Globalization.CultureInfo.GetFormat(System.Type)) relativo restituisce il valore della proprietà [CultureInfo.NumberFormat](xref:System.Globalization.CultureInfo.NumberFormat), che rappresenta l'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che offre informazioni di formattazione specifiche delle impostazioni cultura per i valori numerici.

* Oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che definisce le convenzioni di formattazione specifiche delle impostazioni cultura da usare. Il metodo [GetFormat](xref:System.Globalization.NumberFormatInfo.GetFormat(System.Type)) relativo restituisce un'istanza di se stesso.

Nell'esempio seguente vengono usati gli oggetti [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che rappresentano le impostazioni cultura della lingua inglese di Stati Uniti e di Gran Bretagna, nonché le impostazioni cultura non associate alle lingue francese e russa per formattare un numero a virgola mobile.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {                                                                                                    
      Double value = 1043.62957;
      string[] cultureNames = { "en-US", "en-GB", "ru", "fr" };

      foreach (var name in cultureNames) {
         NumberFormatInfo nfi = CultureInfo.CreateSpecificCulture(name).NumberFormat;
         Console.WriteLine("{0,-6} {1}", name + ":", value.ToString("N3", nfi));
      }   
   }
}
// The example displays the following output:
//       en-US: 1,043.630
//       en-GB: 1,043.630
//       ru:    1 043,630
//       fr:    1 043,630
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim value As Double = 1043.62957
      Dim cultureNames() As String = { "en-US", "en-GB", "ru", "fr" }

      For Each name In cultureNames
         Dim nfi As NumberFormatInfo = CultureInfo.CreateSpecificCulture(name).NumberFormat
         Console.WriteLine("{0,-6} {1}", name + ":", value.ToString("N3", nfi))
      Next   
   End Sub
End Module
' The example displays the following output:
'       en-US: 1,043.630
'       en-GB: 1,043.630
'       ru:    1 043,630
'       fr:    1 043,630
```

### <a name="culture-sensitive-formatting-of-date-and-time-values"></a>Formattazione dipendente dalle impostazioni cultura di valori data e ora

Per impostazione predefinita, la formattazione dei valori data e ora è dipendente dalle impostazioni cultura. Se non si specificano impostazioni cultura quando si chiama un metodo di formattazione, vengono usate le convenzioni di formattazione delle impostazioni cultura del thread corrente. Questa situazione viene illustrata nell'esempio seguente in cui le impostazioni cultura del thread corrente vengono modificate quattro volte e viene chiamato il metodo [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)). In ogni caso, la stringa risultante riflette le convenzioni di formattazione delle impostazioni cultura correnti. Questo avviene perché i metodi [DateTime.ToString()](xref:System.DateTime.ToString), [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)), [DateTimeOffset.ToString()](xref:System.DateTimeOffset.ToString(System.String)) e [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) eseguono il wrapping delle chiamate ai metodi [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) e [DateTimeOffset.ToString(String, IFormatProvider)](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)).

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string[] cultureNames = { "en-US", "fr-FR", "es-MX", "de-DE" };
      DateTime dateToFormat = new DateTime(2012, 5, 28, 11, 30, 0);

      foreach (var cultureName in cultureNames) {
         // Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName);
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name);
         Console.WriteLine(dateToFormat.ToString("F"));
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//       The current culture is en-US
//       Monday, May 28, 2012 11:30:00 AM
//       
//       The current culture is fr-FR
//       lundi 28 mai 2012 11:30:00
//       
//       The current culture is es-MX
//       lunes, 28 de mayo de 2012 11:30:00 a.m.
//       
//       The current culture is de-DE
//       Montag, 28. Mai 2012 11:30:00
```

```vb
Imports System.Globalization
Imports System.Threading 

Module Example
   Public Sub Main()
      Dim cultureNames() As String = { "en-US", "fr-FR", "es-MX", "de-DE" }
      Dim dateToFormat As Date = #5/28/2012 11:30AM#

      For Each cultureName In cultureNames
         ' Change the current thread culture.
         Thread.CurrentThread.CurrentCulture = CultureInfo.CreateSpecificCulture(cultureName)
         Console.WriteLine("The current culture is {0}", 
                           Thread.CurrentThread.CurrentCulture.Name)
         Console.WriteLine(dateToFormat.ToString("F"))
         Console.WriteLine()
      Next                  
   End Sub
End Module
' The example displays the following output:
'       The current culture is en-US
'       Monday, May 28, 2012 11:30:00 AM
'       
'       The current culture is fr-FR
'       lundi 28 mai 2012 11:30:00
'       
'       The current culture is es-MX
'       lunes, 28 de mayo de 2012 11:30:00 a.m.
'       
'       The current culture is de-DE
'       Montag, 28. Mai 2012 11:30:00
```

È anche possibile formattare un valore data e ora per impostazioni cultura specifiche chiamando un overload [DateTime.ToString](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) o [DateTimeOffset.ToString](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) contenente un parametro provider e passandolo agli elementi seguenti: 

* Oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le impostazioni cultura, di cui verranno usate le convenzioni di formattazione. Il metodo [CultureInfo.GetFormat](xref:System.Globalization.CultureInfo.GetFormat(System.Type)) relativo restituisce il valore della proprietà [CultureInfo.NumberFormat](xref:System.Globalization.CultureInfo.NumberFormat), che rappresenta l'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che offre informazioni di formattazione specifiche delle impostazioni cultura per i valori numerici.

* Oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che definisce le convenzioni di formattazione specifiche delle impostazioni cultura da usare. Il metodo [GetFormat](xref:System.Globalization.DateTimeFormatInfo.GetFormat(System.Type)) relativo restituisce un'istanza di se stesso.

Nell'esempio seguente vengono usati gli oggetti [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che rappresentano le impostazioni cultura della lingua inglese di Stati Uniti e Gran Bretagna e le impostazioni cultura non associate alle lingue francese e russa per formattare una data. 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {                                                                                                    
      DateTime dat1 = new DateTime(2012, 5, 28, 11, 30, 0);
      string[] cultureNames = { "en-US", "en-GB", "ru", "fr" };

      foreach (var name in cultureNames) {
         DateTimeFormatInfo dtfi = CultureInfo.CreateSpecificCulture(name).DateTimeFormat;
         Console.WriteLine("{0}: {1}", name, dat1.ToString(dtfi));
      }   
   }
}
// The example displays the following output:
//       en-US: 5/28/2012 11:30:00 AM
//       en-GB: 28/05/2012 11:30:00
//       ru: 28.05.2012 11:30:00
//       fr: 28/05/2012 11:30:00
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dat1 As Date = #5/28/2012 11:30AM#
      Dim cultureNames() As String = { "en-US", "en-GB", "ru", "fr" }

      For Each name In cultureNames
         Dim dtfi As DateTimeFormatInfo = CultureInfo.CreateSpecificCulture(name).DateTimeFormat
         Console.WriteLine("{0}: {1}", name, dat1.ToString(dtfi))
      Next   
   End Sub
End Module
' The example displays the following output:
'       en-US: 5/28/2012 11:30:00 AM
'       en-GB: 28/05/2012 11:30:00
'       ru: 28.05.2012 11:30:00
'       fr: 28/05/2012 11:30:00
```

## <a name="the-iformattable-interface"></a>Interfaccia IFormattable

In genere, i tipi che eseguono l'overload del metodo `ToString` con una stringa di formato e un parametro [IFormatProvider](xref:System.IFormatProvider) implementano anche l'interfaccia [IFormattable](xref:System.IFormattable). Questa interfaccia dispone di un singolo membro, [IFormattable.ToString(String, IFormatProvider)](xref:System.IFormattable.ToString(System.String,System.IFormatProvider)), che include sia una stringa di formato che un provider di formato come parametri.

L'implementazione dell'interfaccia [IFormattable](xref:System.IFormattable) per la classe definita dall'applicazione offre due vantaggi: 

* Supporto per la conversione di stringhe da parte della classe [Convert](xref:System.Convert). Le chiamate ai metodi [Convert.ToString(Object)](xref:System.Convert.ToString(System.Object)) e [Convert.ToString(Object, IFormatProvider)](xref:System.Convert.ToString(System.Object,System.IFormatProvider)) chiamano automaticamente l'implementazione di [IFormattable](xref:System.IFormattable).

* Supporto per la formattazione composita. Se viene usato un elemento di formato che include una stringa di formato per formattare il tipo personalizzato, tramite Common Language Runtime viene chiamata automaticamente l'implementazione di [IFormattable](xref:System.IFormattable), che viene passata alla stringa di formato. Per altre informazioni sulla formattazione composita con metodi come `String.Format` o `Console.WriteLine`, vedere la sezione [Formattazione composita](#composite-formatting).

Nell'esempio seguente viene definita una classe `Temperature` che implementa l'interfaccia [IFormattable](xref:System.IFormattable). Sono supportati gli identificatori di formato "C" e "G" per visualizzare la temperatura in Celsius, l'identificatore di formato "F" per visualizzare la temperatura in Fahrenheit e l'identificatore di formato "K" per visualizzare la temperatura in Kelvin.

```csharp
using System;
using System.Globalization;

public class Temperature : IFormattable
{
   private decimal m_Temp;

   public Temperature(decimal temperature)
   {
      this.m_Temp = temperature;
   }

   public decimal Celsius
   {
      get { return this.m_Temp; }
   }

   public decimal Kelvin
   {
      get { return this.m_Temp + 273.15m; }   
   }

   public decimal Fahrenheit
   {
      get { return Math.Round((decimal) this.m_Temp * 9 / 5 + 32, 2); }
   }

   public override string ToString()
   {
      return this.ToString("G", null);
   }

   public string ToString(string format)
   {
      return this.ToString(format, null);
   }

   public string ToString(string format, IFormatProvider provider)  
   {
      // Handle null or empty arguments.
      if (String.IsNullOrEmpty(format)) format = "G";
      // Remove any white space and convert to uppercase.
      format = format.Trim().ToUpperInvariant();

      if (provider == null) provider = NumberFormatInfo.CurrentInfo;

      switch (format)
      {
         // Convert temperature to Fahrenheit and return string.
         case "F":
            return this.Fahrenheit.ToString("N2", provider) + "°F";
         // Convert temperature to Kelvin and return string.
         case "K":
            return this.Kelvin.ToString("N2", provider) + "K";
         // Return temperature in Celsius.
         case "C":
         case "G":
            return this.Celsius.ToString("N2", provider) + "°C";
         default:
            throw new FormatException(String.Format("The '{0}' format string is not supported.", format));
      }      
   }
}
```

```vb
Imports System.Globalization

Public Class Temperature : Implements IFormattable
   Private m_Temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.m_Temp = temperature
   End Sub

   Public ReadOnly Property Celsius() As Decimal
      Get
         Return Me.m_Temp
      End Get   
   End Property

   Public ReadOnly Property Kelvin() As Decimal
      Get
         Return Me.m_Temp + 273.15d   
      End Get
   End Property

   Public ReadOnly Property Fahrenheit() As Decimal
      Get
         Return Math.Round(CDec(Me.m_Temp * 9 / 5 + 32), 2)
      End Get      
   End Property

   Public Overrides Function ToString() As String
      Return Me.ToString("G", Nothing)
   End Function

   Public Overloads Function ToString(format As String) As String
      Return Me.ToString(format, Nothing)
   End Function

   Public Overloads Function ToString(format As String, provider As IFormatProvider) As String _  
      Implements IFormattable.ToString

      ' Handle null or empty arguments.
      If String.IsNullOrEmpty(format) Then format = "G"
      ' Remove any white space and convert to uppercase.
      format = format.Trim().ToUpperInvariant()

      If provider Is Nothing Then provider = NumberFormatInfo.CurrentInfo

      Select Case format
         ' Convert temperature to Fahrenheit and return string.
         Case "F"
            Return Me.Fahrenheit.ToString("N2", provider) & "°F"
         ' Convert temperature to Kelvin and return string.
         Case "K"
            Return Me.Kelvin.ToString("N2", provider) & "K"
         ' Return temperature in Celsius.
         Case "C", "G"
            Return Me.Celsius.ToString("N2", provider) & "°C"
         Case Else
            Throw New FormatException(String.Format("The '{0}' format string is not supported.", format))
      End Select      
   End Function
End Class
```

Nell'esempio seguente viene creata un'istanza di un oggetto `Temperature`. Viene quindi chiamato il metodo [ToString](xref:System.Convert.ToString(System.Object,System.IFormatProvider)) e vengono usate diverse stringhe di formato composite per ottenere diverse rappresentazioni di stringa di un oggetto `Temperature`. Ognuna di queste chiamate al metodo chiama, a sua volta, l'implementazione di [IFormattable](xref:System.IFormattable) della classe `Temperature`.

```csharp
public class Example
{
   public static void Main()
   {
      Temperature temp1 = new Temperature(22m);
      Console.WriteLine(Convert.ToString(temp1, new CultureInfo("ja-JP")));
      Console.WriteLine("Temperature: {0:K}", temp1);
      Console.WriteLine("Temperature: {0:F}", temp1);
      Console.WriteLine(String.Format(new CultureInfo("fr-FR"), "Temperature: {0:F}", temp1));
   }
}
// The example displays the following output:
//       22.00°C
//       Temperature: 295.15°K
//       Temperature: 71.60°F
//       Temperature: 71,60°F
```

```vb
Public Module Example
   Public Sub Main()
      Dim temp1 As New Temperature(22d)
      Console.WriteLine(Convert.ToString(temp1, New CultureInfo("ja-JP")))
      Console.WriteLine("Temperature: {0:K}", temp1)
      Console.WriteLine("Temperature: {0:F}", temp1)
      Console.WriteLine(String.Format(New CultureInfo("fr-FR"), "Temperature: {0:F}", temp1)) 
   End Sub
End Module
' The example displays the following output:
'       22.00°C
'       Temperature: 295.15°K
'       Temperature: 71.60°F
'       Temperature: 71,60°F
```

## <a name="composite-formatting"></a>Formattazione composita

Alcuni metodi, ad esempio `String.Format` e `StringBuilder.AppendFormat`, supportano la formattazione composita. Una stringa di formato composita è un tipo di modello che restituisce una singola stringa che incorpora la rappresentazione di stringa di zero, uno o più oggetti. Ogni oggetto è rappresentato nella stringa di formato composita da un elemento di formato indicizzato. L'indice dell'elemento di formato corrisponde alla posizione dell'oggetto che esso rappresenta nell'elenco di parametri del metodo. Gli indici sono a base zero. Nella chiamata seguente al metodo `String.Format`, ad esempio, il primo elemento di formato, `{0:D}`, viene sostituito dalla rappresentazione di stringa `thatDate`, il secondo elemento di formato, `{1}`, viene sostituito dalla rappresentazione di stringa `item1` e il terzo elemento di formato, `{2:C2}`, viene sostituito dalla rappresentazione di stringa `item1.Value`.

```csharp
result = String.Format("On {0:d}, the inventory of {1} was worth {2:C2}.", 
                       thatDate, item1, item1.Value);
Console.WriteLine(result);                            
// The example displays output like the following if run on a system
// whose current culture is en-US:
//       On 5/1/2009, the inventory of WidgetA was worth $107.44.
```

```vb
result = String.Format("On {0:d}, the inventory of {1} was worth {2:C2}.", _
                       thatDate, item1, item1.Value)
Console.WriteLine(result)                            
' The example displays output like the following if run on a system
' whose current culture is en-US:
'       On 5/1/2009, the inventory of WidgetA was worth $107.44.
```

Oltre a sostituire un elemento di formato con la rappresentazione di stringa dell'oggetto corrispondente, gli elementi di formato consentono anche di controllare gli aspetti seguenti: 

* Il modo specifico in cui un oggetto è rappresentato come stringa, se l'oggetto implementa l'interfaccia [IFormattable](xref:System.IFormattable) e supporta le stringhe di formato. A tale scopo, dopo l'indice dell'elemento di formato è necessario aggiungere un simbolo : (due punti) seguito da una stringa di formato valida. Nell'esempio precedente viene eseguita questa operazione formattando un valore di data con la stringa di formato "d" (modello di data breve) (ad esempio, `{0:d}`) e formattando un valore numerico con la stringa di formato "C2" (ad esempio, `{2:C2}`) per rappresentare il numero come valore di valuta con due cifre decimali. 

* La larghezza del campo che contiene la rappresentazione di stringa dell'oggetto e l'allineamento della rappresentazione di stringa in tale campo. A tale scopo, dopo l'indice dell'elemento di formato è necessario aggiungere un simbolo , (virgola) seguito dalla larghezza del campo. La stringa viene allineata a destra nel campo se la larghezza del campo è un valore positivo e viene allineata a sinistra se la larghezza del campo è un valore negativo. L'esempio seguente consente di allineare a sinistra i valori di data in un campo di 20 caratteri e di allineare a destra i valori decimali con una cifra frazionaria in un campo di 11 caratteri. 

```csharp
DateTime startDate = new DateTime(2015, 8, 28, 6, 0, 0);
decimal[] temps = { 73.452m, 68.98m, 72.6m, 69.24563m,
                   74.1m, 72.156m, 72.228m };
Console.WriteLine("{0,-20} {1,11}\n", "Date", "Temperature");
for (int ctr = 0; ctr < temps.Length; ctr++)
   Console.WriteLine("{0,-20:g} {1,11:N1}", startDate.AddDays(ctr), temps[ctr]);

// The example displays the following output:
//       Date                 Temperature
//
//       8/28/2015 6:00 AM           73.5
//       8/29/2015 6:00 AM           69.0
//       8/30/2015 6:00 AM           72.6
//       8/31/2015 6:00 AM           69.2
//       9/1/2015 6:00 AM            74.1
//       9/2/2015 6:00 AM            72.2
//       9/3/2015 6:00 AM            72.2
```

```vb
Dim startDate As New Date(2015, 8, 28, 6, 0, 0)
Dim temps() As Decimal = { 73.452, 68.98, 72.6, 69.24563,
                           74.1, 72.156, 72.228 }
Console.WriteLine("{0,-20} {1,11}", "Date", "Temperature")
Console.WriteLine()
For ctr As Integer = 0 To temps.Length - 1
   Console.WriteLine("{0,-20:g} {1,11:N1}", startDate.AddDays(ctr), temps(ctr))
Next
' The example displays the following output:
'       Date                 Temperature
'
'       8/28/2015 6:00 AM           73.5
'       8/29/2015 6:00 AM           69.0
'       8/30/2015 6:00 AM           72.6
'       8/31/2015 6:00 AM           69.2
'       9/1/2015 6:00 AM            74.1
'       9/2/2015 6:00 AM            72.2
'       9/3/2015 6:00 AM            72.2
```

Si noti che, se il componente stringa di allineamento e il componente stringa di formato sono entrambi presenti, il primo precede il secondo, ad esempio `{0,-20:g}`. 

Per altre informazioni sulla formattazione composita, vedere [Formattazione composita](composite-format.md).

## <a name="custom-formatting-with-icustomformatter"></a>Formattazione personalizzata con ICustomFormatter

Due metodi di formattazione composita, [String.Format(IFormatProvider, String, Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object[])) e [StringBuilder.AppendFormat(IFormatProvider, String, Object[])](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)), includono un parametro del provider di formato che supporta la formattazione personalizzata. Quando viene chiamato uno di questi metodi di formattazione, viene passato un oggetto [Type](xref:System.Type) che rappresenta un'interfaccia [ICustomFormatter](xref:System.ICustomFormatter) al metodo `GetFormat` del provider di formato. Il metodo `GetFormat` è quindi responsabile della restituzione dell'implementazione di [ICustomFormatter](xref:System.ICustomFormatter) che fornisce formattazione personalizzata.

L'interfaccia [ICustomFormatter](xref:System.ICustomFormatter) ha un singolo metodo, [Format(String, Object, IFormatProvider)](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)), chiamato automaticamente da un metodo di formattazione composita una volta per ogni elemento di formato in una stringa di formato composita. Il metodo [Format(String, Object, IFormatProvider)](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) ha tre parametri: una stringa di formato, che rappresenta l'argomento *formatString* in un elemento di formato, un oggetto da formattare e un oggetto [IFormatProvider](xref:System.IFormatProvider) che fornisce i servizi di formattazione. In genere, la classe che implementa [ICustomFormatter](xref:System.ICustomFormatter) implementa anche [IFormatProvider](xref:System.IFormatProvider), pertanto quest'ultimo parametro è un riferimento alla classe di formattazione personalizzata stessa. Questo metodo restituisce una rappresentazione di stringa formattata personalizzata dell'oggetto da formattare. Se il metodo non è in grado di formattare l'oggetto, deve restituire un riferimento Null.

Nell'esempio seguente viene fornita un'implementazione di [ICustomFormatter](xref:System.ICustomFormatter) denominata `ByteByByteFormatter` che consente di visualizzare i valori interi come sequenza di valori esadecimali a due cifre seguiti da uno spazio.

```csharp
public class ByteByByteFormatter : IFormatProvider, ICustomFormatter
{
   public object GetFormat(Type formatType)
   { 
      if (formatType == typeof(ICustomFormatter))
         return this;
      else
         return null;
   }

   public string Format(string format, object arg, 
                          IFormatProvider formatProvider)
   {   
      if (! formatProvider.Equals(this)) return null;

      // Handle only hexadecimal format string.
      if (! format.StartsWith("X")) return null;

      byte[] bytes;
      string output = null;

      // Handle only integral types.
      if (arg is Byte) 
         bytes = BitConverter.GetBytes((Byte) arg);
      else if (arg is Int16)
         bytes = BitConverter.GetBytes((Int16) arg);
      else if (arg is Int32)
         bytes = BitConverter.GetBytes((Int32) arg);
      else if (arg is Int64)   
         bytes = BitConverter.GetBytes((Int64) arg);
      else if (arg is SByte)
         bytes = BitConverter.GetBytes((SByte) arg);
      else if (arg is UInt16)
         bytes = BitConverter.GetBytes((UInt16) arg);
      else if (arg is UInt32)
         bytes = BitConverter.GetBytes((UInt32) arg);
      else if (arg is UInt64)
         bytes = BitConverter.GetBytes((UInt64) arg);
      else
         return null;

      for (int ctr = bytes.Length - 1; ctr >= 0; ctr--)
         output += String.Format("{0:X2} ", bytes[ctr]);   

      return output.Trim();
   }
}
```

```vb
Public Class ByteByByteFormatter : Implements IFormatProvider, ICustomFormatter
   Public Function GetFormat(formatType As Type) As Object _
                   Implements IFormatProvider.GetFormat
      If formatType Is GetType(ICustomFormatter) Then
         Return Me
      Else
         Return Nothing
      End If
   End Function

   Public Function Format(fmt As String, arg As Object, 
                          formatProvider As IFormatProvider) As String _
                          Implements ICustomFormatter.Format

      If Not formatProvider.Equals(Me) Then Return Nothing

      ' Handle only hexadecimal format string.
      If Not fmt.StartsWith("X") Then 
            Return Nothing
      End If

      ' Handle only integral types.
      If Not typeof arg Is Byte AndAlso
         Not typeof arg Is Int16 AndAlso
         Not typeof arg Is Int32 AndAlso
         Not typeof arg Is Int64 AndAlso
         Not typeof arg Is SByte AndAlso
         Not typeof arg Is UInt16 AndAlso
         Not typeof arg Is UInt32 AndAlso
         Not typeof arg Is UInt64 Then _
            Return Nothing

      Dim bytes() As Byte = BitConverter.GetBytes(arg)
      Dim output As String = Nothing

      For ctr As Integer = bytes.Length - 1 To 0 Step -1
         output += String.Format("{0:X2} ", bytes(ctr))   
      Next

      Return output.Trim()
   End Function
End Class
```

Nell'esempio seguente viene usata la classe `ByteByByteFormatter` per formattare valori interi. Si noti che il metodo [ICustomFormatter.Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) viene chiamato più di una volta nella seconda chiamata al metodo [String.Format(IFormatProvider, String, Object[])](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) e che il provider [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) predefinito viene usato nella terza chiamata al metodo, in quanto il metodo `.ByteByByteFormatter.Format` non riconosce la stringa di formato "N0" e restituisce un riferimento Null.

```csharp
public class Example
{
   public static void Main()
   {
      long value = 3210662321; 
      byte value1 = 214;
      byte value2 = 19;

      Console.WriteLine(String.Format(new ByteByByteFormatter(), "{0:X}", value));
      Console.WriteLine(String.Format(new ByteByByteFormatter(), "{0:X} And {1:X} = {2:X} ({2:000})", 
                                      value1, value2, value1 & value2));                                
      Console.WriteLine(String.Format(new ByteByByteFormatter(), "{0,10:N0}", value));
   }
}
// The example displays the following output:
//       00 00 00 00 BF 5E D1 B1
//       00 D6 And 00 13 = 00 12 (018)
//       3,210,662,321
```

```vb
Public Module Example
   Public Sub Main()
      Dim value As Long = 3210662321 
      Dim value1 As Byte = 214
      Dim value2 As Byte = 19

      Console.WriteLine((String.Format(New ByteByByteFormatter(), "{0:X}", value)))
      Console.WriteLine((String.Format(New ByteByByteFormatter(), "{0:X} And {1:X} = {2:X} ({2:000})", 
                                      value1, value2, value1 And value2)))                                
      Console.WriteLine(String.Format(New ByteByByteFormatter(), "{0,10:N0}", value))
   End Sub
End Module
' The example displays the following output:
'       00 00 00 00 BF 5E D1 B1
'       00 D6 And 00 13 = 00 12 (018)
'       3,210,662,321
```

## <a name="related-topics"></a>Argomenti correlati

Titolo | Definizione
----- | ----------
[Stringhe di formato numerico standard](standard-numeric.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori numerici. 
[Stringhe di formato numerico personalizzato](custom-numeric.md) | Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori numerici.
[Stringhe di formato di data e ora standard](standard-datetime.md) |  Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori [DateTime](xref:System.DateTime).
[Stringhe di formato di data e ora personalizzato](custom-datetime.md) | Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori [DateTime](xref:System.DateTime).
[Stringhe di formato TimeSpan standard](standard-timespan.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di intervalli di tempo.
[Stringhe di formato TimeSpan personalizzate](custom-timespan.md) | Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per intervalli di tempo.
[Stringhe di formato di enumerazione](enumeration-format.md) | Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa di valori di enumerazione.
[Formattazione composita](composite-format.md) | Viene descritto come incorporare uno o più valori formattati in una stringa, che successivamente può essere visualizzata nella console oppure scritta in un flusso.
[Esecuzione di operazioni di formattazione](performing-formatting-operations.md) | Sono elencati gli argomenti contenenti istruzioni dettagliate per l'esecuzione di operazioni di formattazione specifiche.
[Analisi di stringhe](parsing-strings.md) | Viene descritta l'inizializzazione di oggetti sui valori descritti dalle rappresentazioni in forma di stringa di tali oggetti. L'analisi è l'operazione contraria alla formattazione.

## <a name="reference"></a>Riferimento

[System.IFormattable](xref:System.IFormattable)

[System.IFormatProvider](xref:System.IFormatProvider)

[System.ICustomFormatter](xref:System.ICustomFormatter)

