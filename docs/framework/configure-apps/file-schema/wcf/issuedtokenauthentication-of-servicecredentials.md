---
title: "&lt;issuedTokenAuthentication&gt; di &lt;serviceCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c2e288f-f603-4d13-839a-0fd6d1981bec
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;issuedTokenAuthentication&gt; di &lt;serviceCredentials&gt;
Specifica un token personalizzato emesso come credenziale del servizio.  
  
## Sintassi  
  
```  
  
<issuedTokenAuthentication   
   allowUntrustedRsaIssuers="Boolean"  
   audienceUriMode="Always/BearerKeyOnly/Never"  
      customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
   revocationMode="NoCheck/Online/Offline"  
   samlSerializer="String"  
    trustedStoreLocation="CurrentUser/LocalMachine">  
      <allowedAudienceUris>  
      <add allowedAudienceUri="String"/>  
      </allowedAudienceUris>  
      <knownCertificates>   
         <add findValue="String"  
                 storeLocation="CurrentUser/LocalMachine"  
                storeName=" CurrentUser/LocalMachine"  
                x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"/>  
      </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`allowedAudienceUris`|Ottiene il set di URI di destinazione a cui il token di sicurezza <xref:System.IdentityModel.Tokens.SamlSecurityToken> può essere destinato affinché sia considerato valido dall'istanza di un oggetto <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.  Per altre informazioni sull'utilizzo di questo attributo, vedere <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>.|  
|`allowUntrustedRsaIssuers`|Valore booleano che specifica se sono consentiti emittenti di certificati RSA non attendibili.<br /><br /> I certificati sono firmati dalle Autorità di certificazione \(CA\) per verificarne l'autenticità.  Un emittente non attendibile è un'autorità di certificazione che non è specificata come attendibile per la firma di certificati.|  
|`audienceUriMode`|Ottiene un valore che specifica se occorre convalidare la condizione <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> del token di sicurezza <xref:System.IdentityModel.Tokens.SamlSecurityToken>.  Questo valore è di tipo <xref:System.IdentityModel.Selectors.AudienceUriMode>.  Per altre informazioni sull'utilizzo di questo attributo, vedere <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>.|  
|`certificateValidationMode`|Imposta la modalità di convalida dei certificati.  Uno dei valori validi di <xref:System.ServiceModel.Security.X509CertificateValidationMode>.  Se impostato su `Custom`, è necessario fornire anche un `customCertificateValidator`.  Il valore predefinito è `ChainTrust`.|  
|`customCertificateValidatorType`|Stringa facoltativa.  Un tipo e un assembly usati per convalidare un tipo personalizzato.  Questo attributo deve essere impostato quando `certificateValidationMode` è impostato su `Custom`.|  
|`revocationMode`|Imposta la modalità di revoca che specifica se viene eseguito un controllo di revoca e se viene eseguito in linea o non in linea.  L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>.|  
|`samlSerializer`|Attributo stringa facoltativo che specifica il tipo di serializzatore SamlSerializer usato per la credenziale del servizio.  Il valore predefinito è una stringa vuota.|  
|`trustedStoreLocation`|Enumerazione facoltativa.  Uno di due percorsi dell'archivio di sistema: `LocalMachine` o `CurrentUser`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`knownCertificates`|Specifica una raccolta di elementi <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElement> che specificano emittenti attendibili per la credenziale del servizio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.|  
  
## Note  
 L'emissione di un token di autenticazione prevede tre fasi.  Nella prima fase, un client che tenta di accedere a un servizio viene reindirizzato a un *servizio token di sicurezza*.  Nella seconda fase, il servizio token di sicurezza autentica il client e quindi rilascia a quest'ultimo un token, in genere un token SAML \(Security Assertions Markup Language\),  che il client restituisce in seguito al servizio.  Nella terza fase, il servizio ricerca nel token appena ricevuto i dati da usare per autenticare il token stesso e, pertanto, il client.  Affinché il token venga autenticato è necessario che il servizio riconosca il certificato usato dal servizio token di sicurezza.  
  
 Questo elemento rappresenta il repository dei certificati usati dal servizio token di sicurezza.  Per aggiungere certificati, usare l'[\<certificatiNoti\>](../../../../../docs/framework/configure-apps/file-schema/wcf/knowncertificates.md).  Inserire un [\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-knowncertificates.md) per ogni certificato, come illustrato nell'esempio seguente.  
  
```  
<issuedTokenAuthorization>  
   <knownCertificates>  
      <add findValue="www.contoso.com"   
           storeLocation="LocalMachine" storeName="My"   
           X509FindType="FindBySubjectName" />  
    </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
 Per impostazione predefinita, i certificati devono essere ottenuti da un servizio token di sicurezza.  Questi certificati "riconosciuti" garantiscono che solo i client autorizzati siano in grado di accedere a un determinato servizio.  
  
 Per altre informazioni sull'utilizzo di questo elemento di configurazione, vedere [Procedura: configurare le credenziali in un servizio federativo](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).  
  
## Vedere anche  
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.IssuedTokenAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement>   
 <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A>   
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Procedura: configurare le credenziali in un servizio federativo](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)