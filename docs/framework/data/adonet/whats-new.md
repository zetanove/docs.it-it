---
title: "Novit&#224; di ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Novit&#224; di ADO.NET
Di seguito sono riportate le nuove funzionalità di [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] in [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)].  
  
## Provider di dati SqlClient  
 Di seguito sono riportate le nuove funzionalità del provider di dati di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] in [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]:  
  
-   Le parole chiave della stringa di connessione ConnectRetryCount e ConnectRetryInterval \(<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>\) consentono di controllare la funzionalità di resilienza di una connessione inattiva.  
  
-   Il supporto del flusso da [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] a un'applicazione consente di supportare scenari in cui i dati sul server non sono strutturati.  Per altre informazioni, vedere [Supporto del flusso SqlClient](../../../../docs/framework/data/adonet/sqlclient-streaming-support.md).  
  
-   È stato aggiunto il supporto per la programmazione asincrona.  Per altre informazioni, vedere [Programmazione asincrona](../../../../docs/framework/data/adonet/asynchronous-programming.md).  
  
-   Gli errori di connessione verranno registrati nel registro eventi esteso.  Per altre informazioni, vedere [Analisi dei dati in ADO.NET](../../../../docs/framework/data/adonet/data-tracing.md).  
  
-   In SqlClient è incluso il supporto di AlwaysOn per la funzionalità a disponibilità elevata e ripristino di emergenza di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  Per altre informazioni, vedere [Supporto SqlClient per disponibilità elevata, ripristino di emergenza](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).  
  
-   Una password può essere passata come <xref:System.Security.SecureString> quando si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  Per altre informazioni, vedere <xref:System.Data.SqlClient.SqlCredential>.  
  
-   Quando `TrustServerCertificate` è false e `Encrypt` è true, il nome del server \(o indirizzo IP\) in un certificato SSL di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] deve corrispondere esattamente al nome del server \(o indirizzo IP\) specificato nella stringa di connessione.  In caso contrario, il tentativo di connessione non riuscirà.  Per altre informazioni, vedere la descrizione dell'opzione di connessione `Encrypt` in <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
     Se questa modifica impedisce a un'applicazione esistente di stabilire una connessione in futuro, è possibile correggere l'applicazione usando una delle operazioni seguenti:  
  
    -   Rilasciare un certificato che specifichi il nome breve nel campo relativo al nome comune \(CN\) o al nome alternativo del soggetto \(SAN\).  Questa soluzione funzionerà per il mirroring del database.  
  
    -   Aggiungere un alias che esegua il mapping del nome breve al nome di dominio completo.  
  
    -   Usare il nome di dominio completo nella stringa di connessione.  
  
-   SqlClient supporta la protezione estesa.  Per altre informazioni sulla protezione estesa, vedere [Connessione al motore di database usando la protezione estesa](http://go.microsoft.com/fwlink/?LinkId=219978).  
  
-   SqlClient supporta le connessioni ai database LocalDB.  Per altre informazioni, vedere [Supporto SqlClient per LocalDB](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-localdb.md).  
  
-   `Type System Version=SQL Server 2012;` è il nuovo valore da passare alla proprietà di connessione `Type System Version`.  Il valore `Type System Version=Latest;` è obsoleto ed è diventato equivalente a `Type System Version=SQL Server 2008;`.  Per altre informazioni, vedere <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
-   SqlClient fornisce supporto aggiuntivo per le colonne di tipo sparse, una funzionalità aggiunta in SQL Server 2008.  Se l'applicazione accede già ai dati in una tabella che usa colonne di tipo sparse, si noterà un miglioramento delle prestazioni.  La colonna IsColumnSet di <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> indica se una colonna è di tipo sparse, ovvero membro di un set di colonne.  <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> indica se una colonna è di tipo sparse. Per altre informazioni, vedere [Raccolte di schemi di SQL Server](../../../../docs/framework/data/adonet/sql-server-schema-collections.md).  Per altre informazioni sulle colonne di tipo sparse, vedere [Uso di colonne di tipo sparse](http://go.microsoft.com/fwlink/?LinkId=224244).  
  
-   L'assembly Microsoft.SqlServer.Types.dll, che contiene i tipi di dati spaziali, è stato aggiornato dalla versione 10.0 alla versione 11.0.  Le applicazioni che fanno riferimento a questo assembly potrebbero avere esito negativo.  Per altre informazioni, vedere [Modifiche che possono causare problemi di funzionamento apportate alle funzionalità del Motore di database](http://go.microsoft.com/fwlink/?LinkId=224367).  
  
## ADO.NET Entity Framework  
 In [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)] sono state aggiunte le API che abilitano nuovi scenari quando si usa Entity Framework 5.0.  Per altre informazioni sui miglioramenti e sulle funzionalità che sono stati aggiunti a Entity Framework 5.0, vedere i seguenti argomenti: [Novità](http://go.microsoft.com/fwlink/?LinkID=251106) e [Versioni e controllo delle versioni di Entity Framework](http://go.microsoft.com/fwlink/?LinkId=234899).  
  
## Vedere anche  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [Cenni preliminari su ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [SQL Server e ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)   
 [What's New in WCF Data Services](http://msdn.microsoft.com/it-it/cf22cad5-b8d9-472b-8d7c-b863b64eaae8)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)