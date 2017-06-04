---
title: "&lt;discoveryEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fae2f48b-a635-4e4b-859d-a1432ac37e1c
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;discoveryEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard con un contratto di individuazione fisso.  Quando viene aggiunto alla configurazione del servizio, specifica la posizione di ascolto dei messaggi di individuazione.  Quando viene aggiunto alla configurazione del client, specifica la posizione di invio delle query di individuazione.  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <discoveryEndpoint>   
          <standardEndpoint  
                  discoveryMode=”Adhoc/Managed”  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxResponseDelay=”Timespan”   
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
|`name`|Stringa che specifica il nome della configurazione dell'endpoint standard.  Il nome viene usato nell'attributo `endpointConfiguration` dell'endpoint del servizio per collegare un endpoint standard alla relativa configurazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà \(indirizzo, associazione, contratto\) fisse.|  
  
## Esempio  
 Nell'esempio seguente viene illustrato un servizio in ascolto dei messaggi di individuazione su un trasporto multicast di rete peer.  Nell'esempio viene specificata in modo esplicito la versione WS\-Discovery aprile 2005.  
  
 La configurazione dell'endpoint standard viene definita in base al servizio e non può essere condivisa nel servizio.  Affinché lo stesso endpoint di individuazione possa essere usato da un altro servizio, la stessa configurazione dovrà essere aggiunta alla sezione di tale servizio.  
  
```  
  
<services>  
    <service name="CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
             <endpoint binding="basicHttpBinding"   
                address="calculator" contract="ICalculatorService" />  
             <endpoint name="peerNetDiscovery"  
                binding="peerTcpBinding"  
                address="net.p2p://discoveryMesh/multicast"  
                kind="discoveryEndpoint"  
                endpointConfiguration="peerTcpDiscoveryEndpointConfiguration"  
                bindingConfiguration="discoveryPeerTcpBindingConfig" />      
   </service>  
</services>  
<standardEndpoints>  
  <discoveryEndpoint>  
     <standardEndpoint name="peerTcpDiscoveryEndpointConfiguration "                         
                       version="WSDiscoveryApril2005" />  
   </discoveryEndpoint>  
</standardEndpoints>  
  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>