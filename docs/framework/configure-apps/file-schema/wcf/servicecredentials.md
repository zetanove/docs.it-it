---
title: "&lt;credenzialiServizio&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96db336c-4f7a-4193-81a5-910b8ffd804f
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;credenzialiServizio&gt;
Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.  
  
## Sintassi  
  
```  
  
<serviceCredentials type="String">  
   <clientCertificate>  
   </clientCertificate>  
   <issuedTokenAuthentication>  
   </issuedTokenAuthentication>  
   <peer>  
   </peer>  
   <secureConversationAuthentication>  
   </secureConversationAuthentication>  
   <serviceCertificate>  
   </serviceCertificate>  
   <userNameAuthentication>  
   </userNameAuthentication>  
   <windowsAuthentication>  
   </windowsAuthentication>  
</serviceCredentials>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`type`|Stringa che specifica il tipo di questo elemento di configurazione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificatoClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-servicecredentials.md)|Specifica il certificato client da usare quando il certificato client è disponibile fuori banda.  Questo elemento specifica anche impostazioni di convalida dei certificati client.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>.|  
|[\<autenticazioneTokenEmesso\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md)|Specifica il token corrente emesso per questo servizio.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement>.|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-servicecredentials.md)|Specifica le credenziali correnti per un nodo peer.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.PeerCredentialElement>.|  
|[\<autenticazioneConversazioneProtetta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationauthentication-of-servicecredential.md)|Specifica le credenziali correnti per una conversazione protetta.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.SecureConversationServiceElement>.|  
|[\<certificatoServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)|Specifica un certificato usato da un servizio per identificarsi.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.X509RecipientCertificateServiceElement>.|  
|[\<autenticazioneNomeUtente\>](../../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md)|Specifica le impostazioni per la convalida nome utente e password.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.UserNameServiceElement>.|  
|[\<autenticazioneWindows\>](../../../../../docs/framework/configure-apps/file-schema/wcf/windowsauthentication-of-servicecredentials.md)|Specifica le impostazioni per la convalida di credenziali Windows.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.WindowsServiceElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement>   
 <xref:System.ServiceModel.Description.ServiceCredentials>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)