---
title: "Elemento &lt;httpDigest&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3da4f276-dfd9-4247-8c07-01d83618727c
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Elemento &lt;httpDigest&gt;
Specifica una credenziale di tipo digest usata per autenticare il client presso un servizio.  
  
## Sintassi  
  
```  
  
<digest impersonationLevel="Identification/Impersonation/Delegation/Anonymous/None" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`impersonationLevel`|Imposta la preferenza di rappresentazione che il client comunica al server.  La modalità di rappresentazione selezionata dal client non viene imposta sul server.  Di seguito vengono elencati i valori validi:<br /><br /> -   Identification: il server può ottenere l'identità e i privilegi del client, ma non lo può rappresentare.<br />-   Impersonation: il server può rappresentare il contesto di sicurezza del client nel sistema locale.<br />-   Delegation: il server può rappresentare il contesto di sicurezza del client nei sistemi remoti.<br />-   Anonymous: il server non può rappresentare o identificare il client.<br />-   None: non è assegnato alcun livello di rappresentazione.<br /><br /> L'impostazione predefinita è Identification.  L'attributo è di tipo <xref:System.Security.Principal.TokenImpersonationLevel>.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|Specifica le credenziali usate per autenticare un client presso un servizio.|  
  
## Note  
 Un digest è un hash determinato mediante un algoritmo e un insieme di input.  L'autenticatore e l'autenticato concordano un algoritmo e scambiamo i dati usati come input.  Il client può calcolare l'hash e inviarlo al servizio.  Il servizio calcola anche l'hash e confronta i valori.  Una corrispondenza convalida il client.  
  
 Questa funzionalità deve essere abilitata con Active Directory in Windows e Internet Information Services \(IIS\).  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [Autenticazione del digest in IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88443).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.HttpDigest%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>   
 <xref:System.ServiceModel.Configuration.HttpDigestClientElement>   
 <xref:System.ServiceModel.Security.HttpDigestClientCredential>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)