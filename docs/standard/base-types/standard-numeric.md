---
title: Stringhe di formato numerico standard
description: Stringhe di formato numerico standard
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 285faf73-466a-4af0-8eba-7e509958f240
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 4887a55690e47f7867cee28ab9b9fe258b208e54

---

# <a name="standard-numeric-format-strings"></a>Stringhe di formato numerico standard

Le stringhe di formato numerico standard vengono usate per formattare tipi numerici comuni. Una stringa di formato numerico standard usa il formato **A**_xx_, dove: 

* **A** è un carattere alfabetico denominato *identificatore di formato*. Le stringhe di formato numerico contenenti più caratteri alfabetici, inclusi gli spazi, vengono interpretate come stringhe di formato numerico personalizzate. Per altre informazioni, vedere [Stringhe di formato numerico personalizzato](custom-numeric.md). 

* *xx* è un numero intero facoltativo denominato *identificatore di precisione*. L'identificatore di precisione, compreso tra 0 e 99, controlla il numero di cifre nel risultato. L'identificatore di precisione controlla il numero di cifre nella rappresentazione di stringa di un numero. Non arrotonda il numero stesso. Per eseguire un'operazione di arrotondamento, usare i metodi [Math.Ceiling](xref:System.Math), [Math.Floor](xref:System.Math), o [Math.Round](xref:System.Math). 

Quando l'*identificatore di precisione* controlla il numero di cifre frazionarie nella stringa risultato, le stringhe risultato riflettono numeri che vengono arrotondati per eccesso (vale a dire usando [MidpointRounding.AwayFromZero](xref:System.MidpointRounding.AwayFromZero)). 

> [!NOTE]
> L'identificatore di precisione determina il numero di cifre nella stringa risultato. Per riempire una stringa risultato con spazi iniziali o finali, usare la funzionalità di [formattazione composita](composite-format.md) e definire un *componente allineamento* nell'elemento di formato. 

Le stringhe di formato numerico standard sono supportate da alcuni overload del metodo `ToString` di tutti i tipi numerici. È possibile ad esempio specificare una stringa di formato numerico per i metodi [ToString(String)](xref:System.Int32.ToString(System.String)) e [ToString(String, IFormatProvider)](xref:System.Int32.ToString(System.String,System.IFormatProvider)) di tipo [Int32](xref:System.Int32). Le stringhe di formato numerico standard sono supportate anche dalla funzionalità di [formattazione composita](composite-format.md) di .NET usata da alcuni metodi `Write` e `WriteLine` delle classi [Console](xref:System.Console) e [StreamWriter](xref:System.IO.StreamWriter), dal metodo [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) e dal metodo [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)). La funzionalità di formattazione composta consente di includere la rappresentazione di stringa di più elementi dati in un'unica stringa per specificare la larghezza di un campo e per allinearvi i numeri all'interno. Per altre informazioni, vedere [Formattazione composita](composite-format.md). 

