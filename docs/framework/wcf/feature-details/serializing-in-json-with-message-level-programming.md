---
title: "Serializzazione in Json con la programmazione a livello di messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5f940ba2-57ee-4c49-a779-957c5e7e71fa
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Serializzazione in Json con la programmazione a livello di messaggi
WCF supporta la serializzazione dei dati in formato JSON.In questo argomento viene descritto come comunicare a WCF di serializzare i tipi utilizzando l'oggetto <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.  
  
## Programmazione di messaggi tipizzati  
 L'oggetto <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> viene utilizzato quando l'oggetto <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> viene applicato a un'operazione del servizio.Entrambi gli attributi consentono di specificare `RequestFormat` e `ResponseFormat`.Per utilizzare JSON per le richieste e le risposte, impostarle entrambe su `WebMessageFormat.Json`.Per utilizzare JSON, è necessario utilizzare l'oggetto <xref:System.ServiceModel.WebHttpBinding> che configura automaticamente l'oggetto <xref:System.ServiceModel.Description.WebHttpBehavior>.Per ulteriori informazioni sulla serializzazione in WCF, vedere: [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md) e la pagina relativa alla [serializzazione in Windows Communication Foundation](http://msdn.microsoft.com/magazine/cc163569.aspx).Per ulteriori informazioni su JSON e WCF, vedere le pagine relative a un'[introduzione ai servizi RESTfull con WCF](http://msdn.microsoft.com/magazine/dd315413.aspx), alla [creazione di servizi WCF compatibili con JSON in .NET 3.5](http://www.pluralsight-training.net/community/blogs/fritz/archive/2008/01/31/50121.aspx) e alla [panoramica su REST in WCF](http://msdn.microsoft.com/netframework/dd547388).  
  
> [!IMPORTANT]
>  L'utilizzo di JSON richiede l'utilizzo degli oggetti <xref:System.ServiceModel.WebHttpBinding> e <xref:System.ServiceModel.Description.WebHttpBehavior> che non supportano la comunicazione SOAP.I servizi che comunicano con l'oggetto <xref:System.ServiceModel.WebHttpBinding> non supportano l'esposizione dei metadati del servizio, pertanto non sarà possibile utilizzare la funzionalità Aggiungi riferimento al servizio di Visual Studio o lo strumento della riga di comando svcutil per generare un proxy sul lato client.Per ulteriori informazioni su come chiamare a livello di codice i servizi che utilizzano l'oggetto <xref:System.ServiceModel.WebHttpBinding>, vedere la pagina relativa alla modalità di [utilizzo dei servizi REST con WCF](http://blogs.msdn.com/b/pedram/archive/2008/04/21/how-to-consume-rest-services-with-wcf.aspx).  
  
## Programmazione di messaggi non tipizzati  
 Quando si utilizzano direttamente oggetti Message non tipizzati, è necessario impostare in modo esplicito le proprietà nel messaggio non tipizzato per serializzarlo come JSON.Nel frammento di codice seguente viene illustrato come eseguire questa operazione.  
  
```  
 Message response = Message.CreateMessage(  
                  MessageVersion.None,    // No SOAP message version  
                             "*",                     // SOAP action, ignored since this is JSON  
                             "Response string: JSON format specified", // Message body  
                             new DataContractJsonSerializer(typeof(string))); // Specify DataContractJsonSerializer  
      response.Properties.Add( WebBodyFormatMessageProperty.Name,   
                    new WebBodyFormatMessageProperty(WebContentFormat.Json)); // Use JSON format  
  
```  
  
## Vedere anche  
 [Integrazione AJAX e supporto JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)   
 [Serializzazione JSON autonoma](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md)   
 [Serializzazione JSON](../../../../docs/framework/wcf/samples/json-serialization.md)