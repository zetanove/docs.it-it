---
title: "Esempio Individuare un servizio con modalit&#224; Uri di ascolto univoco | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a6d35b2-0469-43c8-a0c9-63623e3d2733
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Esempio Individuare un servizio con modalit&#224; Uri di ascolto univoco
In questo esempio viene illustrato come individuare un servizio che dispone della proprietà <xref:System.ServiceModel.Channels.BindingContext.ListenUriMode%2A> impostata su <xref:System.ServiceModel.Description.ListenUriMode>.L'impostazione della proprietà <xref:System.ServiceModel.Channels.BindingContext.ListenUriMode%2A> su <xref:System.ServiceModel.Description.ListenUriMode> garantisce l'univocità di ListenUri attraverso l'impostazione della porta che deve essere univoca o del percorso che deve essere univoco mediante l'aggiunta di un GUID.  
  
### Funzionalità nel servizio  
 La proprietà <xref:System.ServiceModel.Channels.BindingContext.ListenUriMode%2A> viene impostata su <xref:System.ServiceModel.Description.ListenUriMode> per l'endpoint TCP.Il servizio viene quindi reso individuabile su un endpoint <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.  
  
### Funzionalità nel client  
 Questo client si connette al servizio utilizzando il `Via.Uri` corretto tramite il metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A>.Sull'oggetto <xref:System.ServiceModel.Discovery.FindResponse> restituito dal metodo viene quindi eseguita una query per determinare se contiene una proprietà <xref:System.ServiceModel.Endpoint.ListenUri%2A> valida e se è diverso da `Address.Uri`.Le informazioni appropriate vengono quindi passate al metodo `InvokeCalculatorService`.Nel metodo `InvokeCalculatorService` la proprietà <xref:System.ServiceModel.Endpoint.ListenUri%2A> viene passata dal chiamante, quindi un oggetto `ClientViaBehavior` con il `Via.Uri` corretto viene aggiunto all'endpoint del client.  
  
##### Per utilizzare questo esempio  
  
1.  Aprire UniqueListenUriMode.sln utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Eseguire l'applicazione del servizio, generata nella cartella \[directory soluzione di base\]\\service\\bin\\debug.  
  
4.  Eseguire l'applicazione client, generata nella cartella \[directory soluzione di base\]\\Client\\bin\\debug.  
  
     Il client individua il servizio in esecuzione e scrive nella console i metadati pubblicati dall'endpoint del servizio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Discovery\UniqueListenUriMode`  
  
## Vedere anche