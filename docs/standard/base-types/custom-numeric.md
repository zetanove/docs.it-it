---
title: Stringhe in formato numerico personalizzato
description: Stringhe in formato numerico personalizzato
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 7b1c16ee-956f-4e9c-8502-c3dd6598c51d
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 2d5a051efd074d02f2a5e9ff03c11e1d9a202d7f

---

# <a name="custom-numeric-format-strings"></a>Stringhe in formato numerico personalizzato

È possibile creare una stringa di formato numerico personalizzata costituita da uno o più identificatori numerici personalizzati, per definire la formattazione dei dati numerici. Viene considerata stringa in formato numerico personalizzato qualsiasi stringa di formato che non rientri nella categoria di [stringa in formato numerico standard](standard-numeric.md). 

Le stringhe di formato numerico personalizzate sono supportate da alcuni overload del metodo `ToString` di tutti i tipi numerici. È possibile ad esempio fornire una stringa in formato numerico ai metodi [ToString(String)](xref:System.Int32.ToString(System.String)) e [ToString(String, IFormatProvider)](xref:System.Int32.ToString(System.String,System.IFormatProvider)) di tipo [Int32](xref:System.Int32). Le stringhe in formato numerico personalizzato sono supportate anche dalla funzionalità di [formattazione composita](composite-format.md) di .NET Framework usata da alcuni metodi `Write` e `WriteLine` delle classi [Console](xref:System.Console) e [StreamWriter](xref:System.IO.StreamWriter), dal metodo [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) e dal metodo [StringBuilder.AppendFormat](xref:System.Text.StringBuilder.AppendFormat(System.IFormatProvider,System.String,System.Object)).

