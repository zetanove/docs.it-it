---
title: "Procedura: chiamare operazioni del servizio WCF in modo asincrono | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0face17f-43ca-417b-9b33-737c0fc360df
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Procedura: chiamare operazioni del servizio WCF in modo asincrono
In questo argomento viene illustrato come un client può accedere a un'operazione del servizio in modo asincrono.Il servizio in questo argomento implementa l'interfaccia `ICalculator`.Il client può chiamare le operazioni in questa interfaccia in modo asincrono utilizzando il modello di chiamata asincrono basato su eventi.Per ulteriori informazioni sul modello di chiamata asincrono basato su eventi, vedere la pagina relativa alla [programmazione multithreading con il modello asincrono basato su eventi](http://go.microsoft.com/fwlink/?LinkId=248184)\).Per un esempio che illustra come implementare in modo asincrono un'operazione in un servizio, vedere [Procedura: implementare un'operazione del servizio asincrona](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md).Per ulteriori informazioni sulle operazioni sincrone e asincrone, vedere [Operazioni sincrone e asincrone](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).  
  
> [!NOTE]
>  Il modello di chiamata asincrono basato su eventi non è supportato quando si utilizza una classe <xref:System.ServiceModel.ChannelFactory%601>.Per ulteriori informazioni sulle chiamate asincrone utilizzando la classe <xref:System.ServiceModel.ChannelFactory%601>, vedere [Procedura: chiamare le operazioni in modo asincrono tramite una channel factory](../../../../docs/framework/wcf/feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md).  
  
## Procedura  
  
#### Per chiamare operazioni del servizio WCF in modo asincrono  
  
1.  Eseguire lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) con entrambe le opzioni di comando `/async` e `/tcv:Version35` come illustrato nel comando seguente.  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a /tcv:Version35  
    ```  
  
     Questa operazione genera, oltre alle operazioni sincrone e a quelle asincrone standard basate su delega, una classe client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]contenente:  
  
    -   Due operazioni \<`operationName`\>`Async` da utilizzare con l’approccio di chiamata asincrono basato su eventi.Ad esempio:  
  
         [!code-csharp[EventAsync#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#1)]
         [!code-vb[EventAsync#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#1)]  
  
    -   Eventi completati dall'operazione del modulo \<`operationName`\>`Completed` da utilizzare con l’approccio di chiamata asincrono basato su eventi.Ad esempio:  
  
         [!code-csharp[EventAsync#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#2)]
         [!code-vb[EventAsync#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#2)]  
  
    -   Tipi <xref:System.EventArgs?displayProperty=fullName> per ciascuna operazione \(del modulo \<`operationName`\>`CompletedEventArgs`\) da utilizzare con l’approccio di chiamata asincrono basato su eventi.Ad esempio:  
  
         [!code-csharp[EventAsync#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#3)]
         [!code-vb[EventAsync#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#3)]  
  
2.  Nell'applicazione chiamante creare un metodo di callback da chiamare al temine dell'operazione asincrona, come illustrato nel codice di esempio seguente.  
  
     [!code-csharp[EventAsync#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#4)]
     [!code-vb[EventAsync#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#4)]  
  
3.  Prima di chiamare l'operazione utilizzare un nuovo metodo <xref:System.EventHandler%601?displayProperty=fullName> generico di tipo \<`operationName`\>`EventArgs` per aggiungere il metodo del gestore eventi \(creato nel passaggio precedente\) all'evento \<`operationName`\>`Completed`.Quindi chiamare il metodo \<`operationName`\>`Async`.Ad esempio:  
  
     [!code-csharp[EventAsync#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#5)]
     [!code-vb[EventAsync#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#5)]  
  
## Esempio  
  
> [!NOTE]
>  Le linee guida di progettazione per il modello asincrono basato su eventi indicano che, se vengono restituiti più valori, un valore viene restituito come proprietà `Result` e i restanti valori sono restituiti come proprietà nell’oggetto  <xref:System.EventArgs>.Di conseguenza, è possibile che, se un client importa metadati utilizzando le opzioni di comando asincrone basate su eventi e l'operazione restituisce più valori, l'oggetto predefinito <xref:System.EventArgs> restituisce un valore come proprietà `Result` e i restanti valori come proprietà dell’oggetto <xref:System.EventArgs>. Se si desidera ricevere l’oggetto del messaggio come proprietà `Result` e i valori restituiti come proprietà in quell’oggetto, utilizzare l’opzione di comando `/messageContract`.Questa operazione genera una firma che restituisce il messaggio di risposta come proprietà `Result` nell’oggetto <xref:System.EventArgs>.Pertanto, tutti i valori restituiti interni sono proprietà dell’oggetto del messaggio di risposta.  
  
 [!code-csharp[EventAsync#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#6)]
 [!code-vb[EventAsync#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#6)]  
  
## Vedere anche  
 [Procedura: implementare un'operazione del servizio asincrona](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)