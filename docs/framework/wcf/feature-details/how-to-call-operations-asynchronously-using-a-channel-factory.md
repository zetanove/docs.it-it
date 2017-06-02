---
title: "Procedura: chiamare le operazioni in modo asincrono tramite una channel factory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cc17dd47-b9ad-451c-a362-e36e0aac7ba0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Procedura: chiamare le operazioni in modo asincrono tramite una channel factory
In questo argomento viene illustrato in che modo un client può accedere a un'operazione del servizio in modalità asincrona quando si usa un'applicazione client basata su <xref:System.ServiceModel.ChannelFactory%601>.  Quando si usa un oggetto <xref:System.ServiceModel.ClientBase%601?displayProperty=fullName> per richiamare un servizio, è possibile usare il modello di chiamata asincrono basato su eventi.  Per altre informazioni, vedere [Procedura: chiamare operazioni del servizio in modo asincrono](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md).  Per altre informazioni sul modello di chiamata asincrono basato su eventi, vedere [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)  
  
 Il servizio in questo argomento implementa l'interfaccia `ICalculator`.  Il client può chiamare in modo asincrono le operazioni su tale interfaccia, il che significa che le operazioni come `Add` vengono suddivise in due metodi, `BeginAdd` ed `EndAdd`, il primo dei quali avvia la chiamata e il secondo recupera il risultato al termine dell'operazione.  Per un esempio che illustra come implementare in modo asincrono un'operazione in un servizio, vedere [Procedura: implementare un'operazione del servizio asincrona](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md).  Per informazioni dettagliate sulle operazioni sincrone e asincrone, vedere [Operazioni sincrone e asincrone](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).  
  
## Procedura  
  
#### Per chiamare operazioni del servizio WCF in modo asincrono  
  
1.  Eseguire lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) con l'opzione `/async` come illustrato nel comando seguente.  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a  
  
    ```  
  
     Questo genera una versione client asincrona del contratto di servizio per l'operazione.  
  
2.  Creare una funzione di callback da chiamare al temine dell'operazione asincrona, come illustrato nel codice di esempio seguente.  
  
     [!code-csharp[C_How_To_CF_Async#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#2)]
     [!code-vb[C_How_To_CF_Async#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#2)]  
  
3.  Per accedere in modo asincrono a un'operazione del servizio, creare il client, chiamare `Begin[Operation]` \(ad esempio, `BeginAdd`\) e specificare una funzione di callback, come illustrato nel codice di esempio seguente.  
  
     [!code-csharp[C_How_To_CF_Async#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#3)]
     [!code-vb[C_How_To_CF_Async#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#3)]  
  
     Quando la funzione di callback viene eseguita, il client chiama `End<operation>``EndAdd` \(ad esempio, \) per recuperare il risultato.  
  
## Esempio  
 Il servizio usato con il codice client della procedura precedente implementa l'interfaccia `ICalculator` come illustrato nel codice seguente.  Sul lato del servizio, le operazioni `Add` e `Subtract` del contratto vengono richiamate in modo sincrono dal runtime [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], anche se i passaggi client precedenti vengono richiamati in modo asincrono sul client.  Le operazioni `Multiply` e `Divide` vengono usate per richiamare il servizio in modo asincrono sul lato del servizio, anche se il client le richiama in modo sincrono.  In questo esempio la proprietà <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> viene impostata su `true`.  Tale impostazione della proprietà, in combinazione con l'implementazione del modello asincrono di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], consente al runtime di richiamare in modo asincrono l'operazione.  
  
 [!code-csharp[C_How_To_CF_Async#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/service.cs#4)]
 [!code-vb[C_How_To_CF_Async#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/service.vb#4)]  
  
## Vedere anche  
 [Service Contract: Asynchronous Sample](http://msdn.microsoft.com/it-it/833db946-f511-4f64-a26f-2759a11217c7)