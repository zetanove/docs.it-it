---
title: "LINQ to SQL a pi&#249; livelli con servizi Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9cb10eb8-957f-4beb-a271-5f682016fed2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# LINQ to SQL a pi&#249; livelli con servizi Web
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è progettato soprattutto per essere usato con il livello intermedio in un livello di accesso ai dati \(DAL\) a regime di controllo libero \("loosely\-coupled"\), ad esempio un servizio Web.  Se il livello di presentazione è una pagina Web ASP.NET, verrà usato il controllo server Web <xref:System.Web.UI.WebControls.LinqDataSource> per gestire il trasferimento dei dati tra l'interfaccia utente e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] nel livello intermedio.  Se il livello di presentazione non è una pagina ASP.NET, sarà necessario eseguire operazioni aggiuntive nel livello intermedio e nel livello di presentazione in modo da gestire la serializzazione e deserializzazione dei dati.  
  
## Configurazione di LINQ to SQL nel livello intermedio  
 In un servizio Web o in un'applicazione a più livelli, il livello intermedio contiene il contesto dati e le classi di entità.  È possibile creare manualmente queste classi oppure usando SQLMetal.exe o la [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] come descritto in un altro punto della documentazione.  In fase di progettazione è possibile rendere le classi di entità serializzabili.  Per altre informazioni, vedere [Procedura: creare entità serializzabili](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md).  Un'altra opzione è creare un set separato di classi che incapsulano i dati da serializzare e quindi proiettare in tali tipi serializzabili quando si restituiscono i dati nelle query [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  
  
 Definire quindi l'interfaccia con i metodi che i client chiameranno per recuperare, inserire e aggiornare i dati.  I metodi di interfaccia eseguono il wrapping delle query [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  È possibile usare qualsiasi tipo di meccanismo di serializzazione per gestire le chiamate al metodo remote e la serializzazione dei dati.  L'unico requisito è che se si hanno relazioni cicliche o bidirezionali nel modello a oggetti, come ad esempio tra Customers e Orders nel modello a oggetti standard Northwind, è necessario usare un serializzatore che lo supporti.  L'oggetto <xref:System.Runtime.Serialization.DataContractSerializer> di Windows Communication Foundation \(WCF\) supporta le relazioni bidirezionali mentre l'oggetto XmlSerializer usato con i servizi Web non WCF non prevede tale tipo di supporto. Se si sceglie di usare XmlSerializer, sarà necessario accertarsi che il modello a oggetti non contenga relazioni cicliche.  
  
 Per altre informazioni su Windows Communication Foundation, vedere [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../Topic/Windows%20Communication%20Foundation%20Services%20and%20WCF%20Data%20Services%20in%20Visual%20Studio.md).  
  
 Implementare le regole business o un'altra regola specifica del dominio usando le classi e i metodi parziali delle classi <xref:System.Data.Linq.DataContext> e di entità per effettuare l'hook negli eventi di runtime [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Per altre informazioni, vedere [Implementazione della logica di business a più livelli](../../../../../../docs/framework/data/adonet/sql/linq/implementing-business-logic-linq-to-sql.md).  
  
## Definizione dei tipi serializzabili  
 Il livello client o di presentazione deve avere le definizioni dei tipi per le classi che riceverà dal livello intermedio.  Tali tipi possono essere classi di entità o classi speciali che eseguono il wrapping solo di determinati campi delle classi di entità per i servizi remoti.  In ogni caso, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non è importante il modo in cui il livello di presentazione acquisisce le definizioni dei tipi.  Ad esempio, il livello di presentazione può usare WCF per generare automaticamente i tipi o può avere una copia di una DLL in cui vengono definiti tali tipi o ancora può definire versioni dei tipi personalizzate.  
  
## Recupero e inserimento dei dati  
 Il livello intermedio definisce un'interfaccia che specifica il modo in cui il livello di presentazione accede ai dati,  ad esempio `GetProductByID(int productID)` o `GetCustomers()`.  Nel livello intermedio, il corpo del metodo crea in genere una nuova istanza di <xref:System.Data.Linq.DataContext> ed esegue una query su una o più tabelle.  Il livello intermedio restituisce quindi il risultato come <xref:System.Collections.Generic.IEnumerable%601>, dove `T` è una classe di entità o un altro tipo usato per la serializzazione.  Il livello di presentazione non invia o riceve direttamente le variabili di query dal livello intermedio.  I due livelli scambiano valori, oggetti e raccolte di dati concreti.  Dopo aver ricevuto una raccolta, il livello di presentazione può usare [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] to Objects per eseguirne una query, se necessario.  
  
 Durante l'inserimento dei dati, il livello di presentazione può costruire un nuovo oggetto e inviarlo al livello intermedio oppure il livello intermedio può costruire l'oggetto in base ai valori forniti dal livello di presentazione.  In generale, il recupero e l'inserimento dei dati nelle applicazioni a più livelli non differiscono molto dal processo nelle applicazioni a 2 livelli.  Per altre informazioni, vedere [Esecuzione di query nel database](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md) e [Scrittura e invio di modifiche di dati](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md).  
  
## Rilevamento delle modifiche per aggiornamenti ed eliminazioni  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] supporta la concorrenza ottimistica basata sui timestamp \(anche denominata RowVersions\) e sui valori originali.  Se le tabelle di database hanno timestamp, gli aggiornamenti e le eliminazioni richiedono operazioni aggiuntive sul livello intermedio o sul livello della presentazione.  Tuttavia, se è necessario usare i valori originali per i controlli di concorrenza ottimistica, il livello di presentazione sarà responsabile del rilevamento e dell'invio di tali valori durante l'aggiornamento  poiché le modifiche effettuate alle entità nel livello di presentazione non vengono rilevate nel livello intermedio.  Infatti, il recupero originale di un'entità e l'eventuale aggiornamento vengono eseguiti in genere da due istanze completamente separate di <xref:System.Data.Linq.DataContext>.  
  
 Maggiore è il numero delle modifiche effettuate dal livello di presentazione, più sono complessi il rilevamento e l'invio delle modifiche al livello intermedio.  L'implementazione di un meccanismo per la comunicazione delle modifiche spetta completamente all'applicazione.  È necessario solo fornire a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] i valori originali necessari per i controlli di concorrenza ottimistica.  
  
 Per altre informazioni, vedere [Recupero dei dati e operazioni CUD in applicazioni a più livelli \(LINQ to SQL\)](../../../../../../docs/framework/data/adonet/sql/linq/data-retrieval-and-cud-operations-in-n-tier-applications.md).  
  
## Vedere anche  
 [Applicazioni a più livelli e remote con LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)   
 [NIB: LinqDataSource Web Server Control Overview](http://msdn.microsoft.com/it-it/104cfc3f-7385-47d3-8a51-830dfa791136)