---
title: "&lt;caches&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4651091b-3a20-40d8-b293-4408c0710143
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;caches&gt;
Registra le cache utilizzate per i token di sessione e token di tipo replay.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sessionSecurityTokenCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md)|Registra una cache per i token di sessione con un servizio o un insieme di gestore del token di protezione.|  
|[\<tokenReplayCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md)|Registra una cache di riesecuzione del token con un servizio o un insieme di gestore del token di protezione.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni di identità a livello di servizio.|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per un insieme di protezione gestori dei token.|  
  
## Note  
 A `<caches>` elemento può essere specificata a livello di servizio sotto il `<identityConfiguration>` elemento o il livello di insieme del gestore del token di protezione nel `<securityTokenHandlerConfiguration>` elemento.  Le impostazioni di un insieme di gestore del token sostituiscono quelli specificati dal servizio.  
  
 Il `<caches>` elemento è rappresentato dal <xref:System.IdentityModel.Configuration.IdentityModelCachesElement> classe.  Le cache di configurazione sono rappresentate dal <xref:System.IdentityModel.Configuration.IdentityModelCaches> classe.  
  
## Esempio  
 Il codice XML riportato di seguito viene illustrata la configurazione di una cache personalizzata per contenere i token di protezione di sessione \(<xref:System.IdentityModel.Tokens.SessionSecurityToken>\).  Da cui proviene la configurazione di `ClaimsAwareWebFarm` campione.  
  
```  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```