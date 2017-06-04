---
title: "Analisi dei dati in ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Analisi dei dati in ADO.NET
In ADO.NET 2.0 è disponibile una funzionalità di analisi dei dati incorporata supportata dai provider di dati .NET per [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)], Oracle, OLE DB e ODBC, nonché dall'oggetto <xref:System.Data.DataSet>ADO.NET e dai protocolli di rete di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  
  
 L'analisi delle chiamate API di accesso ai dati consente di diagnosticare i seguenti problemi:  
  
-   Mancata corrispondenza di schema tra il programma client e il database.  
  
-   Database non disponibile o problemi nella libreria di rete.  
  
-   Sintassi SQL non corretta definita a livello di codice o generata da un'applicazione.  
  
-   Logica di programmazione non corretta.  
  
-   Problemi risultanti dall'interazione tra più componenti ADO.NET o tra ADO.NET e i componenti dell'utente.  
  
 Per supportare tecnologie di traccia diverse, questa funzionalità è estensibile, pertanto uno sviluppatore può tracciare un problema a qualsiasi livello dello stack dell'applicazione.  Sebbene la funzionalità di analisi non sia esclusiva di ADO.NET, i provider Microsoft usano l'analisi generalizzata e le API della strumentazione.  
  
 Per altre informazioni sull'impostazione e sulla configurazione dell'analisi gestita in ADO.NET, vedere [Analisi di accesso ai dati](http://msdn.microsoft.com/library/hh880086.aspx).  
  
## Accesso alle informazioni diagnostiche nel registro di eventi esteso  
 Nel provider di dati di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)], l'analisi dell'accesso ai dati \([Analisi di accesso ai dati](http://msdn.microsoft.com/library/hh880086.aspx)\) è stata aggiornata per rendere più facile correlare gli eventi client con le informazioni diagnostiche, ad esempio errori di connessione, informazioni dal buffer circolare di connettività del server e informazioni sulle prestazioni dell'applicazione nel registro eventi esteso.  Per informazioni sulla lettura del registro eventi esteso, vedere [Visualizzare i dati della sessione eventi](http://msdn.microsoft.com/library/hh710068\(SQL.110\).aspx).  
  
 Per le operazioni di connessione, ADO.NET invierà un ID della connessione client.  Se la connessione non riesce, è possibile accedere al buffer circolare di connettività \([Risoluzione dei problemi di connettività in SQL Server 2008 con il buffer circolare di connettività](http://go.microsoft.com/fwlink/?LinkId=207752)\) e individuare il campo `ClientConnectionID` per ottenere informazioni diagnostiche sull'errore di connessione.  Gli ID della connessione client vengono registrati nel buffer circolare solo se si verifica un errore.  Se la connessione non riesce prima di inviare il pacchetto di preaccesso, non verrà generato un ID di connessione client. L'ID di connessione client è un GUID a 16 byte.  È anche possibile trovare l'ID di connessione client nell'output di destinazione di eventi estesi, se l'azione `client_connection_id` viene aggiunta agli eventi in una sessione di eventi estesi.  È possibile abilitare l'analisi di accesso ai dati ed eseguire di nuovo il comando di connessione e osservare il campo `ClientConnectionID` nell'analisi di accesso ai dati, se si necessita di ulteriore assistenza per la diagnostica dei driver del client.  
  
 È possibile ottenere l'ID di connessione cliente a livello di codice usando la proprietà `SqlConnection.ClientConnectionID`.  
  
 `ClientConnectionID` è disponibile per un oggetto di <xref:System.Data.SqlClient.SqlConnection> che stabilisce correttamente una connessione.  Se un tentativo di connessione non riesce, `ClientConnectionID` può essere disponibile tramite `SqlException.ToString`.  
  
 ADO.NET invia inoltre un ID di attività specifico del thread.  L'ID attività viene acquisito nelle sessioni di eventi estesi se le sessioni vengono avviate all'opzione TRACK\_CAUSAILITY abilitata.  Per i problemi di prestazioni con una connessione attiva, è possibile ottenere un ID attività dell'analisi di accesso ai dati del client \(campo di`ActivityID` \) e quindi individuare gli ID attività nell'output di eventi estesi.  L'ID attività negli eventi estesi è un GUID a 16 byte \(diverso dal GUID per l'ID di connessione client seguito da un numero in sequenza di quattro byte\).  Il numero di sequenze rappresenta l'ordine di una richiesta all'interno di un thread e indica un ordinamento relativo del batch e delle istruzioni RPC per il thread.  `ActivityID` viene attualmente inviato facoltativamente per le istruzioni batch SQL e le richieste RPC quando è abilitata l'analisi di accesso ai dati e il diciottesimo bit della parola di configurazione dell'analisi di accesso ai dati è ON.  
  
 Di seguito viene riportato un esempio che usa [!INCLUDE[tsql](../../../../includes/tsql-md.md)] per avviare una sessione di eventi estesi che verrà archiviata in un buffer circolare e che registrerà l'ID attività inviato da un client nelle operazioni RPC e batch.  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## Vedere anche  
 [Tracciatura di rete in .NET Framework](../../../../docs/framework/network-programming/network-tracing.md)   
 [Tracing and Instrumenting Applications](../../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)   
 [Provider di dati gestiti ADO.NET e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)