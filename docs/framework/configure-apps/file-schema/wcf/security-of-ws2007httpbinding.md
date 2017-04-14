---
title: "&lt;security&gt; di &lt;ws2007HttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fdda0ff7-b462-4e26-af52-e87ddab71945
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# &lt;security&gt; di &lt;ws2007HttpBinding&gt;
Rappresenta le impostazioni di sicurezza usate con l'elemento [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md).  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <bindings>  
        <ws2007HttpBinding>  
            <binding name = "string">  
              <security mode="None/Message/Transport/TransportWithMessageCredential">  
                  <transport>  
                  </transport>  
                  <message>  
                  </message>  
              </security  
        </ws2007HttpBinding>  
    </bindings>  
</system.ServiceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`mode`|-   Parametro facoltativo.  Specifica il tipo di sicurezza applicata.  Il valore predefinito è `Message`.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.SecurityMode>.|  
  
## Attributo mode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`None`|La sicurezza è disabilitata.|  
|`Transport`|La sicurezza è fornita mediante HTTPS.  Il servizio deve essere configurato con certificati Secure Sockets Layer \(SSL\).  Il messaggio è interamente protetto usando HTTPS e il servizio viene autenticato dal client usando il certificato SSL del servizio.  L'autenticazione client è controllata tramite l'attributo `ClientCredentials` dell'elemento [\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md).|  
|`Message`|La sicurezza è fornita mediante la sicurezza dei messaggi SOAP.  Per impostazione predefinita, il corpo SOAP viene crittografato e firmato.  Questa modalità offre varie funzionalità: è ad esempio possibile stabilire se le credenziali del servizio sono disponibili per i client fuori banda nonché specificare la suite di algoritmi da usare e il livello di protezione da applicare al corpo del messaggio tramite la proprietà <xref:System.ServiceModel.Security.SecurityMessageProperty>.  L'autenticazione client viene eseguita una volta per ogni sessione e i risultati vengono memorizzati nella cache per la durata della sessione.|  
|`TransportWithMessageCredential`|In questa modalità, HTTPS fornisce l'integrità, la riservatezza e l'autenticazione server e client, mentre la sicurezza dei messaggi SOAP fornisce l'autenticazione client.  Per impostazione predefinita, l'autenticazione client viene eseguita una volta per ogni sessione e i risultati vengono memorizzati nella cache per la durata della sessione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md)|Definisce le impostazioni di sicurezza del trasporto.  Questo elemento corrisponde al tipo <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>.  Queste impostazioni vengono applicate solo quando la modalità è impostata su Transport.|  
|[\<messaggio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-ws2007httpbinding.md)|Definisce le impostazioni di sicurezza per il messaggio.  Questo elemento corrisponde al tipo <xref:System.ServiceModel.Configuration.MessageSecurityOverHttpElement>.  Queste impostazioni non vengono applicate quando la modalità è impostata su Transport.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)|Associazione protetta per applicazioni di trasporto HTTP.|  
  
## Note  
 Questo elemento è progettato per essere interoperabile con i servizi che implementano le specifiche WS\-\*.  La sicurezza basata sul trasporto di questa associazione è SSL \(Secure Sockets Layer\) su HTTP, ovvero HTTPS.  
  
## Vedere anche  
 <xref:System.ServiceModel.WSHttpSecurity>   
 <xref:System.ServiceModel.WSHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>   
 <xref:System.ServiceModel.BasicHttpSecurity>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)