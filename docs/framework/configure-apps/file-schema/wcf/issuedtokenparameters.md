---
title: "&lt;parametriTokenEmesso&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 120b3f37-7331-4816-b712-d6aab39655a4
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;parametriTokenEmesso&gt;
Specifica i parametri per un token di sicurezza emesso in uno scenario di sicurezza federata.  
  
## Sintassi  
  
```  
  
<issuedTokenParameters   
      DefaultMessageSecurityVersion="System.ServiceModel.MessageSecurityVersion"  
      inclusionMode="AlwaysToInitiator/AlwaysToRecipient/Never/Once"  
      keySize="Integer"  
   keyType="AsymmetricKey/BearerKey/SymmetricKey"  
      tokenType="String" >  
   <additionalRequestParameters />  
      <claimTypeRequirements>  
            <add claimType="URI"  
           isOptional="Boolean" />  
      </claimTypeRequirements>  
      <issuer address="String"   
                      binding=" " />  
      <issuerMetadata address="String" />   
</issuedTokenParameters>  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|defaultMessageSecurityVersion|Specifica le versioni delle specifiche di sicurezza \(WS\-Security, WS\-Trust, WS\-Secure Conversation e WS\-Security Policy\) che devono essere supportate dall'associazione.  Questo valore è di tipo <xref:System.ServiceModel.MessageSecurityVersion>.|  
|inclusionMode|Specifica i requisiti di inclusione del token.  L'attributo è di tipo <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>.|  
|keySize|Valore intero che specifica le dimensioni di chiave del token.  Il valore predefinito è 256.|  
|keyType|Valore valido di <xref:System.IdentityModel.Tokens.SecurityKeyType> che specifica il tipo di chiave.  Il valore predefinito è `SymmetricKey`.|  
|tokenType|Stringa che specifica il tipo di token.  L'impostazione predefinita è "http:\/\/docs.oasis\-open.org\/wss\/oasis\-wss\-saml\-token\-profile\-1.1\#SAML".|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<parametriRichiestaAggiuntivi\>](../../../../../docs/framework/configure-apps/file-schema/wcf/additionalrequestparameters-element.md)|Raccolta di elementi di configurazione che specificano parametri di richiesta aggiuntivi.|  
|[\<requisitiTipoAttestazione\>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-element.md)|Specifica una raccolta di tipi di attestazione obbligatori.<br /><br /> In un scenario federato, i servizi attestano i requisiti per le credenziali in ingresso.  Ad esempio, le credenziali in ingresso devono disporre di un certo set di tipi di attestazioni.  Ogni elemento di questa raccolta specifica i tipi di attestazione obbligatori e facoltativi previsti in una credenziale federata.|  
|[\<issuer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuer-of-issuedtokenparameters.md)|Elemento di configurazione che specifica l'endpoint che emette il token corrente.|  
|[\<issuerMetadata\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata-of-issuedtokenparameters.md)|Elemento di configurazione che specifica l'indirizzo dell'endpoint dei metadati dell'emittente del token.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<bootstrapConversazioneProtetta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)|Specifica i valori predefiniti usati per iniziare un servizio di conversazione protetta.|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|Specifica le opzioni di sicurezza di un'associazione personalizzata.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>   
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement>   
 <xref:System.ServiceModel.Configuration.SecurityElementBase.IssuedTokenParameters%2A>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [Sicurezza delle associazioni personalizzate](../../../../../docs/framework/wcf/samples/custom-binding-security.md)   
 [Identità del servizio e autenticazione](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [Federazione e token emessi](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [Funzionalità di sicurezza con associazioni personalizzate](../../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)   
 [Federazione e token emessi](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)