---
title: "Considerazioni sulla migrazione (Entity Framework) | Microsoft Docs"
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
ms.assetid: c85b6fe8-cc32-4642-8f0a-dc0e5a695936
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Considerazioni sulla migrazione (Entity Framework)
[!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] Entity Framework offre diversi vantaggi alle applicazioni esistenti.  Uno dei principali vantaggi consiste nella possibilità di usare un modello concettuale per separare le strutture di dati impiegate dall'applicazione dallo schema presente nell'origine dati  in modo da apportare facilmente modifiche future al modello di archiviazione o all'origine dati stessa senza effettuare modifiche di compensazione nell'applicazione.  Per altre informazioni sui vantaggi derivanti dall'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], vedere [Panoramica su Entity Framework](../../../../../docs/framework/data/adonet/ef/overview.md) e [Entity Data Model](../../../../../docs/framework/data/adonet/entity-data-model.md).  
  
 Per sfruttare i vantaggi di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è possibile eseguire la migrazione di un'applicazione esistente a [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Alcune attività sono comuni a tutte le applicazioni migrate.  Tra queste figurano l'aggiornamento dell'applicazione per l'uso di [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] a partire dalla versione 3.5 Service Pack 1 \(SP1\), la definizione di modelli e di mapping e la configurazione di Entity Framework.  Quando si esegue la migrazione di un'applicazione a [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] occorre tenere presenti considerazioni aggiuntive.  che dipendono dal tipo di applicazione migrato e dalla funzionalità specifica dell'applicazione.  In questo argomento vengono fornite informazioni grazie alle quali è possibile scegliere l'approccio ideale da usare quando si aggiorna un'applicazione esistente.  
  
## Considerazioni generali sulla migrazione  
 Le considerazioni seguenti riguardano l'esecuzione della migrazione di un'applicazione ad [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]:  
  
-   È possibile eseguire la migrazione a Entity Framework di qualsiasi applicazione che usa [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] a partire dalla versione 3.5 SP1, a condizione che Entity Framework sia supportato dal provider di dati dell'origine dati usata dall'applicazione.  
  
-   Entity Framework potrebbe non supportare tutte le funzionalità di un provider dell'origine dati, anche se supportato da tale provider.  
  
-   Nel caso di applicazioni complesse o di grandi dimensioni non è necessario eseguire la migrazione dell'intera applicazione a Entity Framework in una sola volta.  È comunque necessario sostituire le parti dell'applicazione che non usano Entity Framework quando si cambia l'origine dati.  
  
