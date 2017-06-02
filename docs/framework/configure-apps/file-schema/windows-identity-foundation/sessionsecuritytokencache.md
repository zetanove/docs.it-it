---
title: "&lt;sessionSecurityTokenCache&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d43e676c-0153-485c-ab31-0257a2db7507
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;sessionSecurityTokenCache&gt;
Registra una cache per i token di sessione con un servizio o un insieme di gestore del token di protezione.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
      <sessionSecurityTokenCache type=xs:string>  
      </sessionSecurityTokenCache>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Un tipo che deriva dal <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> classe.  Per ulteriori informazioni su come specificare un personalizzato `type`, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<caches\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|Registra le cache utilizzate da un servizio o un insieme di gestore del token di protezione.|  
  
## Esempio  
 Il codice XML riportato di seguito viene illustrata la configurazione di una cache personalizzata per contenere i token di protezione di sessione \(<xref:System.IdentityModel.Tokens.SessionSecurityToken>\).  Da cui proviene la configurazione di `ClaimsAwareWebFarm` campione.  Per ulteriori informazioni su questo esempio, vedere [Indice degli esempi di codice di WIF](../../../../../docs/framework/security/wif-code-sample-index.md).  
  
```  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>