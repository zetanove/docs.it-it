---
title: "Procedura: esporre un contratto a client SOAP e Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bb765a48-12f2-430d-a54d-6f0c20f2a23a
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Procedura: esporre un contratto a client SOAP e Web
Per impostazione predefinita, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] rende disponibili endpoint solo ai client SOAP.  In [Procedura: creare un servizio HTTP Web WCF](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md) viene reso disponibile un endpoint a client non SOAP.  Possono verificarsi casi in cui si desidera rendere lo stesso contratto disponibile in entrambi i modi, come endpoint Web e come endpoint SOAP.  In questo argomento viene illustrato un esempio di come ottenere tale risultato.  
  
### Per definire il contratto di servizio  
  
1.  Definire un contratto di servizio usando un'interfaccia contrassegnata con gli attributi <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.Web.WebInvokeAttribute> e <xref:System.ServiceModel.Web.WebGetAttribute>, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#0)]
     [!code-vb[htSoapWeb#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#0)]  
  
    > [!NOTE]
    >  Per impostazione predefinita, <xref:System.ServiceModel.Web.WebInvokeAttribute> esegue il mapping delle chiamate POST all'operazione.  Tuttavia, è possibile definire il metodo di mapping all'operazione specificando un parametro "method\=".  <xref:System.ServiceModel.Web.WebGetAttribute> non dispone di un parametro "method\=" ed esegue solo il mapping delle chiamate GET all'operazione del servizio.  
  
2.  Implementare il contratto di servizio, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#1)]
     [!code-vb[htSoapWeb#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#1)]  
  
### Per ospitare il servizio  
  
1.  Creare un oggetto <xref:System.ServiceModel.ServiceHost>, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#2)]
     [!code-vb[htSoapWeb#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#2)]  
  
2.  Aggiungere una classe <xref:System.ServiceModel.Description.ServiceEndpoint> con <xref:System.ServiceModel.BasicHttpBinding> per l'endpoint SOAP, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#3)]
     [!code-vb[htSoapWeb#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#3)]  
  
3.  Aggiungere una classe <xref:System.ServiceModel.Description.ServiceEndpoint> con <xref:System.ServiceModel.WebHttpBinding> per l'endpoint non SOAP e aggiungere <xref:System.ServiceModel.Description.WebHttpBehavior> all'endpoint, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#4)]
     [!code-vb[htSoapWeb#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#4)]  
  
4.  Chiamare `Open()` su un'istanza di <xref:System.ServiceModel.ServiceHost>per aprire l'host del servizio, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#5)]
     [!code-vb[htSoapWeb#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#5)]  
  
### Per chiamare operazioni del servizio mappate a GET in Internet Explorer  
  
1.  Aprire Internet Explorer e digitare "`http://localhost:8000/Web/EchoWithGet?s=Hello, world!`", quindi premere INVIO.  L'URL contiene l'indirizzo di base del servizio \("http:\/\/localhost:8000\/"\), l'indirizzo relativo dell'endpoint \(""\), l'operazione del servizio da chiamare \("EchoWithGet"\) e un punto interrogativo seguito da un elenco di parametri denominati separati da una e commerciale \(&\).  
  
### Per chiamare operazioni del servizio sull'endpoint Web nel codice  
  
1.  Creare un'istanza di <xref:System.ServiceModel.Web.WebChannelFactory%601> all'interno di un blocco `using`, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#6)]
     [!code-vb[htSoapWeb#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#6)]  
  
> [!NOTE]
>  `Close()` viene automaticamente chiamato sul canale alla fine del blocco `using`.  
  
1.  Creare il canale e chiamare il servizio, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#8)]
     [!code-vb[htSoapWeb#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#8)]  
  
### Per chiamare operazioni del servizio sull'endpoint SOAP  
  
1.  Creare un'istanza di <xref:System.ServiceModel.ChannelFactory> all'interno di un blocco `using`, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#10)]
     [!code-vb[htSoapWeb#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#10)]  
  
2.  Creare il canale e chiamare il servizio, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#11)]
     [!code-vb[htSoapWeb#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#11)]  
  
### Per chiudere l'host del servizio  
  
1.  Chiudere l'host del servizio, come mostrato nel codice seguente.  
  
     [!code-csharp[htSoapWeb#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#9)]
     [!code-vb[htSoapWeb#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#9)]  
  
## Esempio  
 Di seguito è riportato il codice completo per questo argomento.  
  
 [!code-csharp[htSoapWeb#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#13)]
 [!code-vb[htSoapWeb#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#13)]  
  
## Compilazione del codice  
 Durante la compilazione di Service.cs fare riferimento a System.ServiceModel.dll e System.ServiceModel.Web.dll.  
  
## Vedere anche  
 <xref:System.ServiceModel.WebHttpBinding>   
 <xref:System.ServiceModel.Web.WebGetAttribute>   
 <xref:System.ServiceModel.Web.WebInvokeAttribute>   
 <xref:System.ServiceModel.Web.WebServiceHost>   
 <xref:System.ServiceModel.ChannelFactory>   
 <xref:System.ServiceModel.Description.WebHttpBehavior>   
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)