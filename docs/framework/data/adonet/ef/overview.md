---
title: "Panoramica su Entity Framework | Microsoft Docs"
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
ms.assetid: a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Panoramica su Entity Framework
[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è un set di tecnologie ADO.NET che supportano lo sviluppo di applicazioni software orientate ai dati.  Gli architetti e gli sviluppatori di questo tipo di applicazioni si trovano nella difficile condizione di dover realizzare due obiettivi molto diversi tra loro,  ovvero la modellazione delle entità, delle relazioni e della logica dei problemi aziendali che sono preposti a risolvere e al tempo stesso la gestione dei motori dei dati usati per archiviare e recuperare i dati stessi.  Dal momento che i dati potrebbero essere distribuiti in più sistemi di archiviazione, ciascuno con i suoi protocolli, è necessario che nelle applicazioni che gestiscono un solo sistema di archiviazione venga rispettato l'equilibrio tra i requisiti del sistema di archiviazione e i requisiti di scrittura di codice dell'applicazione efficiente e gestibile.  
  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] consente agli sviluppatori di usare i dati sotto forma di proprietà e oggetti specifici di un dominio, ad esempio clienti e indirizzi dei clienti, indipendentemente dalle colonne e dalle tabelle di database sottostanti in cui sono archiviati. Con [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], gli sviluppatori possono operare a un livello superiore di astrazione quando gestiscono i dati e possono creare e gestire applicazioni orientate ai dati con meno codice rispetto alle applicazioni tradizionali.  Poiché [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è un componente di [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)], le applicazioni [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] possono essere eseguite su qualsiasi computer in cui è installato [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 3.5 SP1 o versione successiva.  
  
 Nelle sezioni seguenti del presente argomento sono fornite altre informazioni su [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]:  
  
-   [Realizzazione dei modelli](#LifeToModels)  
  
-   [Esecuzione del mapping di oggetti ai dati](#MappingObjectsToData)  
  
-   [Accesso e modifica di dati dell'entità](#AccessingData)  
  
-   [Provider di dati](#DataProviders)  
  
-   [Strumenti di Entity Data Model](#Tools)  
  
-   [Ulteriori informazioni](#LearnMore)  
  
<a name="LifeToModels"></a>   
## Realizzazione dei modelli  
 Un approccio di progettazione comune e consolidato quando si compila un'applicazione o un servizio consiste nel dividere l'applicazione o il servizio in tre parti: un modello di dominio, un modello logico e un modello fisico.  Il modello di dominio definisce le entità e le relazioni nel sistema da modellare.  Il modello logico per un database relazionale normalizza le entità e le relazioni in tabelle con vincoli di chiave esterna.  Il modello fisico gestisce le funzionalità di un determinato motore dei dati specificando dettagli sull'archiviazione come il partizionamento e l'indicizzazione.  
  
 Il modello fisico viene ridefinito dagli amministratori del database per migliorare le prestazioni, ma i programmatori che scrivono il codice delle applicazioni tendono a usare solo il modello logico scrivendo query SQL e chiamando stored procedure.  I modelli di dominio vengono in genere usati come strumento per l'acquisizione e la comunicazione dei requisiti di un'applicazione, spesso come diagrammi inerti visualizzati e discussi nelle fasi iniziali di un progetto e quindi abbandonati.  Molti team di sviluppo saltano la fase di creazione di un modello concettuale e partono direttamente dall'indicazione di tabelle, colonne e chiavi in un database relazionale.  
  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] favorisce la realizzazione dei modelli in quanto consente agli sviluppatori di eseguire query su entità e relazioni del modello di dominio \(denominato modello *concettuale* in [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]\) basandosi al tempo stesso su [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] per convertire le operazioni in comandi specifici dell'origine dati.  Le applicazioni non sono quindi più vincolate a dipendenze hard\-coded su una determinata origine dati.  
  
 Quando si usa Code First, viene eseguito il mapping del modello concettuale al modello di archiviazione nel codice.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] può dedurre il modello concettuale in base ai tipi di oggetto e alle configurazioni aggiuntive definite.  I metadati di mapping vengono generati in fase di esecuzione in base a una combinazione della modalità di definizione dei tipi di dominio e delle informazioni di configurazione aggiuntive fornite nel codice.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] genera il database secondo le necessità in base ai metadati.  Per altre informazioni, vedere la pagina relativa alla [creazione e al mapping di un modello concettuale](http://go.microsoft.com/fwlink/?LinkID=235382).  
  
 Quando si usano gli strumenti di Entity Data Model, il modello concettuale, il modello di archiviazione e i mapping tra i due vengono espressi in schemi basati su XML e definiti in file con estensioni corrispondenti:  
  
-   Il linguaggio CSDL \(Conceptual Schema Definition Language\) definisce il modello concettuale.  CSDL è l'implementazione di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] di [Entity Data Model](../../../../../docs/framework/data/adonet/entity-data-model.md).  L'estensione del file è csdl.  
  
-   Il linguaggio SSDL \(Store Schema Definition Language\) definisce il modello di archiviazione, chiamato anche modello logico.  L'estensione del file è ssdl.  
  
-   Il linguaggio MSL \(Mapping Specification Language\) definisce i mapping tra il modello di archiviazione e il modello concettuale.  L'estensione del file è msl.  
  
 Il modello di archiviazione e i mapping possono essere modificati in base alle esigenze senza che sia necessario modificare il modello concettuale, le classi di dati o il codice dell'applicazione.  Poiché i modelli di archiviazione sono specifici del provider, è possibile usare un modello concettuale coerente in varie origini dati.  
  
 Questi file del modello e di mapping vengono usati da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] per trasformare operazioni di creazione, lettura, aggiornamento ed eliminazione di entità e relazioni del modello concettuale in operazioni equivalenti nell'origine dati.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] supporta anche il mapping di entità del modello concettuale a stored procedure dell'origine dati.  Per altre informazioni, vedere [Specifiche CSDL, SSDL e MSL](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md).  
  
<a name="MappingObjectsToData"></a>   
## Esecuzione del mapping di oggetti ai dati  
 La programmazione orientata a oggetti pone una serie di sfide relativamente all'interazione con i sistemi di archiviazione dei dati.  Anche se l'organizzazione delle classi in genere rispecchia l'organizzazione delle tabelle dei database relazionali, non si può parlare di una corrispondenza esatta.  Più tabelle normalizzate corrispondono spesso a una singola classe e le relazioni tra classi sono spesso rappresentate in modo diverso rispetto alle relazioni tra tabelle.  Per rappresentare il cliente per un determinato ordine, ad esempio, una classe `Order` potrebbe usare una proprietà contenente un riferimento a un'istanza di una classe `Customer`, mentre una riga della tabella `Order` in un database contiene una colonna o un set di colonne di chiave esterna con un valore che corrisponde a un valore di chiave primaria nella tabella `Customer`.  Una classe `Customer` potrebbe disporre di una proprietà denominata `Orders` contenente una raccolta di istanze della classe `Order`, mentre la tabella `Customer` in un database non include colonne confrontabili.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] offre agli sviluppatori la flessibilità per rappresentare relazioni in questo modo o per modellare con maggiore precisione le relazioni come vengono rappresentate nel database.  
  
 Le soluzioni esistenti hanno tentato di colmare questo divario, spesso definito "mancata corrispondenza dell'impedenza" eseguendo solo il mapping di classi e proprietà orientate a oggetti a tabelle e colonne relazionali.  Anziché adottare questo approccio tradizionale, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] esegue il mapping di tabelle relazionali, colonne e vincoli di chiave esterna dei modelli logici a entità e relazioni dei modelli concettuali.  Il risultato ottenuto è una maggiore flessibilità nella definizione degli oggetti e nell'ottimizzazione del modello logico.  Gli strumenti di [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)] generano classi di dati estensibili basate sul modello concettuale.  Queste classi sono classi parziali che è possibile estendere con membri altri aggiunti dallo sviluppatore.  Per impostazione predefinita, le classi generate per un particolare modello concettuale derivano da classi di base che forniscono servizi per la materializzazione di entità come oggetti e per il rilevamento e il salvataggio delle modifiche.  Queste classi possono essere usate dagli sviluppatori per gestire le entità e le relazioni come oggetti correlati da associazioni.  Gli sviluppatori possono inoltre personalizzare le classi generate per un modello concettuale. Per altre informazioni, vedere [Utilizzo di oggetti](../../../../../docs/framework/data/adonet/ef/working-with-objects.md).  
  
<a name="AccessingData"></a>   
## Accesso e modifica di dati dell'entità  
 Oltre a rappresentare una soluzione di mapping relazionale a oggetti, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è uno strumento che consente alle applicazioni di accedere e modificare i dati rappresentati come entità e relazioni nel modello concettuale. [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] usa le informazioni nei file del modello e di mapping per tradurre le query di oggetto eseguite su tipi di entità rappresentati nel modello concettuale in query specifiche dell'origine dati.  I risultati della query vengono materializzati in oggetti gestiti da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  In [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] sono disponibili i seguenti metodi per eseguire query su un modello concettuale e restituire oggetti:  
  
-   [!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)]. Fornisce il supporto LINQ \(Language Integrated Query\) per l'esecuzione di query su tipi di entità definiti in un modello concettuale.  Per altre informazioni, vedere [LINQ to Entities](../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md).  
  
-   [!INCLUDE[esql](../../../../../includes/esql-md.md)]. Sottolinguaggio SQL indipendente dall'archiviazione che interagisce direttamente con le entità del modello concettuale e supporta i concetti di [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)].  [!INCLUDE[esql](../../../../../includes/esql-md.md)] viene usato sia con query di oggetto che con query eseguite tramite il provider EntityClient.  Per altre informazioni, vedere [Panoramica su Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md).  
  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] include il provider di dati EntityClient.  Tale provider gestisce connessioni, converte query di entità in query specifiche dell'origine dati e restituisce un lettore dati usato da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] per materializzare i dati dell'entità in oggetti.  Quando la materializzazione degli oggetti non è richiesta, il provider EntityClient può essere usato anche come provider di dati [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] standard consentendo alle applicazioni di eseguire query [!INCLUDE[esql](../../../../../includes/esql-md.md)] e di usare il lettore dati di sola lettura restituito.  Per altre informazioni, vedere [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
 Nel diagramma seguente viene illustrata l'architettura di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] per l'accesso ai dati:  
  
 ![Diagramma dell'architettura di Entity Framework](../../../../../docs/framework/data/adonet/ef/media/wd-efarchdiagram.gif "wd\_EFArchDiagram")  
  
 Tramite gli strumenti di [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)] è possibile generare una classe derivata da `System.Data.Objects.ObjectContext` o `System.Data.Entity.DbContext` che rappresenta il contenitore di entità definito nel modello concettuale.  Questo contesto dell'oggetto fornisce le funzionalità di registrazione delle modifiche e di gestione di identità, concorrenza e relazioni.  Questa classe espone inoltre un metodo `SaveChanges` che scrive inserimenti, aggiornamenti ed eliminazioni nell'origine dati.  Analogamente alle query, queste modifiche vengono eseguite da comandi generati automaticamente dal sistema o da stored procedure specificate dallo sviluppatore.  
  
<a name="DataProviders"></a>   
## Provider di dati  
 Il provider `EntityClient` estende il modello del provider [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] tramite l'accesso ai dati in termini di relazioni ed entità concettuali.  Esegue query che usano [!INCLUDE[esql](../../../../../includes/esql-md.md)].  [!INCLUDE[esql](../../../../../includes/esql-md.md)] fornisce il linguaggio di query sottostante che consente la comunicazione di `EntityClient` con il database.  Per altre informazioni, vedere [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] include un provider di dati SqlClient aggiornato che supporta gli alberi dei comandi canonici.  Per altre informazioni, vedere [SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md).  
  
<a name="Tools"></a>   
## Strumenti di Entity Data Model  
 Insieme al runtime di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], [!INCLUDE[vs_current_long](../../../../../includes/vs-current-long-md.md)] include gli strumenti di mapping e di modellazione.  Per altre informazioni, vedere [Modellazione e mapping](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md).  
  
<a name="LearnMore"></a>   
## Ulteriori informazioni  
 Per altre informazioni su [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], fare clic sui collegamenti seguenti.  
  
 [Guida introduttiva](../../../../../docs/framework/data/adonet/ef/getting-started.md)  
 Contiene informazioni su come diventare rapidamente operativi mediante la [Quickstart](http://msdn.microsoft.com/it-it/0bc534be-789f-4819-b9f6-76e51d961675), in cui viene illustrata la creazione di una semplice applicazione [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
 [Terminologia relativa a Entity Framework](../../../../../docs/framework/data/adonet/ef/terminology.md)  
 Definisce molti dei termini introdotti da Entity Data Model e [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] e usati nella documentazione di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
 [Risorse di Entity Framework](../../../../../docs/framework/data/adonet/ef/resources.md)  
 Fornisce collegamenti ad argomenti concettuali e collegamenti a risorse ed argomenti esterni per la compilazione di applicazioni [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
## Vedere anche  
 [ADO.NET Entity Framework](../../../../../docs/framework/data/adonet/ef/index.md)