---
title: "&lt;resolver&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0c00200c-f135-4e5c-a024-76b72bcbc021
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# &lt;resolver&gt;
Specifica un resolver peer usato per risolvere un ID della rete di peer in un insieme di indirizzi di nodo peer che rappresenta alcuni nodi che partecipano nella rete.  
  
## Sintassi  
  
```  
  
<resolver mode="Auto/Custom/Pnrp"  
   referralPolicy="DoNotShare/Service/Share">  
</resolver>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`mode`|Stringa che specifica se l'istanza del resolver peer associata a questo servizio è specifica di PNRP, un resolver personalizzato o viene determinata automaticamente.  L'attributo è di tipo <xref:System.ServiceModel.PeerResolvers.PeerResolverMode>.|  
|`referralPolicy`|Una stringa che specifica la modalità di condivisione dei riferimenti fra peer.  L'attributo è di tipo <xref:System.ServiceModel.PeerResolvers.PeerReferralPolicy>.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<intestazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)|Specifica le impostazioni di un servizio resolver peer personalizzato.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione di [\<netPeerTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md).|  
  
## Note  
 Un resolver di nomi peer è un servizio di individuazione usato dai canali peer per trovare i nodi che partecipano a una rete peer.  Un resolver di nomi peer consente inoltre di "registrare" un nodo in una rete di peer, ovvero di renderlo individuabile e disponibile all'interno della rete.  Per altre informazioni sui resolver del peer, vedere [Resolver del peer](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.PeerResolver>   
 <xref:System.ServiceModel.PeerResolvers.PeerResolverSettings>   
 <xref:System.ServiceModel.NetPeerTcpBinding.Resolver%2A>   
 <xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement.Resolver%2A>   
 <xref:System.ServiceModel.Configuration.PeerResolverElement>   
 [Resolver del peer](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md)   
 [Adding a Custom Resolver to a PeerChannel Application](http://msdn.microsoft.com/it-it/12aa3787-2962-439c-ad27-46523c8b0419)