-   La connessione al provider di dati usata da Entity Framework può essere condivisa con altre parti dell'applicazione in quanto [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] usa provider di dati [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] per accedere all'origine dati.  Il provider SqlClient viene ad esempio usato da Entity Framework per accedere a un database di SQL Server.  Per altre informazioni, vedere [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
## Attività comuni di migrazione  
 Il percorso per eseguire la migrazione di un'applicazione esistente a [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] dipende dal tipo di applicazione e dalla strategia di accesso ai dati esistente.  È invece necessario effettuare sempre le attività seguenti quando si esegue la migrazione di un'applicazione esistente a [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
> [!NOTE]
>  Tutte le attività indicate vengono eseguite automaticamente quando si usano gli strumenti di Entity Data Model a partire da [!INCLUDE[vsOrcas](../../../../../includes/vsorcas-md.md)].  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
1.  Aggiornamento dell'applicazione.  
  
     È necessario aggiornare i progetti creati con una versione precedente di [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] e [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] per l'uso di [!INCLUDE[vsOrcas](../../../../../includes/vsorcas-md.md)] SP1 e [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] a partire dalla versione 3.5 SP1.  
  
2.  Definire i modelli e il mapping.  
  
     I file di modello e di mapping definiscono entità nel modello concettuale, ovvero le strutture dell'origine dati, quali le tabelle, le stored procedure e le visualizzazioni, e il mapping tra le entità e tali strutture.  Per altre informazioni, vedere [How to: Manually Define the Model and Mapping Files](http://msdn.microsoft.com/it-it/d4fd6864-f2a1-48f0-aa32-1e318775a99a).  
  
     I tipi definiti nel modello di archiviazione devono corrispondere al nome degli oggetti presenti nell'origine dati.  Se nell'applicazione esistente i dati sono esposti come oggetti, è necessario assicurarsi che le entità e le proprietà definite nel modello concettuale corrispondano ai nomi delle proprietà e delle classi di dati esistenti.  Per altre informazioni, vedere [How to: Customize Modeling and Mapping Files to Work with Custom Objects](http://msdn.microsoft.com/it-it/bb40c4db-0121-4e45-a167-8fb06707a708).  
  
    > [!NOTE]
    >  Entity Data Model Designer consente di rinominare le entità presenti nel modello concettuale in modo che corrispondano agli oggetti esistenti.  Per altre informazioni, vedere [Entity Data Model Designer](http://msdn.microsoft.com/it-it/4ccd7ad6-b934-4f7c-82a0-cfd2d4a95faf).  
  
3.  Definizione della stringa di connessione.  
  
     In [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] viene usata una stringa di connessione con formattazione speciale per l'esecuzione di query sul modello concettuale.  In tale stringa sono incapsulate le informazioni relative ai file di modello e di mapping e alla connessione all'origine dati.  Per altre informazioni, veder [Procedura: definire la stringa di connessione](../../../../../docs/framework/data/adonet/ef/how-to-define-the-connection-string.md).  
  
4.  Configurare il progetto [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)].  
  
     È necessario aggiungere i riferimenti agli assembly di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] e i file di modello e di mapping al progetto [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)].  L'aggiunta di tali file di mapping al progetto consente di garantirne la distribuzione con l'applicazione nel percorso indicato nella stringa di connessione.  Per altre informazioni, vedere [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/it-it/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e).  
  
## Considerazioni per le applicazioni con oggetti esistenti  
 A partire da [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] versione 4, [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] supporta gli oggetti POCO \("plain old" CLR objects\), denominati anche oggetti che non riconoscono la persistenza.  Nella maggior parte dei casi, gli oggetti esistenti possono essere usati con [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] apportando piccole modifiche.  Per altre informazioni, vedere [Working with POCO Entities](http://msdn.microsoft.com/it-it/5e0fb82a-b6d1-41a1-b37b-c12db61629d3). È possibile inoltre eseguire la migrazione di un'applicazione a [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] e usare le classi di dati generate dagli strumenti di Entity Framework.  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
## Considerazioni per le applicazioni che usano provider ADO.NET  
 I provider [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)], ad esempio SqlClient, consentono di eseguire query su un'origine dati in modo che vengano restituiti dati tabulari.  I dati possono anche essere caricati in un set di dati di [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)].  Nell'elenco seguente vengono riportate e illustrate le considerazioni che riguardano l'aggiornamento di un'applicazione che usa un provider [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] esistente:  
  
 Visualizzazione di dati tabulari mediante un lettore dati.  
 È possibile eseguire una query [!INCLUDE[esql](../../../../../includes/esql-md.md)] usando il provider EntityClient ed effettuando l'enumerazione dell'oggetto <xref:System.Data.EntityClient.EntityDataReader> restituito.  Eseguire questa operazione solo se l'applicazione visualizza dati tabulari mediante un lettore dati e non richiede le funzionalità offerte da [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] per la materializzazione dei dati in oggetti, il rilevamento delle modifiche e l'applicazione di aggiornamenti. È possibile continuare a usare il codice di accesso ai dati esistente che applica gli aggiornamenti all'origine dati servendosi comunque della connessione esistente cui si accede dalla proprietà <xref:System.Data.EntityClient.EntityConnection.StoreConnection%2A> di <xref:System.Data.EntityClient.EntityConnection>.  Per altre informazioni, vedere [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
 Uso di set di dati.  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] offre gran parte delle stesse funzionalità fornite dai set di dati, inclusi la persistenza in memoria, il rilevamento delle modifiche, l'associazione dati e la serializzazione degli oggetti come dati XML.  Per altre informazioni, vedere [Utilizzo di oggetti](../../../../../docs/framework/data/adonet/ef/working-with-objects.md).  
  
 Se [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] non fornisce la funzionalità del set di dati necessaria per l'applicazione, è possibile sfruttare comunque i vantaggi delle query LINQ usando [!INCLUDE[linq_dataset](../../../../../includes/linq-dataset-md.md)].  Per altre informazioni, vedere [LINQ to DataSet](../../../../../docs/framework/data/adonet/linq-to-dataset.md).  
  
