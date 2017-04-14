---
title: "&lt;connectionPoolSettings&gt; di &lt;tcpTransport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2fbc3aa7-fcc9-4193-99a3-85d31d60d3f7
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;connectionPoolSettings&gt; di &lt;tcpTransport&gt;
Specifica impostazioni aggiuntive del pool di connessioni per un trasporto TCP.  
  
## Sintassi  
  
```  
  
<connectionPoolSettings  
    groupName=”String”  
    idleTimeout"TimeSpan"  
        leaseTimeout="TimeSpan"  
    maxOutboundConnectionsPerEndpopint=”Integer” />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`groupName`|Stringa che definisce il nome del pool di connessioni usato per canali in uscita.  In modalità di invio nel flusso, le connessioni non sono condivise, pertanto il pool di connessioni è disabilitato.  Il valore predefinito è una stringa "default".  È possibile modificare questo valore per isolare le connessioni per un particolare client in gruppi separati.|  
|`idleTimeout`|Elemento <xref:System.TimeSpan> positivo che specifica il periodo massimo di inattività della connessione prima che venga interrotta.  L'impostazione predefinita è 00:02:00.|  
|`leaseTimeout`|<xref:System.TimeSpan> specifica il periodo di tempo dopo il quale una connessione attiva viene chiusa.  L'impostazione predefinita è 00:05:00.<br /><br /> Una connessione viene chiusa dopo che è stata restituita alla cache di connessione e non durante la trasmissione attiva.  La cache della connessione usata dal trasporto TCP crea nuove connessioni in base a ogni endpoint, fino al limite della cache impostato da `maxOutboundConnectionsPerEndpoint.`.|  
|`maxOutboundConnectionsPerEndpoint`|Numero intero positivo che specifica il numero massimo di connessioni a un endpoint remoto iniziate dal servizio.  Le connessioni in eccesso vengono messe in coda finché il numero di connessioni non risulta inferiore al limite consentito.  `idleTimeout` limita il periodo di tempo entro il quale le connessioni rimangono in coda prima che venga generata un'eccezione.  Il valore predefinito è 10.<br /><br /> Questo attributo limita il numero di connessioni attive simultanee dal client a un particolare endpoint del servizio.  Se questo valore viene superato a causa di un numero maggiore di connessioni client attive, può risultare che il servizio non risponda al client.  In questo caso, il valore deve essere regolato in modo da superare il numero massimo di connessioni client simultanee previste a un endpoint specifico.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<trasportoNamedPipe\>](../../../../../docs/framework/configure-apps/file-schema/wcf/namedpipetransport.md)|Definisce un trasporto che fa in modo che un canale trasferisca messaggi usando named pipe.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.TcpConnectionPoolSettingsElement>   
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement.ConnectionPoolSettings%2A>   
 <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Trasporti](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [Scelta di un trasporto](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)