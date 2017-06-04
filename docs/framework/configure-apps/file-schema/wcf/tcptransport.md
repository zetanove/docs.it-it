---
title: "&lt;trasportoTcp&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 8fcd18c1-9958-42e7-b442-7903f7bdb563
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;trasportoTcp&gt;
Definisce un trasporto TCP che può essere usato da un canale ai messaggi dei trasferimenti per un'associazione personalizzata.  
  
## Sintassi  
  
```  
  
<tcpTransport   
    listenBacklog="Integer"  
        portSharingEnabled="Boolean"  
    teredoEnabled="Boolean"  
    transferMode=”Buffered/Streamed”  
        <connectionPoolSettings  
          groupName=”String”  
        idleTimeout"TimeSpan"  
        leaseTimeout="TimeSpan"  
        maxOutboundConnectionsPerEndpopint=”Integer” />  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|channelInitializationTimeout|Periodo massimo di tempo entro il quale un canale può trovarsi nello stato di inizializzazione prima della disconnessione, espresso in secondi.  La quota include il tempo necessario per l'autenticazione di una connessione TCP usando il protocollo .Net Message Framing.  Un client deve inviare alcuni dati iniziali prima che il server disponga di informazioni sufficienti per effettuare l'autenticazione.  Il valore predefinito è 30 secondi.|  
|listenBacklog|Numero massimo di richieste di connessione in coda che possono essere in sospeso per un servizio Web.  L'attributo `connectionLeaseTimeout` limita il tempo di attesa della connessione da parte del client prima che venga generata un'eccezione.  Si tratta di una proprietà a livello di socket che controlla il numero massimo di richieste di connessione in coda che possono essere in attesa di un servizio Web.  Quando il valore di ListenBacklog è troppo basso, WCF arresta l'accettazione di richieste e pertanto ignora le nuove connessioni finché il server non riconosce alcune delle connessioni esistenti in coda. Per impostazione predefinita il valore è 16 \* numero di processori.|  
|portSharingEnabled|Valore booleano che specifica se è attivata la condivisione delle porte TCP per la connessione.  Se è `false`, ciascuna associazione userà la propria porta esclusiva.  Il valore predefinito è `false`.<br /><br /> Questa impostazione è pertinente solo per i servizi.  I client non ne sono interessati.<br /><br /> L'uso di questa impostazione richiede l'attivazione del servizio di condivisione porte TCP di Windows Communication Foundation \(WCF\) modificando il relativo Tipo di avvio su Manuale o Automatico.|  
|teredoEnabled|Valore booleano che specifica se Teredo \(una tecnologia per l'indirizzamento dei client dietro a firewall\) è attivata.  Il valore predefinito è `false`.<br /><br /> Questa proprietà abilita Teredo per il socket TCP sottostante.  Per altre informazioni, vedere la pagina relativa alla [panoramica di Teredo](http://go.microsoft.com/fwlink/?LinkId=95339).<br /><br /> Questa proprietà è applicabile solo su [!INCLUDE[wxpsp2](../../../../../includes/wxpsp2-md.md)] e [!INCLUDE[ws2003](../../../../../includes/ws2003-md.md)].  [!INCLUDE[wv](../../../../../includes/wv-md.md)] ha un'opzione di configurazione a livello di computer per Teredo, pertanto quando viene eseguito Vista, questa proprietà viene ignorata.  L'uso di Teredo richiede che lo stack IPv6 di Microsoft sia installato sia nei computer client che in quelli di servizio e che tutti siano configurati correttamente.  Per altre informazioni sulla configurazione di Teredo, vedere la pagina relativa alla [panoramica di Teredo](http://go.microsoft.com/fwlink/?LinkId=95339).  Per altre informazioni, vedere la pagina relativa ai [centri tecnologici di Windows Server 2003](http://go.microsoft.com/fwlink/?LinkId=49888).|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 Questo trasporto usa URI nel formato "net.tcp:\/\/nomehost:porta\/percorso".  Gli altri componenti URI sono facoltativi.  
  
 L'elemento `tcpTransport` rappresenta il punto iniziale per la creazione di un'associazione personalizzata che implementa il protocollo di trasporto TCP.  Il trasporto è ottimizzato per le comunicazioni da WCF a WCF.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.TcpTransportElement>   
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Trasporti](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [Scelta di un trasporto](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)