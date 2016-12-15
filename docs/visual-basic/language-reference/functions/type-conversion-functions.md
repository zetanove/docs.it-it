---
title: "Type Conversion Functions (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.CUShort"
  - "vb.csng"
  - "vb.CDate"
  - "CByte"
  - "CSng"
  - "vb.CDec"
  - "CBool"
  - "CStr"
  - "vb.CULng"
  - "CDec"
  - "CVErr"
  - "CDbl"
  - "CShort"
  - "vb.CObj"
  - "vb.CVErr"
  - "CULng"
  - "vb.cdbl"
  - "vb.cbool"
  - "CObj"
  - "CDate"
  - "CLng"
  - "vb.cstr"
  - "vb.cbyte"
  - "vb.clng"
  - "vb.CChar"
  - "CUShort"
  - "vb.CUInt"
  - "vb.cint"
  - "vb.CShort"
  - "CInt"
  - "CUInt"
  - "CChar"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CDate function"
  - "CByte function"
  - "Integer data type, converting"
  - "string conversion, conversion functions"
  - "fractions"
  - "data types [Visual Basic], converting"
  - "text, converting"
  - "CDec function"
  - "Char data type, converting"
  - "type conversion, functions for"
  - "Single data type, converting"
  - "numbers, rounding"
  - "rounding numbers, type conversion"
  - "CUShort function"
  - "Long data type, converting"
  - "return values, data types"
  - "single-precision numbers, converting"
  - "data type conversion, functions for"
  - "CStr function"
  - "times, converting"
  - "CSng function"
  - "conversions, type conversion functions"
  - "CBool function"
  - "CDbl function"
  - "CUInt function"
  - "Currency data type, conversion functions"
  - "numbers, converting"
  - "Double data type, converting"
  - "CLng function"
  - "CSByte function"
  - "double-precision numbers"
  - "Decimal data type, converting"
  - "Boolean data type, converting"
  - "integers, type conversion functions"
  - "dates, converting"
  - "CULng function"
  - "CInt function"
  - "Date data type, converting"
  - "Byte data type, converting"
  - "String data type, converting"
  - "CChar function"
  - "banker's rounding"
  - "Short data type, converting"
  - "rounding numbers, banker's rounding"
  - "type conversion, Visual Basic vs. .NET Framework"
