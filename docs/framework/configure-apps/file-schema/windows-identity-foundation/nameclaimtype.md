---
title: "&lt;nameClaimType&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 17514d95-f0f5-4789-8e28-346640dc227c
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;nameClaimType&gt;
Imposta il tipo di attestazione che specifica la proprietà <xref:System.Security.Principal.IIdentity.Name%2A>.  Il tipo di attestazione viene utilizzato per trovare <xref:System.Security.Claims.Claim> nella raccolta di oggetti <xref:System.Security.Claims.ClaimsIdentity> restituiti dal metodo <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> di questo gestore token.  Il valore della richiesta corrispondente viene quindi impostato come nome <xref:System.Security.Principal.IIdentity> generato da questo gestore token.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement>  
          <nameClaimType value=xs:string>  
          </nameClaimType>  
        </samlSecurityTokenRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|valore|Stringa che specifica l'uri che rappresenta il tipo di attestazione della richiesta di utilizzare per la proprietà <xref:System.Security.Principal.IIdentity.Name%2A>.  Obbligatorio.|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<samlSecurityTokenRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/samlsecuritytokenrequirement.md)|Fornisce la configurazione della classe <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>, la classe <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, o una classe derivata di uno di tali classi.|  
  
## Note  
 Gli insiemi di elementi `<nameClaimType>` la proprietà <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.NameClaimType%2A> quando un oggetto <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> viene inizializzato dalla configurazione.  
  
## Esempio  
  
```  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement>  
        <nameClaimType value="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" />  
    </samlSecurityTokenRequirement>  
</add>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement.NameClaimType%2A>