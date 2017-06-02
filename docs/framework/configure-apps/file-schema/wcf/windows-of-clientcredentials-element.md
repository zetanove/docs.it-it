---
title: "&lt;windows&gt; dell&#39;elemento &lt;clientCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 793e41c2-31ea-4159-abbc-2123bf097233
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;windows&gt; dell&#39;elemento &lt;clientCredentials&gt;
Specifica le impostazioni per una credenziale Windows da usare per rappresentare il client.  
  
## Sintassi  
  
```  
  
<windows   
    allowedImpersonationLevel="Identification/Impersonation/Delegation/Anonymous/None"  
        allowNtlm="Boolean"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`allowedImpersonationLevel`|Imposta la preferenza di rappresentazione che il client comunica al server.  La modalità di rappresentazione selezionata dal client non viene imposta sul server.  Di seguito vengono elencati i valori validi:<br /><br /> -   Identification: il server può ottenere l'identità e i privilegi del client, ma non lo può rappresentare.<br />-   Impersonation: il server può rappresentare il contesto di sicurezza del client nel sistema locale.<br />-   Delegation: il server può rappresentare il contesto di sicurezza del client nei sistemi remoti.<br />-   Anonymous: il server non può rappresentare o identificare il client.<br />-   None: non è assegnato alcun livello di rappresentazione.<br /><br /> L'impostazione predefinita è Identification.  L'attributo è di tipo <xref:System.Security.Principal.TokenImpersonationLevel>.|  
|`allowNtlm`|L'impostazione di questa proprietà su `true` consente di usare l'autenticazione NTLM se Kerberos non è disponibile.<br /><br /> Quando questa proprietà è impostata su `false`, [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] effettua tutti i tentativi possibili per generare un'eccezione se viene usata l'autenticazione NTLM.  Si noti che l'impostazione di questa proprietà su `false` potrebbe non impedire l'invio di credenziali NTLM nella rete.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|Specifica le credenziali usate per autenticare il client presso il servizio.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WindowsClientElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.Windows%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>   
 <xref:System.ServiceModel.Security.WindowsClientCredential>   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)