Nella tabella seguente vengono descritti gli identificatori di formato numerico personalizzati e viene visualizzato l'output di esempio prodotto da ogni identificatore di formato. Vedere la sezione [Note](#notes) per informazioni aggiuntive sull'uso di stringhe in formato numerico personalizzato e la sezione [Esempio](#example) per un'illustrazione completa dell'uso.

Identificatore di formato | Nome | Descrizione | Esempi
---------------- | ---- | ----------- | --------
"0" | Segnaposto zero | Sostituisce lo zero con la cifra corrispondente, se disponibile; in caso contrario, lo zero viene visualizzato nella stringa di risultato. | `1234.5678 ("00000") -> 01235`; `0.45678 ("0.00", en-US) -> 0.46`; `0.45678 ("0.00", fr-FR) -> 0,46`
"#" | Segnaposto per cifre | Sostituisce il simbolo "#" con la cifra corrispondente, se disponibile; in caso contrario, nella stringa di risultato non viene visualizzata nessuna cifra. Si noti che nella stringa di risultato non viene visualizzata nessuna cifra se la cifra corrispondente nella stringa di input equivale a uno 0 non significativo. Ad esempio, 0003 ("####") -> 3. | `1234.5678 ("#####") -> 1235`; `0.45678 ("#.##", en-US) -> .46`; `0.45678 ("#.##", fr-FR) -> ,46`
"." | Separatore decimale | Determina la posizione del separatore decimale nella stringa di risultato. | `0.45678 ("0.00", en-US) -> 0.46`; `0.45678 ("0.00", fr-FR) -> 0,46`
"," | Separatore di gruppi e rappresentazione in scala dei numeri | Viene usato sia come separatore di gruppi che come identificatore di rappresentazione in scala dei numeri. Come separatore di gruppi, inserisce un carattere separatore di gruppi localizzato tra ogni gruppo. Come identificatore di rappresentazione in scala dei numeri, divide un numero per 1000 per ogni virgola specificata. | Identificatore del separatore di gruppi: `2147483647 ("##,#", en-US) -> 2,147,483,647`; `2147483647 ("##,#", es-ES) -> 2.147.483.647`. Identificatore di rappresentazione in scala: `2147483647 ("#,#,,", en-US) -> 2,147`; `2147483647 ("#,#,,", es-ES) -> 2.147`
"%" | Segnaposto percentuale | Moltiplica un numero per 100 e inserisce un simbolo di percentuale localizzato nella stringa di risultato. | `0.3697 ("%#0.00", en-US) -> %36.97`; `0.3697 ("%#0.00", el-GR) -> %36,97`; `0.3697 ("##.0 %", en-US) -> 37.0 %`; `0.3697 ("##.0 %", el-GR) -> 37,0 %`
"‰" | Segnaposto per mille | Moltiplica un numero per 1000 e inserisce un simbolo di per mille localizzato nella stringa di risultato. | `0.03697 ("#0.00‰", en-US) -> 36.97‰`; `0.03697 ("#0.00‰", ru-RU) -> 36,97‰`
"E0", "E+0", "E-0", "e0", "e+0", "e-0" | Notazione esponenziale | Se è seguito da almeno uno 0 (zero), formatta il risultato usando la notazione esponenziale. L'utilizzo di "E" o "e" indica se il simbolo dell'esponente nella stringa di risultato deve essere, rispettivamente, maiuscolo o minuscolo. Il numero di zeri che seguono il carattere "E" o "e" determina il numero minimo di cifre nell'esponente. Un segno più (+) indica che l'esponente è sempre preceduto da un carattere di segno. Un segno meno (-) indica che solo gli esponenti negativi sono preceduti da un carattere di segno. | `987654 ("#0.0e0") -> 98.8e4`; `1503.92311 ("0.0##e+00") -> 1.504e+03`; `1.8901385E-16 ("0.0e+00") -> 1.9e-16`
\ | Carattere di escape | Fa in modo che il carattere successivo venga interpretato come valore letterale anziché come identificatore di formato personalizzato. | `987654 ("\###00\#") -> #987654#`
'string', "string" | Delimitatore di stringa letterale | Indica che i caratteri contenuti devono essere copiati nella stringa di risultato senza essere modificati. | `68 ("# ' degrees'") -> 68 degrees`
; | Separatore di sezione | Definisce le sezioni con stringhe di formato separate per numeri positivi, negativi e zero. | `12.345 ("#0.0#;(#0.0#);-\0-") -> 12.35`; `0 ("#0.0#;(#0.0#);-\0-") -> -0-`; `-12.345 ("#0.0#;(#0.0#);-\0-") -> (12.35)`; `12.345 ("#0.0#;(#0.0#)") -> 12.35`; `0 ("#0.0#;(#0.0#)") -> 0.0 ; -12.345 ("#0.0#;(#0.0#)") -> (12.35)`
Altro | Tutti gli altri caratteri | Il carattere viene copiato nella stringa di risultato senza alcuna modifica. | `68 ("# °") -> 68 °`

Nelle sezioni seguenti vengono fornite informazioni dettagliate su ognuno degli identificatori di formato numerico personalizzati.

## <a name="the-0-custom-specifier"></a>Identificatore personalizzato "0"

L'identificatore di formato personalizzato "0" serve come simbolo di segnaposto zero. Se nel valore da formattare è presente una cifra nella posizione in cui nella stringa di formato si trova lo zero, tale cifra viene copiata nella stringa di risultato. In caso contrario, nella stringa di risultato viene visualizzato uno zero. La posizione dello zero più a sinistra prima del separatore decimale e quella dello zero più a destra dopo il separatore decimale determinano l'intervallo di cifre sempre presenti nella stringa di risultato. 

L'identificatore "00" determina l'arrotondamento del valore alla cifra più vicina prima del decimale, in cui viene sempre usato l'arrotondamento a un valore diverso da zero. La formattazione di 34,5 con "00", ad esempio, restituisce come risultato il valore 35.

Nell'esempio seguente vengono visualizzati diversi valori formattati usando stringhe di formato personalizzate che includono segnaposto zero.

```csharp
double value;

value = 123;
Console.WriteLine(value.ToString("00000"));
Console.WriteLine(String.Format("{0:00000}", value));
// Displays 00123

value = 1.2;
Console.WriteLine(value.ToString("0.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                "{0:0.00}", value));
// Displays 1.20

Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:00.00}", value));
// Displays 01.20

CultureInfo daDK = CultureInfo.CreateSpecificCulture("da-DK");
Console.WriteLine(value.ToString("00.00", daDK)); 
Console.WriteLine(String.Format(daDK, "{0:00.00}", value));
// Displays 01,20

value = .56;
Console.WriteLine(value.ToString("0.0", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.0}", value));
// Displays 0.6

value = 1234567890;
Console.WriteLine(value.ToString("0,0", CultureInfo.InvariantCulture)); 
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0}", value)); 
// Displays 1,234,567,890      

CultureInfo elGR = CultureInfo.CreateSpecificCulture("el-GR");
Console.WriteLine(value.ToString("0,0", elGR)); 
Console.WriteLine(String.Format(elGR, "{0:0,0}", value));   
// Displays 1.234.567.890

value = 1234567890.123456;
Console.WriteLine(value.ToString("0,0.0", CultureInfo.InvariantCulture));   
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.0}", value));   
// Displays 1,234,567,890.1  

value = 1234.567890;
Console.WriteLine(value.ToString("0,0.00", CultureInfo.InvariantCulture));  
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.00}", value));  
// Displays 1,234.57
```

```vb
Dim value As Double

value = 123
Console.WriteLine(value.ToString("00000"))
Console.WriteLine(String.Format("{0:00000}", value))
' Displays 00123

value = 1.2
Console.Writeline(value.ToString("0.00", CultureInfo.InvariantCulture))
Console.Writeline(String.Format(CultureInfo.InvariantCulture, 
                  "{0:0.00}", value))
' Displays 1.20
Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:00.00}", value))
' Displays 01.20
Dim daDK As CultureInfo = CultureInfo.CreateSpecificCulture("da-DK")
Console.WriteLine(value.ToString("00.00", daDK))
Console.WriteLine(String.Format(daDK, "{0:00.00}", value))
' Displays 01,20

value = .56
Console.WriteLine(value.ToString("0.0", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.0}", value))
' Displays 0.6

value = 1234567890
Console.WriteLine(value.ToString("0,0", CultureInfo.InvariantCulture))  
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0}", value))  
' Displays 1,234,567,890      
Dim elGR As CultureInfo = CultureInfo.CreateSpecificCulture("el-GR")
Console.WriteLine(value.ToString("0,0", elGR))
Console.WriteLine(String.Format(elGR, "{0:0,0}", value))    
' Displays 1.234.567.890

value = 1234567890.123456
Console.WriteLine(value.ToString("0,0.0", CultureInfo.InvariantCulture))    
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.0}", value))    
' Displays 1,234,567,890.1  

value = 1234.567890
Console.WriteLine(value.ToString("0,0.00", CultureInfo.InvariantCulture))   
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0,0.00}", value))   
' Displays 1,234.57
```

## <a name="the-custom-specifier"></a>Identificatore personalizzato "#"

L'identificatore di formato personalizzato "#" serve come simbolo di segnaposto per cifre. Se il valore da formattare ha una cifra nella posizione in cui si trova il simbolo "#" nella stringa di formato, tale cifra viene copiata nella stringa di risultato. In caso contrario, nella stringa di risultato non viene memorizzato alcun valore in tale posizione. 

Si noti che questo identificatore non visualizza mai uno zero, che non è una cifra significativa, anche se lo zero è l'unica cifra della stringa. Viene visualizzato zero solo se si tratta di una cifra significativa nel numero da visualizzare. 

La stringa di formato "##" determina l'arrotondamento del valore alla cifra più vicina prima del decimale, in cui viene sempre usato l'arrotondamento a un valore diverso da zero. La formattazione di 34,5 con "##", ad esempio, restituisce come risultato il valore 35.

Nell'esempio seguente vengono visualizzati diversi valori formattati usando stringhe di formato personalizzate che includono segnaposto per cifre.

```csharp
double value;

value = 1.2;
Console.WriteLine(value.ToString("#.##", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#.##}", value));
// Displays 1.2

value = 123;
Console.WriteLine(value.ToString("#####"));
Console.WriteLine(String.Format("{0:#####}", value));
// Displays 123

value = 123456;
Console.WriteLine(value.ToString("[##-##-##]"));      
Console.WriteLine(String.Format("{0:[##-##-##]}", value));      
// Displays [12-34-56]

value = 1234567890;
Console.WriteLine(value.ToString("#"));
Console.WriteLine(String.Format("{0:#}", value));
// Displays 1234567890

Console.WriteLine(value.ToString("(###) ###-####"));
Console.WriteLine(String.Format("{0:(###) ###-####}", value));
// Displays (123) 456-7890
```

```vb
Dim value As Double

value = 1.2
Console.WriteLine(value.ToString("#.##", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#.##}", value))
' Displays 1.2

value = 123
Console.WriteLine(value.ToString("#####"))
Console.WriteLine(String.Format("{0:#####}", value))
' Displays 123

value = 123456
Console.WriteLine(value.ToString("[##-##-##]"))      
Console.WriteLine(String.Format("{0:[##-##-##]}", value))      
' Displays [12-34-56]

value = 1234567890
Console.WriteLine(value.ToString("#"))
Console.WriteLine(String.Format("{0:#}", value))
' Displays 1234567890

Console.WriteLine(value.ToString("(###) ###-####"))
Console.WriteLine(String.Format("{0:(###) ###-####}", value))
' Displays (123) 456-7890
```

Per restituire una stringa di risultato in cui le cifre mancanti o gli zeri iniziali vengono sostituiti da spazi, usare la funzionalità di [formattazione composita](composite-format.md) e specificare una lunghezza di campo, come illustrato nell'esempio seguente.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      Double value = .324;
      Console.WriteLine("The value is: '{0,5:#.###}'", value);
   }
}
// The example displays the following output if the current culture
// is en-US:
//      The value is: ' .324'
```

```vb
Module Example
   Public Sub Main()
      Dim value As Double = .324
      Console.WriteLine("The value is: '{0,5:#.###}'", value)
   End Sub
