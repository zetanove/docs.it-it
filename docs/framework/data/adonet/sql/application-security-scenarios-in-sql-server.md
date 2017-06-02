---
title: "Scenari di sicurezza delle applicazioni in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Scenari di sicurezza delle applicazioni in SQL Server
Non esiste un singolo modo corretto per creare un'applicazione client SQL Server protetta.  Ogni applicazione è univoca in termini di requisiti, ambiente di distribuzione e popolazione di utenti.  Anche se un'applicazione può essere ragionevolmente protetta quando viene distribuita inizialmente, può diventare meno sicura nel corso del tempo.  È impossibile prevedere con accuratezza quali minacce possano emergere nel futuro.  
  
 SQL Server, come prodotto, è stato migliorato da una versione all'altra per incorporare le più recenti funzionalità di sicurezza che consentono agli sviluppatori di creare applicazioni di database protette.  Tuttavia, la sicurezza non è predefinita, ma richiede un monitoraggio e un aggiornamento costanti.  
  
## Minacce comuni  
 Gli sviluppatori devono conoscere le minacce per la sicurezza, gli strumenti disponibili per contrastarle e le misure per evitare problemi di sicurezza provocati internamente.  La sicurezza può essere paragonata a una catena, in cui la rottura di uno degli anelli compromette l'efficacia dell'insieme.  Nell'elenco seguente sono riportate alcune minacce comuni per la sicurezza che verranno descritte in maggior dettaglio negli argomenti di questa sezione.  
  
### SQL injection  
 Per SQL injection si intende il processo mediante il quale un utente malintenzionato immette istruzioni Transact\-SQL anziché input valido.  Se l'input viene passato direttamente al server senza essere convalidato e se l'applicazione esegue inavvertitamente il codice inserito, è possibile che l'attacco danneggi o elimini permanentemente i dati.  Per contrastare gli attacchi SQL Server injection, è possibile usare stored procedure e comandi con parametri, evitare le istruzioni SQL dinamiche e limitare le autorizzazioni per tutti gli utenti.  
  
### Elevazione dei privilegi  
 Gli attacchi tramite elevazione dei privilegi si verificano quando un utente è in grado di assumere i privilegi di un account attendibile, ad esempio un proprietario o un amministratore.  Usare sempre account con privilegi minimi e assegnare solo le autorizzazioni necessarie.  Evitare di usare account di amministratore o di proprietario per l'esecuzione di codice.  In questo modo è possibile limitare l'entità dei danni che possono verificarsi in caso di successo di un attacco.  Quando si eseguono attività che richiedono autorizzazioni aggiuntive, usare la rappresentazione o la firma di stored procedure solo per la durata dell'attività.  È possibile firmare le stored procedure con certificati o usare la rappresentazione per assegnare autorizzazioni temporanee.  
  
### Probe e osservazione intelligente  
 In un attacco di tipo probe è possibile che vengano usati i messaggi di errore generati da un'applicazione per ricercare vulnerabilità di sicurezza.  Implementare la gestione degli errori in tutto il codice procedurale per evitare che le informazioni sugli errori di SQL Server vengano restituite all'utente finale.  
  
### Autenticazione  
 Un attacco injection alle stringhe di connessione può verificarsi quando si usano gli account di accesso di SQL Server se in fase di esecuzione viene creata una stringa di connessione basata sull'input dell'utente.  Se la stringa di connessione non viene controllata per verificare la presenza di coppie di parole chiave valide, un utente non autorizzato può inserire caratteri aggiuntivi, con la possibilità di accedere a dati sensibili o ad altre risorse del server.  Se possibile, usare l'autenticazione di Windows.  Se è necessario usare gli account di accesso di SQL server, usare <xref:System.Data.SqlClient.SqlConnectionStringBuilder> per creare e convalidare le stringhe di connessione in fase di esecuzione.  
  
### Password  
 Gli attacchi spesso riescono perché un intruso è stato in grado di ottenere o indovinare la password di un utente con privilegi.  Le password rappresentano la prima linea di difesa contro le intrusioni, quindi ai fini della sicurezza del sistema è essenziale impostare password complesse.  Creare e applicare criteri password per l'autenticazione in modalità mista.  
  
 Assegnare sempre una password complessa all'account `sa`, anche quando si usa l'autenticazione di Windows.  
  
## Contenuto della sezione  
 [Gestione delle autorizzazioni con le stored procedure in SQL Server](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)  
 Viene descritto come usare le stored procedure per gestire le autorizzazioni e controllare l'accesso ai dati.  L'utilizzo di stored procedure è un sistema efficace per rispondere a molte minacce per la sicurezza.  
  
 [Scrittura di istruzioni SQL dinamiche protette in SQL Server](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)  
 Vengono descritte le tecniche per scrivere istruzioni SQL dinamiche sicure tramite le stored procedure.  
  
 [Firma di stored procedure in SQL Server](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)  
 Viene descritto come firmare una stored procedure con un certificato per consentire agli utenti l'uso di dati cui non possono accedere direttamente.  In questo modo le stored procedure possono eseguire operazioni che il chiamante non può eseguire direttamente in quanto non dispone delle autorizzazioni appropriate.  
  
 [Personalizzazione delle autorizzazioni mediante la rappresentazione in SQL Server](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)  
 Viene descritto come usare la clausola EXECUTE AS per rappresentare un altro utente.  Con la rappresentazione il contesto di esecuzione passa dal chiamante all'utente specificato.  
  
 [Concessione di autorizzazioni a livello di riga in SQL Server](../../../../../docs/framework/data/adonet/sql/granting-row-level-permissions-in-sql-server.md)  
 Viene descritto come implementare autorizzazioni a livello di riga per limitare l'accesso ai dati.  
  
 [Creazione di ruoli applicazione in SQL Server](../../../../../docs/framework/data/adonet/sql/creating-application-roles-in-sql-server.md)  
 Vengono descritte le caratteristiche e le funzionalità dei ruoli applicazione.  
  
 [Abilitazione dell'accesso tra database in SQL Server](../../../../../docs/framework/data/adonet/sql/enabling-cross-database-access-in-sql-server.md)  
 Viene descritto come consentire l'accesso tra database senza compromettere la sicurezza.  
  
## Vedere anche  
 [Sicurezza di SQL Server](../../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [Panoramica della sicurezza di SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)