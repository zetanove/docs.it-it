---
title: "&lt;transport&gt; di &lt;peerTransport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d7116240-845c-4b6f-b203-262de6b597ef
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;transport&gt; di &lt;peerTransport&gt;
Specifica il tipo di trasporto per messaggi protetti inviati dai peer configurati con questa associazione.  
  
## Sintassi  
  
```  
  
<security>  
   <transport credentialType="Certificate/Password" />  
</security>         
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|credentialType|Parametro facoltativo.  Specifica il tipo di credenziali usate per verificare messaggi inviati con il trasporto peer.  L'attributo è di tipo <xref:System.ServiceModel.PeerTransportCredentialType>.|  
  
## Attributo credentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Certificato|L'autenticazione del trasporto del canale peer richiede un certificato X509.|  
|Password|L'autenticazione del trasporto del canale peer richiede una password corretta.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md)|Definisce le impostazioni di sicurezza di un trasporto peer.|  
  
## Note  
 Questo elemento viene impostato solo se l'attributo mode di [\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md) è impostato su `Transport` o `TransportWithMessageCredential`.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement>   
 <xref:System.ServiceModel.PeerSecuritySettings.Transport%2A>   
 <xref:System.ServiceModel.PeerTransportSecuritySettings>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Protezione del trasporto](../../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [Trasporti](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [Scelta di un trasporto](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)