---
title: "Considerazioni sulla sicurezza (Entity Framework) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 84758642-9b72-4447-86f9-f831fef46962
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Considerazioni sulla sicurezza (Entity Framework)
In questo argomento vengono illustrate alcune considerazioni sulla sicurezza che riguardano in modo particolare lo sviluppo, la distribuzione e l'esecuzione di applicazioni [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  È consigliabile inoltre seguire le raccomandazioni relative alla creazione di applicazioni [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] protette.  Per altre informazioni, vedere [Cenni preliminari sulla sicurezza](../../../../../docs/framework/data/adonet/security-overview.md).  
  
## Considerazioni generali sulla sicurezza  
 Le considerazioni sulla sicurezza sono valide per tutte le applicazioni che usano [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
#### Usare solo provider delle origini dati attendibili.  
 Per comunicare con l'origine dati, un provider deve eseguire le operazioni seguenti:  
  
-   Ricevere la stringa di connessione da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
-   Convertire l'albero dei comandi nel linguaggio di query nativo dell'origine dati.  
  
-   Assemblare e restituire i set di risultati.  
  
 Durante l'operazione di accesso, le informazioni basate sulla password dell'utente vengono passate al server tramite le librerie di rete dell'origine dati sottostante.  Un provider malintenzionato può rubare le credenziali utente, generare query dannose o manomettere il set di risultati.  
  
#### Crittografare la connessione per proteggere i dati riservati.  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] non gestisce direttamente la crittografia dei dati.  Se gli utenti accedono ai dati su una rete pubblica, l'applicazione deve stabilire una connessione crittografata all'origine dati per aumentare la sicurezza.  Per altre informazioni, vedere la documentazione relativa alla sicurezza dell'origine dati.  Per un'origine dati SQL Server, vedere [Crittografia delle connessioni a SQL Server](http://go.microsoft.com/fwlink/?LinkId=119544).  
  
#### Proteggere la stringa di connessione.  
 La protezione dell'accesso all'origine dati è uno dei principali obiettivi da raggiungere quando si imposta la sicurezza di un'applicazione.  Una stringa di connessione presenta una potenziale vulnerabilità se non è protetta o se viene costruita in modo improprio.  Se le informazioni di connessione vengono archiviate in testo normale o mantenute in memoria, si rischia di compromettere l'intero sistema.  Di seguito sono riportati i metodi di protezione delle stringhe di connessione consigliati.  
  
-   Usare l'autenticazione di Windows con un'origine dati SQL Server.  
  
     Quando si usa l'autenticazione di Windows per connettersi a un'origine dati SQL Server, la stringa di connessione non contiene informazioni relative all'accesso e alla password.  
  
-   Crittografare le sezioni dei file di configurazione tramite la configurazione protetta.  
  
     In ASP.NET è disponibile una nuova funzionalità, la configurazione protetta, che consente di crittografare le informazioni riservate in un file di configurazione.  Sebbene sia stata progettata principalmente per ASP.NET, può essere usata anche per crittografare sezioni dei file di configurazione delle applicazioni Windows.  Per una descrizione dettagliata della nuova funzionalità di configurazione protetta, vedere [Encrypting Configuration Information Using Protected Configuration](../Topic/Encrypting%20Configuration%20Information%20Using%20Protected%20Configuration.md).  
  
-   Archiviare le stringhe di connessione in file di configurazione protetti.  
  
     Le stringhe di connessione non devono mai essere incorporate nel codice sorgente.  La possibilità di archiviarle nei file di configurazione elimina la necessità di incorporarle nel codice.  Per impostazione predefinita, la procedura guidata Entity Data Model archivia le stringhe di connessione nel file di configurazione dell'applicazione.  Per impedire accessi non autorizzati, è necessario proteggere tale file.  
  
-   Usare i generatori di stringhe di connessione durante la creazione dinamica delle connessioni.  
  
     Se è necessario costruire stringhe di connessione in fase di runtime, usare la classe <xref:System.Data.EntityClient.EntityConnectionStringBuilder>.  Questa classe del generatore di stringhe consente di impedire attacchi injection delle stringhe di connessione attraverso la convalida e l'esecuzione dell'escape delle informazioni di input non valide.  Per altre informazioni, vedere [Procedura: compilare una stringa di connessione EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md).  Usare inoltre la classe del generatore di stringhe adatta per costruire la stringa di connessione dell'origine dati che fa parte della stringa di connessione di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per informazioni sui generatori di stringhe di connessione per i provider ADO.NET, vedere [Compilatori di stringhe di connessione](../../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
 Per altre informazioni, vedere [Protezione delle informazioni di connessione](../../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
#### Non esporre un oggetto EntityConnection a utenti non attendibili.  
 Un oggetto <xref:System.Data.EntityClient.EntityConnection> espone la stringa di connessione della connessione sottostante.  Un utente che dispone dell'accesso a un oggetto <xref:System.Data.EntityClient.EntityConnection> può modificare anche l'oggetto <xref:System.Data.ConnectionState> della connessione sottostante.  La classe <xref:System.Data.EntityClient.EntityConnection> non è thread\-safe.  
  
#### Non passare connessioni al di fuori del contesto di sicurezza.  
 Dopo aver stabilito una connessione, non è possibile passarla al di fuori del contesto di sicurezza.  Un thread con l'autorizzazione ad aprire una connessione, ad esempio, non deve archiviare la connessione in un percorso globale.  Da questo percorso, infatti, potrebbe essere usata da uno script dannoso senza un'autorizzazione esplicitamente concessa.  
  
#### Tenere presente che le informazioni relative all'accesso e alla password possono essere visibili in un'immagine della memoria.  
 Quando nella stringa di connessione vengono fornite informazioni relative all'accesso e alla password della stringa di connessione, tali informazioni vengono conservate in memoria fino a quando le risorse non sono richieste dal processo di Garbage Collection.  Diventa quindi impossibile determinare quando una stringa della password non è più in memoria.  Se un'applicazione si arresta in modo anomalo, è possibile che un file di immagine della memoria contenga informazioni sulla sicurezza riservate che possono quindi diventare visibili all'utente che esegue l'applicazione e a qualsiasi utente con accesso amministrativo al computer.  Usare l'autenticazione di Windows per le connessioni a Microsoft SQL Server.  
  
#### Concedere agli utenti solo le autorizzazioni necessarie nell'origine dati.  
 Un amministratore dell'origine dati deve concedere solo le autorizzazioni necessarie agli utenti.  Sebbene [!INCLUDE[esql](../../../../../includes/esql-md.md)] non supporti istruzioni DML che modificano i dati, ad esempio INSERT, UPDATE o DELETE, gli utenti possono comunque accedere alla connessione all'origine dati.  Un utente malintenzionato potrebbe usare questa connessione per eseguire istruzioni DML nel linguaggio nativo dell'origine dati.  
  
#### Eseguire le applicazioni con le autorizzazioni minime.  
 Quando si consente l'esecuzione di un'applicazione gestita con autorizzazione di attendibilità totale, [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] non limita l'accesso dell'applicazione al computer.  Questo potrebbe rendere vulnerabile l'applicazione e compromettere l'intero sistema.  Per usare la sicurezza dall'accesso di codice e gli altri meccanismi di sicurezza di [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)], è necessario eseguire le applicazioni tramite autorizzazioni parzialmente attendibili e con il set minimo di autorizzazioni necessarie a consentirne il funzionamento.  Le autorizzazioni di accesso al codice seguenti sono le autorizzazioni minime necessarie per l'applicazione [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]:  
  
-   <xref:System.Security.Permissions.FileIOPermission>: <xref:System.Security.Permissions.FileIOPermissionAccess> per aprire i file di metadati specificati o <xref:System.Security.Permissions.FileIOPermissionAccess> per cercare i file di metadati in una directory.  
  
-   <xref:System.Security.Permissions.ReflectionPermission>: <xref:System.Security.Permissions.ReflectionPermissionFlag> per supportare query di LINQ to Entities.  
  
-   <xref:System.Transactions.DistributedTransactionPermission>: <xref:System.Security.Permissions.PermissionState> da inserire in <xref:System.Transactions><xref:System.Transactions.Transaction>.  
  
-   <xref:System.Security.Permissions.SecurityPermission>: <xref:System.Security.Permissions.SecurityPermissionFlag> per serializzare le eccezioni tramite l'interfaccia <xref:System.Runtime.Serialization.ISerializable>.  
  
-   Autorizzazione per aprire una connessione al database ed eseguire comandi sul database, ad esempio <xref:System.Data.SqlClient.SqlClientPermission> per un database di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
 Per altre informazioni, vedere [Sicurezza dall'accesso di codice e ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md).  
  
#### Non installare applicazioni non attendibili.  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] non applica autorizzazioni di sicurezza e richiamerà qualsiasi codice dell'oggetto dati fornito dall'utente in corso, indipendentemente dall'attendibilità.  Assicurarsi che l'autenticazione e l'autorizzazione del client vengano eseguite dall'archivio dati e dall'applicazione.  
  
#### Limitare l'accesso a tutti i file di configurazione.  
 Un amministratore deve limitare l'accesso in scrittura a tutti i file che specificano la configurazione per un'applicazione, inclusi enterprisesec.config, security.config, machine.conf e i file di configurazione dell'applicazione \<*application*\>.exe.config.  
  
 Il nome invariante del provider può essere modificato in app.config.  L'applicazione client deve accedere al provider sottostante tramite il modello di factory di provider standard usando un nome sicuro.  
  
#### Limitare le autorizzazioni ai file di modello e di mapping.  
 Un amministratore deve limitare l'accesso in scrittura ai file di modello e di mapping \(edmx, csdl, ssdl e msl\) solo agli utenti che modificano il modello o i mapping.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] richiede solo l'accesso in lettura a questi file in fase di runtime.  Un amministratore deve limitare anche l'accesso ai file del codice sorgente di visualizzazione precompilati e a livello di oggetto generati dagli strumenti di [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)].  
  
## Considerazioni sulla sicurezza relative alle query  
 Le considerazioni sulla sicurezza illustrate di seguito riguardano l'esecuzione di query su un modello concettuale.  Tali considerazioni si applicano alle query [!INCLUDE[esql](../../../../../includes/esql-md.md)] che usano EntityClient e alle query di oggetto che usano LINQ, [!INCLUDE[esql](../../../../../includes/esql-md.md)] e i metodi del generatore di query.  
  
#### Impedire attacchi SQL injection.  
 Le applicazioni spesso accettano input esterno, ad esempio da un utente o da un altro agente esterno, ed eseguono azioni basate su tale input.  L'eventuale input derivato in modo diretto o indiretto dall'utente o da un agente esterno può includere contenuto che sfrutta la sintassi del linguaggio di destinazione per eseguire azioni non autorizzate.  Quando il linguaggio di destinazione è un linguaggio SQL \(Structured Query Language\), ad esempio [!INCLUDE[tsql](../../../../../includes/tsql-md.md)], questa manipolazione è nota come attacco SQL injection.  Un utente malintenzionato può inserire comandi direttamente nella query e rimuovere una tabella di database, determinare un attacco di tipo Denial of Service o alterare in altro modo la natura dell'operazione da eseguire.  
  
-   Attacchi injection di [!INCLUDE[esql](../../../../../includes/esql-md.md)]:  
  
     Gli attacchi SQL injection possono essere eseguiti in [!INCLUDE[esql](../../../../../includes/esql-md.md)] attraverso l'inserimento di input dannoso nei valori usati in un predicato della query e nei nomi del parametro.  Per evitare il rischio di SQL injection, è necessario non combinare mai l'input dell'utente con il testo dei comandi [!INCLUDE[esql](../../../../../includes/esql-md.md)].  
  
     Le query [!INCLUDE[esql](../../../../../includes/esql-md.md)] accettano parametri ovunque vengano accettati i valori letterali.  È consigliabile usare query con parametri, anziché inserire valori letterali direttamente nella query tramite un agente esterno. Si consiglia inoltre di usare i metodi del generatore di query per costruire [Entity SQL](http://msdn.microsoft.com/it-it/05685434-05e6-41c2-8d5e-8933b88a40b0) in modo sicuro.  
  
-   Attacchi injection di [!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)]:  
  
     Sebbene la composizione di query sia possibile in [!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)], essa viene eseguita attraverso l'API del modello a oggetti. A differenza delle query [!INCLUDE[esql](../../../../../includes/esql-md.md)], le query [!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)] non vengono composte mediante la manipolazione o la concatenazione di stringhe e non sono soggette agli attacchi SQL injection tradizionali.  
  
#### Evitare la creazione di set di risultati molto grandi.  
 Un set di risultati molto grande può causare la chiusura del sistema client se il client sta eseguendo operazioni che usano una quantità di risorse proporzionale alla dimensione del set di risultati.  Set di risultati insolitamente grandi possono essere prodotti in presenza delle condizioni seguenti:  
  
-   In query eseguite su un database molto ampio che non includono condizioni di filtro adatte.  
  
-   In query che creano join cartesiani sul server.  
  
-   In query [!INCLUDE[esql](../../../../../includes/esql-md.md)] annidate.  
  
 Quando si accetta l'input dell'utente, è necessario assicurarsi che esso non causi l'aumento delle dimensioni del set di risultati oltre le capacità di gestione del sistema.  Per limitare le dimensioni, è possibile usare anche il metodo <xref:System.Linq.Queryable.Take%2A> in [!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)] o l'operatore [LIMIT](../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md) in [!INCLUDE[esql](../../../../../includes/esql-md.md)].  
  
#### Evitare di restituire risultati IQueryable quando si espongono metodi a chiamanti potenzialmente non attendibili.  
 Evitare di restituire tipi <xref:System.Linq.IQueryable%601> dai metodi esposti a chiamanti potenzialmente non attendibili per i motivi seguenti:  
  
-   Un utente di una query che espone un tipo <xref:System.Linq.IQueryable%601> potrebbe chiamare metodi sul risultato che espongono dati sicuri o aumentano la dimensione del set di risultati.  Si consideri ad esempio la firma del metodo riportata di seguito:  
  
    ```  
    public IQueryable<Customer> GetCustomer(int customerId)  
    ```  
  
     Un utente di questa query potrebbe chiamare `.Include("Orders")` sul tipo `IQueryable<Customer>` restituito per recuperare dati che la query non dovrebbe esporre.  È possibile evitare questa situazione impostando il tipo restituito del metodo su <xref:System.Collections.Generic.IEnumerable%601> e chiamando un metodo \(quale `.ToList()`\) che materializza i risultati.  
  
-   Poiché le query <xref:System.Linq.IQueryable%601> vengono eseguite quando viene eseguita un'iterazione dei risultati, un utente di una query che espone un tipo <xref:System.Linq.IQueryable%601> potrebbe intercettare le eccezioni generate.  Le eccezioni potrebbero contenere informazioni non destinate all'utente.  
  
## Considerazioni sulla sicurezza relative alle entità  
 Le considerazioni sulla sicurezza illustrate di seguito sono valide in caso di generazione e utilizzo di tipi di entità.  
  
#### Non condividere un oggetto ObjectContext tra domini dell'applicazione.  
 La condivisione di un oggetto <xref:System.Data.Objects.ObjectContext> con più di un dominio dell'applicazione potrebbe esporre le informazioni contenute nella stringa di connessione.  Al contrario, è necessario trasferire oggetti serializzati o oggetti grafici all'altro dominio dell'applicazione e quindi allegarli a un <xref:System.Data.Objects.ObjectContext> nel dominio dell'applicazione.  Per altre informazioni, vedere [Serializing Objects](http://msdn.microsoft.com/it-it/06c77f9b-5b2e-4c78-b3e3-8c148ba0ea99).  
  
#### Impedire violazioni dell'indipendenza dai tipi.  
 Se l'indipendenza dai tipi viene violata, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] non è in grado di garantire l'integrità dei dati negli oggetti.  La violazione può verificarsi se si consente l'esecuzione di applicazioni non attendibili con la sicurezza dall'accesso di codice dall'attendibilità totale.  
  
#### Gestire le eccezioni.  
 Accedere ai metodi e alle proprietà di un oggetto <xref:System.Data.Objects.ObjectContext> all'interno di un blocco try\-catch.  L'intercettazione di eccezioni impedisce alle eccezioni non gestite di esporre voci nell'oggetto <xref:System.Data.Objects.ObjectStateManager> o informazioni del modello \(ad esempio i nomi di tabella\) agli utenti dell'applicazione.  
  
## Considerazioni sulla sicurezza relative ad applicazioni ASP.NET  
 Quando si usano percorsi in applicazioni [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)], è necessario considerare quanto segue.  
  
#### Verificare se l'host esegue i controlli del percorso.  
 Quando viene usata la stringa di sostituzione `|DataDirectory|` \(racchiusa tra barre verticali\), [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] verifica che il percorso risolto sia supportato.  "..", ad esempio, non è consentito dietro `DataDirectory`.  Lo stesso controllo per la risoluzione dell'operatore radice dell'applicazione Web \(`~`\) viene eseguito dal processo che ospita [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)].  IIS esegue questo controllo, ma è possibile che host diversi da IIS non verifichino il supporto del percorso risolto.  È opportuno dunque conoscere il comportamento dell'host su cui viene distribuita un'applicazione [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
#### Non dare per scontati i nomi di percorso risolti.  
 Anche se i valori in cui l'operatore radice \(`~`\) e la stringa di sostituzione `DataDirectory` si risolvono dovrebbero rimanere costanti durante il runtime dell'applicazione, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] non impedisce all'host di modificarli.  
  
#### Verificare la lunghezza del percorso prima della distribuzione.  
 Prima di distribuire un'applicazione [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], occorre assicurarsi che i valori dell'operatore radice \(~\) e la stringa di sostituzione `DataDirectory` sono superino i limiti di lunghezza del percorso del sistema operativo.  I provider di dati [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] non si assicurano che la lunghezza del percorso sia all'interno di limiti validi.  
  
## Considerazioni sulla sicurezza relative ai metadati ADO.NET  
 Le considerazioni sulla sicurezza illustrate di seguito si applicano in caso di generazione e utilizzo di file di mapping e di modello.  
  
#### Non esporre informazioni riservate tramite la registrazione.  
 I componenti del servizio di metadati [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] non registrano informazioni private.  In presenza di risultati che non è possibile restituire a causa di restrizioni di accesso, i sistemi di gestione dei database e i file system devono restituire zero risultati anziché generare un'eccezione che potrebbe contenere informazioni riservate.  
  
#### Non accettare oggetti MetadataWorkspace da fonti non attendibili.  
 Le applicazioni non devono accettare istanze della classe <xref:System.Data.Metadata.Edm.MetadataWorkspace> da fonti non attendibili.  Al contrario, è necessario costruire in modo esplicito un'area di lavoro e popolarla a partire da tale origine.  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Considerazioni sulla distribuzione](../../../../../docs/framework/data/adonet/ef/deployment-considerations.md)   
 [Considerazioni sulla migrazione](../../../../../docs/framework/data/adonet/ef/migration-considerations.md)