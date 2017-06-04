---
title: "&lt;udpDiscoveryEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f485329-2771-43bc-88de-df8f2faa3bb7
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;udpDiscoveryEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard preconfigurato per le operazioni di individuazione su un'associazione multicast UDP.  Questo endpoint dispone di un contratto fisso e supporta due versioni del protocollo WS\-Discovery.  Dispone inoltre di un'associazione UDP fissa e di un indirizzo predefinito come indicato nelle specifiche WS\-Discovery \(WS\-Discovery aprile 2005 o WS\-Discovery V1.1\).  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <discoveryEndpoint>   
          <standardEndpoint  
                  discoveryMode=”Adhoc/Managed”  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxResponseDelay=”Timespan”  
                  multicastAddress=”Uri”   
                  name="String" />  
       </discoveryEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|discoveryMode|Stringa che specifica la modalità del protocollo di individuazione.  I valori validi sono "Adhoc" e "Managed".  Nella modalità gestita il protocollo si basa su un proxy di individuazione che viene usato come un repository di servizi individuabili.  Con la modalità Adhoc è necessario che il protocollo utilizzi il meccanismo multicast UDP per l'individuazione dei servizi disponibili.  Questo valore è di tipo <xref:System.Servicemodel.Discovery.DiscoveryMode>.|  
|discoveryVersion|Stringa che specifica una delle due versioni del protocollo WS\-Discovery.  I valori validi sono WSDiscovery11 e WSDiscoveryApril2005.  Questo valore è di tipo <xref:System.Servicemodel.Discovery.DiscoveryVersion>.|  
|maxResponseDelay|Valore TimeSpan che specifica il valore massimo per il tempo di attesa del protocollo di individuazione prima dell'invio di determinati messaggi, ad esempio Probe Match o Resolve Match.<br /><br /> Se tutti i messaggi ProbeMatch vengono inviati contemporaneamente, potrebbero verificarsi problemi di rete.  Per evitare questo problema, i messaggi ProbeMatch vengono inviati con un ritardo casuale tra ogni ProbeMatch.  Il ritardo casuale è compreso nell'intervallo tra 0 e il valore impostato da questo attributo.  Se questo attributo viene impostato su 0, i messaggi ProbeMatch vengono inviati in un ciclo breve senza alcun ritardo.  In caso contrario, i messaggi ProbeMatch vengono inviati con un ritardo casuale, in modo che il tempo totale richiesto per l'invio di tutti i messaggi ProbeMatch non superi il valore di maxResponseDelay.  Questo valore è importante solo per i servizi e non viene usato dai client.|  
|multicastAddress|URI che specifica un indirizzo multicast da usare per l'invio e la ricezione dei messaggi di individuazione.  Il valore predefinito è l'indirizzo multicast conforme alla specifica del protocollo.|  
|`name`|Stringa che specifica il nome della configurazione dell'endpoint standard.  Il nome viene usato nell'attributo `endpointConfiguration` dell'endpoint del servizio per collegare un endpoint standard alla relativa configurazione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<udpTransportSettings\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udptransportsettings.md)|Raccolta di impostazioni che consentono di configurare il trasporto UDP per l'endpoint UDP.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà \(indirizzo, associazione, contratto\) fisse.|  
  
## Esempio  
 Nell'esempio seguente viene illustrato un servizio in ascolto di messaggi di individuazione su un trasporto multicast UDP.  
  
```  
  
<services>  
    <service name="CalculatorService"  
         behaviorConfiguration="CalculatorServiceBehavior">  
         <endpoint binding="basicHttpBinding"   
           address="calculator" contract="ICalculatorService" />  
         <endpoint name="DiscoveryEndpoint"  
                kind="udpDiscoveryEndpoint" />  
</service>  
<standardEndpoints>  
  <udpDiscoveryEndpoint>  
     <standardEndpoint name="DiscoveryEndpoint"                         
                       version="WSDiscoveryApril2005" />  
   </udpDiscoveryEndpoint>  
</standardEndpoints>  
  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>