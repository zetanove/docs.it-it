---
title: "&lt;udpAnnoucementEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5b3fa9c5-f372-4df9-a9d6-1e426063b721
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;udpAnnoucementEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard usato dai servizi per inviare messaggi di annuncio su un'associazione UDP.  Dispone di un contratto fisso e supporta due versioni di individuazione.  Dispone inoltre di un'associazione UDP fissa e di un valore dell'indirizzo predefinito come indicato nelle specifiche WS\-Discovery \(WS\-Discovery aprile 2005 o versione WS\-Discovery 1.1\).  È possibile specificare l'indirizzo multicast da usare per l'invio e la ricezione dei messaggi di annuncio.  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <announcementEndpoint>   
          <standardEndpoint  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxAnnouncementDelay=”Timespan”   
                  multicastAddress=”Uri”  
                  name="String" />   
       </announcementEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|discoveryVersion|Stringa che specifica una delle due versioni del protocollo WS\-Discovery.  I valori validi sono WSDiscovery11 e WSDiscoveryApril2005.  Questo valore è di tipo <xref:System.ServiceModel.Discovery.Configuration.DiscoveryVersion>.|  
|maxAnnouncementDelay|Valore TimeSpan che specifica il valore massimo per il tempo di attesa del protocollo di individuazione prima dell'invio di un messaggio Hello.  Prima dell'invio dei messaggi, trascorrerà un periodo di attesa il cui valore casuale è compreso tra 0 e il valore di questo attributo.  Questo attributo viene usato per impostare un ritardo casuale limitato che consente di evitare problemi di rete quando la rete si arresta e tutti i servizi ritornano online contemporaneamente.|  
|multicastAddress|URI che specifica un indirizzo multicast da usare per l'invio e la ricezione dei messaggi di individuazione.  Il valore predefinito è l'indirizzo multicast conforme alla specifica del protocollo.|  
|name|Stringa che specifica il nome della configurazione dell'endpoint standard.  Il nome viene usato nell'attributo `endpointConfiguration` dell'endpoint del servizio per collegare un endpoint standard alla relativa configurazione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<udpTransportSettings\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udptransportsettings.md)|Raccolta di impostazioni che consentono di configurare il trasporto UDP per l'endpoint UDP.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà \(indirizzo, associazione, contratto\) fisse.|  
  
## Esempio  
 Nell'esempio seguente viene illustrato un client in ascolto di un annuncio su un trasporto multicast UDP con indirizzo multicast predefinito e trasporto multicast UDP con indirizzo multicast specificato.  
  
```  
  
<services>  
  <service name="ServiceAnnouncementListener">  
      <endpoint name="udpAnnouncementEndpointStandard"  
                kind="udpAnnouncementEndpoint"  
                bindingConfiguration="..." />  
      <endpoint name="udpAnnouncementEndpoint2"  
                kind="udpAnnouncementEndpoint"  
                endpointConfiguration="AnnouncementConfiguration3702"  
                bindingConfiguration="..." />  
...  
  </service>  
</services>  
<standardEndpoints>  
  <udpAnnouncementEndpoint>  
     <standardEndpoint name="AnnouncementConfiguration2"   
          version="WSDiscoveryApril2005"   
          multicastAddress="soap.udp://239.255.255.250:3703"/>          
  </udpAnnouncementEndpoint>  
</standardEndpoints>  
  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>