End Module
' The example displays the following output if the current culture
' is en-US:
'      The value is: ' .324'
```

## <a name="the-custom-specifier"></a>Identificatore personalizzato "."

L'identificatore di formato personalizzato "." inserisce un separatore decimale localizzato nella stringa di risultato. Il primo carattere punto nella stringa di formato determina la posizione del separatore decimale nel valore formattato. Eventuali punti aggiuntivi vengono ignorati. 

Il carattere effettivamente usato come separatore decimale nella stringa di risultato non è sempre un punto, ma viene determinato dalla proprietà [NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che controlla la formattazione.

Nell'esempio seguente viene usato l'identificatore di formato "." per definire la posizione del separatore decimale in alcune stringhe di risultato.

```csharp
double value;

value = 1.2;
Console.WriteLine(value.ToString("0.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.00}", value));
// Displays 1.20

Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:00.00}", value));
// Displays 01.20

Console.WriteLine(value.ToString("00.00", 
                CultureInfo.CreateSpecificCulture("da-DK")));
Console.WriteLine(String.Format(CultureInfo.CreateSpecificCulture("da-DK"),
                "{0:00.00}", value));
// Displays 01,20

value = .086;
Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture)); 
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#0.##%}", value)); 
// Displays 8.6%

value = 86000;
Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                "{0:0.###E+0}", value));
// Displays 8.6E+4
```

```vb
Dim value As Double

  value = 1.2
  Console.Writeline(value.ToString("0.00", CultureInfo.InvariantCulture))
  Console.Writeline(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:0.00}", value))
  ' Displays 1.20

  Console.WriteLine(value.ToString("00.00", CultureInfo.InvariantCulture))
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:00.00}", value))
  ' Displays 01.20

  Console.WriteLine(value.ToString("00.00", _
                    CultureInfo.CreateSpecificCulture("da-DK")))
  Console.WriteLine(String.Format(CultureInfo.CreateSpecificCulture("da-DK"),
                    "{0:00.00}", value))
  ' Displays 01,20

  value = .086
  Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture)) 
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:#0.##%}", value)) 
  ' Displays 8.6%

  value = 86000
  Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture))
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                    "{0:0.###E+0}", value))
' Displays 8.6E+4
```

## <a name="the-custom-specifier"></a>Identificatore personalizzato ","

Il carattere "," viene usato sia come separatore di gruppi che come identificatore di rappresentazione in scala dei numeri. 

* Separatore di gruppi: se vengono specificate una o più virgole tra due segnaposto per cifre (0 o #) che formattano le cifre integrali di un numero, viene inserito un carattere di separazione di gruppi tra ogni gruppo di numeri nella parte integrale dell'output. 

  Le proprietà [NumberGroupSeparator](xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator) e [NumberGroupSizes](xref:System.Globalization.NumberFormatInfo.NumberGroupSizes) dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente determinano il carattere usato come separatore di gruppi di numeri e la dimensione di ognuno di questi ultimi. Se ad esempio vengono usate la stringa "#, #" e le impostazioni cultura invarianti per formattare il numero 1000, l'output sarà "1,000".
  
* Identificatore di rappresentazione in scala dei numeri: se vengono specificate una o più virgole immediatamente a sinistra del separatore decimale esplicito o implicito, il numero da formattare viene diviso per 1000 per ogni virgola presente. Se ad esempio viene usata la stringa "0" per formattare il numero 100 milioni, l'output sarà "100". 

È possibile usare gli identificatori del separatore di gruppi e di rappresentazione in scala dei numeri nella stessa stringa di formato. Se ad esempio vengono usate la stringa "#,0,," e le impostazioni cultura invarianti per formattare il numero un miliardo, l'output sarà "1,000". 

Nell'esempio seguente viene illustrato l'utilizzo della virgola come separatore di gruppi.

```csharp
double value = 1234567890;
Console.WriteLine(value.ToString("#,#", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,#}", value));
// Displays 1,234,567,890      

Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,##0,,}", value));
// Displays 1,235
```

```vb
Dim value As Double = 1234567890
Console.WriteLine(value.ToString("#,#", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,#}", value))
' Displays 1,234,567,890      

Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,##0,,}", value))
' Displays 1,235
```

Nell'esempio seguente viene illustrato l'utilizzo della virgola come identificatore di rappresentazione in scala.

```csharp
double value = 1234567890;
Console.WriteLine(value.ToString("#,,", CultureInfo.InvariantCulture)); 
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,,}", value)); 
// Displays 1235   

Console.WriteLine(value.ToString("#,,,", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,,,}", value));
// Displays 1  

Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture));       
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#,##0,,}", value));       
// Displays 1,235
```  

```vb
Dim value As Double = 1234567890
  Console.WriteLine(value.ToString("#,,", CultureInfo.InvariantCulture))    
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, "{0:#,,}", value))  
  ' Displays 1235   

  Console.WriteLine(value.ToString("#,,,", CultureInfo.InvariantCulture))
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:#,,,}", value))
' Displays 1  

  Console.WriteLine(value.ToString("#,##0,,", CultureInfo.InvariantCulture))       
  Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                  "{0:#,##0,,}", value))       
