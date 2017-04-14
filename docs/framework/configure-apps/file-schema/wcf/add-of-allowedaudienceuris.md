---
title: "&lt;add&gt; di &lt;allowedAudienceUris&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e7b7637-e0ea-4a91-988f-6b6ef28d9fc3
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;add&gt; di &lt;allowedAudienceUris&gt;
Aggiunge un URI di destinazione al quale il token di sicurezza <xref:System.IdentityModel.Tokens.SamlSecurityToken> può essere destinato affinché venga considerato valido da un'istanza di <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.  
  
## Sintassi  
  
```  
  
<allowedAudienceUris>   
   <add allowedAudienceUri="String"/>  
</allowedAudienceUris>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|allowedAudienceUri|Stringa che contiene un URI di destinazione a cui il token di sicurezza <xref:System.IdentityModel.Tokens.SamlSecurityToken> può essere destinato affinché venga considerato valido da un'istanza di <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<allowedAudienceUris\>](../../../../../docs/framework/configure-apps/file-schema/wcf/allowedaudienceuris.md)|Rappresenta una raccolta di URI di destinazione ai quali può essere destinato il token di sicurezza <xref:System.IdentityModel.Tokens.SamlSecurityToken> può essere destinato affinché venga considerato valido da un'istanza di <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.|  
  
## Note  
 Usare questa raccolta in un'applicazione federata che usa un servizio token di sicurezza \(STS, Security Token Service\) che emette token di sicurezza <xref:System.IdentityModel.Tokens.SamlSecurityToken>.  Quando emette il token di sicurezza, il servizio STS può specificare l'URI dei servizi Web per cui si desidera usare il token di sicurezza tramite l'aggiunta di una condizione <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> al token di sicurezza.  Ciò consente all'autenticatore <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> del servizio Web di destinazione di verificare che il token di sicurezza emesso sia associato a questo servizio Web specificando che questo controllo deve essere svolto mediante l'esecuzione delle operazioni seguenti:  
  
-   Impostare l'attributo `audienceUriMode` di `<issuedTokenAuthentication>` su <xref:System.IdentityModel.Selectors.AudienceUriMode> o <xref:System.IdentityModel.Selectors.AudienceUriMode>.  
  
-   Specificare il set di URI validi, aggiungendo gli URI a questa raccolta.  
  
 Per altre informazioni, vedere <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.  
  
 Per altre informazioni sull'utilizzo di questo elemento di configurazione, vedere [Procedura: configurare le credenziali in un servizio federativo](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).  
  
## Vedere anche  
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement.AllowedAudienceUris%2A>   
 <xref:System.ServiceModel.Configuration.AllowedAudienceUriElementCollection>   
 <xref:System.ServiceModel.Configuration.AllowedAudienceUriElement>   
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowedAudienceUris%2A>   
 [\<allowedAudienceUris\>](../../../../../docs/framework/configure-apps/file-schema/wcf/allowedaudienceuris.md)   
 [\<autenticazioneTokenEmesso\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md)   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Procedura: configurare le credenziali in un servizio federativo](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)