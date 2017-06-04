---
title: "&lt;claimsAuthorizationManager&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9354eee3-f692-4ad6-8427-3169686b8bcc
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;claimsAuthorizationManager&gt;
Registra un gestore di autorizzazione di attestazioni per le attestazioni in ingresso.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthorizationManager type = xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthorizationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Un tipo personalizzato che deriva dal <xref:System.Security.Claims.ClaimsAuthorizationManager> classe.  Per ulteriori informazioni su come specificare il `type` di attributo, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).|  
  
### Elementi figlio  
 Se non vi è alcun `type` attributo, o se il `type` i riferimenti dell'attributo il <xref:System.Security.Claims.ClaimsAuthenticationManager> classe, il `<claimsAuthorizationManager>` elemento non ha elementi figlio; Tuttavia, le classi derivate da <xref:System.Security.Claims.ClaimsAuthorizationManager> possibile definire gli elementi di configurazione figlio.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni di identità a livello di servizio.|  
  
## Note  
 Il comportamento predefinito fornito tramite il <xref:System.Security.Claims.ClaimsAuthorizationManager> classe sempre autorizza le attestazioni in ingresso.  Se non `type` viene specificato o se il `type` attributo specifica la <xref:System.Security.Claims.ClaimsAuthorizationManager> classe, il `<claimsAuthorizationManager>` elemento non ha elementi figlio.  È possibile specificare il `type` attributo per registrare un tipo derivato dal <xref:System.Security.Claims.ClaimsAuthorizationManager> classe per implementare un comportamento personalizzato.  Le classi derivate è in grado di supportare la configurazione tramite gli elementi figlio del `<claimsAuthorizationManager>` elemento eseguendo l'override di <xref:System.Security.Claims.ClaimsAuthorizationManager.LoadCustomConfiguration%2A> metodo per gestire questi elementi.  Lo schema definito per gli elementi figlio è la finestra di progettazione della classe.  
  
> [!IMPORTANT]
>  Quando si utilizza il <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> o <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> classe per fornire il controllo di accesso basato sui crediti nel codice, la configurazione di identità a cui fa riferimento la `<federationConfiguration>` elemento configura i criteri utilizzati per prendere decisioni di autorizzazione e in Gestione autorizzazioni attestazioni.  Questo è vero, anche in scenari non sono passivi scenari Web, ad esempio un'applicazione che non è basata sul Web o applicazioni di Windows Communication Foundation \(WCF\).  Se l'applicazione non è un'applicazione Web passiva, la `<claimsAuthorizationManager>` l'elemento \(e relativi elementi del criterio figlio, se presente\) della configurazione dell'identità di cui si fa riferimento sono le uniche impostazioni applicate.  Tutte le altre impostazioni vengono ignorate.  Per ulteriori informazioni, vedere l'elemento [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md).  
  
 Questo elemento imposta il <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthorizationManager%2A?displayProperty=fullName> proprietà.  
  
## Esempio  
 il XML riportato di seguito viene illustrata la configurazione per un'autorizzazione di attestazioni manager implementa criteri composto da coppie di azione risorsa ognuna delle quali specifica combinazioni booleane delle domande che un richiedente deve possedere per eseguire l'azione sulla risorsa.  Il codice che implementa la gestione di autorizzazioni di attestazioni in grado di utilizzare questo criterio sono disponibili i `ClaimsBasedAuthorization` campione.  
  
```  
<system.identityModel>  
    <identityConfiguration>  
      <claimsAuthorizationManager type="ClaimsAuthorizationLibrary.MyClaimsAuthorizationManager, ClaimsAuthorizationLibrary">  
        <policy resource="http://localhost:28491/Developers.aspx" action="GET">  
          <or>  
            <claim claimType="http://schemas.microsoft.com/ws/2008/06/identity/claims/role" claimValue="developer" />  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
          </or>  
        </policy>  
        <policy resource="http://localhost:28491/Administrators.aspx" action="GET">  
          <and>  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
            <claim claimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country" claimValue="USA" />  
          </and>  
        </policy>  
        <policy resource="http://localhost:28491/Default.aspx" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/Claims.aspx" action="GET">  
        </policy>  
      </claimsAuthorizationManager>  
    <identityConfiguration>  
<system.identityModel>  
```