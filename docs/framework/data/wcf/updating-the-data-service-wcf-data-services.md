---
title: "Aggiornamento del servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, modifica di dati"
  - "WCF Data Services, libreria client"
ms.assetid: 00d993be-ffed-4dea-baf7-6eea982cdb54
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Aggiornamento del servizio dati (WCF Data Services)
Quando si usa la libreria client di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per usare un feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)], la libreria traduce le voci del feed in istanze delle classi del servizio dati client.  Queste classi del servizio dati vengono rilevate usando l'elemento <xref:System.Data.Services.Client.DataServiceContext> a cui appartiene <xref:System.Data.Services.Client.DataServiceQuery%601>. Il client rileva le modifiche alle entità segnalate usando i metodi su <xref:System.Data.Services.Client.DataServiceContext>.  Questi metodi consentono al client di rilevare le entità aggiunte ed eliminate, nonché le modifiche apportate ai valori delle proprietà o alle relazioni tra le istanze di entità.  Le modifiche rilevate vengono restituite al servizio dati sotto forma di operazioni basate su REST quando si chiama il metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>.  
  
> [!NOTE]
>  Quando si usa un'istanza di <xref:System.Data.Services.Client.DataServiceCollection%601> per associare i dati ai controlli, le modifiche apportate ai dati nel controllo associato vengono automaticamente segnalate in <xref:System.Data.Services.Client.DataServiceContext>.  Per altre informazioni, vedere [Associazione di dati a controlli](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md).  
  
