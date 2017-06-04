---
title: "Statistiche del provider per SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Statistiche del provider per SQL Server
A partire da .NET Framework versione 2.0, il provider di dati .NET Framework per SQL Server supporta le statistiche in fase di esecuzione.  È necessario abilitare le statistiche impostando la proprietà <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> dell'oggetto <xref:System.Data.SqlClient.SqlConnection> su `True` dopo aver creato un oggetto di connessione valido.  Dopo aver abilitato le statistiche, è possibile visualizzarle come "snapshot" recuperando un riferimento <xref:System.Collections.IDictionary> mediante il metodo <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> dell'oggetto <xref:System.Data.SqlClient.SqlConnection>.  È possibile enumerare l'elenco come un set di voci di dizionario delle coppie nome\/valore.  Queste coppie nome\/valore non seguono alcun ordine.  È possibile chiamare il metodo <xref:System.Data.SqlClient.SqlConnection.ResetStatistics%2A> dell'oggetto <xref:System.Data.SqlClient.SqlConnection> per azzerare i contatori in qualsiasi momento.  Se non è stata abilitata la raccolta delle statistiche, non viene generata alcuna eccezione.  Inoltre, se il metodo <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> viene chiamato senza la proprietà <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A>, i valori recuperati sono i valori iniziali per ciascuna voce.  Se vengono abilitate le statistiche, eseguire l'applicazione, quindi disabilitare le statistiche. I valori recuperati rifletteranno i valori raccolti fino al momento in cui le statistiche sono state disabilitate.  Tutti i valori delle statistiche vengono raccolti in base alla connessione.  
  
## Valori statistici disponibili  
 Attualmente sono disponibili 18 voci diverse del provider Microsoft SQL Server.  È possibile accedere alle voci disponibili tramite la proprietà **Count** del riferimento dell'interfaccia <xref:System.Collections.IDictionary> restituito da <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>.  Tutti i contatori delle statistiche del provider usano il tipo <xref:System.Int64> di Common Language Runtime \(**long** in C\# e Visual Basic\), da 64 bit.  Il valore massimo del tipo di dati **int64**, definito dal campo **int64.MaxValue**, è \(\(2^63\)\-1\)\).  Quando i valori del contatore raggiungono il valore massimo, non possono più essere considerati esatti.  Ciò significa che **int64.MaxValue**\-1 \(\(2^63\)\-2\) è realmente il valore massimo valido per le statistiche.  
  
> [!NOTE]
>  Viene usato un dizionario per restituire le statistiche del provider poiché il numero, i nomi e l'ordine delle statistiche restituite può variare nel tempo.  Le applicazioni non devono fare riferimento a un valore specifico rilevato nel dizionario, ma devono controllare se il valore è presente e creare rami di conseguenza.  
  
 Nella tabella seguente vengono descritti i valori statistici disponibili.  Si noti che i nomi delle chiavi per i singoli valori non sono localizzati nelle versioni internazionali di Microsoft .NET Framework.  
  
