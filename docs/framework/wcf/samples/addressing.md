---
title: "Indirizzamento | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d438e6f2-d0f3-43aa-b259-b51b5bda2e64
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Indirizzamento
Nell'esempio relativo all'Indirizzamento vengono illustrati i vari aspetti e le funzionalità degli indirizzi endpoint.  L'esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  In questo esempio, il servizio è indipendente.  Sia il client che il servizio sono applicazioni console.  Il servizio definisce più endpoint usando una combinazione di indirizzi endpoint relativi e assoluti.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Il file di configurazione del servizio specifica un indirizzo di base e quattro endpoint.  L'indirizzo di base viene specificato usando l'elemento Add, in service\/host\/baseAddresses, come illustrato nell'esempio di configurazione seguente.  
  
```  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
  ...  
</service>  
```  
  
 La prima definizione dell'endpoint descritta nell'esempio di configurazione seguente specifica un indirizzo relativo, che indica che l'indirizzo endpoint è una combinazione dell'indirizzo di base e dell'indirizzo relativo, in base alle regole di composizione URI.  
  
```  
<!-- Empty relative address specified:   
     use the base address provided by the host. -->  
<!-- The endpoint address is  
     http://localhost:8000/ServiceModelSamples/service. -->  
<endpoint address=""  
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 In questo caso, l'indirizzo relativo è vuoto \(""\), pertanto l'indirizzo endpoint corrisponde all'indirizzo di base.  L'indirizzo endpoint effettivo è http:\/\/localhost:8000\/servicemodelsamples\/service.  
  
 Anche la seconda definizione dell'endpoint specifica un indirizzo relativo, come illustrato nell'esempio di configurazione seguente.  
  
```  
<!-- The relative address specified: use the base address -->  
<!-- provided by the host + path. The endpoint address is -->  
<!-- http://localhost:8000/servicemodelsamples/service/test. -->  
<endpoint address="/test"  
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 L'indirizzo relativo, "test", viene accodato all'indirizzo di base.  L'indirizzo endpoint effettivo è http:\/\/localhost:8000\/servicemodelsamples\/service\/test.  
  
 La terza definizione dell'endpoint specifica un indirizzo assoluto, come illustrato nell'esempio di configurazione seguente.  
  
```  
<endpoint address="http://localhost:8001/hello/servicemodelsamples"  
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 L'indirizzo di base non ha alcun ruolo nell'indirizzo.  L'indirizzo endpoint effettivo è http:\/\/localhost:8001\/hello\/servicemodelsamples.  
  
 Il quarto indirizzo endpoint specifica un indirizzo assoluto e un trasporto diverso, cioè TCP.  L'indirizzo di base non ha alcun ruolo nell'indirizzo.  L'indirizzo dell'endpoint effettivo è net.tcp:\/\/localhost:9000\/servicemodelsamples\/service.  
  
```  
<!-- The absolute address specified, different transport: -->  
<!-- use the specified address, and ignore the base address. -->  
<!-- The endpoint address is -->  
<!-- net.tcp://localhost:9000/servicemodelsamples/service. -->  
<endpoint address=  
          "net.tcp://localhost:9000/servicemodelsamples/service"  
          binding="netTcpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
</service>  
```  
  
 Il client accede a uno dei quattro endpoint del servizio, ma tutti e quattro vengono definiti nel file di configurazione.  Il client seleziona un endpoint quando crea l'oggetto `CalculatorProxy`.  Modificando il nome della configurazione da `CalculatorEndpoint1` a `CalculatorEndpoint4`, è possibile verificare il funzionamento di ognuno degli endpoint.  
  
 Quando si esegue l'esempio, il servizio enumera l'indirizzo, il nome dell'associazione e il nome del contratto per ognuno degli endpoint.  Per ServiceHost, l'endpoint di scambio di metadati \(MEX\) è solo un altro endpoint, per cui viene incluso nell'elenco.  
  
```  
Service endpoints:  
Endpoint - address:  http://localhost:8000/ServiceModelSamples/service  
           binding:  WSHttpBinding  
           contract: ICalculator  
Endpoint - address:  http://localhost:8000/ServiceModelSamples/service/test  
           binding:  WSHttpBinding  
           contract: ICalculator  
Endpoint - address:  http://localhost:8001/hello/servicemodelsamples  
           binding:  WSHttpBinding  
           contract: ICalculator  
Endpoint - address:  net.tcp://localhost:9000/servicemodelsamples/service  
           binding:  NetTcpBinding  
           contract: ICalculator  
Endpoint - address:  http://localhost:8000/ServiceModelSamples/service/mex  
           binding:  MetadataExchangeHttpBinding  
           contract: IMetadataExchange  
  
The service is ready.  
Press <ENTER> to terminate service.  
  
```  
  
 Quando si esegue il client, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.  Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
    > [!NOTE]
    >  Se si usa Svcutil.exe per rigenerare la configurazione di questo esempio, assicurarsi di modificare il nome dell'endpoint nella configurazione client in modo che corrisponda al codice client.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Addressing`  
  
## Vedere anche