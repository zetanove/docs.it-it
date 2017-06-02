---
title: "Configurazione semplificata per servizi WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e39ec25-18a3-4fdc-b6a3-9dfafbd60112
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Configurazione semplificata per servizi WCF
In questo esempio viene illustrato come implementare e configurare un tipico servizio e un client mediante [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Questo esempio è la base per tutti gli altri esempi della tecnologia di base.  
  
 Questo servizio, che espone un endpoint per comunicare con il servizio, utilizza la configurazione semplificata in [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)].Prima di [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)], l'endpoint viene in genere definito in un file di configurazione \(Web.config\), come mostrato nel codice di configurazione di esempio seguente.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright ©) Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Samples.GettingStarted.CalculatorService"  
               behaviorConfiguration="CalculatorServiceBehavior">  
        <endpoint address="" binding="basicHttpBinding" contract="ICalculator"/>  
        <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange"/>  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 In [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)], l'elemento `<service>` è facoltativo.Quando un servizio non definisce alcun endpoint, al servizio viene aggiunto un endpoint per ogni indirizzo di base e contratto implementato.L'indirizzo di base viene aggiunto al nome del contratto per determinare l'endpoint e l'associazione è determinata dallo schema dell'indirizzo.Nell'esempio di codice seguente viene illustrato un file di configurazione semplificato.In questa configurazione un client sullo stesso computer può accedere al servizio da http:\/\/localhost\/servicemodelsamples\/service.svc.Affinché i client presenti nei computer remoti accedano al servizio, è necessario specificare un nome di dominio completo anziché localhost.Per impostazione predefinita, il servizio non espone metadati.In quanto tale, il servizio attiva il comportamento <xref:System.ServiceModel.Description.ServiceMetadataBehavior>.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright © Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### Per utilizzare questo esempio  
  
1.  Verificare di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Eseguire l'esempio attenendosi ai passaggi seguenti:  
  
    1.  Fare clic con il pulsante destro del mouse sul progetto **Service** e selezionare **Imposta come progetto di avvio**, quindi premere **Ctrl\+F5**.  
  
    2.  Attendere l'output della console che conferma che il servizio è in esecuzione.  
  
    3.  Fare clic con il pulsante destro del mouse sul progetto **Client** e selezionare **Imposta come progetto di avvio**, quindi premere **Ctrl\+F5**.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\ConfigSimplificationIn40`  
  
## Vedere anche  
 [Gestione](http://go.microsoft.com/fwlink/?LinkId=193960)   
 [Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md)