---
title: "&lt;securityTokenHandlers&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f11a631d-4094-4e11-bb03-4ede74b30281
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;securityTokenHandlers&gt;
Specifica un insieme di gestori di token di protezione che sono registrati con l'endpoint.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Specifica il nome di un insieme di gestore del token.  Gli unici valori riconosciuti dal framework sono "ActAs" e "OnBehalfOf".  Se con uno di questi nomi vengono specificati gli insiemi di gestore del token, verrà utilizzato l'insieme durante l'elaborazione di ActAs o OnBehalfOf i token rispettivamente.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|Aggiunge un gestore del token di protezione insieme del gestore del token.|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/clear.md)|Cancella tutti i gestori di token di protezione dall'insieme del gestore del token.|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/remove.md)|Rimuove un gestore del token di protezione dall'insieme del gestore del token.|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per l'insieme di gestori di token.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni di identità a livello di servizio.|  
  
## Note  
 È possibile specificare uno o più insiemi di gestori di token di protezione in una configurazione del servizio.  È possibile specificare un nome per un insieme utilizzando il `name` attributo.  Solo i nomi che gestisce il framework sono "ActAs" e "OnBehalfOf".  In presenza di gestori di questi insiemi, vengono utilizzati da un servizio token di protezione \(STS\) anziché i gestori predefiniti durante l'elaborazione di `ActAs` e `OnBehalfOf` token.  
  
 Per impostazione predefinita, l'insieme viene popolato con i seguenti tipi di gestore: <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>, e <xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>.  È possibile modificare l'insieme utilizzando il `<add>`, `<remove>`, e `<clear>` gli elementi.  È necessario assicurarsi che solo un singolo gestore di nessun tipo particolare è presente nell'insieme.  Ad esempio, se si deriva un gestore di <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> class, il gestore o il <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> può essere configurato in un unico insieme, ma non entrambi.  
  
 Utilizzo di `<securityTokenHandlerConfiguration>` elemento per specificare le impostazioni di configurazione per i gestori dell'insieme.  Le impostazioni specificate tramite questo elemento eseguire l'override di quelli specificati al servizio tramite il [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento.  Alcuni gestori \(compresi diversi tipi di gestore predefinito di\) è in grado di supportare configurazioni aggiuntive tramite un elemento figlio dell'elemento di `<add>` elemento.  Le impostazioni specificate in un gestore di ignorare le impostazioni equivalenti specificate nell'insieme o il servizio.