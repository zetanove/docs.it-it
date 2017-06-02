---
title: "Transazioni locali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Transazioni locali
Le transazioni in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] consentono di associare più attività in modo da poterle eseguire come un'unità di lavoro singola.  Ad esempio, si supponga che un'applicazione esegua due attività.  Ovvero che prima aggiorni una tabella con le informazioni sull'ordine  e che, successivamente, aggiorni una tabella contenente le informazioni d'inventario addebitando gli articoli ordinati.  Se le due attività non vengono eseguite correttamente, verrà eseguito il rollback dei due aggiornamenti.  
  
## Determinazione del tipo di transazione  
 Una transazione è considerata locale quando è composta da una sola fase e viene gestita direttamente dal database.  Le transazioni sono considerate distribuite, invece, quando vengono coordinate da un monitoraggio delle transazioni e sono completate con meccanismi fail\-safe \(quale il commit in due fasi\).  
  
 Ogni provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] dispone di un oggetto `Transaction` per l'esecuzione delle transazioni locali.  Per eseguire una transazione in un database di SQL Server, selezionare una transazione <xref:System.Data.SqlClient>.  Per una transazione Oracle usare il provider <xref:System.Data.OracleClient>.  È inoltre disponibile una nuova classe <xref:System.Data.Common.DbTransaction> che consente di scrivere codice indipendente dal provider che richiede transazioni.  
  
> [!NOTE]
>  Le transazioni più efficienti sono quelle eseguite sul server.  Se si usa un database SQL Server in cui sono ampiamente usate le transazioni esplicite, è consigliabile scrivere queste transazioni come stored procedure usando l'istruzione BEGIN TRANSACTION Transact\-SQL.  Per altre informazioni sull'esecuzione di transazioni sul lato server, vedere la documentazione online di SQL Server.  
  
## Esecuzione di una transazione con una singola connessione  
 In [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] è possibile controllare le transazioni mediante l'oggetto `Connection`.  È possibile avviare una transazione locale con il metodo `BeginTransaction`.  Una volta iniziata una transazione, è possibile inserire un comando nell'elenco della transazione usando la proprietà `Transaction` di un oggetto `Command`.  In seguito è possibile eseguire il commit o il rollback delle modifiche apportate nell'origine dati in base all'esito corretto o errato dei componenti della transazione.  
  
> [!NOTE]
>  Il metodo `EnlistDistributedTransaction` non deve essere usato per una transazione locale.  
  
 L'ambito della transazione si limita alla connessione.  Nell'esempio seguente viene eseguita una transazione esplicita composta da due comandi separati nel blocco `try`.  I comandi eseguono le istruzioni INSERT sulla tabella Production.ScrapReason nel database di esempio AdventureWorks di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] e, se non vengono generate eccezioni, viene eseguito il commit.  Se, invece, viene generata un'eccezione, il codice del blocco `catch` esegue il rollback della transazione.  Allo stesso modo, se la transazione viene interrotta oppure la connessione viene chiusa prima del completamento della transazione, viene eseguito automaticamente il rollback della transazione.  
  
## Esempio  
 Per eseguire una transazione, usare la procedura seguente:  
  
1.  Chiamare il metodo <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> dell'oggetto <xref:System.Data.SqlClient.SqlConnection> per contrassegnare l'inizio della transazione.  Il metodo <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> restituisce un riferimento alla transazione.  Questo riferimento viene assegnato agli oggetti <xref:System.Data.SqlClient.SqlCommand> contenuti nell'elenco della transazione.  
  
2.  Assegnare l'oggetto `Transaction` alla proprietà <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> dell'oggetto <xref:System.Data.SqlClient.SqlCommand> da eseguire.  Se un comando viene eseguito su una connessione con una transazione attiva e l'oggetto `Transaction` non è stato assegnato alla proprietà `Transaction` dell'oggetto `Command`, viene generata un'eccezione.  
  
3.  Eseguire i comandi richiesti.  
  
4.  Chiamare il metodo <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> dell'oggetto <xref:System.Data.SqlClient.SqlTransaction> per completare la transazione oppure il metodo <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> per interrompere la transazione.  Se la connessione viene chiusa o eliminata prima che venga eseguito il metodo <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> o <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A>, viene eseguito il rollback della transazione.  
  
 Nell'esempio di codice seguente viene illustrata la logica transazionale usando [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] con Microsoft SQL Server.  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## Vedere anche  
 [Transazioni e concorrenza](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [Transazioni distribuite](../../../../docs/framework/data/adonet/distributed-transactions.md)   
 [Integrazione di System.Transactions con SQL Server](../../../../docs/framework/data/adonet/system-transactions-integration-with-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)