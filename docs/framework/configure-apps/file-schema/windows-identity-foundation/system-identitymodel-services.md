---
title: "&lt;system.identityModel.services&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa1624dd-2d74-4ae3-942e-498cee261ac5
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# &lt;system.identityModel.services&gt;
Sezione di configurazione per l'autenticazione utilizzando il protocollo WS\-Federation.  
  
 \<system.identityModel.services\>  
  
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
 Nessuno  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)|Contiene le impostazioni che configurano il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) e il <xref:System.IdentityModel.Services.SessionAuthenticationModule> moduli HTTP \(SAM\).|  
  
### Elementi padre  
 Nessuno  
  
## Note  
 Aggiungere una `<system.identityModel.services>` sezione al file di configurazione dell'applicazione per fornire le impostazioni per il SAM e WSFAM.  
  
> [!IMPORTANT]
>  Quando si utilizza il <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> o la <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> classe per fornire il controllo di accesso basato sui crediti nel codice, attestazioni authorization manager \(<xref:System.Security.Claims.ClaimsAuthorizationManager>\) e criteri utilizzati per prendere decisioni di autorizzazione vengono configurati mediante un `<identityConfiguration>` elemento a cui fa riferimento in modo implicito o esplicito da un `<federationConfiguration>` elemento in questa sezione.  Per ulteriori informazioni, vedere la  **note** sotto il [\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) elemento.  
  
 Il `<system.identityModel.services>` sezione è rappresentato dal <xref:System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection> classe.  L'insieme di figlio `<federationConfiguration>` elementi configurati nella sezione è rappresentato dal <xref:System.IdentityModel.Services.Configuration.FederationConfigurationElementCollection> classe.  
  
## Esempio  
 Il file XML riportato di seguito viene illustrato come aggiungere una `<system.identityModel.services>` sezione in un file di configurazione.  È innanzitutto necessario aggiungere le dichiarazioni di sezione per entrambi i `<system.identityModel.services>` sezione e il `<system.identityModel>` le sezioni.  \(Quando si aggiunge un `<system.identityModel.services>` sezione, è inoltre necessario aggiungere una dichiarazione per il `<system.identityModel>` sezione per garantire che un valore predefinito `<identityConfiguration>` sezione può essere creati da Common Language runtime, se necessario.\) Dopo aver aggiunto le dichiarazioni di sezione, è possibile configurare le impostazioni di autenticazione federata sotto il `<system.identityModel.services>` elemento.  
  
```  
<configuration>  
  <configSections>  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
  </configSections>  
  
  <!-- Additional elements (not shown) -->  
  
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
  
</configuration>  
```