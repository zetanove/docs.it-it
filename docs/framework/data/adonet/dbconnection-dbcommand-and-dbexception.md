---
title: "DbConnection, DbCommand e DbException | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58aab611-7e6f-4749-b983-28ab7ae87dbe
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# DbConnection, DbCommand e DbException
Dopo aver creato un oggetto <xref:System.Data.Common.DbProviderFactory> e un oggetto <xref:System.Data.Common.DbConnection>, è possibile usare comandi e lettori di dati per recuperare i dati dall'origine dati.  
  
## Esempio di recupero di dati  
 In questo esempio viene usato un oggetto `DbConnection` come argomento.  Viene creato un oggetto <xref:System.Data.Common.DbCommand> per selezionare dati dalla tabella Categories impostando <xref:System.Data.Common.DbCommand.CommandText%2A> su un'istruzione SQL SELECT.  Nel codice si presuppone che la tabella Categories esista nell'origine dati.  La connessione viene aperta e i dati vengono recuperati tramite <xref:System.Data.Common.DbDataReader>.  
  
 [!code-csharp[DataWorks DbProviderFactories.DbCommandData#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommandData/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbCommandData#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommandData/VB/source.vb#1)]  
  
## Esempio di esecuzione di un comando  
 In questo esempio viene usato un oggetto `DbConnection` come argomento.  Se `DbConnection` è valido, la connessione viene aperta e viene creato ed eseguito un oggetto <xref:System.Data.Common.DbCommand>.  <xref:System.Data.Common.DbCommand.CommandText%2A> viene impostato su un'istruzione SQL INSERT che esegue un inserimento nella tabella Categories del database Northwind.  Nel codice si presuppone che il database Northwind esista nell'origine dati e che la sintassi SQL usata nell'istruzione INSERT sia valida per il provider specificato.  Gli errori che si verificano nell'origine dati vengono gestiti dal blocco di codice <xref:System.Data.Common.DbException>, mentre tutte le altre eccezioni vengono gestite nel blocco <xref:System.Exception>.  
  
 [!code-csharp[DataWorks DbProviderFactories.DbCommand#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommand/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbCommand#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommand/VB/source.vb#1)]  
  
## Gestione di errori dei dati con DbException  
 La classe <xref:System.Data.Common.DbException> è la classe di base per tutte le eccezioni generate per conto di un'origine dati.  È possibile usarla nel codice di gestione delle eccezioni per gestire le eccezioni generate da provider diversi senza dover fare riferimento a una classe di eccezioni specifica.  Nel frammento di codice seguente viene illustrato come usare <xref:System.Data.Common.DbException> per visualizzare le informazioni sugli errori restituiti dall'origine dati tramite le proprietà <xref:System.Exception.GetType%2A>, <xref:System.Exception.Source%2A>, <xref:System.Runtime.InteropServices.ExternalException.ErrorCode%2A> e <xref:System.Exception.Message%2A>.  Nell'output verranno visualizzati il tipo di errore, l'origine indicante il nome del provider, un codice di errore e il messaggio associato all'errore.  
  
```vb  
Try  
    ' Do work here.  
Catch ex As DbException  
    ' Display information about the exception.  
    Console.WriteLine("GetType: {0}", ex.GetType())  
    Console.WriteLine("Source: {0}", ex.Source)  
    Console.WriteLine("ErrorCode: {0}", ex.ErrorCode)  
    Console.WriteLine("Message: {0}", ex.Message)  
Finally  
    ' Perform cleanup here.  
End Try  
```  
  
```csharp  
try  
{  
    // Do work here.  
}  
catch (DbException ex)  
{  
    // Display information about the exception.  
    Console.WriteLine("GetType: {0}", ex.GetType());  
    Console.WriteLine("Source: {0}", ex.Source);  
    Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);  
    Console.WriteLine("Message: {0}", ex.Message);  
}  
finally  
{  
    // Perform cleanup here.  
}  
```  
  
## Vedere anche  
 [DbProviderFactory](../../../../docs/framework/data/adonet/dbproviderfactories.md)   
 [Recupero di un oggetto DbProviderFactory](../../../../docs/framework/data/adonet/obtaining-a-dbproviderfactory.md)   
 [Modifica di dati con un DbDataAdapter](../../../../docs/framework/data/adonet/modifying-data-with-a-dbdataadapter.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)