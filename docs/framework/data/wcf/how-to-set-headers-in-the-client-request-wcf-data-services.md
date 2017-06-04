---
title: "Procedura: impostare le intestazioni nella richiesta del client (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, personalizzazione delle richieste"
ms.assetid: 3d55168d-5901-4f48-8117-6c93da3ab5ae
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: impostare le intestazioni nella richiesta del client (WCF Data Services)
Quando si usa libreria client di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per accedere a un servizio dati che supporta [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)], la libreria client imposta automaticamente le intestazioni HTTP richieste nei messaggi di richiesta inviati al servizio dati.  Tuttavia, tramite la libreria client non vengono impostate le intestazioni del messaggio richieste in determinati casi, ad esempio quando il servizio dati richiede l'autenticazione basata sulle attestazioni o i cookie.  Per altre informazioni, vedere [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md#clientAuthentication).  In questi casi, è necessario impostare manualmente le intestazioni nel messaggio di richiesta prima che venga inviato.  L'esempio in questo argomento illustra come gestire l'evento <xref:System.Data.Services.Client.DataServiceContext.SendingRequest> per aggiungere una nuova intestazione al messaggio di richiesta prima che venga inviato al servizio dati.  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  È anche possibile usare il [servizio dati di esempio di Northwind](http://go.microsoft.com/fwlink/?LinkId=187426) pubblicato sul sito Web [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]. Questo servizio dati di esempio è di sola lettura e viene restituito un errore se si tenta di salvare le modifiche.  I servizi dati di esempio del sito Web [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] permettono l'autenticazione anonima.  
  
## Esempio  
 Nell'esempio seguente viene registrato un gestore per l'evento <xref:System.Data.Services.Client.DataServiceContext.SendingRequest>, quindi viene eseguita una query sul servizio dati.  
  
> [!NOTE]
>  Quando un servizio dati richiede che l'intestazione del messaggio venga impostata manualmente per ogni richiesta, considerare registrare il gestore per l'evento <xref:System.Data.Services.Client.DataServiceContext.SendingRequest> eseguendo l'override del metodo parziale `OnContextCreated` nel contenitore di entità che rappresenta il servizio dati che in questo caso è `NorthwindEntities`.  
  
 [!code-csharp[Astoria Northwind Client#RegisterHeadersQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#registerheadersquery)]
 [!code-vb[Astoria Northwind Client#RegisterHeadersQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#registerheadersquery)]  
  
## Esempio  
 Nel metodo seguente viene gestito l'evento <xref:System.Data.Services.Client.DataServiceContext.SendingRequest> e viene aggiunta un'intestazione di autenticazione alla richiesta.  
  
 [!code-csharp[Astoria Northwind Client#OnSendingRequest](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#onsendingrequest)]
 [!code-vb[Astoria Northwind Client#OnSendingRequest](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#onsendingrequest)]  
  
## Vedere anche  
 [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)   
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)