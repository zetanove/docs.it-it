---
title: "&lt;samlSecurityTokenRequirement&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 09202d12-88d3-49cc-953b-703bcc1690eb
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;samlSecurityTokenRequirement&gt;
Fornisce la configurazione della classe <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>, la classe <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, o una classe derivata di uno di tali classi.  Rappresentato dalla classe <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement>.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement   
            issuerCertificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
            issuerCertificateRevocationMode="NoCheck||Offline||Online"  
            issuerCertificateTrustedStoreLocation="CurrentLocation||LocalMachine"  
            issuerCertificateValidator="Namespace.Class Assembly"  
            mapToWindows=xs:boolean  
          <nameClaimType value=xs:string />  
          <roleClaimType value=xs:string />  
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
|mapToWindows|Specifica se il gestore di eseguire il mapping del token convalidante a un account Windows utilizzando la richiesta in arrivo di UPN.  L'impostazione predefinita è “false„.|  
|issuerCertificateRevocationMode|Un valore <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> che specifica la modalità di revoca da utilizzare per il certificato X.509.  Il valore predefinito è “online„.|  
|issuerCertificateValidationMode|Un valore <xref:System.ServiceModel.Security.X509CertificateValidationMode> che specifica la modalità di convalida da utilizzare per il certificato X.509.  Il valore predefinito è “PeerOrChainTrust„.|  
|issuerCertificateTrustedStoreLocation|Un valore <xref:System.Security.Cryptography.X509Certificates.StoreLocation> che specifica archivio certificati X.509.  Il valore predefinito è “LocalMachine„.|  
|issuerCertificateValidator|Un tipo personalizzato che deriva da <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  Se l'attributo `issuerCertificateValidationMode` è custom, un'istanza di questo tipo consente di convalida del certificato dell'autorità.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<nameClaimType\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/nameclaimtype.md)|Imposta il tipo di attestazione che specifica la proprietà <xref:System.Security.Principal.IIdentity.Name%2A>.|  
|[\<roleClaimType\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/roleclaimtype.md)|Specifica il tipo di attestazione che definisce il ruolo di richieste del tipo della raccolta di oggetti <xref:System.Security.Claims.ClaimsIdentity> restituiti dal metodo <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> del gestore dei token.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|Aggiunge il gestore specificato del token di sicurezza alla raccolta dei token del gestore.|  
  
## Note  
 L'elemento `<samlSecurityTokenRequirement>` è rappresentato dalla classe <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> nel modello a oggetti e viene utilizzato per configurare la proprietà `SamlSecurityTokenRequirement` su <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> o su <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>.  
  
## Esempio  
  
```  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement issuerCertificateValidationMode="PeerOrChainTrust"  
                                  issuerCertificateRevocationMode="Online"  
                                  issuerCertificateTrustedStoreLocation="LocalMachine"  
                                  mapToWindows="false">  
  
        <nameClaimType value="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" />  
        <roleClaimType value="schemas.microsoft.com/ws/2006/04/identity/claims/role" />  
    </samlSecurityTokenRequirement>  
</add>  
```