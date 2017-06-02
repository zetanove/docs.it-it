---
title: "Proiezioni di query (WCF Data Services) | Microsoft Docs"
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
  - "proiezione [WCF Data Service]"
  - "proiezioni di query [WCF Data Services]"
  - "WCF Data Services, proiezione"
  - "WCF Data Services, esecuzione di query"
ms.assetid: a09f4985-9f0d-48c8-b183-83d67a3dfe5f
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Proiezioni di query (WCF Data Services)
In [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] la proiezione fornisce un meccanismo per ridurre la quantità di dati nel feed restituiti da una query specificando che solo determinate proprietà di un'entità vengano restituite nella risposta.  Per altre informazioni, vedere la pagina relativa all'[opzione query di sistema Select \($select\) in OData](http://go.microsoft.com/fwlink/?LinkId=186076).  
  
 In questo argomento viene descritto come definire una proiezione di query e quali sono i requisiti per i tipi di entità e non entità. Viene inoltre illustrato come eseguire gli aggiornamenti dei risultati proiettati e creare i tipi proiettati e vengono elencate alcune considerazioni sulla proiezione.  
  
## Definizione di una proiezione di query  
 È possibile aggiungere una clausola di proiezione a una query usando l'opzione query `$select` in un URI o la clausola [select](../Topic/select%20clause%20\(C%23%20Reference\).md) \([Select](../Topic/Select%20Clause%20\(Visual%20Basic\).md) in Visual Basic\) in una query LINQ.  I dati di entità restituiti possono essere proiettati in tipi di entità o non entità sul client.  Negli esempi di questo argomento viene illustrato l'uso della clausola `select` in una query LINQ.  
  
> [!IMPORTANT]
>  Quando si salvano gli aggiornamenti apportati ai tipi proiettati, potrebbe verificarsi una perdita di dati nel servizio dati.  Per altre informazioni, vedere [Considerazioni sulla proiezione](#considerations).  
  
## Requisiti per tipi di entità e non entità  
 I tipi di entità devono disporre di una o più proprietà Identity che costituiscono la chiave di entità.  I tipi di entità vengono definiti nei client usando uno dei modi riportati di seguito.  
  
-   Tramite l'applicazione di <xref:System.Data.Services.Common.DataServiceKeyAttribute> o <xref:System.Data.Services.Common.DataServiceEntityAttribute> al tipo.  
  
-   Tramite la proprietà `ID` del tipo.  
  
-   Tramite la proprietà *tipo*`ID` del tipo, dove *tipo* corrisponde al nome del tipo.  
  
 Per impostazione predefinita, quando si proiettano i risultati delle query in un tipo definito nel client, le proprietà richieste nella proiezione devono esistere nel tipo di client.  Tuttavia, quando si specifica un valore `true` per la proprietà <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A> di <xref:System.Data.Services.Client.DataServiceContext>, non è necessario che le proprietà specificate nella proiezione siano presenti nel tipo di client.  
  
### Aggiornamenti dei risultati proiettati  
 Quando si proiettano i risultati di una query in tipi di entità nel client, <xref:System.Data.Services.Client.DataServiceContext> può rilevare gli oggetti con aggiornamenti da restituire al servizio dati quando viene chiamato il metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>.  Tuttavia, gli aggiornamenti apportati ai dati proiettati in tipi di non entità nel client non possono essere restituiti al servizio dati,  perché il servizio dati non può aggiornare l'entità corretta nell'origine dati senza una chiave per identificare l'istanza di entità.  I tipi di non entità non vengono associati a <xref:System.Data.Services.Client.DataServiceContext>.  
  
 Quando una o più proprietà di un tipo di entità definito nel servizio dati non sono presenti nel tipo di client in cui viene proiettata l'entità, gli inserimenti di nuove entità non conterranno le proprietà mancanti.  In questo caso, **anche** gli aggiornamenti apportati alle entità esistenti non includeranno le proprietà mancanti.  Quando esiste un valore per la proprietà, l'aggiornamento ripristina il valore predefinito della proprietà, secondo quanto definito nell'origine dati.  
  
### Creazione di tipi proiettati  
 Nell'esempio seguente viene usata una query LINQ anonima che proietta le proprietà correlate all'indirizzo del tipo `Customers` in un nuovo tipo `CustomerAddress`, definito nel client ed attribuito come tipo di entità:  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddressSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#selectcustomeraddressspecific)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddressSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#selectcustomeraddressspecific)]  
  
 In questo esempio, il modello dell'inizializzatore di oggetti viene usato per creare una nuova istanza del tipo `CustmerAddress`, anziché chiamare un costruttore.  I costruttori non sono supportati in caso di proiezione in tipi di entità, ma possono essere usati durante la proiezione in tipi di non entità e anonimi.  Poiché `CustomerAddress` è un tipo di entità, le modifiche possono essere apportate e restituite al servizio dati.  
  
 Inoltre, i dati del tipo `Customer` vengono proiettati in un'istanza del tipo di entità `CustomerAddress`, anziché di un tipo anonimo.  La proiezione in tipi anonimi è supportata, ma i dati sono di sola lettura perché i tipi anonimi vengono considerati come tipi di non entità.  
  
 Le impostazioni <xref:System.Data.Services.Client.MergeOption> di <xref:System.Data.Services.Client.DataServiceContext> vengono usate per la risoluzione di identità durante la proiezione di query.  Pertanto, se un'istanza del tipo `Customer` esiste già in <xref:System.Data.Services.Client.DataServiceContext>, un'istanza di `CustomerAddress` con la stessa identità seguirà le regole di risoluzione di identità specificate da <xref:System.Data.Services.Client.MergeOption>  
  
 Nella tabella seguente vengono descritti i comportamenti durante la proiezione dei risultati di tipi di entità e non entità:  
  
|Azione|Tipo di entità|Tipo di non entità|  
|------------|--------------------|------------------------|  
|Creazione di una nuova istanza proiettata tramite inizializzatori, come nell'esempio seguente:<br /><br /> [!code-csharp[Astoria Northwind Client#ProjectWithInitializer](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#projectwithinitializer)]
 [!code-vb[Astoria Northwind Client#ProjectWithInitializer](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#projectwithinitializer)]|Supportato|Supportato|  
|Creazione di una nuova istanza proiettata tramite costruttori, come nell'esempio seguente:<br /><br /> [!code-csharp[Astoria Northwind Client#ProjectWithConstructor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#projectwithconstructor)]
 [!code-vb[Astoria Northwind Client#ProjectWithConstructor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#projectwithconstructor)]|Viene generato un oggetto <xref:System.NotSupportedException>.|Supportato|  
|Uso di una proiezione per trasformare un valore di proprietà, come nell'esempio seguente:<br /><br /> [!code-csharp[Astoria Northwind Client#ProjectWithTransform](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#projectwithtransform)]
 [!code-vb[Astoria Northwind Client#ProjectWithTransform](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#projectwithtransform)]<br /><br /> Questa trasformazione non è supportata per i tipi di entità perché può generare confusione e la potenziale sovrascrittura dei dati nell'origine dati appartenenti a un'altra entità.|Viene generato un oggetto <xref:System.NotSupportedException>.|Supportato|  
  
<a name="considerations"></a>   
## Considerazioni sulla proiezione  
 Alla definizione di una proiezione di query si applicano le considerazioni aggiuntive seguenti:  
  
-   Quando si definiscono feed personalizzati per il formato Atom, è necessario assicurarsi che tutte le proprietà dell'entità che dispongono di definizioni di mapping personalizzate vengano incluse nella proiezione.  Se una proprietà di entità mappata non è inclusa nella proiezione potrebbe verificarsi una perdita di dati.  Per altre informazioni, vedere [Personalizzazione di feed](../../../../docs/framework/data/wcf/feed-customization-wcf-data-services.md).  
  
-   Quando vengono apportati inserimenti a un tipo proiettato che non contiene tutte le proprietà dell'entità nel modello di dati del servizio dati, le proprietà non incluse nella proiezione vengono impostate sui valori predefiniti nel client.  
  
-   Quando vengono apportati aggiornamenti a un tipo proiettato che non contiene tutte le proprietà dell'entità nel modello di dati del servizio dati, i valori esistenti non inclusi nella proiezione vengono sovrascritti con i valori predefiniti non inizializzati nel client.  
  
-   Quando una proiezione include una proprietà complessa, è necessario che venga restituito l'intero oggetto complesso.  
  
-   Quando una proiezione include una proprietà di navigazione, gli oggetti correlati vengono caricati in modo implicito senza necessità di chiamare il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A>.  Il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> non è supportato in una query proiettata.  
  
-   Le proiezioni di query eseguite nel client vengono convertite per l'uso dell'opzione query `$select` nell'URI della richiesta.  Se una query con proiezione viene eseguita su una versione precedente di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] che non supporta l'opzione query `$select`, viene restituito un errore. Questa situazione può inoltre verificarsi quando <xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A> di <xref:System.Data.Services.DataServiceBehavior> per il servizio dati viene impostato sul valore <xref:System.Data.Services.Common.DataServiceProtocolVersion>.  Per altre informazioni, vedere [Controllo delle versioni del servizio dati](../../../../docs/framework/data/wcf/data-service-versioning-wcf-data-services.md).  
  
 Per altre informazioni, vedere [Procedura: proiettare i risultati delle query](../../../../docs/framework/data/wcf/how-to-project-query-results-wcf-data-services.md).  
  
## Vedere anche  
 [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)