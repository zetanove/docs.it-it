---
title: "Client tipizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 62c40e8f-e9b4-4b1a-939a-93c37393d343
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Client tipizzati
L'esempio illustra come ottenere informazioni da un client tipizzato generato da [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.In questo esempio, il client è un'applicazione console \(exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 La proprietà `Endpoint` del client consente l'accesso alle informazioni sull'endpoint del servizio con cui il client sta comunicando, inclusi indirizzo, informazioni sull'associazione e sul contratto.La proprietà `InnerChannel` del client è un'istanza di <xref:System.ServiceModel.IClientChannel> che consente l'accesso a informazioni sul canale sottostante, ad esempio stato e ID di sessione.  
  
```  
// Create a client.  
CalculatorClient client = new CalculatorClient();  
...  
Console.WriteLine("Client - endpoint:  " + client.Endpoint.Address);  
Console.WriteLine("Client - binding:  " + client.Endpoint.Binding.Name);  
Console.WriteLine("Client - contract: " + client.Endpoint.Contract.Name);  
  
IClientChannel channel = client.InnerChannel;  
Console.WriteLine("Client channel - state: " + channel.State);  
Console.WriteLine("Client channel - session identifier: " + channel.SessionId);  
  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Client - endpoint:  http://localhost/servicemodelsamples/service.svc  
Client - binding:  WSHttpBinding  
Client - contract: ICalculator  
Client channel - state: Opened  
Client channel - session identifier: urn:uuid:ae16fbc4-2964-4e87-9fb1-c5aa78fc567e  
  
Press <ENTER> to terminate client.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Client\TypedClient`  
  
## Vedere anche