---
title: "Procedura: creare un servizio HTTP Web WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 877662d3-d372-4e08-b417-51f66a0095cd
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Procedura: creare un servizio HTTP Web WCF
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente di creare un servizio che espone un endpoint Web.Gli endpoint Web inviano dati in XML o JSON, senza SOAP envelope.In questo argomento viene dimostrato come esporre un endpoint di questo tipo.  
  
> [!NOTE]
>  L'unico modo per proteggere un endpoint Web è esporlo tramite HTTPS utilizzando la sicurezza del trasporto.Quando si utilizza la sicurezza basata sul messaggio, le informazioni sulla sicurezza vengono inserite generalmente nelle intestazioni SOAP e poiché i messaggi inviati a endpoint non SOAP non contengono SOAP envelope, non esiste altra posizione in cui inserire le informazioni sulla sicurezza ed è necessario affidarsi alla sicurezza del trasporto.  
  
### Per creare un endpoint Web  
  
1.  Definire un contratto di servizio utilizzando un'interfaccia contrassegnata con gli attributi <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.Web.WebInvokeAttribute> e <xref:System.ServiceModel.Web.WebGetAttribute>.  
  
     [!code-csharp[htBasicService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#0)]
     [!code-vb[htBasicService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#0)]  
  
    > [!NOTE]
    >  Per impostazione predefinita, <xref:System.ServiceModel.Web.WebInvokeAttribute> esegue il mapping delle chiamate POST all'operazione.È possibile tuttavia definire il metodo HTTP, ad esempio HEAD, PUT o DELETE, per eseguire il mapping all'operazione specificando un parametro "method\=".<xref:System.ServiceModel.Web.WebGetAttribute> non dispone di un parametro "method\=" ed esegue solo il mapping delle chiamate GET all'operazione del servizio.  
  
2.  Implementare il contratto di servizio.  
  
     [!code-csharp[htBasicService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#1)]
     [!code-vb[htBasicService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#1)]  
  
### Per ospitare il servizio  
  
1.  Creare un oggetto <xref:System.ServiceModel.Web.WebServiceHost>.  
  
     [!code-csharp[htBasicService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#2)]
     [!code-vb[htBasicService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#2)]  
  
2.  Aggiungere un <xref:System.ServiceModel.Description.ServiceEndpoint> con <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
     [!code-csharp[htBasicService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#3)]
     [!code-vb[htBasicService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#3)]  
  
    > [!NOTE]
    >  Se non viene aggiunto un endpoint, l'oggetto <xref:System.ServiceModel.Web.WebServiceHost> ne crea automaticamente uno predefinito.L'oggetto <xref:System.ServiceModel.Web.WebServiceHost> aggiunge anche l'oggetto <xref:System.ServiceModel.Description.WebHttpBehavior> e disabilita la pagina della Guida HTTP e la funzionalità WSDL \(Web Services Description Language\) GET in modo che l'endpoint dei metadati non interferisca con l'endpoint HTTP predefinito.  
    >   
    >  L'aggiunta di un endpoint non SOAP con un URL "" provoca un comportamento imprevisto quando si tenta di chiamare un'operazione sull'endpoint.La ragione è che l'URI di ascolto dell'endpoint è lo stesso URI della pagina della Guida \(la pagina visualizzata quando si esplora all'indirizzo di base di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\).  
  
     Per evitare che ciò accada è possibile svolgere una delle azioni seguenti:  
  
    -   Specificare sempre un URI non vuoto per un endpoint non SOAP.  
  
    -   Disattivare la pagina della Guida.Per questa operazione utilizzare il codice seguente:  
  
     [!code-csharp[htBasicService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#4)]
     [!code-vb[htBasicService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#4)]  
  
3.  Aprire l'host del servizio e attendere finché l'utente non preme INVIO.  
  
     [!code-csharp[htBasicService#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#5)]
     [!code-vb[htBasicService#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#5)]  
  
     In questo esempio viene dimostrato come ospitare un servizio Web con un'applicazione console.È anche possibile ospitare tale servizio all'interno di IIS.A questo scopo, specificare la classe <xref:System.ServiceModel.Activation.WebServiceHostFactory> in un file con estensione svc come è dimostrato nel codice seguente.  
  
    ```  
    <%ServiceHost   
        language=c#  
        Debug="true"  
        Service="Microsoft.Samples.Service"  
        Factory=System.ServiceModel.Activation.WebServiceHostFactory%>  
    ```  
  
### Per chiamare operazioni del servizio mappate a GET in Internet Explorer  
  
1.  Aprire Internet Explorer e digitare "`http://localhost:8000/EchoWithGet?s=Hello, world!`" e premere INVIO.L'URL contiene l'indirizzo di base del servizio \("http:\/\/localhost:8000\/"\), l'indirizzo relativo dell'endpoint \(""\) l'operazione del servizio da chiamare \("EchoWithGet"\) e un punto interrogativo seguito da un elenco di parametri denominati separati mediante una e commerciale \(&\).  
  
### Per chiamare operazioni del servizio nel codice  
  
1.  Creare un'istanza di <xref:System.ServiceModel.Web.WebChannelFactory> all'interno di un blocco `using`.  
  
     [!code-csharp[htBasicService#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#6)]
     [!code-vb[htBasicService#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#6)]  
  
2.  Aggiungere <xref:System.ServiceModel.Description.WebHttpBehavior> all'endpoint che viene chiamato da <xref:System.ServiceModel.ChannelFactory>.  
  
     [!code-csharp[htBasicService#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#7)]
     [!code-vb[htBasicService#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#7)]  
  
3.  Creare il canale e chiamare il servizio.  
  
     [!code-csharp[htBasicService#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#8)]
     [!code-vb[htBasicService#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#8)]  
  
4.  Chiudere la classe <xref:System.ServiceModel.Web.WebServiceHost>.  
  
     [!code-csharp[htBasicService#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#9)]
     [!code-vb[htBasicService#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#9)]  
  
## Esempio  
 Di seguito è riportato il codice completo per questo esempio.  
  
 [!code-csharp[htBasicService#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#10)]
 [!code-vb[htBasicService#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#10)]  
  
## Compilazione del codice  
 Durante la compilazione di Service.cs fare riferimento a System.ServiceModel.dll e System.ServiceModel.Web.dll.  
  
## Vedere anche  
 <xref:System.ServiceModel.WebHttpBinding>   
 <xref:System.ServiceModel.Web.WebGetAttribute>   
 <xref:System.ServiceModel.Web.WebInvokeAttribute>   
 <xref:System.ServiceModel.Web.WebServiceHost>   
 <xref:System.ServiceModel.Web.WebChannelFactory>   
 <xref:System.ServiceModel.Description.WebHttpBehavior>   
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)