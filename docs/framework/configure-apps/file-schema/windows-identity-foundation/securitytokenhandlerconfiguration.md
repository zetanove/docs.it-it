---
title: "&lt;securityTokenHandlerConfiguration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 28724cc6-020c-4a06-9a1f-d7594f315019
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;securityTokenHandlerConfiguration&gt;
Fornisce la configurazione per l'insieme di gestori di token.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration saveBootstrapContext=xs:boolean  
          maximumClockSkew=TimeSpan>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|saveBootstrapContext|Specifica se il token di bootstrap deve essere incluso nel token di sessione.  Il valore può essere anche impostato su un insieme di gestore del token impostando il `saveBootstrapContext` di attributo sul [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento.  Un valore impostato per l'insieme di token gestore sostituisce il valore impostato per il servizio.|  
|maximumClockSkew|A <xref:System.TimeSpan> che specifica l'inclinazione di clock massima.  Controlla l'inclinazione di clock massima quando si eseguono operazioni sensibili al tempo, quali la convalida della data di scadenza di una sessione di accesso.  Il valore predefinito è 5 minuti, "00: 00".  Per ulteriori informazioni su come specificare <xref:System.TimeSpan> valori, vedere [Timespan Values](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_TimespanValues).  L'inclinazione massima orologio può inoltre impostare a livello di servizio impostando il `maximumClockSkew` di attributo sul [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento.  Un valore impostato per l'insieme di token gestore sostituisce il valore impostato per il servizio.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<audienceUris\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/audienceuris.md)|Specifica l'insieme di URI sono accettabili identificatori di questo componente.  Parametro facoltativo.|  
|[\<caches\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|Registra le cache utilizzate per i token di sessione e token di tipo replay.  È possibile specificare a livello di servizio o un insieme di gestore del token di protezione.  Parametro facoltativo.|  
|[\<certificateValidation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidation.md)|Controlla le impostazioni che i gestori di token utilizzano per la convalida dei certificati.  È possibile specificare a livello di servizio o un insieme di gestore del token di protezione.  Queste impostazioni vengono ignorate se un gestore specifico è configurato con un proprio validator.  Parametro facoltativo.|  
|[\<issuerNameRegistry\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuernameregistry.md)|Consente di configurare il Registro di sistema del nome dell'emittente che viene utilizzato dai gestori dell'insieme di gestore del token.  Parametro facoltativo.|  
|[\<issuerTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuertokenresolver.md)|Registra il resolver del token emittente utilizzato dai gestori dell'insieme di gestore del token.  Resolver del token emittente viene utilizzato per risolvere il token di firma di token in arrivo e messaggi.  Parametro facoltativo.|  
|[\<serviceTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicetokenresolver.md)|Registra il resolver del token servizio utilizzato dai gestori dell'insieme di gestore del token.  Resolver del token di servizio viene utilizzato per risolvere il token di crittografia in token in arrivo e messaggi.  Parametro facoltativo.|  
|[\<tokenReplayDetection\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaydetection.md)|Consente il rilevamento riproduzione token e specifica l'ora di scadenza per i token.  È possibile specificare a livello di servizio o un insieme di gestore del token di protezione.  Parametro facoltativo.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|Specifica un insieme di gestori di token di protezione che sono registrati con l'endpoint.|  
  
## Note  
 In questa sezione fornisce i valori delle proprietà per un <xref:System.IdentityModel.Tokens.SecurityTokenHandlerConfiguration> oggetto.  Le impostazioni configurate in questa sezione la precedenza su quelle configurate nel servizio.  Alcune di queste impostazioni può, a sua volta, eseguire l'override delle impostazioni specificate quando viene aggiunto un gestore per l'insieme del gestore del token di protezione.  
  
## Esempio  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>   
      <securityTokenHandlerConfiguration>  
  
        <audienceUris>  
          <clear/>  
          <add value="http://www.example.com/myapp/" />  
        </audienceUris>  
  
        <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel">  
          <trustedIssuers>  
            <add thumbprint="97249e1a … 4c9158de" name="contoso.com" />  
          </trustedIssuers>  
        </issuerNameRegistry>  
  
        <issuerTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
        <serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```