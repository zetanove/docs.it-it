---
title: "&lt;indirizziDiBase&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 78918102-2898-46e0-9ea8-6b8afe65603e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;indirizziDiBase&gt;
Rappresenta una raccolta di elementi `baseAddress` costituiti da indirizzi di base per un host del servizio in un ambiente indipendente.  Se è presente un indirizzo di base, gli endpoint possono essere configurati con indirizzi relativi all'indirizzo di base.  
  
## Sintassi  
  
```  
  
<baseAddresses>  
   <add baseAddress="string" />  
</baseAddresses>  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddresses.md)|Elemento di configurazione che specifica gli indirizzi di base usati dall'host del servizio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<host\>](../../../../../docs/framework/configure-apps/file-schema/wcf/host.md)|Elemento di configurazione che specifica le impostazioni per un host del servizio.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.HostElement>   
 <xref:System.ServiceModel.ServiceHost>   
 <xref:System.ServiceModel.ServiceHostBase.BaseAddresses%2A>   
 [Hosting](../../../../../docs/framework/wcf/feature-details/hosting.md)