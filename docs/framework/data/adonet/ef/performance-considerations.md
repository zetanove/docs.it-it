---
title: "Considerazioni relative alle prestazioni (Entity Framework) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 61913f3b-4f42-4d9b-810f-2a13c2388a4a
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Considerazioni relative alle prestazioni (Entity Framework)
In questo argomento vengono descritte le caratteristiche relative alle prestazioni di ADO.NET Entity Framework e vengono illustrate alcune considerazioni per migliorare le prestazioni di applicazioni Entity Framework.  
  
## Fasi di esecuzione di query  
 Per capire meglio le prestazioni delle query in Entity Framework, è utile capire le operazioni che si verificano quando una query viene eseguita su un modello concettuale e restituisce dati come oggetti.  Nella tabella seguente viene descritta questa serie di operazioni.  
  
|Operazione|Costo relativo|Frequenza|Commenti|  
|----------------|--------------------|---------------|--------------|  
|Caricamento di metadati|Moderato|Una volta in ogni dominio dell'applicazione.|I metadati del modello e di mapping usati da Entity Framework sono caricati in un <xref:System.Data.Metadata.Edm.MetadataWorkspace>.  Questi metadati sono memorizzati nella cache globalmente e sono disponibili per altre istanze di <xref:System.Data.Objects.ObjectContext> nello stesso dominio dell'applicazione.|  
|Apertura della connessione al database|Moderato<sup>1</sup>|Secondo le necessità.|Poiché una connessione aperta al database usa una risorsa preziosa, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] apre e chiude la connessione al database solo in base alle necessità.  È possibile aprire anche in modo esplicito la connessione.  Per altre informazioni, vedere [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99).|  
|Generazione di visualizzazioni|High|Una volta in ogni dominio dell'applicazione.  Possono essere generate anticipatamente.|Prima di poter eseguire una query su un modello concettuale o salvare delle modifiche all'origine dati, Entity Framework deve generare un set di visualizzazioni query locali per accedere al database.  A causa del costo elevato della generazione di queste visualizzazioni, è possibile generarle in anticipo e aggiungerle al progetto in fase di progettazione.  Per altre informazioni, vedere [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/it-it/b18a9d16-e10b-4043-ba91-b632f85a2579).|  
|Preparazione della query|Moderato<sup>2</sup>|Una volta per ogni query univoca.|Include i costi per creare il comando della query, generare un albero dei comandi basato sui metadati del modello e di mapping e definire la forma dei dati restituiti.  Poiché vengono memorizzati nella cache sia i comandi delle query Entity SQL sia le query LINQ, le successive esecuzioni dei comandi della stessa query sono più veloci.  Tuttavia, è possibile usare le query LINQ compilate per ridurre il costo nelle esecuzioni successive e le query compilate possono essere più efficienti di quelle LINQ che vengono memorizzate nella cache automaticamente.  Per altre informazioni, vedere [Query compilate \(LINQ to Entities\)](../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md).  Per informazioni generali sull'esecuzione di query LINQ, vedere [LINQ to Entities](../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md). **Note:**  Le query LINQ to Entities che applicano l'operatore `Enumerable.Contains` alle raccolte in memoria non vengono memorizzate automaticamente nella cache.  Inoltre, la parametrizzazione delle raccolte in memoria nelle query LINQ compilate non è consentita.|  
|Esecuzione della query|Basso<sup>2</sup>|Una volta per ogni query.|Costo dell'esecuzione del comando sull'origine dati tramite il provider di dati ADO.NET.  Poiché la maggior parte delle origini dati memorizzano nella cache i piani di query, è possibile che le successive esecuzioni della stessa query siano ancor più veloci.|  
|Caricamento e convalida di tipi|Basso<sup>3</sup>|Una volta per ciascuna istanza <xref:System.Data.Objects.ObjectContext>.|I tipi vengono caricati e convalidati rispetto ai tipi definiti nel modello concettuale.|  
|Rilevamento|Basso<sup>3</sup>|Una volta per ogni oggetto restituito da una query.  <sup>4</sup>|Se una query usa l'opzione di unione <xref:System.Data.Objects.MergeOption>, questa fase non influisce sulle prestazioni.<br /><br /> Se la query usa l'opzione di unione <xref:System.Data.Objects.MergeOption>, <xref:System.Data.Objects.MergeOption> o <xref:System.Data.Objects.MergeOption>, i risultati della query vengono rilevati nell'oggetto <xref:System.Data.Objects.ObjectStateManager>.  Un oggetto <xref:System.Data.EntityKey> viene generato per ogni oggetto rilevato che la query restituisce e viene usato per creare un oggetto <xref:System.Data.Objects.ObjectStateEntry> in <xref:System.Data.Objects.ObjectStateManager>.  Se è possibile trovare un oggetto <xref:System.Data.Objects.ObjectStateEntry> per <xref:System.Data.EntityKey>, viene restituito l'oggetto esistente.  Se viene usata l'opzione <xref:System.Data.Objects.MergeOption> o <xref:System.Data.Objects.MergeOption>, l'oggetto viene aggiornato prima di essere restituito.<br /><br /> Per altre informazioni, vedere [Identity Resolution, State Management, and Change Tracking](http://msdn.microsoft.com/it-it/3bd49311-0e72-4ea4-8355-38fe57036ba0).|  
|Materializzazione degli oggetti|Moderato<sup>3</sup>|Una volta per ogni oggetto restituito da una query.  <sup>4</sup>|Processo di lettura dell'oggetto <xref:System.Data.Common.DbDataReader> restituito, di creazione di oggetti e di impostazione di valori di proprietà che si basano sui valori in ciascuna istanza della classe <xref:System.Data.Common.DbDataRecord>.  Se l'oggetto esiste già in <xref:System.Data.Objects.ObjectContext> e la query usa l'opzione di unione <xref:System.Data.Objects.MergeOption> o <xref:System.Data.Objects.MergeOption>, questa fase non influisce sulle prestazioni.  Per altre informazioni, vedere [Identity Resolution, State Management, and Change Tracking](http://msdn.microsoft.com/it-it/3bd49311-0e72-4ea4-8355-38fe57036ba0).|  
  
 <sup>1</sup> Quando un provider dell'origine dati implementa pool di connessioni, il costo di apertura di una connessione è distribuito nel pool.  Il provider .NET per SQL Server supporta i pool di connessioni.  
  
 <sup>2</sup> Il costo aumenta con la maggiore complessità della query.  
  
 <sup>3</sup> Il costo totale aumenta proporzionalmente al numero di oggetti restituiti dalla query.  
  
 <sup>4</sup> Questo overhead non è richiesto per le query EntityClient perché le query EntityClient restituiscono un <xref:System.Data.EntityClient.EntityDataReader> anziché oggetti.  Per altre informazioni, vedere [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
## Considerazioni aggiuntive  
 Di seguito sono illustrate altre considerazioni che possono influire sulle prestazioni di applicazioni Entity Framework.  
  
### Esecuzione di query  
 Poiché le query possono richiedere l'uso intenso delle risorse, è bene considerare in quale punto del codice e in quale computer viene eseguita una query.  
  
#### Esecuzione posticipata e immediata  
 Quando si crea un oggetto <xref:System.Data.Objects.ObjectQuery%601> o una query LINQ, è possibile che la query non sia eseguita immediatamente.  L'esecuzione della query è rinviata fino a quando i risultati non diventano necessari, ad esempio durante un'enumerazione `foreach` \(C\#\) o `For Each` \(Visual Basic\) o quando è assegnata per completare una raccolta <xref:System.Collections.Generic.List%601>.  L'esecuzione della query inizia immediatamente quando si chiama il metodo <xref:System.Data.Objects.ObjectQuery%601.Execute%2A> in un oggetto <xref:System.Data.Objects.ObjectQuery%601> o quando si chiama un metodo LINQ che restituisce una query Singleton, ad esempio <xref:System.Linq.Enumerable.First%2A> o <xref:System.Linq.Enumerable.Any%2A>.  Per altre informazioni, vedere [Object Queries](http://msdn.microsoft.com/it-it/0768033c-876f-471d-85d5-264884349276) e [Esecuzione di query \(LINQ to Entities\)](../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md).  
  
#### Esecuzione di query LINQ sul lato client  
 Sebbene l'esecuzione di una query LINQ avvenga nel computer che ospita l'origine dati, è possibile che alcune parti della query LINQ vengano valutate nel computer client.  Per altre informazioni, vedere la sezione Esecuzione nell'archivio di [Esecuzione di query \(LINQ to Entities\)](../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md).  
  
### Complessità delle query e del mapping  
 La complessità di query singole e del mapping nel modello dell'entità influirà in modo significativo sulle prestazioni delle query.  
  
#### Complessità del mapping  
 I modelli che sono più complessi di un mapping uno a uno tra entità nel modello concettuale e tabelle nel modello di archiviazione generano comandi più complessi rispetto ai modelli che dispongono di un mapping uno a uno.  
  
#### Complessità delle query  
 Le query con un elevato numero di join nei comandi che sono eseguite sull'origine dati o che restituiscono una grande quantità di dati influiscono sulle prestazioni nei seguenti modi:  
  
-   Le query su un modello concettuale che sembrano semplici possono comportare l'esecuzione di query più complesse sull'origine dati.  Il motivo consiste nel fatto che Entity Framework traduce una query su un modello concettuale in una equivalente query sull'origine dati.  Quando un singolo set di entità nel modello concettuale esegue il mapping a più tabelle nell'origine dati, o quando una relazione tra entità viene mappata a una tabella di join, è possibile che il comando di query eseguito sulla query dell'origine dati richieda uno o più join.  
  
    > [!NOTE]
    >  Usare il metodo <xref:System.Data.Objects.ObjectQuery.ToTraceString%2A> della classe <xref:System.Data.Objects.ObjectQuery%601> o <xref:System.Data.EntityClient.EntityCommand> per visualizzare i comandi che sono eseguiti sull'origine dati per una data query.  Per altre informazioni, vedere [How to: View the Store Commands](http://msdn.microsoft.com/it-it/f9771c6e-3b62-4b24-a5d4-55d68e14fa79).  
  
-   Le query Entity SQL annidate possono creare join nel server e possono restituire un elevato numero di righe.  
  
     Di seguito è riportato un esempio di query annidata in una clausola di proiezione:  
  
    ```  
    SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2   
        FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1   
        FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
    ```  
  
     Inoltre, tali query fanno in modo che la pipeline delle query generi un'unica query con duplicazione di oggetti tra le query annidate.  Per questo motivo una singola colonna può essere duplicata più volte.  In alcuni database, tra cui SQL Server, questo può causare un forte aumento delle dimensioni della tabella TempDB, con effetti negativi sulle prestazioni del server.  Occorre quindi prestare attenzione quando si eseguono query annidate.  
  
-   Qualsiasi query che restituisce un elevato numero di dati può causare una diminuzione delle prestazioni se il client in quel momento sta eseguendo operazioni che consumano risorse in modo proporzionale alle dimensioni del set dei risultati.  In tali casi, è necessario limitare la quantità di dati restituiti dalla query.  Per altre informazioni, vedere [How to: Page Through Query Results](http://msdn.microsoft.com/it-it/ffc0f920-e7de-42e0-9b12-ef356421d030).  
  
 Qualsiasi comando generato automaticamente da Entity Framework può essere più complesso degli analoghi comandi scritti in modo esplicito da un sviluppatore del database.  Se è necessario avere il controllo esplicito sui comandi eseguiti sull'origine dati, si può definire un mapping a una funzione con valori di tabella o una stored procedure.  
  
#### Relazioni  
 Per ottenere prestazioni ottimali nell'esecuzione delle query, è necessario definire delle relazioni tra entità sia come associazioni nel modello di entità che come relazioni logiche nell'origine dati.  
  
### Percorsi della query  
 Per impostazione predefinita, quando si esegue un <xref:System.Data.Objects.ObjectQuery%601>, gli oggetti correlati non vengono restituiti \(anche se si tratta di oggetti che rappresentano le relazioni\).  È possibile caricare oggetti correlati in una delle tre modalità riportate di seguito:  
  
1.  Impostando il percorso della query prima che venga eseguito l'oggetto <xref:System.Data.Objects.ObjectQuery%601>.  
  
2.  Chiamando il metodo `Load` sulla proprietà di navigazione esposta dall'oggetto.  
  
3.  Impostando l'opzione <xref:System.Data.Objects.ObjectContextOptions.LazyLoadingEnabled%2A> nell'oggetto <xref:System.Data.Objects.ObjectContext> su `true`.  Si noti che questa operazione viene eseguita automaticamente quando si genera codice del livello oggetti con [Entity Data Model Designer](http://msdn.microsoft.com/it-it/4ccd7ad6-b934-4f7c-82a0-cfd2d4a95faf).  Per altre informazioni, vedere [Generated Code Overview](http://msdn.microsoft.com/it-it/6a88ea38-6a90-4107-bc33-531b79ce5b6a).  
  
 Nella scelta dell'opzione da usare, considerare il compromesso tra il numero di richieste nel database e la quantità di dati restituiti in una singola query.  Per altre informazioni, vedere [Loading Related Objects](http://msdn.microsoft.com/it-it/452347d2-7b3b-44cd-9001-231299a28cb1).  
  
#### Uso di percorsi della query  
 I percorsi della query definiscono il grafico degli oggetti restituiti da una query.  Quando si definisce un percorso della query, è sufficiente una sola richiesta al database per restituire tutti gli oggetti definiti dal percorso.  L'utilizzo di percorsi della query può comportare l'esecuzione di comandi complessi nell'origine dati, derivanti da query di oggetto apparentemente semplici.  Questo si verifica in quanto per restituire oggetti correlati in una singola query sono necessari uno o più join.  Questa complessità è maggiore nelle query su un modello di entità complesso, ad esempio un'entità con ereditarietà o un percorso che include relazioni molti\-a\-molti.  
  
> [!NOTE]
>  Usare il metodo <xref:System.Data.Objects.ObjectQuery.ToTraceString%2A> per visualizzare il comando che verrà generato da un oggetto <xref:System.Data.Objects.ObjectQuery%601>.  Per altre informazioni, vedere [How to: View the Store Commands](http://msdn.microsoft.com/it-it/f9771c6e-3b62-4b24-a5d4-55d68e14fa79).  
  
 Quando un percorso della query include troppi oggetti correlati o gli oggetti contengono troppi dati delle righe, potrebbe non essere possibile completare la query dall'origine dati.  Questo si verifica se la query richiede un'archiviazione temporanea intermedia superiore alle possibilità dell'origine dati.  In questo caso, è possibile ridurre la complessità della query sull'origine dati caricando in modo esplicito gli oggetti correlati.  
  
#### Caricamento esplicito di oggetti correlati  
 È possibile caricare in modo esplicito degli oggetti correlati chiamando il metodo `Load` in una proprietà di navigazione che restituisce un oggetto <xref:System.Data.Objects.DataClasses.EntityCollection%601> o <xref:System.Data.Objects.DataClasses.EntityReference%601>.  Il caricamento esplicito di oggetti richiede un round trip al database ad ogni chiamata del metodo `Load`.  
  
> [!NOTE]
>  Se si chiama il metodo `Load` durante l'esecuzione di ciclo in una raccolta di oggetti restituiti, come quando si usa l'istruzione `foreach` \(`For Each` in Visual Basic\), è necessario che il provider specifico dell'origine dati supporti più set dei risultati attivi in un'unica connessione.  Per un database di SQL Server, è necessario specificare un valore di `MultipleActiveResultSets = true` nella stringa di connessione del provider.  
  
 È inoltre possibile usare il metodo <xref:System.Data.Objects.ObjectContext.LoadProperty%2A> quando non si dispone di proprietà <xref:System.Data.Objects.DataClasses.EntityCollection%601> o <xref:System.Data.Objects.DataClasses.EntityReference%601> sulle entità.  Questa situazione si rivela utile quando si usano entità POCO.  
  
 Anche se il caricamento esplicito di oggetti correlati ridurrà il numero di join e ridurrà la quantità di dati ridondanti, `Load` richiede ripetute connessioni al database e questa procedura può diventare costosa se si caricano in modo esplicito molti oggetti.  
  
### Salvataggio delle modifiche  
 Quando si chiama il metodo <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> in un oggetto <xref:System.Data.Objects.ObjectContext>, viene generato un comando di creazione, aggiornamento o eliminazione distinto per ogni oggetto aggiunto, aggiornato o eliminato nel contesto.  Questi comandi vengono eseguiti sull'origine dati in una sola transazione.  Come avviene per le query, le prestazioni delle operazioni di creazione, aggiornamento ed eliminazione dipendono dalla complessità del mapping nel modello concettuale.  
  
### Transazioni distribuite  
 Le operazioni in una transazione esplicita che richiedono risorse gestite dal DTC \(Distributed Transaction Coordinator\) saranno molto più costose di un'operazione analoga che non richiede il DTC.  Una promozione al DTC avverrà nelle situazioni seguenti:  
  
-   Una transazione esplicita con un'operazione su un database SQL Server 2000 o altra origine dati che promuove sempre transazioni esplicite al DTC.  
  
-   Una transazione esplicita con un'operazione a SQL Server 2005 quando la connessione è gestita da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Ciò si verifica perché SQL Server 2005 promuove a un DTC ogni qualvolta una connessione viene chiusa e riaperta all'interno di una singola transazione, che è il comportamento predefinito di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Questa promozione al DTC non avviene quando si usa SQL Server 2008. Per evitare questa promozione quando si usa SQL Server 2005, è necessario aprire e chiudere la connessione in modo esplicito all'interno della transazione.  Per altre informazioni, vedere [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99).  
  
 Una transazione esplicita viene usata quando una o più operazioni vengono eseguite all'interno di una transazione <xref:System.Transactions>.  Per altre informazioni, vedere [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99).  
  
## Strategie per migliorare le prestazioni  
 È possibile migliorare le prestazioni complessive delle query in Entity Framework usando le strategie seguenti.  
  
#### Generare in anticipo le visualizzazioni  
 La generazione di visualizzazioni basate su un modello di entità ha un costo significativo la prima volta che un'applicazione esegue una query.  Usare EdmGen.exe per generare in anticipo visualizzazioni come un file di codice Visual Basic o C\# che può essere aggiunto al progetto nella fase di progettazione.  Per generare visualizzazioni pre\-compilate, è inoltre possibile usare il toolkit di trasformazione dei modelli di testo.  Le visualizzazioni generate in anticipo vengono convalidate in fase di esecuzione per garantirne la coerenza con la versione corrente del modello di entità specificato.  Per altre informazioni, vedere [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/it-it/b18a9d16-e10b-4043-ba91-b632f85a2579) e la pagina relativa all'[isolamento delle prestazioni nelle visualizzazioni pre\-compilate o generate in anticipo in Entity Framework 4](http://go.microsoft.com/fwlink/?LinkID=201337&clcid=0x409).  
  
 Quando si usano modelli di dimensioni elevate, si applica la considerazione seguente:  
  
 Il formato dei metadati .NET limita il numero di caratteri di stringa specificabili dall'utente in un file binario a 16.777.215 \(0xFFFFFF\).  Se si generano visualizzazioni per un modello di dimensioni elevate e il file relativo raggiunge questo limite, verrà visualizzato l'errore di compilazione "Nessuno spazio logico lasciato per creare altre stringhe utente".  Questa limitazione delle dimensioni si applica a tutti i file binari gestiti.  Per altre informazioni, vedere il [blog](http://go.microsoft.com/fwlink/?LinkId=201476) che descrive come evitare l'errore quando si usano modelli complessi e di dimensioni elevate.  
  
#### Usare l'opzione di unione NoTracking per le query  
 Esiste un costo necessario per tenere traccia degli oggetti restituiti nel contesto dell'oggetto.  Il rilevamento di modifiche agli oggetti e la garanzia che più richieste per la stessa l'entità logica restituiscano la stessa istanza dell'oggetto richiedono che gli oggetti siano allegati a un'istanza <xref:System.Data.Objects.ObjectContext>.  Se non si intende effettuare aggiornamenti o eliminazioni di oggetti e non si richiede la gestione di identità, può essere utile usare le opzioni di unione <xref:System.Data.Objects.MergeOption> per l'esecuzione di query.  
  
#### Restituire la quantità corretta di dati  
 In alcuni scenari, la specifica di un percorso della query usando il metodo <xref:System.Data.Objects.ObjectQuery%601.Include%2A> è molto più veloce perché richiede meno round trip al database.  Tuttavia, in altri scenari, l'esecuzione di round trip aggiuntivi al database per caricare oggetti correlati potrebbe risultare più veloce perché le query più semplici con meno join comportano meno ridondanza di dati.  Per questo motivo si consiglia di testare le prestazioni usando varie modalità di recupero di oggetti correlati.  Per altre informazioni, vedere [Loading Related Objects](http://msdn.microsoft.com/it-it/452347d2-7b3b-44cd-9001-231299a28cb1).  
  
 Per evitare la restituzione di troppi dati in una sola query, si può considerare di eseguire il paging dei risultati della query in gruppi più gestibili.  Per altre informazioni, vedere [How to: Page Through Query Results](http://msdn.microsoft.com/it-it/ffc0f920-e7de-42e0-9b12-ef356421d030).  
  
#### Limitare l'ambito di ObjectContext  
 Nella maggior parte dei casi, è necessario creare un'istanza <xref:System.Data.Objects.ObjectContext> all'interno di un'istruzione `using` \(`Using…End Using` in Visual Basic\).  In questo modo le prestazioni migliorano in quanto viene garantita l'eliminazione automatica delle risorse associate al contesto dell'oggetto quando il codice esce dal blocco di istruzioni.  Tuttavia, quando i controlli vengono associati a oggetti gestiti dal contesto dell'oggetto, l'istanza <xref:System.Data.Objects.ObjectContext> deve essere gestita finché l'associazione è necessaria e viene eliminata manualmente.  Per altre informazioni, vedere [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99).  
  
#### Aprire manualmente la connessione al database  
 Quando l'applicazione esegue una serie di query di oggetto o chiama spesso <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> per operazioni di creazione, aggiornamento ed eliminazione permanente all'origine dati, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] deve continuamente aprire e chiudere la connessione all'origine dati.  In queste situazioni, può essere utile aprire manualmente la connessione all'inizio di queste operazioni e chiuderla o eliminarla quando le operazioni sono completate.  Per altre informazioni, vedere [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99).  
  
## Dati sulle prestazioni  
 Alcuni dati relativi alle prestazioni di Entity Framework sono pubblicati nei post seguenti nel [blog del team di ADO.NET](http://go.microsoft.com/fwlink/?LinkId=91905):  
  
-   [Analisi delle prestazioni di ADO.NET Entity Framework \- Parte 1](http://go.microsoft.com/fwlink/?LinkId=123907)  
  
-   [Analisi delle prestazioni di ADO.NET Entity Framework \- Parte 2](http://go.microsoft.com/fwlink/?LinkId=123909)  
  
-   [Confronto di prestazioni di ADO.NET Entity Framework](http://go.microsoft.com/fwlink/?LinkID=123913)  
  
## Vedere anche  
 [Considerazioni sullo sviluppo e sulla distribuzione](../../../../../docs/framework/data/adonet/ef/development-and-deployment-considerations.md)