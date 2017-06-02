---
title: "Configurazione semplificata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcbe1f84-437c-495f-9324-2bc09fd79ea9
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Configurazione semplificata
La configurazione di servizi [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] può risultare un'attività complessa.  Esistono diverse opzioni e non è sempre semplice determinare quali impostazioni sono necessarie.  Se da una parte i file di configurazione aumentano la flessibilità dei servizi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], dall'altra rappresentano anche l'origine di molti problemi difficili da individuare.  In [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] questi problemi vengono risolti e viene offerto un modo per ridurre la dimensione e la complessità della configurazione dei servizi.  
  
## Configurazione semplificata  
 Nei file di configurazione dei servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], la sezione \<`system.serviceModel`\> contiene un elemento \<`service`\> per ogni servizio ospitato.  L'elemento \<`service`\> contiene una raccolta di elementi \<`endpoint`\> che specificano gli endpoint esposti per ogni servizio e facoltativamente un set dei comportamenti del servizio.  Gli elementi \<`endpoint`\> specificano l'indirizzo, l'associazione e il contratto esposti dall'endpoint e facoltativamente la configurazione di associazione e i comportamenti dell'endpoint.  La sezione \<`system.serviceModel`\> contiene anche un elemento \<`behaviors`\> che consente di specificare i comportamenti del servizio o dell'endpoint.  L'esempio seguente mostra la sezione \<`system.serviceModel`\> di un file di configurazione.  
  
```  
system.serviceModel>  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="MyServiceBehavior">  
        <serviceMetadata httpGetEnabled="true">  
        <serviceDebug includeExceptionDetailInFaults="false">  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  <bindings>  
   <basicHttpBinding>  
      <binding name=MyBindingConfig"  
               maxBufferSize="100"  
               maxReceiveBufferSize="100" />  
   </basicHttpBinding>  
   </bindings>   <services>  
    <service behaviorConfiguration="MyServiceBehavior"  
             name="MyService">  
      <endpoint address=""  
                binding="basicHttpBinding"  
                contract="ICalculator"  
                bindingConfiguration="MyBindingConfig" />  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange"/>  
    </service>  
  </services>  
</system.serviceModel>  
  
```  
  
 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] facilita la configurazione di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] rimuovendo il requisito per l'elemento \<`service`\>.  Se non si aggiunge una sezione \<`service`\> o non si aggiungono endpoint in una sezione \<`service`\> e il servizio non definisce endpoint a livello di codice, viene automaticamente aggiunto al servizio un set di endpoint predefiniti, uno per ogni indirizzo di base del servizio e per ogni contratto implementato dal servizio  In ognuno di questi endpoint l'indirizzo endpoint corrisponde all'indirizzo di base, l'associazione viene determinata dallo schema dell'indirizzo di base e il contratto corrisponde a quell'implementato dal servizio.  Se non è necessario specificare endpoint o comportamenti del servizio oppure apportare modifiche alle impostazioni dell'associazione, non è necessario specificare un file di configurazione dei servizi.  Se un servizio implementa due contratti e l'host abilita sia il trasporto HTTP sia quello TCP, l'host del servizio crea quattro endpoint predefiniti, uno per ogni contratto che usa ogni trasporto.  Per creare endpoint predefiniti, l'host del servizio deve sapere quali associazioni usare.  Queste impostazioni vengono specificate in una sezione \<`protocolMappings`\> all'interno della sezione \<`system.serviceModel`\>.  La sezione \<`protocolMappings`\> contiene un elenco di schemi del protocollo di trasporto mappati ai tipi di associazione.  L'host del servizio usa gli indirizzi di base passati per determinare quale associazione usare.  L'esempio seguente usa l'elemento \<`protocolMappings`\>.  
  
> [!WARNING]
>  La modifica di elementi predefiniti della configurazione, quali associazioni o comportamenti, potrebbe influire sugli eventuali servizi definiti nei livelli inferiori della gerarchia di configurazione che usino tali elementi.  Pertanto, quando ci si accinge a modificare le associazioni e i comportamenti predefiniti, tenere sempre presente che tali modifiche potrebbero avere effetto su altri servizi nella gerarchia.  
  
