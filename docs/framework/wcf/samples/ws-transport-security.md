---
title: "Sicurezza del trasporto WS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33a20358-5e1b-458a-a6a9-15753bc7b99b
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# Sicurezza del trasporto WS
In questo esempio viene illustrato l'utilizzo della sicurezza del trasporto SSL con l'associazione <xref:System.ServiceModel.WSHttpBinding>.Per impostazione predefinita, l'associazione `wsHttpBinding` consente la comunicazione HTTP.Se viene configurata per la sicurezza del trasporto, l'associazione supporta la comunicazione HTTPS.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.L'associazione `wsHttpBinding` è specificata e configurata nei file di configurazione dell'applicazione per il client e il servizio.  
  
> [!NOTE]
>  La procedura di configurazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\WS\wsTransportSecurity`  
  
 Il codice di programma nell'esempio è quasi identico a quello del servizio dell'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).È necessario creare un certificato e assegnarlo utilizzando la Gestione guidata certificati server Web prima di compilare ed eseguire l'esempio.Le definizioni dell'endpoint e dell'associazione nelle impostazioni del file di configurazione abilitano la modalità di sicurezza `Transport`, come illustrato nella configurazione di esempio seguente per il client.  
  
```  
<system.serviceModel>  
  
    <client>  
      <!-- this endpoint has an https: address -->  
      <endpoint address="https://localhost/servicemodelsamples/service.svc" binding="wsHttpBinding" bindingConfiguration="Binding1" contract="Microsoft.Samples.TransportSecurity.ICalculator"/>  
    </client>  
  
    <bindings>  
      <wsHttpBinding>  
        <!-- configure wsHttpbinding with Transport security mode  
                   and clientCredentialType as None -->  
        <binding name="Binding1">  
          <security mode="Transport">  
            <transport clientCredentialType="None"/>  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  
  </system.serviceModel>  
  
```  
  
 L'indirizzo specificato utilizza lo schema https:\/\/.La configurazione dell'associazione imposta la modalità di sicurezza su `Transport`.La stessa modalità di sicurezza deve essere specificata nel file Web.config del servizio.  
  
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
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 utilizzando il comando seguente.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Verificare di avere eseguito [Istruzioni di installazione certificato server IIS \(Internet Information Services\)](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md).  
  
4.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
5.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche