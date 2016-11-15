---
title: 'Procedura: Eseguire il round trip dei valori di data e ora'
description: Come eseguire il round trip dei valori di data e ora
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 15690f18-1bb9-4bb8-bc11-0b737e2f0859
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 00a09c8a60138a1828d4e8c62dd72b88abbf4bbe

---

# <a name="how-to-roundtrip-date-and-time-values"></a>Procedura: Eseguire il round trip dei valori di data e ora

In molte applicazioni un valore di data e ora deve identificare una data e un'ora singole in modo non ambiguo. In questo argomento viene illustrato come salvare e ripristinare un valore [DateTime](xref:System.DateTime) e un valore [DateTimeOffset](xref:System.DateTimeOffset) in modo che il valore ripristinato identifichi la stessa ora del valore salvato.

## <a name="to-roundtrip-a-datetime-value"></a>Per eseguire il round trip di un valore DateTime

1. Convertire il valore [DateTime](xref:System.DateTime) nella rappresentazione di stringa relativa chiamando il metodo [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)) con l'identificatore di formato "o".

2. Salvare la rappresentazione di stringa del valore [DateTime](xref:System.DateTime) in un file o passarlo in un processo, un dominio dell'applicazione o un limite della macchina.

3. Recuperare la stringa che rappresenta il valore [DateTime](xref:System.DateTime).