> [!NOTE]
>  I servizi ospitati in Internet Information Services \(IIS\) o nel servizio Attivazione processo Windows \(WAS, Windows Process Activation Service\) usano la directory virtuale come indirizzo di base.  
  
```  
<protocolMapping>  
  <add scheme="http"     binding="basicHttpBinding" bindingConfiguration="MyBindingConfiguration"/>  
  <add scheme="net.tcp"  binding="netTcpBinding"/>  
  <add scheme="net.pipe" binding="netNamedPipeBinding"/>  
  <add scheme="net.msmq" binding="netMSMQBinding"/>  
</protocolMapping>  
  
```  
  
 Nell'esempio precedente un endpoint con un indirizzo di base che inizia con lo schema "http" usa <xref:System.ServiceModel.BasicHttpBinding>.  Un endpoint con un indirizzo di base che inizia con lo schema "net.tcp" usa <xref:System.ServiceModel.NetTcpBinding>.  È possibile eseguire l'override delle impostazioni in un file App.config locale o un file Web.config.  
  
 Ogni elemento all'interno della sezione \<`protocolMappings`\> deve specificare uno schema e un'associazione.  Facoltativamente, è possibile specificare un attributo `bindingConfiguration` che indica una configurazione dell'associazione all'interno della sezione \<`bindings`\> del file di configurazione.  Se non viene specificato alcun elemento `bindingConfiguration`, viene usata la configurazione di associazione anonima del tipo di associazione appropriata.  
  
 I comportamenti del servizio vengono configurati per gli endpoint predefiniti tramite sezioni \<`behavior`\> anonime all'interno delle sezioni \<`serviceBehaviors`\>.  Per configurare i comportamenti del servizio viene usato qualsiasi elemento \<`behavior`\> sprovvisto di nome all'interno di \<`serviceBehaviors`\>.  Il file di configurazione seguente abilita ad esempio la pubblicazione dei metadati del servizio per tutti i servizi all'interno del host.  
  
```  
<system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>    <!-- No <service> tag is necessary. Default endpoints are added to the service -->  
    <!-- The service behavior with name="" is picked up by the service -->  
 </system.serviceModel>  
```  
  
 I comportamenti dell'endpoint vengono configurati tramite le sezioni \<`behavior`\> all'interno delle sezioni \<`serviceBehaviors`\>.  
  
 L'esempio seguente è costituito da un file di configurazione equivalente a quello indicato all'inizio di questo argomento che usa il modello di configurazione semplificato.  
  
```  
<system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="false"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>    <bindings>  
       <basicHttpBinding>  
          <binding maxBufferSize="100"  
                   maxReceiveBufferSize="100" />  
       </basicHttpBinding>  
    </bindings>    <!-- No <service> tag is necessary. Default endpoints will be added to the service -->  
    <!-- The service behavior with name="" will be picked up by the service -->  
    <protocolMapping>  
      <add scheme="http"     binding="basicHttpBinding" / </protocolMapping>  
  </system.serviceModel>  
```  
  
> [!IMPORTANT]
>  Questa funzionalità si riferisce solo alla configurazione del servizio WCF, non alla configurazione client.  Nella maggior parte dei casi, la configurazione client WCF viene generata da uno strumento come svcutil.exe o aggiungendo un riferimento al servizio da Visual Studio.  Se si configura manualmente un client WCF, è necessario aggiungere un elemento \<client\> alla configurazione e specificare tutti gli endpoint da chiamare.  
  
## Vedere anche  
 [Configurazione dei servizi tramite file di configurazione](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)   
 [Configurazione di associazioni per servizi](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)   
 [Configurazione di associazioni fornite dal sistema](../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Configurazione dei servizi](../../../docs/framework/wcf/configuring-services.md)   
 [Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/it-it/13cb368e-88d4-4c61-8eed-2af0361c6d7a)   
 [Configurazione dei servizi WCF nel codice](../../../docs/framework/wcf/configuring-wcf-services-in-code.md)