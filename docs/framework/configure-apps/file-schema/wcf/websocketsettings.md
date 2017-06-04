---
title: "&lt;webSocketSettings&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bbf97e02-8dd1-4922-acac-3cd33397b249
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;webSocketSettings&gt;
Elemento di configurazione usato per specificare le impostazioni relative a Web Socket.  
  
## Sintassi  
  
```  
  
<netHttpBinding>  
   <binding>   
       <webSocketSettings createNotificationOnConnection="boolean"  
                              disablePayloadMasking="boolean"  
                              keepAliveInterval="TimeSpan"  
                              maxPendingConnections="Integer"  
                              receiveBufferSize="Integer"  
                              sendBufferSize="Integer"  
                              subProtocol="String"  
                              transportUsage="WhenDuplex/Always/Never"/>  
   </binding>  
</netHttpBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|createNotificationOnConnection|Specifica se una notifica viene inviata alla connessione.|  
|disablePayloadMasking|Specifica se il mascheramento di Web Socket è disabilitato.|  
|keepAliveInterval|Specifica l'intervallo keep\-alive.|  
|maxPendingConnections|Specifica il numero massimo di connessioni in attesa dell'invio nel servizio.|  
|receiveBufferSize|Specifica le dimensioni del buffer di ricezione.|  
|sendBufferSize|Specifica le dimensioni del buffer di invio.|  
|subProtocol|Specifica il sottoprotocollo Web Socket.|  
|transportUsage|Specifica quando usare Web Sockets.|  
  
## transportUsage Attribute  
  
|Valore|Descrizione|  
|------------|-----------------|  
|WhenDuplex|Usare il protocollo Web Socket quando il contratto è di tipo duplex.|  
|Always|Usare sempre il protocollo Web Socket indipendentemente dal contratto.|  
|Never|Non usare mai il protocollo Web Socket.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<netHttpBinding\>|Specifica NetHttpBinding|  
  
## Esempio  
 L'esempio seguente illustra come usare l'elemento \<webSocketSettings\>.  
  
```xml  
<netHttpBinding>  
        <binding>  
          <webSocketSettings createNotificationOnConnection="true"  
                              disablePayloadMasking="false  
                              keepAliveInterval="00:10:00"  
                              maxPendingConnections="100"  
                              receiveBufferSize="1000"  
                              sendBufferSize="1000"  
                              subProtocol="Soap"  
                              transportUsage="WhenDuplex/Always/Never"/>  
  
        </binding>  
      </netHttpBinding>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.Binding>   
 <xref:System.ServiceModel.Channels.BindingElement>   
 <xref:System.ServiceModel.BasicHttpBinding>   
 <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)