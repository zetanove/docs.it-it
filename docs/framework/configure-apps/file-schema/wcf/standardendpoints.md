---
title: "&lt;standardEndpoints&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d62153d7-a6e6-462a-a784-cca61e9c2ba1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;standardEndpoints&gt;
Questa sezione di configurazione consente di definire una raccolta di endpoint standard rappresentati da endpoint preconfigurati riusabili.  Un endpoint standard disporrà di uno o più indirizzi, attributi di associazione e del contratto impostati su un valore fisso.  Ad esempio, nell'endpoint di individuazione il contratto è fisso.  È inoltre possibile usare endpoint standard per estendere endpoint servizio con nuove proprietà in modo analogo alla definizione di associazioni personalizzate.  
  
 \<system.ServiceModel\>  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
  
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<announcementEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/announcementendpoint.md)|Definisce un endpoint standard con un contratto di annuncio fisso.  Un servizio può annunciare la propria disponibilità inviando un messaggio di annuncio online oppure offline rispettivamente quando viene aperto o chiuso.  Un servizio [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] specifica gli endpoint per gli annunci nell'elemento [\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md) e usa AnnouncementClient per eseguire gli annunci.  Un client che desidera stare in ascolto dell'annuncio dall'altro servizio opera in effetti come un servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]. È pertanto necessario configurare gli endpoint per gli annunci per tale client nella sezione [\<servizi\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md).|  
|[\<discoveryEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/discoveryendpoint.md)|Definisce un endpoint standard con contratto di individuazione fisso.  Quando viene aggiunto alla configurazione del servizio, specifica la posizione di ascolto dei messaggi di individuazione.  Quando viene aggiunto alla configurazione del client, specifica la posizione di invio delle query di individuazione.|  
|[\<dynamicEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/dynamicendpoint.md)|Questo elemento di configurazione definisce un endpoint standard contenente le informazioni che consentono a un'applicazione di essere usata come un programma client in grado di individuare l'indirizzo dell'endpoint in modo dinamico durante la fase di esecuzione.|  
|[\<mexEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/mexendpoint.md)|Definisce un endpoint standard con un contratto IMetadataExchange fisso.  Poiché tutti gli endpoint per lo scambio di metadati specificano IMetadataExchange come contratto, è possibile usare questo endpoint standard anziché definirne uno personalizzato.|  
|[\<udpAnnoucementEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udpannoucementendpoint.md)|Definisce un endpoint standard usato dai servizi per l'invio di messaggi di annuncio su un'associazione UDP.  Dispone di un contratto fisso e supporta due versioni di individuazione.  Dispone inoltre di un'associazione UDP fissa e di un valore dell'indirizzo predefinito come indicato nelle specifiche WS\-Discovery \(WS\-Discovery aprile 2005 o versione WS\-Discovery 1.1\).  È possibile specificare l'indirizzo multicast da usare per l'invio e la ricezione dei messaggi di annuncio.|  
|[\<udpDiscoveryEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udpdiscoveryendpoint.md)|Definisce un endpoint standard preconfigurato per le operazioni di individuazione su un'associazione multicast UDP.  Questo endpoint dispone di un contratto fisso e supporta due versioni del protocollo WS\-Discovery.  Dispone inoltre di un'associazione UDP fissa e di un indirizzo predefinito come indicato nelle specifiche WS\-Discovery \(WS\-Discovery aprile 2005 o WS\-Discovery V1.1\).|  
|[\<webHttpEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpendpoint.md)|Definisce un endpoint standard con un'associazione [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) fissa che determina l'aggiunta automatica del comportamento [\<webHttp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md).  Usare questo endpoint per la scrittura di un servizio REST.|  
|[\<webScriptEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webscriptendpoint.md)|Definisce un endpoint standard con un'associazione [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) fissa che determina l'aggiunta automatica del comportamento [\<enableWebScript\>](../../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md).  Usare questo endpoint per la scrittura di un servizio chiamato da un'applicazione AJAX ASP.NET.|  
|[\<workflowControlEndpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/workflowcontrolendpoint.md)|Definisce un endpoint standard per il controllo dell'esecuzione di istanze del flusso di lavoro \(creazione, esecuzione, sospensione, terminazione e così via\).|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<system.ServiceModel\>|Elemento radice di tutti gli elementi di configurazione WCF.|  
  
## Vedere anche  
 [Endpoint standard](../../../../../docs/framework/wcf/feature-details/standard-endpoints.md)