ms.assetid: d9d8d165-f967-44ff-a6cd-598e4740a99e
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type Conversion Functions (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Queste funzioni vengono compilate inline, ossia il codice di conversione fa parte del codice con cui viene valutata l'espressione.  Talvolta non sono presenti chiamate a una routine per effettuare la conversione e questo contribuisce al miglioramento delle prestazioni.  Ciascuna funzione consente la conversione di un'espressione in un tipo di dati specifico.  
  
## Sintassi  
  
```  
CBool(expression)  
CByte(expression)  
CChar(expression)  
CDate(expression)  
CDbl(expression)  
CDec(expression)  
CInt(expression)  
CLng(expression)  
CObj(expression)  
CSByte(expression)  
CShort(expression)  
CSng(expression)  
CStr(expression)  
CUInt(expression)  
CULng(expression)  
CUShort(expression)  
```  
  
## Parte  
 `expression`  
 Obbligatorio.  Qualsiasi espressione del tipo di dati di origine.  
  
## Tipo di dati del valore restituito  
 Il nome della funzione determina il tipo di dati del valore restituito, come illustrato nella tabella riportata di seguito.  
  
|Nome funzione|Tipo di dati restituito|Intervallo per l'argomento `expression`|  
|-------------------|-----------------------------|---------------------------------------------|  
|`CBool`|[Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|Qualsiasi espressione `Char`, `String` o numerica valida.|  
|`CByte`|[Byte Data Type](../../../visual-basic/language-reference/data-types/byte-data-type.md)|Da 0 a 255 \(senza segno\). Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CChar`|[Char Data Type](../../../visual-basic/language-reference/data-types/char-data-type.md)|Qualsiasi espressione `Char` o `String` valida. Viene convertito solo il primo carattere di un'espressione `String`. Il valore può essere compreso tra 0 e 65.535 \(senza segno\).|  
|`CDate`|[Date Data Type](../../../visual-basic/language-reference/data-types/date-data-type.md)|Qualsiasi rappresentazione valida di data e ora.|  
|`CDbl`|[Double Data Type](../../../visual-basic/language-reference/data-types/double-data-type.md)|Da \-1,79769313486231570E\+308 a \-4,94065645841246544E\-324 per valori negativi; da 4,94065645841246544E\-324 a 1,79769313486231570E\+308 per valori positivi.|  
|`CDec`|[Decimal Data Type](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|\+\/\-79.228.162.514.264.337.593.543.950.335 per numeri con fattore di divisione zero, ossia numeri senza decimali.  Per numeri con 28 posizioni decimali, l'intervallo è \+\/\-7,9228162514264337593543950335.  Il numero più basso possibile diverso da zero è 0,0000000000000000000000000001 \(\+\/\-1E\-28\).|  
|`CInt`|[Integer Data Type](../../../visual-basic/language-reference/data-types/integer-data-type.md)|Da \-2.147.483.648 a 2.147.483.647. Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CLng`|[Long Data Type](../../../visual-basic/language-reference/data-types/long-data-type.md)|Da \-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807. Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CObj`|[Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md)|Qualsiasi espressione valida.|  
|`CSByte`|[SByte Data Type](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|Da \-128 a 127. Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CShort`|[Short Data Type](../../../visual-basic/language-reference/data-types/short-data-type.md)|Da \-32.768 a 32.767. Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CSng`|[Single Data Type](../../../visual-basic/language-reference/data-types/single-data-type.md)|Da \-3,402823E\+38 a \-1,401298E\-45 per valori negativi; da 1,401298E\-45 a 3,402823E\+38 per valori positivi.|  
|`CStr`|[String Data Type](../../../visual-basic/language-reference/data-types/string-data-type.md)|I valori restituiti da `CStr` variano in base all'argomento `expression`.  Vedere [Return Values for the CStr Function](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md).|  
|`CUInt`|[UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|Da 0 a 4.294.967.295 \(senza segno\). Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CULng`|[ULong Data Type](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|Da 0 a 18.446.744.073.709.551.615 \(senza segno\). Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
|`CUShort`|[UShort Data Type](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|Da 0 a 65.535 \(senza segno\). Le parti frazionarie vengono arrotondate.<sup>1</sup>|  
  
 <sup>1</sup> Alle parti frazionarie può essere applicato uno speciale tipo di *arrotondamento*.  Per ulteriori informazioni, vedere la sezione relativa alle osservazioni.  
  
## Note  
 Di norma si consiglia di utilizzare le funzioni di conversione dei tipi di Visual Basic anziché i metodi .NET Framework, ad esempio `ToString()`, sulla classe <xref:System.Convert> oppure su una singola classe o struttura di tipi.  Le funzioni di Visual Basic sono state appositamente progettate per l'interazione ottimale con il codice Visual Basic e contribuiscono a rendere il codice sorgente più breve e più facilmente leggibile.  Inoltre, i metodi di conversione .NET Framework non producono sempre gli stessi risultati delle funzioni di Visual Basic, ad esempio quando vengono convertiti valori `Boolean` in `Integer`.  Per ulteriori informazioni, vedere [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
## Comportamento  
  
-   **Coercizione.** In generale, è possibile utilizzare le funzioni di conversione dei tipi di dati per assegnare il risultato di un'operazione a uno specifico tipo di dati anziché al tipo predefinito.  È possibile, ad esempio, utilizzare `CDec` per eseguire operazioni aritmetiche su valori decimali nei casi in cui in genere si effettuano operazioni a precisione singola, a precisione doppia o con valori integer.  
  
-   **Conversioni non riuscite.** Se il valore `expression` passato alla funzione non è compreso nell'intervallo del tipo di dati in cui viene convertito, verrà generata un'eccezione <xref:System.OverflowException>.  
  
-   **Parti frazionarie.** Quando si converte un valore non integrale in un tipo integrale, le funzioni di conversione dei valori integer \(`CByte`, `CInt`, `CLng`, `CSByte`, `CShort`, `CUInt`, `CULng` e `CUShort`\) rimuovono la parte frazionaria e arrotondano il valore all'integer più vicino.  
  
     Se la parte frazionaria corrisponde esattamente a 0,5, le funzioni di conversione dei valori integer la arrotondano al valore integer pari più vicino.  Ad esempio, 0,5 si arrotonda a 0, e 1,5 e 2,5 si arrotondano entrambi a 2.  Alcune volte viene chiamato *arrotondamento* e ha lo scopo di compensare la distorsione che potrebbe accumularsi quando si aggiungono molti numeri di questo tipo.  
  
     `CInt` e `CLng` differiscono dalle funzioni <xref:Microsoft.VisualBasic.Conversion.Int%2A> e <xref:Microsoft.VisualBasic.Conversion.Fix%2A> che troncano la parte frazionaria di un numero anziché arrotondarla.  Le funzioni `Fix` e `Int`, inoltre, restituiscono sempre un valore dello stesso tipo di quello passato.  
  
-   **Conversioni di data\/ora.** Utilizzare la funzione <xref:Microsoft.VisualBasic.Information.IsDate%2A> per determinare se è possibile convertire un valore in una data e ora.  `CDate` riconosce valori letterali di data e ora, ma non i valori numerici.  Per convertire un valore `Date` di Visual Basic 6.0 in un valore `Date` di Visual Basic 2005 o versioni successive, è possibile utilizzare il metodo <xref:System.DateTime.FromOADate%2A?displayProperty=fullName>.  
  
-   **Valori di data\/ora neutri.** Il [Date Data Type](../../../visual-basic/language-reference/data-types/date-data-type.md) contiene sempre informazioni sia sulla data che sull'ora.  Ai fini della conversione del tipo, Visual Basic considera 1\/1\/0001 \(1 gennaio dell'anno 1\) come *valore neutro* per la data e 00:00:00 \(mezzanotte\) come valore neutro per l'ora.  Se si converte un valore `Date` in una stringa, `CStr` non include i valori neutri nella stringa risultante.  Se ad esempio il valore `#January 1, 0001 9:30:00#` viene convertito in una stringa, il risultato sarà "9:30:00 AM" e le informazioni sulla data non verranno visualizzate.  Le informazioni della data, tuttavia, sono comunque presenti nel valore `Date` originale e possono essere recuperate con funzioni quali <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>.  
  
-   **Sensibilità alle impostazioni cultura.** Le funzioni di conversione dei tipi che riguardano le stringhe eseguono conversioni in base alle impostazioni cultura correnti per l'applicazione.  La funzione `CDate`, ad esempio, riconosce i formati di data in base alle impostazioni locali del sistema.  È necessario specificare il giorno, il mese e l'anno nell'ordine corretto in base alle impostazioni locali utilizzate. In caso contrario, è possibile che la data non venga interpretata correttamente.  Un formato di data esteso contenente la stringa del giorno della settimana, ad esempio "mercoledì", non viene riconosciuto.  
  
     Se è necessario eseguire la conversione in o da una rappresentazione di stringa di un valore in un formato diverso da quello specificato dalle impostazioni locali, non è possibile utilizzare le funzioni di conversione dei tipi di Visual Basic.  A tale scopo, utilizzare i metodi `ToString(IFormatProvider)` e `Parse(String, IFormatProvider)` del tipo di valore.  Utilizzare ad esempio <xref:System.Double.Parse%2A?displayProperty=fullName> per la conversione di una stringa in un tipo `Double` e <xref:System.Double.ToString%2A?displayProperty=fullName> per la conversione di un valore di tipo `Double` in una stringa.  
  
## Funzione CType  
 La [funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md) accetta un secondo argomento, `typename`, e assegna `expression` a `typename`. `typename` può essere un qualsiasi tipo di dati, struttura, classe o interfaccia per cui esiste una conversione valida.  
  
 Per un confronto di `CType` con le altre parole chiave di conversione dei tipi, vedere [DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md) e [TryCast Operator](../../../visual-basic/language-reference/operators/trycast-operator.md).  
  
## Esempio di CBool  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CBool` per convertire espressioni in valori `Boolean`.  Se un'espressione restituisce un valore diverso da zero, `CBool` restituisce `True`, altrimenti restituisce `False`.  
  
 [!code-vb[VbVbalrFunctions#1](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_1.vb)]  
  
## Esempio di CByte  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CByte` per convertire un'espressione in un valore `Byte`.  
  
 [!code-vb[VbVbalrFunctions#2](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_2.vb)]  
  
## Esempio di CChar  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CChar` per convertire il primo carattere di un'espressione `String` in un tipo `Char`.  
  
 [!code-vb[VbVbalrFunctions#3](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_3.vb)]  
  
 L'argomento di input per `CChar` deve essere costituito da un tipo di dati `Char` o `String`.  La funzione `CChar` non può essere utilizzata per convertire un numero in un carattere. `CChar` non è infatti in grado di accettare tipi di dati numerici.  Nell'esempio riportato di seguito viene ottenuto un numero che rappresenta un punto di codice \(codice carattere\) e viene convertito nel carattere corrispondente.  È possibile utilizzare la funzione <xref:Microsoft.VisualBasic.Interaction.InputBox%2A> per ottenere la stringa di cifre, `CInt` per convertire la stringa nel tipo `Integer` e `ChrW` per convertire il numero nel tipo `Char`.  
  
 [!code-vb[VbVbalrFunctions#4](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_4.vb)]  
  
## Esempio di CDate  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CDate` per convertire stringhe in valori `Date`.  Non è in genere consigliabile definire a livello di codice le date e le ore come stringhe \(come illustrato in questo esempio\).  Utilizzare invece valori letterali di data e ora, quali \#Feb 12, 1969\# e \#4:35:47 PM\#.  
  
 [!code-vb[VbVbalrFunctions#5](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_5.vb)]  
  
## Esempio di CDbl  
 [!code-vb[VbVbalrFunctions#6](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_6.vb)]  
  
## Esempio di CDec  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CDec` per convertire un valore numerico in `Decimal`.  
  
 [!code-vb[VbVbalrFunctions#7](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_7.vb)]  
  
## Esempio di CInt  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CInt` per convertire un valore nel tipo `Integer`.  
  
 [!code-vb[VbVbalrFunctions#8](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_8.vb)]  
  
## Esempio di CLng  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CLng` per convertire valori nel tipo `Long`.  
  
 [!code-vb[VbVbalrFunctions#9](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_9.vb)]  
  
## Esempio di CObj  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CObj` per convertire un valore numerico in `Object`.  La variabile `Object` contiene solo un puntatore a quattro byte che fa riferimento al valore `Double` assegnato.  
  
 [!code-vb[VbVbalrFunctions#10](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_10.vb)]  
  
## Esempio di CSByte  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CSByte` per convertire un valore numerico in `SByte`.  
  
 [!code-vb[VbVbalrFunctions#11](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_11.vb)]  
  
## Esempio di CShort  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CShort` per convertire un valore numerico in `Short`.  
  
 [!code-vb[VbVbalrFunctions#12](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_12.vb)]  
  
## Esempio di CSng  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CSng` per convertire valori nel tipo `Single`.  
  
 [!code-vb[VbVbalrFunctions#13](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_13.vb)]  
  
## Esempio di CStr  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CStr` per convertire un valore numerico in `String`.  
  
 [!code-vb[VbVbalrFunctions#14](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_14.vb)]  
  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CStr` per convertire valori `Date` in valori `String`.  
  
 [!code-vb[VbVbalrFunctions#15](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_15.vb)]  
  
 La funzione `CStr` visualizza sempre un valore `Date` nel formato breve standard per le impostazioni locali correnti, ad esempio "6\/15\/2003 4:35:47 PM".  Tuttavia, `CStr` elimina i *valori neutri* 1\/1\/0001 per la data e 00:00:00 per l'ora.  
  
 Per informazioni dettagliate sui valori restituiti da `CStr`, vedere [Return Values for the CStr Function](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md).  
  
## Esempio di CUInt  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CUInt` per convertire un valore numerico in `UInteger`.  
  
 [!code-vb[VbVbalrFunctions#16](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_16.vb)]  
  
## Esempio di CULng  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CULng` per convertire un valore numerico in `ULong`.  
  
 [!code-vb[VbVbalrFunctions#17](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_17.vb)]  
  
## Esempio di CUShort  
 Nell'esempio riportato di seguito viene utilizzata la funzione `CUShort` per convertire un valore numerico in `UShort`.  
  
 [!code-vb[VbVbalrFunctions#18](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/type-conversion-functions_18.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Int%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Fix%2A>   
 <xref:Microsoft.VisualBasic.Strings.Format%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Hex%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Oct%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Str%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Val%2A>   
 [Conversion Functions](../../../visual-basic/language-reference/functions/conversion-functions.md)   
 [Type Conversions in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)