4. Chiamare il metodo [DateTime.Parse(String, IFormatProvider, DateTimeStyles)](xref:System.DateTime.Parse(System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) e passare [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind) come valore del parametro *DateTimeStyles*.

L'esempio seguente illustra come eseguire il round trip di un valore [DateTime](xref:System.DateTime).

```csharp
const string fileName = @".\DateFile.txt";

StreamWriter outFile = new StreamWriter(fileName);

// Save DateTime value.
DateTime dateToSave = DateTime.SpecifyKind(new DateTime(2008, 6, 12, 18, 45, 15), 
                                           DateTimeKind.Local);
string dateString = dateToSave.ToString("o");      
Console.WriteLine("Converted {0} ({1}) to {2}.", 
                  dateToSave.ToString(), 
                  dateToSave.Kind.ToString(), 
                  dateString);      
outFile.WriteLine(dateString);
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName);
outFile.Close();

// Restore DateTime value.
DateTime restoredDate;

StreamReader inFile = new StreamReader(fileName);
dateString = inFile.ReadLine();
inFile.Close();
restoredDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Read {0} ({2}) from {1}.", restoredDate.ToString(), 
                                              fileName, 
                                              restoredDate.Kind.ToString());
// The example displays the following output:
//    Converted 6/12/2008 6:45:15 PM (Local) to 2008-06-12T18:45:15.0000000-05:00.
//    Wrote 2008-06-12T18:45:15.0000000-05:00 to .\DateFile.txt.
//    Read 6/12/2008 6:45:15 PM (Local) from .\DateFile.txt.
```

```vb
Const fileName As String = ".\DateFile.txt"

Dim outFile As New StreamWriter(fileName)

' Save DateTime value.
Dim dateToSave As Date = DateTime.SpecifyKind(#06/12/2008 6:45:15 PM#, _
                                              DateTimeKind.Local)
Dim dateString As String = dateToSave.ToString("o")      
Console.WriteLine("Converted {0} ({1}) to {2}.", dateToSave.ToString(), _
                  dateToSave.Kind.ToString(), dateString)      
outFile.WriteLine(dateString)
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName)
outFile.Close()   

' Restore DateTime value.
Dim restoredDate As Date

Dim inFile As New StreamReader(fileName)
dateString = inFile.ReadLine()
inFile.Close()
restoredDate = DateTime.Parse(dateString, Nothing, DateTimeStyles.RoundTripKind)
Console.WriteLine("Read {0} ({2}) from {1}.", restoredDate.ToString(), _
                  fileName, restoredDAte.Kind.ToString())
' The example displays the following output:
'    Converted 6/12/2008 6:45:15 PM (Local) to 2008-06-12T18:45:15.0000000-05:00.
'    Wrote 2008-06-12T18:45:15.0000000-05:00 to .\DateFile.txt.
'    Read 6/12/2008 6:45:15 PM (Local) from .\DateFile.txt.
```

Quando si esegue il round trip di un valore [DateTime](xref:System.DateTime), questa tecnica consente di mantenere correttamente l'ora per tutte le ore locali e UTC. Ad esempio, se un valore [DateTime](xref:System.DateTime) viene salvato in un sistema con fuso orario ora solare pacifico e viene ripristinato in un sistema con fuso orario ora solare centrale, la data e l'ora ripristinate saranno due ore avanti rispetto all'orario originale. Ciò riflette la differenza tra i due fusi orari. Tuttavia, questa tecnica non è sempre accurata per le ore non specificate. Tutti i valori [DateTime](xref:System.DateTime) la cui proprietà [Kind](xref:System.DateTime.Kind) è [Unspecified](xref:System.DateTimeKind.Unspecified) vengono considerati come ora locale. Se così non è, il valore [DateTime](xref:System.DateTime) non identificherà correttamente data e ora. La soluzione alternativa per questa limitazione consiste nell'associare un valore di data e ora al proprio fuso orario per l'operazione di salvataggio e ripristino.

## <a name="to-roundtrip-a-datetimeoffset-value"></a>Per eseguire il round trip di un valore DateTimeOffset

Convertire il valore [DateTimeOffset](xref:System.DateTimeOffset) nella rappresentazione di stringa relativa chiamando il metodo [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) con l'identificatore di formato "o".

2. Salvare la rappresentazione di stringa del valore [DateTimeOffset](xref:System.DateTimeOffset) in un file o passarlo in un processo, un dominio dell'applicazione o un limite della macchina.

3. Recuperare la stringa che rappresenta il valore [DateTimeOffset](xref:System.DateTimeOffset).

4. Chiamare il metodo [DateTime.Parse(String, IFormatProvider, DateTimeStyles)](xref:System.DateTimeOffset.Parse(System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) e passare [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind) come valore del parametro *styles*.

L'esempio seguente illustra come eseguire il round trip di un valore [DateTimeOffset](xref:System.DateTimeOffset).

```csharp
const string fileName = @".\DateOff.txt";

StreamWriter outFile = new StreamWriter(fileName);

// Save DateTime value.
DateTimeOffset dateToSave = new DateTimeOffset(2008, 6, 12, 18, 45, 15, 
                                               new TimeSpan(7, 0, 0));
string dateString = dateToSave.ToString("o");      
Console.WriteLine("Converted {0} to {1}.", dateToSave.ToString(), 
                  dateString);      
outFile.WriteLine(dateString);
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName);
outFile.Close();

// Restore DateTime value.
DateTimeOffset restoredDateOff;

StreamReader inFile = new StreamReader(fileName);
dateString = inFile.ReadLine();
inFile.Close();
restoredDateOff = DateTimeOffset.Parse(dateString, null, 
                                       DateTimeStyles.RoundtripKind);
Console.WriteLine("Read {0} from {1}.", restoredDateOff.ToString(), 
                  fileName);
// The example displays the following output:
//    Converted 6/12/2008 6:45:15 PM +07:00 to 2008-06-12T18:45:15.0000000+07:00.
//    Wrote 2008-06-12T18:45:15.0000000+07:00 to .\DateOff.txt.
//    Read 6/12/2008 6:45:15 PM +07:00 from .\DateOff.txt.
```

```vb
Const fileName As String = ".\DateOff.txt"

Dim outFile As New StreamWriter(fileName)

' Save DateTime value.
Dim dateToSave As New DateTimeOffset(2008, 6, 12, 18, 45, 15, _
                                     New TimeSpan(7, 0, 0))
Dim dateString As String = dateToSave.ToString("o")      
Console.WriteLine("Converted {0} to {1}.", dateToSave.ToString(), dateString)      
outFile.WriteLine(dateString)
Console.WriteLine("Wrote {0} to {1}.", dateString, fileName)
outFile.Close()   

' Restore DateTime value.
Dim restoredDateOff As DateTimeOffset

Dim inFile As New StreamReader(fileName)
dateString = inFile.ReadLine()
inFile.Close()
restoredDateOff = DateTimeOffset.Parse(dateString, Nothing, DateTimeStyles.RoundTripKind)
Console.WriteLine("Read {0} from {1}.", restoredDateOff.ToString(), fileName)
' The example displays the following output:
'    Converted 6/12/2008 6:45:15 PM +07:00 to 2008-06-12T18:45:15.0000000+07:00.
'    Wrote 2008-06-12T18:45:15.0000000+07:00 to .\DateOff.txt.
'    Read 6/12/2008 6:45:15 PM +07:00 from .\DateOff.txt.
```

Questa tecnica consente sempre di identificare in modo non ambiguo il valore [DateTimeOffset](xref:System.DateTimeOffset) come data e ora singole. Il valore può quindi essere convertito nell'ora UTC (Coordinated Universal Time) chiamando il metodo [DateTimeOffset.ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) o può essere convertito nell'ora di un particolare fuso orario chiamando il metodo [DateTimeOffset.ToOffset](xref:System.DateTimeOffset.ToOffset(System.TimeSpan)) o [TimeZoneInfo.ConvertTime(DateTimeOffset,TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo). La limitazione principale di questa tecnica è che la data e l'ora in numeri, quando vengono eseguite in un valore [DateTimeOffset](xref:System.DateTimeOffset) che rappresenta l'ora di un particolare fuso orario, possono dare risultati non precisi per quel fuso orario. Ciò si verifica perché quando viene creata un'istanza di un valore [DateTimeOffset](xref:System.DateTimeOffset), questo viene dissociato dal proprio fuso orario. Di conseguenza, le regole di rettifica del fuso orario non possono più essere applicate quando si eseguono i calcoli di data e ora. È possibile risolvere questo problema mediante la definizione di un tipo personalizzato che includa sia un valore di data e ora sia il fuso orario ad esso associato.

## <a name="see-also"></a>Vedere anche

[Esecuzione di operazioni di formattazione](performing-formatting-operations.md)

[Stringhe di formato di data e ora standard](standard-datetime.md)




<!--HONumber=Nov16_HO1-->


