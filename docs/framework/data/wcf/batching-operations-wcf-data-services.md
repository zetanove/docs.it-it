---
title: "Invio in batch di operazioni (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, libreria client"
ms.assetid: 962a49d1-cc11-4b96-bc7d-071dd6607d6c
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Invio in batch di operazioni (WCF Data Services)
[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] supporta l'elaborazione batch di richieste a un servizio basato su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Per altre informazioni, vedere [OData: Elaborazione batch](http://go.microsoft.com/fwlink/?LinkId=186075). In [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] ogni operazione che usa <xref:System.Data.Services.Client.DataServiceContext>, ad esempio l'esecuzione di una query o il salvataggio di modifiche, determina l'invio di una richiesta separata al servizio dati.  Per mantenere un ambito logico per i set di operazioni, è possibile definire in modo esplicito batch operativi.  In questo modo si ha la certezza che tutte le operazioni nel batch vengano inviate al servizio dati in una sola richiesta HTTP, consentendo al server di elaborare in modo unitario le operazioni e di ridurre il numero di round trip al servizio dati.  
  
## Invio in batch di operazioni di query  
 Per eseguire più query in un unico batch, è necessario creare ogni query del batch come istanza separata della classe <xref:System.Data.Services.Client.DataServiceRequest%601>.  Quando si crea una richiesta di query in questo modo, la query stessa viene definita come URI a cui vengono applicate le regole per l'indirizzamento di risorse.  Per altre informazioni, vedere [Accesso alle risorse del servizio dati](../../../../docs/framework/data/wcf/accessing-data-service-resources-wcf-data-services.md).  Le richieste di query in batch vengono inviate al servizio dati quando viene chiamato il metodo <xref:System.Data.Services.Client.DataServiceContext.ExecuteBatch%2A> contenente gli oggetti della richiesta di query.  Questo metodo restituisce un oggetto <xref:System.Data.Services.Client.DataServiceResponse> corrispondente a una raccolta di oggetti <xref:System.Data.Services.Client.QueryOperationResponse%601> che rappresentano risposte a singole query incluse nel batch, ognuna delle quali contiene una raccolta di oggetti restituiti dalla query o informazioni sull'errore.  Quando una singola operazione di query inclusa nel batch ha esito negativo, le informazioni sull'errore vengono restituite nell'oggetto <xref:System.Data.Services.Client.QueryOperationResponse%601> per l'operazione non riuscita e le operazioni rimanenti vengono comunque eseguite.  Per altre informazioni, vedere [Procedura: eseguire query in un batch](../../../../docs/framework/data/wcf/how-to-execute-queries-in-a-batch-wcf-data-services.md).  
  
 Le query in batch possono inoltre essere eseguite in modo asincrono.  Per altre informazioni, vedere [Operazioni asincrone](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md).  
  
## Invio in batch dell'operazione SaveChanges  
 Quando si chiama il metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>, tutte le modifiche rilevate dal contesto vengono tradotte in operazioni basate su REST che vengono inviate al servizio come richieste al servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Per impostazione predefinita, queste modifiche non vengono inviate in un unico messaggio di richiesta.  Per fare in modo che tutte le modifiche vengano inviate in un'unica richiesta, è necessario chiamare il metodo <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%28System.Data.Services.Client.SaveChangesOptions%29> e includere il valore <xref:System.Data.Services.Client.SaveChangesOptions> nell'enumerazione <xref:System.Data.Services.Client.SaveChangesOptions> fornita al metodo.  
  
 È inoltre possibile salvare modifiche in batch in modo asincrono.  Per altre informazioni, vedere [Operazioni asincrone](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md).  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)