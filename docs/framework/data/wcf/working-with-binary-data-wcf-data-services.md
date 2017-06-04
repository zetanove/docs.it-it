---
title: "Utilizzo di dati binari (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, dati binari"
  - "WCF Data Services, flussi"
ms.assetid: aeccc45c-d5c5-4671-ad63-a492ac8043ac
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Utilizzo di dati binari (WCF Data Services)
La libreria client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente di recuperare e aggiornare i dati binari da un feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] in una delle modalità seguenti:  
  
-   Come proprietà di tipo primitivo di un'entità.  Si tratta del metodo consigliato per l'uso di oggetti dati binari di dimensioni ridotte che possono essere caricati facilmente in memoria.  In questo caso, la proprietà binaria è una proprietà dell'entità esposta dal modello di dati e il servizio dati serializza i dati binari come codice XML binario in base 64 nel messaggio di risposta.  
  
-   Come flusso separato di risorse binarie.  Si tratta del metodo consigliato per l'accesso e la modifica di dati di oggetti binari di grandi dimensioni \(BLOB\) che possono rappresentare una foto, un video o qualsiasi altro tipo di dati codificati binari.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] implementa il flusso di dati binari tramite HTTP come definito in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  In questo meccanismo i dati binari vengono trattati come una risorsa multimediale separata ma correlata a un'entità denominata entry di collegamento multimediale \(Media Link Entry\).  Per altre informazioni, vedere [Provider di flusso](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md).  
  
> [!TIP]
>  Per un esempio dettagliato di come creare un'applicazione client [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] che scarica file di immagine binari da un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] che archivia foto, vedere l'argomento [Serie provider di flusso di servizi dati: accesso a un flusso di risorsa multimediale dal client \(parte 2\)](http://go.microsoft.com/fwlink/?LinkId=201637).  Per scaricare il codice di esempio per il servizio dati di foto di flusso rappresentato nel post di blog, vedere [Esempio di servizio dati di foto di flusso](http://go.microsoft.com/fwlink/?LinkId=198988) in MSDN Code Gallery.  
  
## Metadati dell'entità  
 Un'entità che dispone di un flusso di risorsa multimediale correlato viene indicata nei metadati del servizio dati dall'attributo `HasStream` applicato a un tipo di entità che è la voce di collegamento multimediale.  Nell'esempio seguente, l'entità `PhotoInfo`è una voce di collegamento multimediale che dispone di una risorsa multimediale correlata, indicata dall'attributo `HasStream`.  
  
 [!code-xml[Astoria Photo Streaming Service#HasStream](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria photo streaming service/xml/photodata.edmx#hasstream)]  
  
 Negli esempi restanti di questo argomento viene illustrato come accedere e modificare il flusso di risorsa multimediale.  Per un esempio completo su come usare un flusso di risorsa multimediale in un'applicazione client .NET Framework tramite la libreria client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] vedere l'argomento [Accesso al flusso di risorsa multimediale dal client](http://go.microsoft.com/fwlink/?LinkID=201637).  
  
## Accesso al flusso di risorsa binaria  
 La libreria client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] fornisce i metodi per l'accesso ai flussi di risorse binarie da un servizio dati basato su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Quando si scarica una risorsa multimediale, è possibile usare l'URI della risorsa multimediale od ottenere un flusso binario contenente i dati della risorsa multimediale.  È possibile caricare i dati della risorsa multimediale anche come un flusso binario.  
  
> [!TIP]
>  Per un esempio dettagliato di come creare un'applicazione client [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] che scarica file di immagine binari da un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] che archivia foto, vedere l'argomento [Serie provider di flusso di servizi dati: accesso a un flusso di risorsa multimediale dal client \(parte 2\)](http://go.microsoft.com/fwlink/?LinkId=201637).  Per scaricare il codice di esempio per il servizio dati di foto di flusso rappresentato nel post di blog, vedere [Esempio di servizio dati di foto di flusso](http://go.microsoft.com/fwlink/?LinkId=198988) in MSDN Code Gallery.  
  
### Recupero dell'URI del flusso binario  
 Quando si recuperano determinati tipi di risorse multimediali, ad esempio immagini e altri file multimediali, è spesso più semplice usare l'URI della risorsa multimediale nell'applicazione anziché gestire il flusso di dati binari.  Per ottenere l'URI di un flusso di risorsa associato a una data voce di collegamento multimediale, è necessario chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.GetReadStreamUri%2A> sull'istanza <xref:System.Data.Services.Client.DataServiceContext> che tiene traccia dell'entità.  Nell'esempio seguente viene mostrato come chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.GetReadStreamUri%2A> per ottenere l'URI di un flusso di risorsa multimediale usato per creare una nuova immagine nel client:  
  
 [!code-csharp[Astoria Photo Streaming Client#GetReadStreamUri](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria photo streaming client/cs/photowindow.xaml.cs#getreadstreamuri)]
 [!code-vb[Astoria Photo Streaming Client#GetReadStreamUri](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria photo streaming client/vb/photowindow.xaml.vb#getreadstreamuri)]  
  
### Download del flusso di risorsa binaria  
 Quando si recupera un flusso di risorsa binaria, è necessario chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> sull'istanza di <xref:System.Data.Services.Client.DataServiceContext> che tiene traccia della voce di collegamento multimediale.  Questo metodo invia una richiesta al servizio dati che restituisce un oggetto <xref:System.Data.Services.Client.DataServiceStreamResponse> che presenta un riferimento al flusso contenente la risorsa.  Usare questo metodo quando l'applicazione richiede la risorsa binaria come <xref:System.IO.Stream>.  Nell'esempio seguente viene mostrato come chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> per recuperare un flusso usato per creare una nuova immagine nel client:  
  
 [!code-csharp[Astoria Streaming Client#GetReadStreamClient](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria streaming client/cs/customerphotowindow.xaml.cs#getreadstreamclient)]
 [!code-vb[Astoria Streaming Client#GetReadStreamClient](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria streaming client/vb/customerphotowindow.xaml.vb#getreadstreamclient)]  
  
> [!NOTE]
>  L'intestazione Content\-Length nel messaggio di risposta che contiene il flusso binario non è impostata dal servizio dati.  È possibile che questo valore non rifletta la lunghezza effettiva del flusso di dati binari.  
  
### Caricamento di una risorsa multimediale come flusso  
 Per inserire o aggiornare una risorsa multimediale, chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> sull'istanza <xref:System.Data.Services.Client.DataServiceContext> che tiene traccia dell'entità.  Questo metodo invia una richiesta al servizio dati che contiene la risorsa multimediale letta dal flusso fornito.  Nell'esempio seguente viene indicato come chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> per inviare un'immagine al servizio dati:  
  
 [!code-csharp[Astoria Photo Streaming Client#SetSaveStream](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria photo streaming client/cs/photodetailswindow.xaml.cs#setsavestream)]
 [!code-vb[Astoria Photo Streaming Client#SetSaveStream](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria photo streaming client/vb/photodetailswindow.xaml.vb#setsavestream)]  
  
 In questo esempio il metodo <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> viene chiamato fornendo un valore `true` per il parametro `closeStream`.  Ciò garantisce che <xref:System.Data.Services.Client.DataServiceContext> chiuda il flusso dopo aver caricato i dati binari nel servizio dati.  
  
> [!NOTE]
>  Quando si chiama <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A>, il flusso non viene inviato al servizio dati fino a quando non viene chiamato il metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>.  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [Associazione di dati a controlli](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)