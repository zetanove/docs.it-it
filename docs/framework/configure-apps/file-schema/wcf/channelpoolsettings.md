---
title: "&lt;impostazioniPoolCanali&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4755f3d3-4213-4c68-ae7f-45b67d744459
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;impostazioniPoolCanali&gt;
Specifica le impostazioni del pool di canali per un'associazione personalizzata.  
  
## Sintassi  
  
```  
  
<channelPoolSettings  
    idleTimeout"TimeSpan"  
        leaseTimeout"TimeSpan"  
    maxOutboundConnectionsPerEndpopint=”Integer” />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`idleTimeout`|Oggetto <xref:System.TimeSpan> positivo che specifica il periodo massimo di inattività dei canali nel pool prima della disconnessione.  L'impostazione predefinita è 00:02:00.|  
|`leaseTimeout`|Oggetto <xref:System.TimeSpan> che specifica l'intervallo di tempo trascorso il quale un canale, dopo essere stato restituito al pool, viene chiuso.  L'impostazione predefinita è 00:10:00.|  
|`maxOutboundChannelsPerEndpoint`|Numero intero positivo che specifica il numero massimo di canali che possono essere memorizzati nel pool per ogni endpoint remoto.  Il valore predefinito è 10.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<oneWay\>](../../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)|Attiva il routing dei pacchetti per un'associazione personalizzata.|  
  
## Note  
 Le quote sono usate come meccanismo di criterio per impedire un consumo eccessivo di risorse.  Impediscono attacchi di tipo Denial of Service \(DoS\), dannosi o non intenzionali.  Usare questo elemento durante l'impostazione delle quote dei canali in un canale personalizzato.  
  
 `ChannelPoolSettings` specifica tre quote:  
  
-   La quota `idleTimeout` viene usata per ridurre il rischio di attacchi di tipo Denial of Service \(DoS\) nel server basati sul blocco di risorse per periodi di tempo prolungati.  Nel client, l'impostazione del valore corretto può aumentare l'affidabilità della connessione con il servizio.  Il valore predefinito è basato su un'allocazione conservativamente modesta di risorse.  È adatto per un ambiente di sviluppo e in scenari con installazioni di piccole dimensioni.  Gli amministratori del servizio devono rivedere il valore se un'installazione sta esaurendo le risorse o se le connessioni sono limitate nonostante la disponibilità di risorse aggiuntive.  
  
-   La quota `leaseTimeout` viene usata per l'integrazione con i servizi di bilanciamento del carico e per migliorare l'affidabilità.  Il valore predefinito è basato su un'allocazione conservativa di risorse.  È adatto per un ambiente di sviluppo e in scenari con installazioni di piccole dimensioni.  Gli amministratori del servizio devono rivedere il valore se un'installazione sta esaurendo le risorse o se le connessioni sono limitate nonostante la disponibilità di risorse aggiuntive.  
  
-   La quota `maxOutboundChannelsPerEndpoint` imposta limiti della cache sia nel server che nel client ed è usata per migliorare l'affidabilità.  Il valore predefinito è basato su un'allocazione conservativamente modesta di risorse idonee per ambienti di sviluppo e scenari con installazioni di piccole dimensioni.  Gli amministratori del servizio devono rivedere il valore se un'installazione sta esaurendo le risorse o se le connessioni sono limitate nonostante la disponibilità di risorse aggiuntive.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.OneWayBindingElement.ChannelPoolSettings%2A>   
 <xref:System.ServiceModel.Channels.ChannelPoolSettings>   
 <xref:System.ServiceModel.Configuration.OneWayElement.ChannelPoolSettings%2A>   
 <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [\<oneWay\>](../../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)