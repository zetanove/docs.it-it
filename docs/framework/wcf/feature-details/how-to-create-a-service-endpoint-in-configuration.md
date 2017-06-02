---
title: "Procedura: creare un endpoint di servizio nella configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "2016-06-16"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f474e25d-2a27-4f31-84c5-395c442b8e70
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: creare un endpoint di servizio nella configurazione
Gli endpoint forniscono ai client l'accesso alla funzionalità offerta da un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. È possibile definire uno o più endpoint per un servizio usando una combinazione di indirizzi di endpoint assoluti e relativi. In alternativa, se non si definisce alcun endpoint per il servizio, il runtime ne fornirà automaticamente alcuni per impostazione predefinita. In questo argomento viene illustrato come aggiungere endpoint usando un file di configurazione che contiene indirizzi sia relativi che assoluti.  
  
## Esempio  
 Nella configurazione del servizio seguente vengono specificati un indirizzo di base e cinque endpoint.  
  
```xml  
<configuration>  
  
  <appSettings>  
    <!-- use appSetting to configure base address provided by host -->  
    <add key="baseAddress" value="http://localhost:8000/servicemodelsamples/service" />  
  </appSettings>  
  
  <system.serviceModel>  
    <services>  
    <!-- This section is optional with the default configuration introduced  
         in .NET Framework 4. -->  
      <service  
          name="Microsoft.ServiceModel.Samples.CalculatorService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
          </baseAddresses>  
        </host>  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="/test"  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="http://localhost:8001/hello/servicemodelsamples"  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="net.tcp://localhost:9000/servicemodelsamples/service"  
                  binding="netTcpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is another relative address exposed at   
             http://localhost:8000/ServiceModelSamples/service/mex -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
  
```  
  
## Esempio  
 L'indirizzo di base viene specificato usando l'elemento `add`, in service\/host\/baseAddresses, come illustrato nell'esempio seguente.  
  
```xml  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
```  
  
## Esempio  
 La prima definizione dell'endpoint descritta nella configurazione di esempio seguente specifica un indirizzo relativo, che indica che l'indirizzo endpoint è una combinazione dell'indirizzo di base e dell'indirizzo relativo, in base alle regole di composizione URI \(Uniform Resource Identifier\). L'indirizzo relativo è vuoto \(""\), pertanto l'indirizzo endpoint corrisponde all'indirizzo di base. L'indirizzo endpoint effettivo è http:\/\/localhost:8000\/servicemodelsamples\/service.  
  
```xml  
<endpoint address=""   
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## Esempio  
 Anche la seconda definizione dell'endpoint specifica un indirizzo relativo, come illustrato nell'esempio di configurazione seguente. L'indirizzo relativo, "test", viene accodato all'indirizzo di base. L'indirizzo endpoint effettivo è http:\/\/localhost:8000\/servicemodelsamples\/service\/test.  
  
```xml  
<endpoint address="/test"  
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## Esempio  
 La terza definizione dell'endpoint specifica un indirizzo assoluto, come illustrato nell'esempio di configurazione seguente. L'indirizzo di base non ha alcun ruolo nell'indirizzo. L'indirizzo endpoint effettivo è http:\/\/localhost:8001\/hello\/servicemodelsamples.  
  
```xml  
<endpoint address="http://localhost:8001/hello/servicemodelsamples"  
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## Esempio  
 Il quarto indirizzo endpoint specifica un indirizzo assoluto e un trasporto diverso, cioè TCP. L'indirizzo di base non ha alcun ruolo nell'indirizzo. L'indirizzo dell'endpoint effettivo è net.tcp:\/\/localhost:9000\/servicemodelsamples\/service.  
  
```xml  
<endpoint address="net.tcp://localhost:9000/servicemodelsamples/service"  
    binding="netTcpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## Esempio  
 Per usare gli endpoint predefiniti forniti dal runtime, non specificare alcun endpoint del servizio nel codice né nel file di configurazione. In questo esempio, il runtime crea gli endpoint predefiniti all'apertura del servizio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] endpoint, associazioni e comportamenti predefiniti, vedere [Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
```xml  
<configuration>  
  
  <appSettings>  
    <!-- use appSetting to configure base address provided by host -->  
    <add key="baseAddress" value="http://localhost:8000/servicemodelsamples/service" />  
  </appSettings>  
  
  <system.serviceModel>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```