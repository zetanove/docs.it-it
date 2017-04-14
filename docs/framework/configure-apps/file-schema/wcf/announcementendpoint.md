---
title: "&lt;announcementEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 034b7c69-a770-4502-8cef-38007bbcd025
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;announcementEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard con un contratto di annuncio fisso.  Un servizio può annunciare la propria disponibilità inviando un messaggio di annuncio online oppure offline rispettivamente quando viene aperto o chiuso.  Un servizio [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] specifica gli endpoint per gli annunci nell'elemento [\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md) e usa AnnouncementClient per eseguire gli annunci.  Un client che desidera stare in ascolto dell'annuncio dall'altro servizio opera in effetti come un servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]. È pertanto necessario configurare gli endpoint per gli annunci per tale client nella sezione [\<servizi\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md).  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <announcementEndpoint>   
          <standardEndpoint  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxAnnouncementDelay=”Timespan”   
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
|name|Stringa che specifica il nome della configurazione dell'endpoint standard.  Il nome viene usato nell'attributo `endpointConfiguration` dell'endpoint del servizio per collegare un endpoint standard alla relativa configurazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà \(indirizzo, associazione, contratto\) fisse.|  
  
## Esempio  
 Nell'esempio seguente viene illustrato un client in ascolto di messaggi di annuncio su http e peernet.  
  
```  
  
<services>  
  <service name="ServiceAnnouncementListener">  
              <endpoint name="httpAnnouncementEndpoint"  
                        kind="announcementEndpoint"  
                        binding="basicHttpBinding"  
                        address="announcements" />  
              <endpoint name="peerNetAnnouncementEndpoint"  
                        kind="announcementEndpoint"  
                        binding="peerTcpBinding"  
                        address="net.p2p://discoveryMesh/multicast"  
                        bindingConfiguration="discoveryPeerTcpBindingConfig" />  
  ...  
  </service>  
</services>  
  
<standardEndpoints>  
  <announcementEndpoint>  
     <standardEndpoint name="httpAnnouncementEndpoint"                         
                       version="WSDiscoveryApril2005" />  
     <standardEndpoint name="peerNetAnnouncementEndpoint"                         
                       version="WSDiscoveryApril2005" />  
   </announcementEndpoint>  
</standardEndpoints>  
  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>