|Nome della chiave|Descrizione|  
|-----------------------|-----------------|  
|`BuffersReceived`|Restituisce il numero dei pacchetti TSD ricevuti dal provider mediante SQL Server dopo che l'applicazione è stata avviata tramite il provider e le statistiche sono state abilitate.|  
|`BuffersSent`|Restituisce il numero di pacchetti TDS inviati a SQL Server dal provider dopo l'abilitazione delle statistiche.  I comandi di grandi dimensioni possono richiedere più buffer.  Se, ad esempio, al server viene inviato un comando di grandi dimensioni per il quale sono necessari sei pacchetti, `ServerRoundtrips` viene incrementato di uno e `BuffersSent` di sei.|  
|`BytesReceived`|Restituisce il numero di byte di dati nei pacchetti TDS ricevuti dal provider mediante SQL Server dopo che l'applicazione è stata avviata tramite il provider e le statistiche sono state abilitate.|  
|`BytesSent`|Restituisce il numero di byte di dati inviati a SQL Server in pacchetti TDS dopo che l'applicazione è stata avviata tramite il provider e le statistiche sono state abilitate.|  
|`ConnectionTime`|Il periodo di tempo \(in millisecondi\) durante il quale la connessione è stata aperta dopo l'abilitazione delle statistiche \(tempo di connessione totale se le statistiche sono state abilitate prima di aprire la connessione\).|  
|`CursorOpens`|Restituisce il numero di volte che il cursore è stato aperto tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.<br /><br /> Notare che i risultati di sola lettura\/forward\-only restituiti dall'istruzione SELECT non sono considerati cursori e pertanto non influiscono su questo contatore.|  
|`ExecutionTime`|Restituisce l'intervallo di tempo cumulativo \(in millisecondi\) usato dal provider per l'elaborazione dopo l'abilitazione delle statistiche, incluso il tempo di attesa per le risposte del server nonché il tempo di esecuzione del codice nel provider stesso.<br /><br /> Le classi che includono il codice relativo ai tempi sono:<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> Per mantenere i membri performance\-critical più piccoli possibile, per i membri seguenti non vengono monitorati i tempi:<br /><br /> SqlDataReader<br /><br /> this\[\] operator \(all overloads\)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|Restituisce il numero totale di istruzioni INSERT, DELETE e UPDATE eseguite tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
|`IduRows`|Restituisce il numero totale di righe interessate dalle istruzioni INSERT, DELETE e UPDATE eseguite tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
|`NetworkServerTime`|Restituisce il tempo cumulativo di attesa \(in millisecondi\) del provider per le risposte dal server dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
|`PreparedExecs`|Restituisce il numero di comandi preparati eseguiti tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
|`Prepares`|Restituisce il numero di istruzioni preparate tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
|`SelectCount`|Restituisce il numero di istruzioni SELECT eseguite tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.  Include le istruzioni FETCH per il recupero delle righe dai cursori e il conteggio per le istruzioni SELECT viene aggiornato quando viene raggiunta la fine di un tipo <xref:System.Data.SqlClient.SqlDataReader>.|  
|`SelectRows`|Restituisce il numero di righe selezionate dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.  Il contatore riflette tutte le righe generate da istruzioni SQL, anche da quelle non usate dal chiamante.  Ad esempio, se un lettore di dati viene arrestato prima di leggere l'intero set di risultati, il conteggio non verrà compromesso.  Vengono incluse le righe recuperate dai cursori mediante istruzioni FETCH.|  
|`ServerRoundtrips`|Restituisce il numero di volte che la connessione ha inviato i comandi al server e ottenuto una risposta dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
|`SumResultSets`|Restituisce il numero dei set di risultati usati dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.  Ad esempio, viene incluso qualsiasi set di risultati restituito al client.  Per i cursori, ciascuna operazione fetch o ciascuna operazione block\-fetch viene considerata come un set di risultati indipendente.|  
|`Transactions`|Restituisce il numero di transazioni utente iniziate dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.  Se una connessione viene eseguita in modalità di commit automatico, ciascun comando viene considerato come una transazione.<br /><br /> Il contatore incrementa il conteggio delle transazioni non appena viene eseguita l'istruzione BEGIN TRAN, indipendentemente dal fatto che successivamente venga eseguito il commit o il rollback della transazione.|  
|`UnpreparedExecs`|Restituisce il numero di istruzioni non preparate eseguite tramite la connessione dopo che l'applicazione è stata avviata e le statistiche sono state abilitate.|  
  
### Recupero di valori  
 Nell'applicazione console seguente viene illustrato come abilitare le statistiche su una connessione, recuperare quattro singoli valori statistici e riportarli nella finestra della console.  
  
> [!NOTE]
>  Nell'esempio seguente viene usato il database di esempio **AdventureWorks** incluso in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Per la stringa di connessione fornita nel codice di esempio si presuppone che il database sia installato e disponibile nel computer locale.  Modificare la stringa di connessione per adattarla all'ambiente, se necessario.  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the   
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      ' Retrieve a few individual values  
      ' related to the previous command.  
      Dim bytesReceived As Long = _  
          CLng(currentStatistics.Item("BytesReceived"))  
      Dim bytesSent As Long = _  
          CLng(currentStatistics.Item("BytesSent"))  
      Dim selectCount As Long = _  
          CLng(currentStatistics.Item("SelectCount"))  
      Dim selectRows As Long = _  
          CLng(currentStatistics.Item("SelectRows"))  
  
      Console.WriteLine("BytesReceived: " & bytesReceived.ToString())  
      Console.WriteLine("BytesSent: " & bytesSent.ToString())  
      Console.WriteLine("SelectCount: " & selectCount.ToString())  
      Console.WriteLine("SelectRows: " & selectRows.ToString())  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrive it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
 \[C\#\]  
  
```  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrive it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### Recupero di tutti i valori  
 Nell'applicazione console seguente viene illustrato come abilitare le statistiche su una connessione, recuperare tutti i valori statistici con l'enumeratore e riportarli nella finestra della console.  
  
> [!NOTE]
>  Nell'esempio seguente viene usato il database di esempio **AdventureWorks** incluso in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Per la stringa di connessione fornita nel codice di esempio si presuppone che il database sia installato e disponibile nel computer locale.  Modificare la stringa di connessione per adattarla all'ambiente, se necessario.  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the   
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      Console.WriteLine("Key Name and Value")  
  
      ' Note the entries are unsorted.  
      For Each entry As DictionaryEntry In currentStatistics  
        Console.WriteLine(entry.Key.ToString() & _  
            ": " & entry.Value.ToString())  
      Next  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrive it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrive it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)