## Aggiunta e modifica delle entità  
 Quando si usa la finestra di dialogo **Aggiungi riferimento al servizio** in Visual Studio per aggiungere un riferimento a un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)], ogni classe del servizio dati client risultante dispone di un metodo *Create* statico che accetta un parametro per ogni proprietà di entità non nullable.  È possibile usare questo metodo per creare istanze delle classi di tipo entità, come illustrato nell'esempio seguente:  
  
 [!code-csharp[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#createnewproduct)]
 [!code-vb[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#createnewproduct)]  
  
 Per aggiungere un'istanza di entità, chiamare il metodo *AddTo* appropriato sulla classe <xref:System.Data.Services.Client.DataServiceContext> generata mediante la finestra di dialogo **Aggiungi riferimento al servizio**, come illustrato nell'esempio seguente:  
  
 [!code-csharp[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addproductspecific)]
 [!code-vb[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addproductspecific)]  
  
 L'oggetto verrà aggiunto al contesto e inserito nel set di entità corretto.  È inoltre possibile chiamare <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>, ma in questo caso è necessario fornire il nome del set di entità.  Se l'entità aggiunta dispone di una o più relazioni con altre entità, sarà possibile usare il metodo <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> o uno dei metodi precedenti e definire inoltre in modo esplicito tali collegamenti.  Queste operazioni verranno illustrate più avanti in questo argomento.  
  
 Per modificare un'istanza di entità esistente, eseguire innanzitutto una query per tale entità, apportare le modifiche desiderate alle proprietà corrispondenti, quindi chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> sull'oggetto <xref:System.Data.Services.Client.DataServiceContext> per indicare alla libreria client la necessità di inviare un aggiornamento per tale oggetto, come illustrato nell'esempio seguente:  
  
 [!code-csharp[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#modifycustomerspecific)]
 [!code-vb[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#modifycustomerspecific)]  
  
 Per eliminare un'istanza di entità, chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> sull'oggetto <xref:System.Data.Services.Client.DataServiceContext>, come illustrato nell'esempio seguente:  
  
 [!code-csharp[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#deleteproductspecific)]
 [!code-vb[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#deleteproductspecific)]  
  
 Per altre informazioni, vedere [Procedura: aggiungere, modificare ed eliminare entità](../../../../docs/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services.md).  
  
## Collegamento di entità  
 La libreria client consente di salvare gli aggiornamenti apportati a un'entità senza prima eseguire una query per il caricamento dell'entità in <xref:System.Data.Services.Client.DataServiceContext>.  Usare il metodo <xref:System.Data.Services.Client.DataServiceContext.AttachTo%2A> per collegare un oggetto esistente a un set di entità specifico nell'oggetto <xref:System.Data.Services.Client.DataServiceContext>.  Sarà quindi possibile modificare l'oggetto e salvare le modifiche nel servizio dati.  Nell'esempio seguente un oggetto cliente modificato in precedenza viene collegato al contesto e viene quindi chiamato il metodo <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> per contrassegnare l'oggetto collegato come <xref:System.Data.Services.Client.EntityStates> prima della chiamata del metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>:  
  
 [!code-csharp[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#attachobjectspecific)]
 [!code-vb[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#attachobjectspecific)]  
  
 Le considerazioni seguenti riguardano la connessione di oggetti:  
  
-   Un oggetto viene collegato nello stato <xref:System.Data.Services.Client.EntityStates>.  
  
-   Il collegamento di un oggetto non determina il collegamento degli oggetti correlati all'oggetto collegato.  
  
-   Non è possibile collegare un oggetto se l'entità è già in fase di rilevamento da parte del contesto.  
  
-   L'overload del metodo <xref:System.Data.Services.Client.DataServiceContext.AttachTo%28System.String%2CSystem.Object%2CSystem.String%29> che accetta un parametro `etag` viene usato quando si collega un oggetto entità ricevuto insieme a un valore eTag.  Questo valore eTag verrà quindi usato per il controllo della concorrenza durante il salvataggio delle modifiche nell'oggetto collegato.  
  
 Per altre informazioni, vedere [Procedura: collegare un'entità esistente a DataServiceContext](../../../../docs/framework/data/wcf/attach-an-existing-entity-to-dc-wcf-data.md).  
  
## Creazione e modifica dei collegamenti delle relazioni  
 Quando si aggiunge una nuova entità usando il metodo <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> o il metodo *AddTo* appropriato della classe <xref:System.Data.Services.Client.DataServiceContext> generata tramite la finestra di dialogo **Aggiungi riferimento al servizio**, le relazioni tra la nuova entità e le entità correlate non vengono definite automaticamente.  
  
 È possibile creare e modificare le relazioni tra istanze di entità e fare in modo che tali modifiche vengano apportate nel servizio dati mediante la libreria client.  Le relazioni tra entità vengono definite come associazioni nel modello e l'oggetto <xref:System.Data.Services.Client.DataServiceContext> rileva ogni relazione come oggetto collegamento nel contesto.  Per creare, modificare ed eliminare questi collegamenti, in [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] sono disponibili i metodi della classe <xref:System.Data.Services.Client.DataServiceContext> seguenti:  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A>|Crea un nuovo collegamento tra due oggetti entità correlati.  La chiamata a questo metodo equivale alla chiamata al metodo <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> e <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> per creare il nuovo oggetto e definire la relazione a un oggetto esistente.|  
|<xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>|Crea un nuovo collegamento tra due oggetti entità correlati.|  
|<xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>|Aggiorna un collegamento esistente tra due oggetti entità correlati.  <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> viene usato anche per eliminare collegamenti con una cardinalità di zero\-o\-uno\-a\-uno \(`0..1:1`\) e uno\-a\-uno \(`1:1`\).  A tale scopo è possibile impostare l'oggetto correlato su `null`.|  
|<xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A>|Contrassegna un collegamento rilevato dal contesto per l'eliminazione quando viene chiamato il metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>.  Usare questo metodo quando si elimina un oggetto correlato o si modifica una relazione eliminando prima il collegamento all'oggetto esistente e aggiungendo quindi un collegamento al nuovo oggetto correlato.|  
|<xref:System.Data.Services.Client.DataServiceContext.AttachLink%2A>|Notifica al contesto l'esistenza di un collegamento tra due oggetti entità.  Il contesto presuppone che questa relazione esista già nel servizio dati e non effettua alcun tentativo di creare il collegamento durante la chiamata del metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>.  Usare questo metodo quando si collegano oggetti a un contesto e si ha inoltre la necessità di creare il collegamento tra l'oggetto e il contesto.  Se si sta definendo una nuova relazione, è invece necessario usare <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>.|  
|<xref:System.Data.Services.Client.DataServiceContext.DetachLink%2A>|Arresta il rilevamento del collegamento specificato nel contesto.  Questo metodo è usato per eliminare relazioni uno\-a\-molti \(`*:*`\).  Per i collegamenti delle relazioni con una cardinalità di uno, è necessario usare invece <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>.|  
  
 Nell'esempio seguente viene illustrato come usare il metodo <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> per aggiungere un nuovo oggetto `Order_Detail` correlato a un'entità `Orders` esistente.  Dal momento che il nuovo oggetto `Order_Details` viene ora rilevato da <xref:System.Data.Services.Client.DataServiceContext>, la relazione dell'oggetto `Order_Details` aggiunto all'entità `Products` esistente è definita tramite la chiamata al metodo <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>:  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addorderdetailtoorderspecific)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addorderdetailtoorderspecific)]  
  
 Mentre il metodo <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> definisce i collegamenti che devono essere creati nel servizio dati, per fare in modo che questi collegamenti vengano riflessi negli oggetti inclusi nel contesto, è inoltre necessario impostare le proprietà di navigazione sugli oggetti stessi.  Nell'esempio precedente le proprietà di navigazione devono essere impostate nel modo seguente:  
  
 [!code-csharp[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#setnavprops)]
 [!code-vb[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#setnavprops)]  
  
 Per altre informazioni, vedere [Procedura: definire relazioni tra entità](../../../../docs/framework/data/wcf/how-to-define-entity-relationships-wcf-data-services.md).  
  
## Salvataggio delle modifiche  
 Le modifiche vengono rilevate nell'istanza di <xref:System.Data.Services.Client.DataServiceContext>, ma non vengono inviate immediatamente al server.  Dopo aver apportato le modifiche necessarie per un'attività specificata, chiamare <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> per inviare tutte le modifiche al servizio dati.  Per altre informazioni, vedere [Gestione del contesto del servizio dati](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md).  È inoltre possibile salvare le modifiche in modo asincrono usando i metodi <xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A> e <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A>.  Per altre informazioni, vedere [Operazioni asincrone](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md).  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)   
 [Operazioni asincrone](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)   
 [Invio in batch di operazioni](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)   
 [Materializzazione di oggetti](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)   
 [Gestione del contesto del servizio dati](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)