---
title: "&lt;discoveryClient&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a78f74c3-1152-4149-ab29-3f12d316caeb
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;discoveryClient&gt;
Rappresenta un elemento di configurazione che consente a un'applicazione client di cercare automaticamente un servizio flusso di lavoro individuabile e di trovarne l'indirizzo in fase di esecuzione.  
  
## Sintassi  
  
```  
  
<discoveryClient discoveryEndpoint=”String” >  
   <findCriteria duration=”TimeSpan”  
       maxResults=”Integer”   
       scopeMatchBy=”Uri” >  
       <contractTypeNames>  
          <add name="String" namespace="String" />  
       <contractTypeNames>  
       <extensions />  
       <scopes>  
          <add scope="URI"/>  
       </scopes>  
   </findCriteria>  
</discoveryClient>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|discoveryEndpoint|Stringa contenente il nome dell'endpoint di individuazione che consente a un'applicazione client di cercare automaticamente un servizio flusso di lavoro individuabile e di trovarne l'indirizzo in fase di esecuzione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Elemento di configurazione che fornisce un set di criteri usati da un'applicazione client per la ricerca di un servizio di individuazione.  I criteri possono essere raggruppati nei criteri di ricerca \(specificando i servizi da cercare\) e nei criteri di terminazione della ricerca \(durata della ricerca\).|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>   
 <xref:System.ServiceModel.Discovery.Configuration.DiscoveryClientElement>