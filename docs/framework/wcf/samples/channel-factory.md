---
title: "Channel factory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 09b53aa1-b13c-476c-a461-e82fcacd2a8b
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Channel factory
In questo esempio viene illustrato in che modo un'applicazione client può creare un canale con la classe <xref:System.ServiceModel.ChannelFactory> anziché un client generato.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 In questo esempio viene utilizzata la classe <xref:System.ServiceModel.ChannelFactory%601> per creare un canale a un endpoint del servizio.In genere, per creare un canale a un endpoint del servizio si genera un tipo client con [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) e si crea un'istanza del tipo generato.È anche possibile creare un canale utilizzando la classe <xref:System.ServiceModel.ChannelFactory%601>, come illustrato in questo esempio.Il servizio creato dal codice di esempio seguente è identico al servizio in [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
```  
EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
WSHttpBinding binding = new WSHttpBinding();  
ChannelFactory<ICalculator> factory = new   
                    ChannelFactory<ICalculator>(binding, address);  
ICalculator channel = factory.CreateChannel();  
```  
  
> [!IMPORTANT]
>  Se si esegue questo esempio in uno scenario a più computer, è necessario sostituire "localhost" nel codice precedente con il nome completo del computer che sta eseguendo il servizio.In questo esempio non viene utilizzata la configurazione per impostare l'indirizzo dell'endpoint, pertanto questa operazione deve essere eseguita nel codice.  
  
 Quando il canale è stato creato, le operazioni del servizio possono essere richiamate in modo analogo a un client generato.  
  
```  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = channel.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
```  
  
 Per chiudere il canale, è necessario prima eseguirne il cast a un'interfaccia <xref:System.ServiceModel.IClientChannel>.Ciò è necessario in quanto il canale generato viene dichiarato nell'applicazione client utilizzando l'interfaccia `ICalculator` che dispone di metodi quali `Add` e `Subtract` ma non `Close`.Il metodo `Close` ha origine sull'interfaccia <xref:System.ServiceModel.ICommunicationObject>.  
  
```  
// Close the channel.  
 ((IClientChannel)client).Close();  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare l'applicazione client.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).Si noti che in questo esempio non viene abilitata la pubblicazione di metadati.Per rigenerare il tipo client, è necessario innanzitutto abilitare la pubblicazione dei metadati per questo esempio.  
  
3.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### Per eseguire l'esempio su più computer  
  
1.  Sostituire "localhost" nel codice seguente con il nome completo del computer che sta eseguendo il servizio.  
  
    ```  
    EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
    ```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Client\ChannelFactory`  
  
## Vedere anche