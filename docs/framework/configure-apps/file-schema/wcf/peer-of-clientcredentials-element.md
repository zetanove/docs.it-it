---
title: "Elemento &lt;peer&gt; di &lt;clientCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 505bd987-0042-4622-b68e-94f439729d53
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Elemento &lt;peer&gt; di &lt;clientCredentials&gt;
Specifica le credenziali usate per l'autenticazione di client peer\-to\-peer.  
  
## Sintassi  
  
```  
  
<peer>  
  <certificate/>  
  <peerAuthentication/>  
  <messageSenderAuthentication/>  
</peer>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificato\>](../../../../../docs/framework/configure-apps/file-schema/wcf/certificate-element.md)|Specifica un certificato X.509 da usare per firmare e crittografare i messaggi di client peer\-to\-peer.  .|  
|[\<autenticazionePeer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peerauthentication-element.md)|Specifica le opzioni di autenticazione dei client peer.|  
|[\<autenticazioneMittenteMessaggio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/messagesenderauthentication-element.md)|Specifica le opzioni di autenticazione dei mittenti di messaggi.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|Specifica le credenziali usate per autenticare un client presso un servizio.|  
  
## Note  
 Questo elemento di configurazione specifica le credenziali che un nodo peer usa per autenticare se stesso agli altri nodi della rete, nonché le impostazioni di autenticazione usate da un nodo peer per autenticare altri nodi peer.  Per altre informazioni, vedere [Peer Channel Message Authentication](http://msdn.microsoft.com/it-it/80e73386-514e-4c30-9e4a-b9ca8c173a95) e [Protezione di applicazioni del canale peer](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.Peer%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.Peer%2A>   
 <xref:System.ServiceModel.Security.PeerCredential>   
 [Rete peer\-to\-peer](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/it-it/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/it-it/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Protezione di applicazioni del canale peer](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)