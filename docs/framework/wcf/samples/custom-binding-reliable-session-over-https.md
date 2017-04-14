---
title: "Sessione affidabile di associazione personalizzata su HTTPS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 16aaa80d-3ffe-47c4-8b16-ec65c4d25f8d
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Sessione affidabile di associazione personalizzata su HTTPS
In questo esempio viene illustrato l'utilizzo della sicurezza del trasporto SSL con le sessioni affidabili.Le sessioni affidabili implementano il protocollo WS\-RM \(WS\-Reliable Messaging\).È possibile ottenere una sessione affidabile protetta componendo WS\-Security su sessioni affidabili.Tuttavia, è anche possibile scegliere di utilizzare la sicurezza del trasporto HTTP con SSL.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\ReliableSessionOverHttps`  
  
## Dettagli dell'esempio  
 SSL assicura che i pacchetti stessi siano protetti.È importante notare che questo meccanismo è diverso dalla protezione della sessione affidabile mediante WS\-Secure Conversation.  
  
 Per utilizzare sessioni affidabili su HTTPS, è necessario creare un'associazione personalizzata.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.Un'associazione personalizzata viene creata utilizzando l'elemento di associazione della sessione affidabile e l'[\<trasportoHttps\>](../../../../docs/framework/configure-apps/file-schema/wcf/httpstransport.md).La configurazione seguente riguarda l'associazione personalizzata.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- use base address provided by host -->  
        <endpoint address=""  
                  binding="customBinding"  
                  bindingConfiguration="reliableSessionOverHttps"   
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is exposed as http://localhost/servicemodelsamples/service.svc/mex-->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
  
    <bindings>  
      <customBinding>  
        <binding name="reliableSessionOverHttps">  
          <reliableSession />  
          <httpsTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="true" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 Il codice di programma nell'esempio è quasi identico a quello del servizio dell'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).È necessario creare un certificato e assegnarlo utilizzando la Gestione guidata certificati server Web prima di compilare ed eseguire l'esempio.Le definizioni dell'endpoint e dell'associazione nelle impostazioni del file di configurazione abilitano l'uso dell'associazione personalizzata, come illustrato nella configurazione di esempio seguente per il client.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
  
    <client>  
      <!-- this endpoint has an https: address -->  
      <endpoint name=""  
                address="https://localhost/servicemodelsamples/service.svc"   
                binding="customBinding"   
                bindingConfiguration="reliableSessionOverHttps"   
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </client>  
  
      <bindings>  
        <customBinding>  
          <binding name="reliableSessionOverHttps">  
            <reliableSession />  
            <httpsTransport />  
          </binding>  
        </customBinding>        
    </bindings>  
  
  </system.serviceModel>  
  
</configuration>  
  
```  
  
 L'indirizzo specificato utilizza lo schema https:\/\/.  
  
 Poiché il certificato utilizzato in questo esempio è un certificato di prova creato con Makecert.exe, viene visualizzato un avviso di sicurezza quando si tenta di accedere a un indirizzo https: nel browser, ad esempio https:\/\/localhost\/servicemodelsamples\/service.svc.Per consentire al client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] di lavorare con un certificato di prova, è stato aggiunto altro codice al client per sopprimere l'avviso di sicurezza.Il codice e la classe associata non sono richiesti quando si utilizzano i certificati di produzione.  
  
```  
// This code is required only for test certificates like those created by Makecert.exe.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 utilizzando il comando seguente.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Verificare di avere eseguito [Istruzioni di installazione certificato server IIS \(Internet Information Services\)](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md).  
  
4.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
5.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche