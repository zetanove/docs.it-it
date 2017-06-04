---
title: "&lt;comportamenti&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e5da4e6-1aa5-466c-924e-f10efee57f0b
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;comportamenti&gt;
Questo elemento definisce due raccolte figlio denominate `endpointBehaviors` e `serviceBehaviors`.  Ogni raccolta definisce elementi di comportamento usati rispettivamente da endpoint e servizi.  Ogni elemento di comportamento è identificato dal relativo attributo `name` univoco.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
 \<system.ServiceModel\>  
  
## Sintassi  
  
```  
  
<behaviors>  
   <serviceBehaviors>  
   </serviceBehaviors>  
   <endpointBehaviors>  
   </endpointBehaviors>  
</behaviors>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 None  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamentiEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)|Questa sezione di configurazione rappresenta tutti i comportamenti definiti per un endpoint specifico.|  
|[\<comportamentiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)|Questa sezione di configurazione rappresenta tutti i comportamenti definiti per un servizio specifico.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.serviceModel\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)|L'elemento radice di tutti gli elementi di configurazione di Windows Communication Foundation \(WCF\).|  
  
## Note  
 È possibile usare l'elemento `<remove>` per rimuovere un determinato comportamento dalla raccolta.  A tale scopo, è sufficiente fornire il nome del comportamento da rimuovere nell'attributo `name` dell'elemento `<remove>`.  È inoltre possibile usare l'elemento `<clear>` per garantire che una raccolta di comportamenti venga avviata vuota cancellando tutto il contenuto della raccolta.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.BehaviorsSection>   
 <xref:System.ServiceModel.Configuration.EndpointBehaviorElementCollection>   
 <xref:System.ServiceModel.Configuration.EndpointBehaviorElement>   
 <xref:System.ServiceModel.Configuration.ServiceBehaviorElementCollection>   
 <xref:System.ServiceModel.Configuration.ServiceBehaviorElement>   
 [Configurazione ed estensione del runtime con i comportamenti](../../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)   
 [Configurazione dei comportamenti client](../../../../../docs/framework/wcf/configuring-client-behaviors.md)   
 [Specifica del comportamento in fase di esecuzione dei client](../../../../../docs/framework/wcf/specifying-client-run-time-behavior.md)   
 [Specifica del comportamento in fase di esecuzione del servizio](../../../../../docs/framework/wcf/specifying-service-run-time-behavior.md)   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)