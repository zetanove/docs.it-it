---
title: "&lt;federationConfiguration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b14054c-6d07-46ab-ab58-03f14beac0f2
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# &lt;federationConfiguration&gt;
Consente di configurare il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) e il <xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) quando si utilizza l'autenticazione tramite il protocollo WS\-Federation una federazione.  Consente di configurare il <xref:System.Security.Claims.ClaimsAuthorizationManager> quando si utilizza il <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> o <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> classe per fornire il controllo di accesso basati sulle attestazioni.  
  
## Sintassi  
  
```  
<system.identityModel.services>  
  <federationConfiguration name=xs:string identityConfigurationName=xs:string>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Il nome di questo elemento di configurazione della federazione.  Questo attributo fornisce principalmente un punto di estendibilità per i protocolli futuri.  Parametro facoltativo.|  
|identityConfigurationName|Il nome della sezione di configurazione di identità come specificato in un [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento da utilizzare.  Se questo attributo non è specificato, viene utilizzata la sezione di configurazione predefinita di identità.  Parametro facoltativo.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<cookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|Consente di configurare il gestore del cookie utilizzato da SAM.  Parametro facoltativo.|  
|[\<serviceCertificate\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicecertificate.md)|Consente di configurare il certificato utilizzato per crittografare e decrittografare i token.  Parametro facoltativo.|  
|[\<wsFederation\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/wsfederation.md)|Consente di configurare il modulo di autenticazione WS\-Federation \(WSFAM\).  Parametro facoltativo.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.identityModel.services\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)|Sezione di configurazione per l'autenticazione utilizzando il protocollo WS\-Federation.|  
  
## Note  
 \<federationConfiguration\> elemento fornisce le impostazioni in due scenari diversi:  
  
-   Quando si utilizza WS\-Federation in un'applicazione Web passiva, l'elemento contiene impostazioni che configurano il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) e il <xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\).  Inoltre, fa riferimento la configurazione di identità da utilizzare per configurare i gestori di token di protezione e i certificati e i componenti quali Gestione autorizzazioni richieste e la gestione dell'autenticazione di attestazioni.  
  
-   Quando si utilizza il <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> o <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> di classe per fornire il controllo di accesso basato sui crediti nel codice, l'elemento fa riferimento la configurazione di identità che consente di configurare i criteri utilizzati per prendere decisioni di autorizzazione e in Gestione autorizzazioni attestazioni.  Questo è vero, anche in scenari non sono scenari Web passivi; ad esempio, le applicazioni di Windows Communication Foundation \(WCF\) o un'applicazione che non è basato sul Web.  Se l'applicazione non è un'applicazione Web passiva, la [\<claimsAuthorizationManager\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md) l'elemento \(e relativi elementi del criterio figlio, se presente\) della configurazione dell'identità a cui fa riferimento la `<federationConfiguration>` elemento sono le uniche impostazioni applicate.  Tutti gli altri vengono ignorati.  
  
 Indipendentemente dallo scenario verrà caricata la configurazione predefinita di federazione.  Il comportamento è definito come segue:  
  
1.  Se non vi è alcun `<federationConfiguration>` elemento presente, il runtime crea una configurazione della federazione e viene popolato con i valori predefiniti.  Questa configurazione di federazione predefinita fa riferimento la configurazione predefinita di identità.  
  
2.  Se un singolo `<federationConfiguration>` l'elemento è presente, è la configurazione di federazione predefinita indipendentemente se è denominato o senza nome.  Se il `identityConfiguration` viene specificato, a cui fa riferimento la configurazione di identità denominato; in caso contrario, la configurazione predefinita di identità viene fatto riferimento.  
  
3.  Se un senza nome `<federationConfiguration>` l'elemento è presente, è la configurazione predefinita di federazione.  Se il `identityConfiguration` viene specificato, a cui fa riferimento la configurazione di identità denominato; in caso contrario, la configurazione predefinita di identità viene fatto riferimento.  
  
4.  Se un nome più `<federationConfiguration>` gli elementi sono presenti e non senza nome `<federationConfiguration>` l'elemento è presente, viene generata un'eccezione.  
  
 In genere, una sola `<federationConfiguration>` sezione è definita.  In questa sezione è la configurazione predefinita di federazione.  È possibile specificare più, in modo univoco denominato `<federationConfiguration>` elementi; Tuttavia, in questo caso, se si desidera caricare una configurazione di federazione diverso da quello senza nome, è necessario fornire un gestore per il.  <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated>eventi e set di <xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=fullName> proprietà all'interno del gestore per un <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> oggetto inizializzato con i valori appropriati `<federationConfiguration>` elemento nel file di configurazione.  
  
 Il `<federationConfiguration>` elemento è rappresentato dal <xref:System.IdentityModel.Services.Configuration.FederationConfigurationElement> classe.  L'oggetto di configurazione è rappresentato dal <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> classe.  Un singolo <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> istanza è impostato sui <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName> proprietà e fornisce federati configurazione dell'applicazione.  
  
## Esempio  
 Nel XML seguente un `<federationConfiguration>` elemento che specifica le impostazioni per la WSFAM e specifica che il gestore di cookie predefinito \(un'istanza del <xref:System.IdentityModel.Services.ChunkedCookieHandler> classe\) utilizzabile da SAM.  
  
> [!WARNING]
>  In questo esempio, WSFAM né il gestore dei cookie sono necessari per utilizzare HTTPS.  Infatti, il `requireHttps` di attributo sul `<wsFederation>` elemento e il `requireSsl` attributo sul `<cookieHandlerElement>` sono `false`.  Queste impostazioni non sono consigliate per la maggior parte degli ambienti di produzione come essi possono presentare un rischio di protezione.  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation passiveRedirectEnabled="true"   
      issuer="http://localhost:15839/wsFederationSTS/Issue"   
      realm="http://localhost:50969/" reply="http://localhost:50969/"   
      requireHttps="false"   
      signOutReply="http://localhost:50969/SignedOutPage.html"   
      signOutQueryString="Param1=value2&Param2=value2"   
      persistentCookiesOnPassiveRedirects="true" />  
    <cookieHandler requireSsl="false" />  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>   
 <xref:System.IdentityModel.Services.SessionAuthenticationModule>   
 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>   
 [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)