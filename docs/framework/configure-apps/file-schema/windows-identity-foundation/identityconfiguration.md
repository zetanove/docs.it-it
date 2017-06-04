---
title: "&lt;identityConfiguration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1db76253-07da-447b-9e7a-3705c7228cf4
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# &lt;identityConfiguration&gt;
Specifica le impostazioni di identità a livello di servizio.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration  
      name=xs:string  
      saveBootstrapContext=xs:boolean>  
      maximumClockSkew=TimeSpan >  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Il nome della sezione di configurazione di identità.  È possibile utilizzare questo nome per fare riferimento a una sezione di configurazione specifici.  Se non `name` viene specificato, la sezione definisce la configurazione predefinita.  La configurazione predefinita viene sempre utilizzata per gli scenari di federazione passivo.  Per ulteriori informazioni, vedere l'elemento [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md).|  
|saveBootstrapContext|Specifica se il token di bootstrap deve essere incluso nel token di sessione.  Il valore può essere anche impostato su un insieme di gestore del token impostando il `saveBootstrapContext` di attributo sul [\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) elemento.  Un valore impostato per l'insieme di token gestore sostituisce il valore impostato per il servizio.|  
|maximumClockSkew|A <xref:System.TimeSpan> che specifica l'inclinazione di clock massima.  Controlla l'inclinazione di clock massima quando si eseguono operazioni sensibili al tempo, quali la convalida della data di scadenza di una sessione di accesso.  Il valore predefinito è 5 minuti, "00: 00".  Per ulteriori informazioni su come specificare <xref:System.TimeSpan> valori, vedere [Timespan Values](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_TimespanValues).  L'inclinazione massima orologio può inoltre impostare su un insieme di token gestore impostando il `maximumClockSkew` di attributo sul [\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) elemento.  Un valore impostato per l'insieme di token gestore sostituisce il valore impostato per il servizio.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<caches\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|Registra le cache utilizzate per i token di sessione e token di tipo replay.  È possibile specificare a livello di servizio o un insieme di gestore del token di protezione.  Parametro facoltativo.|  
|[\<certificateValidation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidation.md)|Controlla le impostazioni che i gestori di token utilizzano per la convalida dei certificati.  È possibile specificare a livello di servizio o un insieme di gestore del token di protezione.  Parametro facoltativo.|  
|[\<claimsAuthenticationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthenticationmanager.md)|Registra un gestore di autenticazione di attestazioni di attestazioni in ingresso.  Parametro facoltativo.|  
|[\<claimsAuthorizationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md)|Registra un gestore di autorizzazione di attestazioni per le attestazioni in ingresso.  Parametro facoltativo.|  
|[\<claimTypeRequired\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimtyperequired.md)|Specifica il set di attestazioni necessarie per i token di protezione in ingresso.  Parametro facoltativo.|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|Specifica un insieme di gestori di token di protezione.  È possibile specificare zero o più insiemi di gestori di token di protezione.  Parametro facoltativo.|  
|[\<tokenReplayDetection\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaydetection.md)|Consente il rilevamento riproduzione token e specifica l'ora di scadenza per i token.  È possibile specificare a livello di servizio o un insieme di gestore del token di protezione.  Parametro facoltativo.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.identityModel\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md)|Fornisce la configurazione per l'attivazione delle opzioni di base di identità di Windows \(WIF\) nelle applicazioni.|  
  
## Note  
 Identità più configurazioni possono essere definite, ciascuno con un nome univoco.  Il comportamento è il seguente:  
  
1.  Se non `<identityConfiguration>` l'elemento è specificato.  Una configurazione di identità predefinita viene creata in fase di esecuzione e inserire i valori predefiniti.  
  
2.  Se un singolo `<identityConfiguration>` l'elemento è specificato.  È la configurazione predefinita di identità.  Non è importante se si è definito o meno.  
  
3.  Se più `<identityConfiguration>` elementi vengono specificati.  L'elemento senza nome specifica la configurazione predefinita di identità.  È consigliabile che, quando si specificano più `<identityConfiguration>` gli elementi, uno di essi deve essere senza nome.  
  
> [!WARNING]
>  Se si specificano più `<identityConfiguration>` gli elementi, uno di essi deve essere senza nome.  L'elemento senza nome sarà la configurazione predefinita di identità.  
  
 Alcune delle impostazioni specificate nel `<identityConfiguration>` elemento può essere sottoposto a override mediante le impostazioni di un insieme di gestore del token di protezione o mediante le impostazioni di gestori di token di protezione individuale.  
  
> [!IMPORTANT]
>  Quando si utilizza il <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> o <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> classe per fornire il controllo di accesso basato sui crediti nel codice, la configurazione di identità a cui fa riferimento la `<federationConfiguration>` elemento configura i criteri utilizzati per prendere decisioni di autorizzazione e in Gestione autorizzazioni attestazioni.  Questo è vero, anche in scenari non sono passivi scenari Web, ad esempio un'applicazione che non è basata sul Web o applicazioni di Windows Communication Foundation \(WCF\).  Se l'applicazione non è un'applicazione Web passiva, la [\<claimsAuthorizationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md) l'elemento \(e relativi elementi del criterio figlio, se presente\) della configurazione dell'identità di cui si fa riferimento sono le uniche impostazioni applicate.  Tutte le altre impostazioni vengono ignorate.  Per ulteriori informazioni, vedere l'elemento [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md).  
  
 Il `<identityConfiguration>` elemento è rappresentato dal <xref:System.IdentityModel.Configuration.IdentityConfigurationElement> classe.  Una sezione di configurazione di identità è rappresentata dal <xref:System.IdentityModel.Configuration.IdentityConfiguration> classe.  
  
> [!IMPORTANT]
>  Specificare i seguenti elementi come elementi figlio del `<identityConfiguration>` elemento è stato dichiarato obsoleto, anche se il problema è ancora supportato per compatibilità con le versioni precedenti.  Questi elementi dovrebbero, invece, da specificare sotto il [\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) elemento.  
>   
>  -   [\<audienceUris\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/audienceuris.md)  
> -   [\<issuerNameRegistry\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuernameregistry.md)  
> -   [\<issuerTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuertokenresolver.md)  
> -   [\<serviceTokenResolver\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicetokenresolver.md)  
  
## Esempio  
 Nell'esempio seguente viene creata una configurazione di identità denominata "alternateConfiguration".  La configurazione di identità consente di specificare le impostazioni predefinite.  
  
```  
<system.identityModel>  
    <identityConfiguration name="alternateConfiguration"/>  
</system.identityModel>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Configuration.IdentityConfiguration>   
 <xref:System.IdentityModel.Configuration.IdentityConfigurationElement>