---
title: "Esecuzione di query sul servizio dati (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, accesso ai dati"
  - "WCF Data Services, libreria client"
  - "WCF Data Services, esecuzione di query"
ms.assetid: 823e9444-27aa-4f1f-be8e-0486d67f54c0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Esecuzione di query sul servizio dati (WCF Data Services)
La libreria client di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente di eseguire query su un servizio dati mediante i modelli di programmazione comuni di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], compreso il linguaggio LINQ \(Language Integrated Query\).  La libreria client traduce una query, definita nel client come un'istanza della classe <xref:System.Data.Services.Client.DataServiceQuery%601>, in un messaggio di richiesta HTTP GET.  La libreria riceve il messaggio di risposta e lo converte in istanze delle classi del servizio dati client.  Queste classi vengono rilevate dall'oggetto <xref:System.Data.Services.Client.DataServiceContext> a cui appartiene <xref:System.Data.Services.Client.DataServiceQuery%601>.  
  
## Query sul servizio dati  
 La classe generica <xref:System.Data.Services.Client.DataServiceQuery%601> rappresenta una query che restituisce una raccolta di zero o più istanze di tipi di entità.  Una query sul servizio dati appartiene sempre a un contesto del servizio dati esistente.  Il contesto gestisce l'URI del servizio e le informazioni sui metadati necessarie per comporre ed eseguire la query.  
  
 Quando si usa la finestra di dialogo **Aggiungi riferimento al servizio** per aggiungere un servizio dati a un'applicazione client basata su [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], viene creata una classe contenitore di entità che eredita dalla classe <xref:System.Data.Services.Client.DataServiceContext>.  Tale classe include proprietà che restituiscono istanze della classe <xref:System.Data.Services.Client.DataServiceQuery%601> tipizzate.  Esiste una proprietà per ogni set di entità esposto dal servizio dati.  Tali proprietà semplificano la creazione di un'istanza di <xref:System.Data.Services.Client.DataServiceQuery%601> tipizzata.  
  
 Una query viene eseguita negli scenari seguenti:  
  