Nella tabella seguente vengono descritti gli identificatori di formato numerico standard e viene visualizzato l'output di esempio prodotto da ogni identificatore di formato. Vedere la sezione [Note](#notes) per informazioni aggiuntive sull'uso di stringhe di formato numerico standard e la sezione [Esempio](#example) per un'illustrazione completa dell'uso.

|Identificatore di formato|Nome|Descrizione|Esempi|  
|----------------------|----------|-----------------|--------------|  
|"C" o "c"|Valuta|Risultato: un valore di valuta.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre decimali.<br /><br /> Identificatore di precisione predefinito: definito da [NumberFormatInfo.CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits).<br /><br /> |123.456 ("C", en-US) -> $123.46<br /><br /> 123.456 ("C", fr-FR) -> 123,46 €<br /><br /> 123.456 ("C", ja-JP) -> ¥123<br /><br /> -123.456 ("C3", en-US) -> ($123.456)<br /><br /> -123.456 ("C3", fr-FR) -> -123,456 €<br /><br /> -123.456 ("C3", ja-JP) -> -¥123.456|  
|"D" o "d"|Decimal|Risultato: cifre intere con segno negativo facoltativo.<br /><br /> Supportato da: solo tipi integrali.<br /><br /> Identificatore di precisione: numero minimo di cifre.<br /><br /> Identificatore di precisione predefinito: numero minimo di cifre richieste.<br /><br /> |1234 ("D") -> 1234<br /><br /> -1234 ("D6") -> -001234|  
|"E" o "e"|Esponenziale (scientifico)|Risultato: notazione esponenziale.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre decimali.<br /><br /> Identificatore di precisione predefinito: 6.<br /><br /> |1052.0329112756 ("E", en-US) -> 1.052033E+003<br /><br /> 1052.0329112756 ("e", fr-FR) -> 1,052033e+003<br /><br /> -1052.0329112756 ("e2", en-US) -> -1.05e+003<br /><br /> -1052.0329112756 ("E2", fr_FR) -> -1,05E+003|  
|"F" o "f"|A virgola fissa|Risultato: cifre integrali e decimali con segno negativo facoltativo.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre decimali.<br /><br /> Identificatore di precisione predefinito: definito da [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits).<br /><br /> |1234.567 ("F", en-US) -> 1234.57<br /><br /> 1234.567 ("F", de-DE) -> 1234,57<br /><br /> 1234 ("F1", en-US) -> 1234.0<br /><br /> 1234 ("F1", de-DE) -> 1234,0<br /><br /> -1234.56 ("F4", en-US) -> -1234.5600<br /><br /> -1234.56 ("F4", de-DE) -> -1234,5600|  
|"G" o "g"|Generale|Risultato: la più compatta tra la notazione a virgola fissa e quella scientifica.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre significative.<br /><br /> Identificatore di precisione predefinito: dipende dal tipo numerico.<br /><br /> |-123.456 ("G", en-US) -> -123.456<br /><br /> -123.456 ("G", sv-SE) -> -123,456<br /><br /> 123.4546 ("G4", en-US) -> 123.5<br /><br /> 123.4546 ("G4", sv-SE) -> 123,5<br /><br /> -1.234567890e-25 ("G", en-US) -> -1.23456789E-25<br /><br /> -1.234567890e-25 ("G", sv-SE) -> -1,23456789E-25|  
|"N" o "n"|Numero|Risultato: cifre integrali e decimali, separatori di gruppi e un separatore decimale con segno negativo facoltativo.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero desiderato di posizioni decimali.<br /><br /> Identificatore di precisione predefinito: definito da [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits).<br /><br /> |1234.567 ("N", en-US) -> 1,234.57<br /><br /> 1234.567 ("N", ru-RU) -> 1 234,57<br /><br /> 1234 ("N1", en-US) -> 1,234.0<br /><br /> 1234 ("N1", ru-RU) -> 1 234,0<br /><br /> -1234.56 ("N3", en-US) -> -1,234.560<br /><br /> -1234.56 ("N3", ru-RU) -> -1 234,560|  
|"P" o "p"|Percentuale|Risultato: numero moltiplicato per 100 e visualizzato con un simbolo di percentuale.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero desiderato di posizioni decimali.<br /><br /> Identificatore di precisione predefinito: definito da [NumberFormatInfo.PercentDecimalDigits](assetId:///P:System.Globalization.NumberFormatInfo.PercentDecimalDigits?qualifyHint=True&autoUpgrade=True).<br /><br /> |1 ("P", en-US) -> 100.00 %<br /><br /> 1 ("P", fr-FR) -> 100,00 %<br /><br /> -0.39678 ("P1", en-US) -> -39.7 %<br /><br /> -0.39678 ("P1", fr-FR) -> -39,7 %|  
|"R" o "r"|Round trip|Risultato: stringa che può eseguire il round trip a un numero identico.<br /><br /> Supportato da: [Single](xref:System.Single), [Double](xref:System.Double), e [BigInteger](xref:System.Numerics.BigInteger).<br /><br /> Identificatore di precisione: ignorato.<br /><br /> |123456789.12345678 ("R") -> 123456789.12345678<br /><br /> -1234567890.12345678 ("R") -> -1234567890.1234567|  
|"X" o "x"|Esadecimale|Risultato: stringa esadecimale.<br /><br /> Supportato da: solo tipi integrali.<br /><br /> Identificatore di precisione: numero di cifre nella stringa di risultato.<br /><br /> |255 ("X") -> FF<br /><br /> -1 ("x") -> ff<br /><br /> 255 ("x4") -> 00ff<br /><br /> -1 ("X4") -> 00FF|  
|Qualsiasi altro carattere singolo|Identificatore sconosciuto|Risultato: genera una [FormatException](xref:System.FormatException) in fase di esecuzione.|| 

## <a name="using-standard-numeric-format-strings"></a>Uso di stringhe di formato numerico standard

È possibile usare una stringa di formato numerico standard per definire la formattazione di un valore numerico in uno dei due modi seguenti:

* È possibile passare la stringa a un overload del metodo `ToString` che ha un parametro *format*. Nell'esempio seguente un valore numerico viene formattato come stringa di valuta nelle impostazioni cultura correnti (in questo caso, en-US). 

  ```csharp
  decimal value = 123.456m;
  Console.WriteLine(value.ToString("C2"));
  // Displays $123.46
  ```

  ```vb
  Dim value As Decimal = 123.456d
  Console.WriteLine(value.ToString("C2"))         
  ' Displays $123.46
  ```
  
* Può essere specificato come l'argomento *formatString* in un elemento di formato usato con metodi come [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)), [Console.WriteLine](xref:System.Console.WriteLine) e [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)). Per altre informazioni, vedere [Formattazione composita](composite-format.md). Nell'esempio seguente viene usato un elemento di formato per inserire un valore di valuta in una stringa.

  ```csharp
  decimal value = 123.456m;
  Console.WriteLine("Your account balance is {0:C2}.", value);
  // Displays "Your account balance is $123.46."
  ```

  ```vb
  Dim value As Decimal = 123.456d
  Console.WriteLine("Your account balance is {0:C2}.", value)
  ' Displays "Your account balance is $123.46."
  ```
  
  Facoltativamente, specificare un argomento alignment per indicare la lunghezza del campo numerico e se il relativo valore è allineato a destra o a sinistra. L'esempio seguente allinea a sinistra un valore corrente in un campo a 28 caratteri e allinea a destra un valore di valuta in un campo a 14 caratteri.
  
  ```csharp
  decimal[] amounts = { 16305.32m, 18794.16m };
  Console.WriteLine("   Beginning Balance           Ending Balance");
  Console.WriteLine("   {0,-28:C2}{1,14:C2}", amounts[0], amounts[1]);
  // Displays:
  //        Beginning Balance           Ending Balance
  //        $16,305.32                      $18,794.16
  ```

  ```vb
  Dim amounts() As Decimal = { 16305.32d, 18794.16d }
  Console.WriteLine("   Beginning Balance           Ending Balance")
  Console.WriteLine("   {0,-28:C2}{1,14:C2}", amounts(0), amounts(1))
  ' Displays:
  '        Beginning Balance           Ending Balance
  '        $16,305.32                      $18,794.16
  ```
  
Nelle sezioni seguenti vengono fornite informazioni dettagliate su ognuna delle stringhe di formato numerico standard.

## <a name="the-currency-c-format-specifier"></a>Identificatore di formato di valuta ("C")

L'identificatore di formato di valuta ("C") consente di convertire un numero in una stringa che rappresenta un importo di valuta. L'identificatore di precisione indica il numero desiderato di posizioni decimali nella stringa di risultato. Se l'identificatore di precisione viene omesso, viene usata la precisione predefinita definita dalla proprietà [NumberFormatInfo.CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits).

Se il valore da formattare contiene un numero di posizioni decimali maggiore del numero specificato o predefinito, il valore frazionario viene arrotondato nella stringa di risultato. Se il valore a destra del numero di posizioni decimali specificate è maggiore o uguale a 5, l'ultima cifra nella stringa di risultato viene arrotondata per eccesso.

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa restituita.

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[CurrencyPositivePattern](xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern) | Definisce la posizione del simbolo di valuta per i valori positivi.
[CurrencyNegativePattern](xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern) | Definisce la posizione del simbolo di valuta per i valori negativi e specifica se il segno negativo è rappresentato da parentesi o dalla proprietà [NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign).
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce il segno negativo usato se [CurrencyNegativePattern](xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern) indica che non vengono usate le parentesi. 
[CurrencySymbol](xref:System.Globalization.NumberFormatInfo.CurrencySymbol) | Definisce il simbolo di valuta.
[CurrencyDecimalDigits](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits) | Definisce il numero predefinito di cifre decimali in un valore di valuta. È possibile eseguire l'override di questo valore usando l'identificatore di precisione.
[CurrencyDecimalSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator) | Definisce la stringa che separa le cifre integrali da quelle decimali.
[CurrencyGroupSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator) | Definisce la stringa che separa i gruppi di numeri integrali. 
[CurrencyGroupSizes](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes) | Definisce il numero di cifre intere visualizzate in un gruppo.

Nell'esempio seguente viene formattato un valore [Double](xref:System.Double) con l'identificatore di formato di valuta. 

```csharp
double value = 12345.6789;
Console.WriteLine(value.ToString("C", CultureInfo.CurrentCulture));

Console.WriteLine(value.ToString("C3", CultureInfo.CurrentCulture));

Console.WriteLine(value.ToString("C3", 
                  CultureInfo.CreateSpecificCulture("da-DK")));
// The example displays the following output on a system whose
// current culture is English (United States):
//       $12,345.68
//       $12,345.679
//       kr 12.345,679
```

```vb
Dim value As Double = 12345.6789
Console.WriteLine(value.ToString("C", CultureInfo.CurrentCulture))

Console.WriteLine(value.ToString("C3", CultureInfo.CurrentCulture))

Console.WriteLine(value.ToString("C3", _
                  CultureInfo.CreateSpecificCulture("da-DK")))
' The example displays the following output on a system whose
' current culture is English (United States):
'       $12,345.68
'       $12,345.679
'       kr 12.345,679
```

## <a name="the-decimal-d-format-specifier"></a>Identificatore di formato decimale ("D")

L'identificatore di formato decimale ("D") consente di convertire un numero in una stringa di cifre decimali, da 0 a 9, preceduta da un segno meno se il numero è negativo. Questo formato è supportato solo per i tipi integrali.

L'identificatore di precisione indica il numero minimo di cifre che si vogliono visualizzare nella stringa risultante. Se necessario, alla sinistra del numero verranno aggiunti degli zeri in modo da raggiungere il numero di cifre specificato dall'identificatore di precisione. Se non viene specificato alcun identificatore di precisione, il valore predefinito corrisponde al valore minimo richiesto per rappresentare il numero intero senza zeri iniziali.

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Come illustrato nella tabella seguente, una singola proprietà influisce sulla formattazione della stringa di risultato. 

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo. 

Nell'esempio seguente viene formattato un valore [Int32](xref:System.Int32) con l'identificatore di formato decimale.

```csharp
int value; 

value = 12345;
Console.WriteLine(value.ToString("D"));
// Displays 12345
Console.WriteLine(value.ToString("D8"));
// Displays 00012345

value = -12345;
Console.WriteLine(value.ToString("D"));
// Displays -12345
Console.WriteLine(value.ToString("D8"));
// Displays -00012345
```

```vb
Dim value As Integer 

value = 12345
Console.WriteLine(value.ToString("D"))
' Displays 12345   
Console.WriteLine(value.ToString("D8"))
' Displays 00012345

value = -12345
Console.WriteLine(value.ToString("D"))
' Displays -12345
Console.WriteLine(value.ToString("D8"))
' Displays -00012345
```

## <a name="the-exponential-e-format-specifier"></a>Identificatore di formato esponenziale ("E")

L'identificatore di formato esponenziale ("E") consente di convertire un numero in una stringa nel formato "-d.ddd…E+ddd" o "-d.ddd…e+ddd", dove ciascuna "d" indica una cifra da 0 a 9. Se il numero è negativo, la stringa inizierà con un segno meno. Il separatore decimale è sempre preceduto esattamente da una cifra. 

L'identificatore di precisione indica il numero di cifre desiderato dopo il separatore decimale. Se l'identificatore di precisione viene omesso, verrà usato il numero predefinito di sei cifre dopo il separatore decimale. 

Il fatto che per l'identificatore di formato venga usata una lettera maiuscola o minuscola indica, rispettivamente, se l'esponente debba essere preceduto dal prefisso "E" o "e". L'esponente consiste sempre in un segno più o meno e in un minimo di tre cifre. Se necessario, vengono aggiunti all'esponente degli zeri in modo da raggiungere tale numero di cifre.

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa restituita.

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo sia per il coefficiente che per l'esponente. 
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | Definisce la stringa che separa la cifra integrale dalle cifre decimali nel coefficiente.
[PositiveSign](xref:System.Globalization.NumberFormatInfo.PositiveSign) | Definisce la stringa che indica che un esponente è positivo.

Nell'esempio seguente viene formattato un valore [Double](xref:System.Double) con l'identificatore di formato esponenziale. 

```csharp
double value = 12345.6789;
Console.WriteLine(value.ToString("E", CultureInfo.InvariantCulture));
// Displays 1.234568E+004

Console.WriteLine(value.ToString("E10", CultureInfo.InvariantCulture));
// Displays 1.2345678900E+004

Console.WriteLine(value.ToString("e4", CultureInfo.InvariantCulture));
// Displays 1.2346e+004

Console.WriteLine(value.ToString("E", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 1,234568E+004
```

```vb
Dim value As Double = 12345.6789
Console.WriteLine(value.ToString("E", CultureInfo.InvariantCulture))
' Displays 1.234568E+004

Console.WriteLine(value.ToString("E10", CultureInfo.InvariantCulture))
' Displays 1.2345678900E+004

Console.WriteLine(value.ToString("e4", CultureInfo.InvariantCulture))
' Displays 1.2346e+004

Console.WriteLine(value.ToString("E", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 1,234568E+004
```

## <a name="the-fixedpoint-f-format-specifier"></a>Identificatore di formato a virgola fissa ("F")

L'identificatore di formato a virgola fissa ("F) converte il numero di una stringa nel formato "-ddd.ddd…" dove ciascuna "d" indica una cifra (0-9). Se il numero è negativo, la stringa inizierà con un segno meno. 

L'identificatore di precisione indica il numero di posizioni decimali desiderato. Se l'identificatore di precisione viene omesso, la precisione numerica viene specificata dalla proprietà [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) corrente.

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa di risultato.

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo.
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | Definisce la stringa che separa le cifre integrali da quelle decimali.
[NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) | Definisce il numero predefinito di cifre decimali. È possibile eseguire l'override di questo valore usando l'identificatore di precisione.

Nell'esempio seguente vengono formattati un valore [Double](xref:System.Double) e un valore [Int32](xref:System.Int32) con l'identificatore di formato a virgola fissa.

```csharp
int integerNumber;
integerNumber = 17843;
Console.WriteLine(integerNumber.ToString("F", 
                  CultureInfo.InvariantCulture));
// Displays 17843.00

integerNumber = -29541;
Console.WriteLine(integerNumber.ToString("F3", 
                  CultureInfo.InvariantCulture));
// Displays -29541.000

double doubleNumber;
doubleNumber = 18934.1879;
Console.WriteLine(doubleNumber.ToString("F", CultureInfo.InvariantCulture));
// Displays 18934.19

Console.WriteLine(doubleNumber.ToString("F0", CultureInfo.InvariantCulture));
// Displays 18934

doubleNumber = -1898300.1987;
Console.WriteLine(doubleNumber.ToString("F1", CultureInfo.InvariantCulture));  
// Displays -1898300.2

Console.WriteLine(doubleNumber.ToString("F3", 
                  CultureInfo.CreateSpecificCulture("es-ES")));
// Displays -1898300,199 
```

```vb
Dim integerNumber As Integer
integerNumber = 17843
Console.WriteLine(integerNumber.ToString("F", CultureInfo.InvariantCulture))
' Displays 17843.00

integerNumber = -29541
Console.WriteLine(integerNumber.ToString("F3", CultureInfo.InvariantCulture))
' Displays -29541.000

Dim doubleNumber As Double
doubleNumber = 18934.1879
Console.WriteLine(doubleNumber.ToString("F", CultureInfo.InvariantCulture))
' Displays 18934.19

Console.WriteLine(doubleNumber.ToString("F0", CultureInfo.InvariantCulture))
' Displays 18934

doubleNumber = -1898300.1987
Console.WriteLine(doubleNumber.ToString("F1", CultureInfo.InvariantCulture))  
' Displays -1898300.2

Console.WriteLine(doubleNumber.ToString("F3", _ 
                  CultureInfo.CreateSpecificCulture("es-ES")))
' Displays -1898300,199                        
```

## <a name="the-general-g-format-specifier"></a>Identificatore di formato generale ("G")

L'identificatore di formato generale ("G") consente di convertire un numero nel formato più compatto tra la notazione scientifica e quella a virgola fissa, a seconda del tipo di numero e della presenza di un identificatore di precisione. L'identificatore di precisione definisce il numero massimo di cifre significative che possono essere visualizzate nella stringa di risultato. Se l'identificatore di precisione viene omesso o è uguale a zero, il tipo di numero determina la precisione predefinita, come indicato nella tabella seguente. 

Tipo numerico | Precisione predefinita
------------ | -----------------
[Byte](xref:System.Byte) o [SByte](xref:System.SByte) | 3 cifre
[Int16](xref:System.Int16) o [UInt16](xref:System.UInt16) | 5 cifre
[Int32](xref:System.Int32) o [UInt32](xref:System.UInt32) | 10 cifre
[Int64](xref:System.Int64) | 19 cifre
[UInt64](xref:System.UInt64) | 20 cifre
[BigInteger](xref:System.Numerics.BigInteger) | Senza limiti (come "R")
[Single](xref:System.Single) | 7 cifre
[Double](xref:System.Double) | 15 cifre
[Decimal](xref:System.Decimal) | 29 cifre

La notazione a virgola fissa verrà usata se l'esponente ottenuto esprimendo il numero con la notazione scientifica risulta maggiore di -5 e minore dell'identificatore di precisione. In caso contrario, verrà usata la notazione scientifica. Il risultato contiene un separatore decimale, se richiesto, e gli zeri finali dopo la virgola decimale vengono omessi. Se l'identificatore di precisione è presente e il numero di cifre significative nel risultato è superiore alla precisione specificata, le cifre finali in eccesso vengono rimosse mediante arrotondamento. 

Se, tuttavia, il numero è di tipo [Decimal](xref:System.Decimal) e l'identificatore di precisione viene omesso, viene usata sempre la notazione a virgola fissa e gli zeri finali vengono mantenuti.

Se viene usata la notazione scientifica, l'esponente nel risultato sarà preceduto da un prefisso "E" se l'identificatore di formato è "G" o da un prefisso "e" se l'identificatore di formato è "g". L'esponente contiene un minimo di due cifre. Questo aspetto è diverso rispetto al formato per la notazione scientifica, prodotto dall'identificatore di formato esponenziale, che include un minimo di tre cifre nell'esponente.

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa risultato.

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo.
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | Definisce la stringa che separa le cifre integrali da quelle decimali.
[PositiveSign](xref:System.Globalization.NumberFormatInfo.PositiveSign) | Definisce la stringa che indica che un esponente è positivo. 

Nell'esempio seguente vengono formattati diversi valori a virgola mobile con l'identificatore di formato generale.

```csharp
double number;

number = 12345.6789;      
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture));
// Displays  12345.6789
Console.WriteLine(number.ToString("G", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 12345,6789

Console.WriteLine(number.ToString("G7", CultureInfo.InvariantCulture));
// Displays 12345.68 

number = .0000023;
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture));
// Displays 2.3E-06       
Console.WriteLine(number.ToString("G", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 2,3E-06

number = .0023;
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture));
// Displays 0.0023

number = 1234;
Console.WriteLine(number.ToString("G2", CultureInfo.InvariantCulture));
// Displays 1.2E+03

number = Math.PI;
Console.WriteLine(number.ToString("G5", CultureInfo.InvariantCulture));
// Displays 3.1416    
```

```vb
Dim number As Double

number = 12345.6789      
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture))
' Displays  12345.6789
Console.WriteLine(number.ToString("G", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 12345,6789

Console.WriteLine(number.ToString("G7", CultureInfo.InvariantCulture))
' Displays 12345.68 

number = .0000023
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture))
' Displays 2.3E-06       
Console.WriteLine(number.ToString("G", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 2,3E-06

number = .0023
Console.WriteLine(number.ToString("G", CultureInfo.InvariantCulture))
' Displays 0.0023

number = 1234
Console.WriteLine(number.ToString("G2", CultureInfo.InvariantCulture))
' Displays 1.2E+03

number = Math.Pi
Console.WriteLine(number.ToString("G5", CultureInfo.InvariantCulture))
' Displays 3.1416
```

## <a name="the-numeric-n-format-specifier"></a>Identificatore di formato numerico ("N")

L'identificatore di formato numerico ("N") converte un numero in una stringa in formato "-c.ccc.ccc,ccc…", dove "-" indica un simbolo di numero negativo, se richiesto, "c" indica una cifra (0-9), "." indica il separatore delle migliaia tra gruppi numerici e "," indica il simbolo di separatore decimale. L'identificatore di precisione indica il numero di cifre desiderato dopo il separatore decimale. Se l'identificatore di precisione viene omesso, il numero di cifre decimali viene definito dalla proprietà [NumberFormatInfo.NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) corrente.

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa risultato.

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo.
[NumberNegativePattern](xref:System.Globalization.NumberFormatInfo.NumberNegativePattern) | Definisce il formato dei valori negativi e specifica se il segno negativo è rappresentato da parentesi o dalla proprietà [NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign).
[NumberGroupSizes](xref:System.Globalization.NumberFormatInfo.NumberGroupSizes) | Definisce il numero di cifre integrali visualizzate tra i separatori di gruppi.
[NumberGroupSeparator](xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator) | Definisce la stringa che separa i gruppi di numeri integrali.
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | Definisce la stringa che separa le cifre integrali da quelle decimali.
[NumberDecimalDigits](xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits) | Definisce il numero predefinito di cifre decimali. È possibile eseguire l'override di questo valore usando un identificatore di precisione.

Nell'esempio seguente vengono formattati diversi valori a virgola mobile con l'identificatore di formato numerico.

```csharp
double dblValue = -12445.6789;
Console.WriteLine(dblValue.ToString("N", CultureInfo.InvariantCulture));
// Displays -12,445.68
Console.WriteLine(dblValue.ToString("N1", 
                  CultureInfo.CreateSpecificCulture("sv-SE")));
// Displays -12 445,7

int intValue = 123456789;
Console.WriteLine(intValue.ToString("N1", CultureInfo.InvariantCulture));
// Displays 123,456,789.0 
```

```vb
Dim dblValue As Double = -12445.6789
Console.WriteLine(dblValue.ToString("N", CultureInfo.InvariantCulture))
' Displays -12,445.68
Console.WriteLine(dblValue.ToString("N1", _
                  CultureInfo.CreateSpecificCulture("sv-SE")))
' Displays -12 445,7

Dim intValue As Integer = 123456789
Console.WriteLine(intValue.ToString("N1", CultureInfo.InvariantCulture))
' Displays 123,456,789.0 
```

## <a name="the-percent-p-format-specifier"></a>Identificatore di formato percentuale ("P")

L'identificatore di formato percentuale ("P") moltiplica un numero per 100 e lo converte in una stringa che rappresenta una percentuale. L'identificatore di precisione indica il numero di posizioni decimali desiderato. Se l'identificatore di precisione viene omesso, viene usata la precisione numerica predefinita specificata dalla proprietà [PercentDecimalDigits](xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits) corrente.

Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa restituita.

proprietà NumberFormatInfo | Descrizione
------------------------- | -----------
[PercentPositivePattern](xref:System.Globalization.NumberFormatInfo.PercentPositivePattern) | Definisce la posizione del simbolo di percentuale per i valori positivi.
[PercentNegativePattern](xref:System.Globalization.NumberFormatInfo.PercentNegativePattern) | 
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo.
[PercentSymbol](xref:System.Globalization.NumberFormatInfo.PercentSymbol) | Definisce il simbolo di percentuale.
[PercentDecimalDigits](xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits) | Definisce il numero predefinito di cifre decimali in un valore percentuale. È possibile eseguire l'override di questo valore usando l'identificatore di precisione.
[PercentDecimalSeparator](xref:System.Globalization.NumberFormatInfo.PercentDecimalSeparator) | Definisce la stringa che separa le cifre integrali da quelle decimali.
[PercentGroupSeparator](xref:System.Globalization.NumberFormatInfo.PercentGroupSeparator) | Definisce la stringa che separa i gruppi di numeri integrali. 
[PercentGroupSizes](xref:System.Globalization.NumberFormatInfo.PercentGroupSizes) | Definisce il numero di cifre intere visualizzate in un gruppo.

Nell'esempio seguente vengono formattati diversi valori a virgola mobile con l'identificatore di formato percentuale.

```csharp
double number = .2468013;
Console.WriteLine(number.ToString("P", CultureInfo.InvariantCulture));
// Displays 24.68 %
Console.WriteLine(number.ToString("P", 
                  CultureInfo.CreateSpecificCulture("hr-HR")));
// Displays 24,68%     
Console.WriteLine(number.ToString("P1", CultureInfo.InvariantCulture));
// Displays 24.7 %
```

```vb
Dim number As Double = .2468013
Console.WriteLine(number.ToString("P", CultureInfo.InvariantCulture))
' Displays 24.68 %
Console.WriteLine(number.ToString("P", _
                  CultureInfo.CreateSpecificCulture("hr-HR")))
' Displays 24,68%     
Console.WriteLine(number.ToString("P1", CultureInfo.InvariantCulture))
' Displays 24.7 %
```

## <a name="the-roundtrip-r-format-specifier"></a>Identificatore di formato di round trip ("R")

L'identificatore di formato di round trip ("R") viene usato per garantire che un valore numerico convertito in una stringa venga riportato al medesimo valore numerico. Questo formato è supportato solo per i tipi [Single](xref:System.Single), [Double](xref:System.Double) e [BigInteger](xref:System.Numerics.BigInteger). 

Quando un valore [BigInteger](xref:System.Numerics.BigInteger) viene formattato usando questo identificatore, la relativa rappresentazione di stringa contiene tutte le cifre significative nel valore [BigInteger](xref:System.Numerics.BigInteger). Quando un valore [Single](xref:System.Single) o [Double](xref:System.Double) viene formattato con questo identificatore, ne viene dapprima eseguito il test usando il formato generale, con 15 cifre di precisione nel caso di un tipo [Double](xref:System.Double) e 7 cifre nel caso di un tipo [Single](xref:System.Single). Se la riconversione del valore nello stesso valore numerico iniziale viene eseguita correttamente, il valore verrà formattato con l'identificatore di formato generale. Se il valore non viene riconvertito correttamente nello stesso valore numerico, viene formattato con 17 cifre di precisione nel caso di un tipo [Double](xref:System.Double) e 9 cifre nel caso di un tipo [Single](xref:System.Single). 

Sebbene sia possibile includere un identificatore di precisione, questo viene ignorato. Quando si usa questo identificatore, infatti, il formato della riconversione ha la precedenza sulla precisione. 

La stringa risultato è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che consentono di controllare la formattazione della stringa risultato.

Proprietà di NumberFormatInfo | Descrizione
------------------------- | -----------
[NegativeSign](xref:System.Globalization.NumberFormatInfo.NegativeSign) | Definisce la stringa che indica che un numero è negativo.
[NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) | Definisce la stringa che separa le cifre integrali da quelle decimali.
[PositiveSign](xref:System.Globalization.NumberFormatInfo.PositiveSign) | Definisce la stringa che indica che un esponente è positivo.

 Nell'esempio seguente vengono formattati valori [Double](xref:System.Double) con l'identificatore di formato round trip.

```csharp
double value;

value = Math.PI;
Console.WriteLine(value.ToString("r"));
// Displays 3.1415926535897931
Console.WriteLine(value.ToString("r", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays 3,1415926535897931
value = 1.623e-21;
Console.WriteLine(value.ToString("r"));
// Displays 1.623E-21
```

```vb
Dim value As Double

value = Math.Pi
Console.WriteLine(value.ToString("r"))
' Displays 3.1415926535897931
Console.WriteLine(value.ToString("r", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays 3,1415926535897931
value = 1.623e-21
Console.WriteLine(value.ToString("r"))
' Displays 1.623E-21
```

## <a name="the-hexadecimal-x-format-specifier"></a>Identificatore di formato esadecimale ("X")

L'identificatore di formato esadecimale ("X") consente di convertire un numero in una stringa di cifre esadecimali. Il fatto che per l'identificatore di formato venga usata una lettera maiuscola o minuscola indica, rispettivamente, se usare caratteri maiuscoli o minuscoli per le cifre esadecimali maggiori di 9. usare ad esempio "X" per produrre la stringa "ABCDEF" e "x" per produrre "abcdef". Questo formato è supportato solo per i tipi integrali.

L'identificatore di precisione indica il numero minimo di cifre che si vogliono visualizzare nella stringa risultante. Se necessario, alla sinistra del numero verranno aggiunti degli zeri in modo da raggiungere il numero di cifre specificato dall'identificatore di precisione.

La stringa risultato non è influenzata dalle informazioni sulla formattazione dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente. 

Nell'esempio seguente vengono formattati valori [Int32](xref:System.Int32) con l'identificatore di formato esadecimale.

```csharp
int value; 

value = 0x2045e;
Console.WriteLine(value.ToString("x"));
// Displays 2045e
Console.WriteLine(value.ToString("X"));
// Displays 2045E
Console.WriteLine(value.ToString("X8"));
// Displays 0002045E

value = 123456789;
Console.WriteLine(value.ToString("X"));
// Displays 75BCD15
Console.WriteLine(value.ToString("X2"));
// Displays 75BCD15
```

```vb
Dim value As Integer 

value = &h2045e
Console.WriteLine(value.ToString("x"))
' Displays 2045e
Console.WriteLine(value.ToString("X"))
' Displays 2045E
Console.WriteLine(value.ToString("X8"))
' Displays 0002045E

value = 123456789
Console.WriteLine(value.ToString("X"))
' Displays 75BCD15
Console.WriteLine(value.ToString("X2"))
' Displays 75BCD15
```

## <a name="notes"></a>Note

### <a name="numberformatinfo-properties"></a>Proprietà NumberFormatInfo

La formattazione è influenzata dalle proprietà dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente, che viene specificato in modo implicito dalle impostazioni cultura del thread corrente o in modo esplicito dal parametro [IFormatProvider](xref:System.IFormatProvider) del metodo che chiama la formattazione. Specificare un oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) o [CultureInfo](xref:System.Globalization.CultureInfo) per il parametro. 

### <a name="integral-and-floatingpoint-numeric-types"></a>Tipi numerici integrali e a virgola mobile

Alcune descrizioni di identificatori di formato numerico standard fanno riferimento a tipi numerici integrali o a virgola mobile. I tipi numerici integrali sono [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), [UInt64](xref:System.UInt64) e [BigInteger](xref:System.Numerics.BigInteger). I tipi numerici a virgola mobile sono [Decimal](xref:System.Decimal), [Single](xref:System.Single) e [Double](xref:System.Double). 

### <a name="floatingpoint-infinities-and-nan"></a>Valori infiniti a virgola mobile e NaN

Indipendentemente dalla stringa di formato, se il valore di un tipo a virgola mobile [Single](xref:System.Single) o [Double](xref:System.Double) è un numero infinito positivo, un numero infinito negativo o un valore NaN (Not a Number, non un numero), la stringa formattata corrisponde al valore della proprietà [PositiveInfinitySymbol](xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol), [NegativeInfinitySymbol](xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol) o [NaNSymbol](xref:System.Globalization.NumberFormatInfo.NaNSymbol) corrispondente specificata dall'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) attualmente applicabile.

## <a name="example"></a>Esempio

Nell'esempio seguente vengono formattati un valore numerico a virgola mobile e uno integrale usando le impostazioni cultura en-US e tutti gli identificatori di formato numerico standard. In questo esempio vengono usati due tipi numerici particolari ([Double](xref:System.Double) e [Int32](xref:System.Int32)), ma i risultati sarebbero simili per tutti gli altri tipi di base numerici ([Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [Int64](xref:System.Int64), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), [UInt64](xref:System.UInt64) e [BigInteger](xref:System.Numerics.BigInteger), [Decimal](xref:System.Decimal) e [Single](xref:System.Single)). 

```csharp
using System;
using System.Globalization;
using System.Threading;

public class NumericFormats
{
   public static void Main()
   {
      // Display string representations of numbers for en-us culture
      CultureInfo ci = new CultureInfo("en-us");

      // Output floating point values
      double floating = 10761.937554;
      Console.WriteLine("C: {0}", 
              floating.ToString("C", ci));           // Displays "C: $10,761.94"
      Console.WriteLine("E: {0}", 
              floating.ToString("E03", ci));         // Displays "E: 1.076E+004"
      Console.WriteLine("F: {0}", 
              floating.ToString("F04", ci));         // Displays "F: 10761.9376"         
      Console.WriteLine("G: {0}",  
              floating.ToString("G", ci));           // Displays "G: 10761.937554"
      Console.WriteLine("N: {0}", 
              floating.ToString("N03", ci));         // Displays "N: 10,761.938"
      Console.WriteLine("P: {0}", 
              (floating/10000).ToString("P02", ci)); // Displays "P: 107.62 %"
      Console.WriteLine("R: {0}", 
              floating.ToString("R", ci));           // Displays "R: 10761.937554"            
      Console.WriteLine();

      // Output integral values
      int integral = 8395;
      Console.WriteLine("C: {0}", 
              integral.ToString("C", ci));           // Displays "C: $8,395.00"
      Console.WriteLine("D: {0}", 
              integral.ToString("D6", ci));          // Displays "D: 008395" 
      Console.WriteLine("E: {0}", 
              integral.ToString("E03", ci));         // Displays "E: 8.395E+003"
      Console.WriteLine("F: {0}", 
              integral.ToString("F01", ci));         // Displays "F: 8395.0"    
      Console.WriteLine("G: {0}",  
              integral.ToString("G", ci));           // Displays "G: 8395"
      Console.WriteLine("N: {0}", 
              integral.ToString("N01", ci));         // Displays "N: 8,395.0"
      Console.WriteLine("P: {0}", 
              (integral/10000.0).ToString("P02", ci)); // Displays "P: 83.95 %"
      Console.WriteLine("X: 0x{0}", 
              integral.ToString("X", ci));           // Displays "X: 0x20CB"
      Console.WriteLine();
   }
}
```

```vb
Option Strict On

Imports System.Globalization
Imports System.Threading

Module NumericFormats
   Public Sub Main()
      ' Display string representations of numbers for en-us culture
      Dim ci As New CultureInfo("en-us")

      ' Output floating point values
      Dim floating As Double = 10761.937554
      Console.WriteLine("C: {0}", _
              floating.ToString("C", ci))           ' Displays "C: $10,761.94"
      Console.WriteLine("E: {0}", _
              floating.ToString("E03", ci))         ' Displays "E: 1.076E+004"
      Console.WriteLine("F: {0}", _
              floating.ToString("F04", ci))         ' Displays "F: 10761.9376"         
      Console.WriteLine("G: {0}", _ 
              floating.ToString("G", ci))           ' Displays "G: 10761.937554"
      Console.WriteLine("N: {0}", _
              floating.ToString("N03", ci))         ' Displays "N: 10,761.938"
      Console.WriteLine("P: {0}", _
              (floating/10000).ToString("P02", ci)) ' Displays "P: 107.62 %"
      Console.WriteLine("R: {0}", _
              floating.ToString("R", ci))           ' Displays "R: 10761.937554"            
      Console.WriteLine()

      ' Output integral values
      Dim integral As Integer = 8395
      Console.WriteLine("C: {0}", _
              integral.ToString("C", ci))           ' Displays "C: $8,395.00"
      Console.WriteLine("D: {0}", _
              integral.ToString("D6"))              ' Displays "D: 008395" 
      Console.WriteLine("E: {0}", _
              integral.ToString("E03", ci))         ' Displays "E: 8.395E+003"
      Console.WriteLine("F: {0}", _
              integral.ToString("F01", ci))         ' Displays "F: 8395.0"    
      Console.WriteLine("G: {0}", _ 
              integral.ToString("G", ci))           ' Displays "G: 8395"
      Console.WriteLine("N: {0}", _
              integral.ToString("N01", ci))         ' Displays "N: 8,395.0"
      Console.WriteLine("P: {0}", _
              (integral/10000).ToString("P02", ci)) ' Displays "P: 83.95 %"
      Console.WriteLine("X: 0x{0}", _
              integral.ToString("X", ci))           ' Displays "X: 0x20CB"
      Console.WriteLine()
   End Sub
End Module
```

## <a name="see-also"></a>Vedere anche

[System.Globalization.NumberFormatInfo](xref:System.Globalization.NumberFormatInfo)

[Stringhe di formato numerico personalizzato](custom-numeric.md)

[Formattazione di tipi](formatting-types.md)

[Procedura: Aggiungere zeri iniziali a un numero](pad-number.md)

[Formattazione composita](composite-format.md)



<!--HONumber=Nov16_HO3-->


