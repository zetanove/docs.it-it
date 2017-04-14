---
title: "&lt;behavior&gt; di &lt;endpointBehaviors&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: b90ca3bc-3c22-4174-b903-e3a39898bd27
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# &lt;behavior&gt; di &lt;endpointBehaviors&gt;
L'elemento `behavior` contiene una raccolta di impostazioni per il comportamento di un endpoint.  Ogni comportamento è indicizzato in base al relativo `name`.  Gli endpoint possono essere collegati a ciascun comportamento tramite questo nome.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## Sintassi  
  
```  
  
<system.ServiceModel>  
  <behaviors>  
    <endpointBehaviors>  
       <behavior name="String" />  
    </endpointBehaviors>  
  </behaviors>  
</system.ServiceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Stringa univoca che contiene il nome di configurazione del comportamento.  Questo valore è una stringa definita dall'utente che deve essere univoca in quanto funge da stringa di identificazione dell'elemento.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|Specifica le credenziali usate per autenticare il client presso un servizio.|  
|[\<debugCallback\>](../../../../../docs/framework/configure-apps/file-schema/wcf/callbackdebug.md)|Specifica il debug del servizio per un oggetto di callback [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].|  
|[\<timeoutCallback\>](../../../../../docs/framework/configure-apps/file-schema/wcf/callbacktimeouts.md)|Specifica il timeout per il callback client.|  
|[\<clientVia\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientvia.md)|Specifica la route che un messaggio deve prendere.|  
|[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer.md)|Contiene i dati di configurazione per DataContractSerializer.|  
|[\<dispatcherSynchronization\>](../../../../../docs/framework/configure-apps/file-schema/wcf/dispatchersynchronization.md)|Specifica un comportamento dell'endpoint che consente a un servizio di inviare risposte in modo asincrono.|  
|[\<enableWebScript\>](../../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md)|Abilita il comportamento dell'endpoint che rende possibile l'uso del servizio da pagine Web ASP.NET AJAX.  Questo comportamento deve essere usato solo in combinazione con l'associazione standard \<webHttpBinding\> o l'elemento di associazione \<webMessageEncoding\>.|  
|[\<endpointDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpointdiscovery.md)|Specifica le varie impostazioni di individuazione per un endpoint, quali l'individuazione, gli ambiti e le eventuali estensioni personalizzate ai relativi metadati.|  
|[\<soapProcessing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/soapprocessing.md)|Definisce il comportamento dell'endpoint client usato per effettuare il marshalling dei messaggi tra versioni del messaggio e tipi di associazione diversi.|  
|[\<ricezioneSincrona\>](../../../../../docs/framework/configure-apps/file-schema/wcf/synchronousreceive-element.md)|Specifica il comportamento di run\-time per la ricezione di messaggi in un'applicazione client o di servizio.  Non prevede attributi o elementi figlio.|  
|[\<batchTransazionale\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transactedbatching.md)|Specifica se il batch delle transazioni è supportato per le operazioni di ricezione.|  
|[\<webHttp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md)|Specifica il WebHttpBehavior in un endpoint tramite configurazione.  Questo comportamento, quando viene usato insieme all'associazione standard \<webHttpBinding\>, consente di usare il modello di programmazione Web per un servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamentiEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)|Raccolta di elementi di comportamento dell'endpoint.|