-   Quando i risultati vengono enumerati in modo implicito, ad esempio:  
  
    -   Quando viene enumerata una proprietà della classe <xref:System.Data.Services.Client.DataServiceContext> che rappresenta un set di entità, ad esempio durante un ciclo `foreach` \(C\#\) o `For Each` \([!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\).  
  
    -   Quando la query viene assegnata a una raccolta `List`.  
  
-   Quando viene chiamato il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> o <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> in modo esplicito.  
  
-   Quando viene chiamato un operatore di esecuzione di query LINQ, ad esempio <xref:System.Linq.Enumerable.First%2A> o <xref:System.Linq.Enumerable.Single%2A>.  
  
 La query seguente, al termine dell'esecuzione, restituisce tutte le entità `Customers` nel servizio dati Northwind:  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getallcustomersspecific)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getallcustomersspecific)]  
  
 Per altre informazioni, vedere [Procedura: eseguire query sul servizio dati](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md).  
  
 Il client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta le query per gli oggetti ad associazione tardiva, ad esempio quando si usa il tipo *dinamico* in C\#.  Tuttavia, per preservare le prestazioni, è necessario comporre sempre query fortemente tipizzate per il servizio dati.  Il tipo <xref:System.Tuple> e oggetti dinamici non sono supportati dal client.  
  
## Query LINQ  
 Poiché la classe <xref:System.Data.Services.Client.DataServiceQuery%601> implementa l'interfaccia <xref:System.Linq.IQueryable%601> definita tramite LINQ, la libreria client di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è in grado di trasformare le query LINQ sui dati di set di entità in un URI che rappresenta un'espressione di query valutata in base a una risorsa del servizio dati.  Nell'esempio seguente viene mostrata una query LINQ equivalente alla precedente classe <xref:System.Data.Services.Client.DataServiceQuery%601> che restituisce le entità `Orders` con un costo di spedizione maggiore di 30 dollari e ordina i risultati in base al costo di spedizione:  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptionslinqspecific)]
 [!code-vb[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptionslinqspecific)]  
  
 Questa query LINQ viene convertita nel seguente URI di query che viene eseguito sul servizio dati [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md) basato su Northwind:  
  
```  
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30  
```  
  
> [!NOTE]
>  La sintassi LINQ consente di esprimere un set di query più ampio di quello consentito dalla sintassi URI basata su REST \(Representational State Transfer\) usata dai servizi dati.  Quando non è possibile eseguire il mapping della query a un URI nel servizio dati di destinazione, viene generato un oggetto <xref:System.NotSupportedException>.  
  
 Per altre informazioni, vedere [Considerazioni su LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md).  
  
## Aggiunta di opzioni di query  
 Le query del servizio dati supportano tutte le opzioni di query fornite da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  È possibile chiamare il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> per aggiungere opzioni di query a un'istanza <xref:System.Data.Services.Client.DataServiceQuery%601>.  <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> restituisce una nuova istanza di <xref:System.Data.Services.Client.DataServiceQuery%601> equivalente alla query originale ma con il nuovo set di opzioni.  La query seguente al termine dell'esecuzione restituisce oggetti `Orders` filtrati in base al valore di `Freight` e ordinati in ordine decrescente per `OrderID`:  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptionsspecific)]
 [!code-vb[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptionsspecific)]  
  
 È possibile usare l'opzione di query `$orderby` per ordinare e filtrare una query in base a una singola proprietà, come nell'esempio seguente in cui gli oggetti `Orders` restituiti vengono filtrati e ordinati in base al valore della proprietà `Freight`:  
  
 [!code-csharp[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#orderwithfilter)]
 [!code-vb[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#orderwithfilter)]  
  
 È possibile chiamare consecutivamente il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> per costruire espressioni di query complesse.  Per altre informazioni, vedere [Procedura: aggiungere opzioni di query a una query del servizio dati](../../../../docs/framework/data/wcf/how-to-add-query-options-to-a-data-service-query-wcf-data-services.md).  
  
 Le opzioni di query costituiscono un altro modo per esprimere i componenti sintattici di una query LINQ.  Per altre informazioni, vedere [Considerazioni su LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md).  
  
> [!NOTE]
>  L'opzione di query `$select` non può essere aggiunta a un URI di query tramite il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>.  Si consiglia di usare il metodo LINQ <xref:System.Linq.Enumerable.Select%2A> in modo che il client generi l'opzione di query `$select` nell'URI della richiesta.  
  
<a name="executingQueries"></a>   
## Esecuzione del client e del server  
 Il client esegue una query in due parti.  Ogni qualvolta possibile, le espressioni di una query vengono prima valutate sul client e quindi viene generata una query basata sull'URI che viene inviata al servizio dati per la valutazione rispetto ai dati del servizio.  Si consideri la query LINQ riportata di seguito:  
  
 [!code-csharp[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#linqqueryclientevalspecific)]
 [!code-vb[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#linqqueryclientevalspecific)]  
  
 In questo esempio, l'espressione `(basePrice – (basePrice * discount))` viene valutata sul client.  Di conseguenza, l'URI di query effettivo `http://localhost:12345/northwind.svc/Products()?$filter=(UnitPrice gt 90.00M) and substringof('bike',ProductName)` che viene inviato al servizio dati contiene il valore decimale già calcolato `90` nella clausola di filtro.  Le altre parti dell'espressione dei filtri, compresa l'espressione della sottostringa, vengono valutate dal servizio dati.  Le espressioni valutate sul client seguono la semantica di Common Language Runtime \(CLR\), mentre le espressioni inviate al servizio dati si basano sull'implementazione del servizio dati del protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  È anche necessario tenere presente scenari in cui questa valutazione separata può provocare risultati imprevisti, ad esempio quando il client e il servizio eseguono valutazioni basate sull'ora in fusi orari diversi.  
  
## Risposte alle query  
 Se eseguita, <xref:System.Data.Services.Client.DataServiceQuery%601> restituisce un oggetto <xref:System.Collections.Generic.IEnumerable%601> del tipo di entità richiesto.  È possibile eseguire il cast di questo risultato della query a un oggetto <xref:System.Data.Services.Client.QueryOperationResponse%601>, come nell'esempio seguente:  
  
 [!code-csharp[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getresponsespecific)]
 [!code-vb[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getresponsespecific)]  
  
 Le istanze del tipo di entità che rappresentano entità nel servizio dati vengono create nel client tramite un processo denominato "materializzazione degli oggetti".  Per altre informazioni, vedere [Materializzazione di oggetti](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md).  L'oggetto <xref:System.Data.Services.Client.QueryOperationResponse%601> implementa <xref:System.Collections.Generic.IEnumerable%601> per fornire accesso ai risultati della query.  
  
 <xref:System.Data.Services.Client.QueryOperationResponse%601> dispone inoltre dei membri seguenti che consentono di accedere a informazioni aggiuntive sul risultato della query:  
  
-   <xref:System.Data.Services.Client.OperationResponse.Error%2A>: ottiene un eventuale errore generato dall'operazione.  
  
-   <xref:System.Data.Services.Client.OperationResponse.Headers%2A>: contiene la raccolta di intestazioni di risposta HTTP associate alla risposta alla query.  
  
-   <xref:System.Data.Services.Client.QueryOperationResponse.Query%2A>: ottiene l'istanza <xref:System.Data.Services.Client.DataServiceQuery%601> originale generata da <xref:System.Data.Services.Client.QueryOperationResponse%601>.  
  
-   <xref:System.Data.Services.Client.OperationResponse.StatusCode%2A>: ottiene il codice di risposta HTTP per la risposta alla query.  
  
-   <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A>: ottiene il numero complessivo di entità del set di entità quando viene chiamato il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> su <xref:System.Data.Services.Client.DataServiceQuery%601>.  
  
-   <xref:System.Data.Services.Client.QueryOperationResponse.GetContinuation%2A>: restituisce un oggetto <xref:System.Data.Services.Client.DataServiceQueryContinuation> che contiene l'URI della pagina di risultati successiva.  
  
 Per impostazione predefinita, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] restituisce solo i dati selezionati in modo esplicito dall'URI di query.  Ciò consente di caricare in modo esplicito dati aggiuntivi dal servizio dati, quando necessario.  Una richiesta viene inviata al servizio dati ogni volta che vengono caricati in modo esplicito dati dal servizio dati.  I dati che possono essere caricati in modo esplicito comprendono entità correlate, dati di risposta di paging e flussi di dati binari.  
  
> [!NOTE]
>  Poiché un servizio dati può restituire una risposta di paging, si consiglia di gestire una risposta del servizio dati sottoposta a paging tramite un modello di programmazione dell'applicazione.  Per altre informazioni, vedere [Caricamento di contenuto posticipato](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
 È inoltre possibile ridurre la quantità di dati restituiti da una query specificando che solo determinate proprietà di un'entità vengano restituite nella risposta.  Per altre informazioni, vedere [Proiezioni di query](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md).  
  
## Conteggio del numero complessivo di entità nel set  
 In alcuni scenari è utile conoscere il numero complessivo di entità contenute in un set di entità e non soltanto il numero restituito dalla query.  Chiamare il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> in <xref:System.Data.Services.Client.DataServiceQuery%601> per richiedere che nel risultato della query venga incluso il conteggio totale delle entità presenti nel set.  In questo caso la proprietà <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> dell'oggetto <xref:System.Data.Services.Client.QueryOperationResponse%601> restituito contiene il numero totale di entità nel set.  
  
 È anche possibile ottenere solo il conteggio totale delle entità nel set come valore <xref:System.Int32> o <xref:System.Int64> chiamando rispettivamente i metodi <xref:System.Linq.Enumerable.Count%2A> o <xref:System.Linq.Enumerable.LongCount%2A>.  Quando vengono chiamati questi metodi, viene restituito solo il valore del conteggio senza <xref:System.Data.Services.Client.QueryOperationResponse%601>.  Per altre informazioni, vedere [Procedura: determinare il numero di entità restituite da una query](../../../../docs/framework/data/wcf/number-of-entities-returned-by-a-query-wcf.md).  
  
## Contenuto della sezione  
 [Proiezioni di query](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)  
  
 [Materializzazione di oggetti](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)  
  
 [Considerazioni su LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md)  
  
 [Procedura: eseguire query sul servizio dati](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md)  
  
 [Procedura: aggiungere opzioni di query a una query del servizio dati](../../../../docs/framework/data/wcf/how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)  
  
 [Procedura: determinare il numero di entità restituite da una query](../../../../docs/framework/data/wcf/number-of-entities-returned-by-a-query-wcf.md)  
  
 [Procedura: specificare le credenziali del client per una richiesta del servizio dati](../../../../docs/framework/data/wcf/specify-client-creds-for-a-data-service-request-wcf.md)  
  
 [Procedura: impostare le intestazioni nella richiesta del client](../../../../docs/framework/data/wcf/how-to-set-headers-in-the-client-request-wcf-data-services.md)  
  
 [Procedura: proiettare i risultati delle query](../../../../docs/framework/data/wcf/how-to-project-query-results-wcf-data-services.md)  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)