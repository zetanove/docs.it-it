---
title: "&lt;resolverPeerPnrp&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1b34f3b-68e5-4911-a367-de49fb61dbc6
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;resolverPeerPnrp&gt;
Specifica l'uso di PNRP \(Peer Name Resolution Protocol\) come resolver.  Questo elemento è facoltativo perché PNRP è il resolver predefinito.  
  
## Sintassi  
  
```  
  
<pnrpResolver resolverType="String" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|resolverType|Stringa che specifica il resolver da usare.  L'attributo è facoltativo.  Se non è impostato o se è impostato su una stringa vuota, viene usato PNRP.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Esempio  
  
```  
<pnrpResolver resolverType="" />  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.PnrpPeerResolverElement>   
 <xref:System.ServiceModel.Channels.PnrpPeerResolverBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Resolver del peer](../../../../../docs/framework/wcf/feature-details/peer-resolvers.md)