## Considerazioni per le applicazioni che associano dati ai controlli  
 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] consente di incapsulare dati in un'origine dati, ad esempio un set di dati o un controllo origine dati [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)], quindi di associare elementi dell'interfaccia utente ai controlli dati.  Nell'elenco seguente vengono riportate e illustrate le considerazioni relative all'associazione dei controlli ai dati di Entity Framework.  
  
 Associazione di dati a controlli.  
 Quando si esegue una query sul modello concettuale [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] restituisce i dati sotto forma di oggetti che sono istanze di tipi di entità.  Tali oggetti possono essere associati direttamente a controlli e l'associazione definita supporta gli aggiornamenti. In altre parole, le modifiche apportate ai dati di un controllo, ad esempio una riga in un oggetto <xref:System.Windows.Forms.DataGridView>, vengono automaticamente salvate nel database quando viene chiamato il metodo <xref:System.Data.Objects.ObjectContext.SaveChanges%2A>.  
  
 Se l'applicazione enumera i risultati di una query per visualizzare i dati in un controllo <xref:System.Windows.Forms.DataGridView> o in un altro tipo di controllo che supporti l'associazione dati, è possibile modificarla in modo da associare il controllo al risultato di un oggetto <xref:System.Data.Objects.ObjectQuery%601>.  
  
 Per altre informazioni, vedere [Binding Objects to Controls](http://msdn.microsoft.com/it-it/2fd34855-929b-4303-a91e-4bb69d958f2b).  
  
 Controlli origine dati [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)].  
 In [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è incluso un controllo origine dati progettato per semplificare l'associazione dati nelle applicazioni Web [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)].  Per altre informazioni, vedere [Controllo origine dati di Entity Framework](../Topic/EntityDataSource%20Web%20Server%20Control%20Overview.md).  
  
## Altre considerazioni  
 Di seguito vengono riportate le considerazioni di cui è possibile tenere conto quando si esegue la migrazione di tipi specifici di applicazione a Entity Framework.  
  
 Applicazioni che espongono servizi di dati.  
 I servizi e le applicazioni Web basati su Windows Communication Foundation \(WCF\) espongono i dati provenienti da un'origine dati sottostante usando un formato di messaggistica di richiesta\/risposta XML.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] supporta la serializzazione degli oggetti entità mediante la serializzazione dei contratti di dati WCF, binaria o XML.  I tipi di serializzazione binaria e WCF implicano la serializzazione completa degli oggetti grafici.  Per altre informazioni, vedere [Building N\-Tier Applications](http://msdn.microsoft.com/it-it/9439d2ba-6b5f-44e8-be65-8a442d922cbb).  
  
 Applicazioni che usano dati XML.  
 La serializzazione degli oggetti consente di creare servizi di dati di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Tali servizi forniscono dati alle applicazioni che usano dati XML, quali le applicazioni Internet basate su Ajax.  In questi casi usare [!INCLUDE[ssAstoria](../../../../../includes/ssastoria-md.md)].  Tali servizi sono basati sul modello EDM e forniscono accesso dinamico ai dati delle entità tramite azioni HTTP REST \(Representational State Transfer\) standard, come GET, PUT e POST.  Per altre informazioni, vedere [WCF Data Services 4.5](../../../../../docs/framework/data/wcf/index.md).  
  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] non supporta un tipo di dati XML nativo.  Ciò significa che, quando viene eseguito il mapping di un'entità a una tabella con una colonna XML, la proprietà dell'entità equivalente della colonna XML è una stringa.  Gli oggetti possono essere disconnessi e serializzati come XML.  Per altre informazioni, vedere [Serializing Objects](http://msdn.microsoft.com/it-it/06c77f9b-5b2e-4c78-b3e3-8c148ba0ea99).  
  
 Se l'applicazione richiede la funzionalità di query sui dati XML, è comunque possibile sfruttare i vantaggi delle query LINQ usando LINQ to XML.  Per altre informazioni, vedere [LINQ to XML](../../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md).  
  
 Applicazioni che gestiscono lo stato.  
 Le applicazioni Web [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)] devono gestire frequentemente lo stato di una pagina Web o di una sessione utente.  Gli oggetti presenti in un'istanza di <xref:System.Data.Objects.ObjectContext> possono essere archiviati nello stato di visualizzazione del client o nello stato della sessione sul server ed essere successivamente recuperati e riassociati a un nuovo contesto dell'oggetto.  Per altre informazioni, vedere [Attaching and Detaching Objects](http://msdn.microsoft.com/it-it/41d5c1ef-1b78-4502-aa10-7e1438d62d23).  
  
## Vedere anche  
 [Considerazioni sulla distribuzione](../../../../../docs/framework/data/adonet/ef/deployment-considerations.md)   
 [Terminologia relativa a Entity Framework](../../../../../docs/framework/data/adonet/ef/terminology.md)