---
title: "&lt;behavior&gt; di &lt;serviceBehaviors&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 78fc0a08-55de-416a-ac12-a5e6ffc9a987
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;behavior&gt; di &lt;serviceBehaviors&gt;
L'elemento `behavior` contiene una raccolta di impostazioni per il comportamento di un servizio.  Ogni comportamento è indicizzato in base al relativo `name`.  I servizi sono in grado di collegarsi a ogni comportamento tramite tale nome usando l'attributo `behaviorConfiguration` dell'elemento [\<endpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md).  In questo modo gli endpoint possono condividere configurazioni del comportamento comuni senza ridefinire le impostazioni.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
> [!NOTE]
>  Gli elementi di comportamento specifici delle attività dei flussi di lavoro di Windows, quale l'elemento [\<sendMessageChannelCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/sendmessagechannelcache.md), vengono documentati nella pagina [\<behavior\> di \<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md).  
  
## Sintassi  
  
```  
  
<system.ServiceModel>  
  <behaviors>  
    <serviceBehaviors>  
       <behavior name="String" />  
    </serviceBehaviors>  
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
|[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)|Contiene i dati di configurazione per DataContractSerializer.|  
|[\<providerPersistenza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/persistenceprovider.md)|Specifica il tipo di implementazione del provider di persistenza da usare, nonché il timeout da usare per le operazioni di persistenza.|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md)|Fornisce l'accesso in fase di esecuzione al servizio di routing per consentire la modifica dinamica della configurazione di routing.|  
|[\<serviceAuthenticationManager\>](../../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthenticationmanager.md)|Fornisce un elemento di configurazione del flusso di lavoro che stabilisce a livello di servizio la validità di una trasmissione, di un messaggio o di un creatore.|  
|[\<autorizzazioneServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)|Specifica le impostazioni che autorizzano l'accesso alle operazioni del servizio.|  
|[\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.|  
|[\<debugServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md)|Specifica informazioni di debug e di Guida per un servizio [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].|  
|[\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md)|Specifica l'individuabilità degli endpoint del servizio.|  
|[\<serviceMetadata\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md)|Specifica la pubblicazione dei metadati del servizio e delle informazioni associate.|  
|[\<controlloSicurezzaServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md)|Specifica impostazioni che abilitano controllo di eventi di sicurezza durante le operazioni del servizio.|  
|[\<limitazioneServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicethrottling.md)|Specifica il meccanismo di limitazione di un servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].|  
|[\<serviceTimeouts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicetimeouts.md)|Specifica il timeout per un servizio.|  
|[\<runtimeFlussoDiLavoro\>](../../../../../docs/framework/configure-apps/file-schema/wcf/workflowruntime.md)|Specifica le impostazioni di un'istanza di WorkflowRuntime per l'hosting di servizi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] basati sul flusso di lavoro.|  
|[\<useRequestHeadersForMetadataAddress\>](../../../../../docs/framework/configure-apps/file-schema/wcf/userequestheadersformetadataaddress.md)|Abilita il recupero di informazioni sull'indirizzo di metadati dalle intestazioni del messaggio di richiesta.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamentiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)|Raccolta di elementi di comportamento del servizio.|