' Displays 1,235
```

## <a name="the-custom-specifier"></a>Identificatore personalizzato "%"

La presenza di un segno di percentuale ("%") in una stringa di formato fa sì che un numero venga moltiplicato per 100 prima di essere formattato. Il simbolo di percentuale localizzato viene inserito nel numero stesso nella posizione in cui è stato inserito il segno % nella stringa di formato. Il carattere percentuale usato è definito dalla proprietà [PercentSymbol](xref:System.Globalization.NumberFormatInfo.PercentSymbol) dell'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) corrente.

Nell'esempio seguente vengono definite diverse stringhe di formato personalizzate che includono l'identificatore personalizzato "%".

```csharp
double value = .086;
Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#0.##%}", value));
// Displays 8.6%     
```

```vb
Dim value As Double = .086
Console.WriteLine(value.ToString("#0.##%", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:#0.##%}", value))
' Displays 8.6% 
```

## <a name="the-custom-specifier"></a>Identificatore personalizzato "‰"

Un carattere per mille (‰ or \u2030) in una stringa di formato fa sì che un numero venga moltiplicato per 1000 prima di essere formattato. Il simbolo per mille appropriato viene inserito nella stringa restituita nella posizione in cui è stato inserito il simbolo ‰ nella stringa di formato. Il carattere per mille usato viene definito dalla proprietà [NumberFormatInfo.PerMilleSymbol](xref:System.Globalization.NumberFormatInfo.PerMilleSymbol) dell'oggetto che fornisce informazioni di formattazione specifiche delle impostazioni cultura.

Nell'esempio seguente viene definita una stringa di formato personalizzata che include l'identificatore personalizzato "‰".

```csharp
double value = .00354;
string perMilleFmt = "#0.## " + '\u2030';
Console.WriteLine(value.ToString(perMilleFmt, CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:" + perMilleFmt + "}", value));
// Displays 3.54‰   
```

```vb
Dim value As Double = .00354
Dim perMilleFmt As String = "#0.## " & ChrW(&h2030)
Console.WriteLine(value.ToString(perMilleFmt, CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:" + perMilleFmt + "}", value))
' Displays 3.54 ‰
```

## <a name="the-e-and-e-custom-specifiers"></a>Identificatori personalizzati "E" e "e"

Se nella stringa di formato è presente una delle stringhe "E", "E+", "E-", "e", "e+" o "e-" immediatamente seguita da almeno uno zero, il numero viene formattato usando la notazione scientifica con una "E" o "e" inserita tra il numero e l'esponente. Il numero di zeri che seguono l'indicatore della notazione scientifica determina il numero minimo di cifre da visualizzare nell'output per l'esponente. I formati "E+" ed "e+" indicano che l'esponente deve essere sempre preceduto da un segno più o meno. I formati "E", "E-", "e" ed "e-" indicano che solo gli esponenti negativi devono essere preceduti da un carattere di segno.

Nell'esempio seguente vengono formattati alcuni valori numerici usando gli identificatori per notazione scientifica.

```csharp
double value = 86000;
Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+0}", value));
// Displays 8.6E+4

Console.WriteLine(value.ToString("0.###E+000", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+000}", value));
// Displays 8.6E+004

Console.WriteLine(value.ToString("0.###E-000", CultureInfo.InvariantCulture));
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E-000}", value));
// Displays 8.6E004
```

```vb
Dim value As Double = 86000
Console.WriteLine(value.ToString("0.###E+0", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+0}", value))
' Displays 8.6E+4

Console.WriteLine(value.ToString("0.###E+000", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E+000}", value))
' Displays 8.6E+004

Console.WriteLine(value.ToString("0.###E-000", CultureInfo.InvariantCulture))
Console.WriteLine(String.Format(CultureInfo.InvariantCulture, 
                                "{0:0.###E-000}", value))
' Displays 8.6E004
```

## <a name="the-escape-character"></a>Carattere di escape "\"

I simboli "#", "0", ".", ",", "%" e "‰" in una stringa di formato vengono interpretati come identificatori di formato anziché come caratteri letterali. A seconda della posizione in una stringa di formato personalizzata, anche la "E" maiuscola e minuscola nonché i simboli + e - possono essere interpretati come identificatori di formato. 

Per impedire che un carattere venga interpretato come un identificatore di formato, è possibile anteporvi una barra rovesciata (\), che rappresenta il carattere di escape. Il carattere di escape indica che il carattere seguente è un valore letterale carattere che deve essere incluso nella stringa di risultato senza modifiche.

Per includere una barra rovesciata in una stringa dei risultati, è necessario aggiungere un carattere di escape facendolo quindi precedere da un'altra barra rovesciata (\\). 

> [!NOTE]
> Alcuni compilatori, ad esempio il compilatore C#, possono anche interpretare un singolo carattere barra rovesciata come carattere di escape. Per assicurarsi che una stringa venga interpretata correttamente quando viene eseguita la formattazione, è possibile usare il carattere letterale di stringa verbatim (carattere @) prima della stringa in C# o aggiungere un altro carattere barra rovesciata prima di ogni barra rovesciata. Nell'esempio C# seguente vengono illustrati entrambi gli approcci.

Nell'esempio seguente viene usato il carattere di escape per evitare che durante l'operazione di formattazione i caratteri "#", "0" e "\" vengano interpretati come caratteri di escape o identificatori di formato. Nell'esempio viene usata una barra rovesciata aggiuntiva per garantire che la barra rovesciata venga interpretata come carattere letterale.

```csharp
int value = 123;
Console.WriteLine(value.ToString("\\#\\#\\# ##0 dollars and \\0\\0 cents \\#\\#\\#"));
Console.WriteLine(String.Format("{0:\\#\\#\\# ##0 dollars and \\0\\0 cents \\#\\#\\#}",
                                value));
// Displays ### 123 dollars and 00 cents ###

Console.WriteLine(value.ToString(xref:"\#\#\# ##0 dollars and \0\0 cents \#\#\#"));
Console.WriteLine(String.Format(xref:"{0:\#\#\# ##0 dollars and \0\0 cents \#\#\#}",
                                value));
// Displays ### 123 dollars and 00 cents ###

Console.WriteLine(value.ToString("\\\\\\\\\\\\ ##0 dollars and \\0\\0 cents \\\\\\\\\\\\"));
Console.WriteLine(String.Format("{0:\\\\\\\\\\\\ ##0 dollars and \\0\\0 cents \\\\\\\\\\\\}",
                                value));
// Displays \\\ 123 dollars and 00 cents \\\

Console.WriteLine(value.ToString(xref:"\\\\\\ ##0 dollars and \0\0 cents \\\\\\"));
Console.WriteLine(String.Format(xref:"{0:\\\\\\ ##0 dollars and \0\0 cents \\\\\\}",
                                value));
// Displays \\\ 123 dollars and 00 cents \\\
```

```vb
Dim value As Integer = 123
Console.WriteLine(value.ToString("\#\#\# ##0 dollars and \0\0 cents \#\#\#"))
Console.WriteLine(String.Format("{0:\#\#\# ##0 dollars and \0\0 cents \#\#\#}", 
                                value))
' Displays ### 123 dollars and 00 cents ###

Console.WriteLine(value.ToString("\\\\\\ ##0 dollars and \0\0 cents \\\\\\"))
Console.WriteLine(String.Format("{0:\\\\\\ ##0 dollars and \0\0 cents \\\\\\}", 
                                value))
' Displays \\\ 123 dollars and 00 cents \\\
```

## <a name="the-section-separator"></a>Separatore di sezione ";"

Il punto e virgola (;) è un identificatore di formato condizionale che applica una formattazione diversa a un numero, a seconda del fatto che il suo valore sia positivo, negativo o zero. A tale scopo, una stringa di formato personalizzata può contenere un massimo di tre sezioni separate da punti e virgola. Queste sezioni sono descritte nella tabella seguente. 

Numero di sezioni | Descrizione
------------------ | -----------
Una | La stringa di formato viene applicata a tutti i valori.
Due | La prima sezione viene applicata ai valori positivi e agli zeri, la seconda ai valori negativi. Se il numero da formattare è negativo, ma diventa zero dopo l'arrotondamento in base al formato della seconda sezione, lo zero risultante viene formattato in base alla prima sezione.
Tre | La prima sezione viene applicata ai valori positivi, la seconda ai valori negativi e la terza agli zeri. È possibile che la seconda sezione venga lasciata vuota, ovvero senza alcun valore tra i punti e virgola. In questo caso la prima sezione viene applicata a tutti i valori diversi da zero. Se il numero da formattare è diverso da zero, ma diventa zero dopo l'arrotondamento in base al formato della prima o della seconda sezione, lo zero risultante viene formattato in base alla terza sezione.

Con i separatori di sezione, quando viene formattato il valore finale viene ignorata qualsiasi formattazione preesistente associata a un numero. Quando vengono usati separatori di sezione, ad esempio, i numeri negativi vengono sempre visualizzati senza segno meno. Se si desidera che il valore formattato finale disponga di un segno meno, è opportuno includere il segno meno in modo esplicito nell'ambito dell'identificatore di formato personalizzato. 

Nell'esempio seguente viene usato l'identificatore di formato ";" per formattare numeri positivi, negativi e zero in modo diverso.

```csharp
double posValue = 1234;
double negValue = -1234;
double zeroValue = 0;

string fmt2 = "##;(##)";
string fmt3 = "##;(##);**Zero**";

Console.WriteLine(posValue.ToString(fmt2));  
Console.WriteLine(String.Format("{0:" + fmt2 + "}", posValue));    
// Displays 1234

Console.WriteLine(negValue.ToString(fmt2));  
Console.WriteLine(String.Format("{0:" + fmt2 + "}", negValue));    
// Displays (1234)

Console.WriteLine(zeroValue.ToString(fmt3)); 
Console.WriteLine(String.Format("{0:" + fmt3 + "}", zeroValue));
// Displays **Zero**
```

```vb
Dim posValue As Double = 1234
Dim negValue As Double = -1234
Dim zeroValue As Double = 0

Dim fmt2 As String = "##;(##)"
Dim fmt3 As String = "##;(##);**Zero**"

Console.WriteLine(posValue.ToString(fmt2))   
Console.WriteLine(String.Format("{0:" + fmt2 + "}", posValue))    
' Displays 1234

Console.WriteLine(negValue.ToString(fmt2))   
Console.WriteLine(String.Format("{0:" + fmt2 + "}", negValue))    
' Displays (1234)

Console.WriteLine(zeroValue.ToString(fmt3))  
Console.WriteLine(String.Format("{0:" + fmt3 + "}", zeroValue))
' Displays **Zero**
```

## <a name="notes"></a>Note

### <a name="floatingpoint-infinities-and-nan"></a>Valori infiniti a virgola mobile e NaN

Indipendentemente dalla stringa di formato, se il valore di un tipo a virgola mobile [Single](xref:System.Single) o [Double](xref:System.Double) è un numero infinito positivo, un numero infinito negativo o un valore NaN (Not a Number, non un numero), la stringa formattata corrisponde al valore della proprietà [PositiveInfinitySymbol](xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol), [NegativeInfinitySymbol](xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol) o [NaNSymbol](xref:System.Globalization.NumberFormatInfo.NaNSymbol) corrispondente specificata dall'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) attualmente applicabile. 

### <a name="rounding-and-fixedpoint-format-strings"></a>Arrotondamento e stringhe di formato a virgola fissa

Per le stringhe di formato a virgola fissa, ovvero stringhe di formato non contenenti caratteri di formato in notazione scientifica, i numeri vengono arrotondati al numero di posizioni decimali corrispondente al numero di segnaposto per cifre a destra del separatore decimale. Se la stringa di formato non contiene alcun separatore decimale, il numero viene arrotondato all'intero più vicino. Se le cifre del numero sono più numerose dei segnaposto per le cifre riportati a sinistra del separatore decimale, le cifre eccedenti vengono copiate nella stringa di risultato immediatamente prima del primo segnaposto per le cifre.

## <a name="example"></a>Esempio

Nell'esempio seguente vengono illustrate due stringhe di formato numerico personalizzate. In entrambi i casi il segnaposto per le cifre (#) consente di visualizzare i dati numerici e tutti gli altri caratteri vengono copiati nella stringa di risultato.

```csharp
double number1 = 1234567890;
string value1 = number1.ToString("(###) ###-####");
Console.WriteLine(value1);

int number2 = 42;
string value2 = number2.ToString("My Number = #");
Console.WriteLine(value2);
// The example displays the following output:
//       (123) 456-7890
//       My Number = 42
```

```vb
Dim number1 As Double = 1234567890
Dim value1 As String = number1.ToString("(###) ###-####")
Console.WriteLine(value1)

Dim number2 As Integer = 42
Dim value2 As String = number2.ToString("My Number = #")
Console.WriteLine(value2)
' The example displays the following output:
'       (123) 456-7890
'       My Number = 42
```

## <a name="see-also"></a>Vedere anche

[System.Globalization.NumberFormatInfo](xref:System.Globalization.NumberFormatInfo)

[Formattazione di tipi](formatting-types.md)

[Stringhe di formato numerico standard](standard-numeric.md)

[Procedura: Aggiungere zeri iniziali a un numero](pad-number.md)

[Formattazione composita](composite-format.md)




<!--HONumber=Nov16_HO3-->


