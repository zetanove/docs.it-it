---
title: "&lt;credenzialiClient&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e6eef0d-a34e-4d74-b0f7-f65d2181858d
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;credenzialiClient&gt;
Specifica le credenziali usate per autenticare il client presso un servizio.  
  
## Sintassi  
  
```  
  
<clientCredentials type="String"  
      supportInteractive="Boolean" >  
   <clientCertificate>  
   </clientCertificate>  
   <digest>  
   </digest>  
   <isuedToken>  
   </isuedToken>  
   <peer>  
   </peer>  
   <serviceCertificate>  
   </serviceCertificate>  
   <windowsAuthentication>  
   </windowsAuthentication>  
</clientCredentials>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`supportInteractive`|Valore booleano che specifica se un utente interattivo può essere coinvolto nella selezione di una credenziale client in fase di esecuzione.  Il valore predefinito è `true`.|  
|`type`|Stringa che specifica il tipo di questo elemento di configurazione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificatoClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md)|Specifica il certificato usato per autenticare il client presso il servizio.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.X509InitiatorCertificateClientElement>.|  
|[\<httpDigest\>](../../../../../docs/framework/configure-apps/file-schema/wcf/httpdigest-element.md)|Specifica un digest usato per autenticare il client presso il servizio.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.HttpDigestClientElement>.|  
|[\<tokenEmesso\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)|Specifica un tipo di token personalizzato usato per autenticare il client presso un servizio token di sicurezza \(STS, Secure Token Service\).  L'elemento è di tipo <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>.|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-clientcredentials-element.md)|Specifica una credenziale peer corrente.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.PeerCredentialElement>.|  
|[\<certificatoServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)|Specifica il certificato usato per autenticare il servizio presso il client e fornisce una struttura per l'impostazione delle opzioni del certificato.  Questo certificato deve essere fornito fuori banda dal servizio al client.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>.|  
|[\<finestre\>](../../../../../docs/framework/configure-apps/file-schema/wcf/windows-of-clientcredentials-element.md)|Specifica una credenziale Windows.  Il valore predefinito è la credenziale del thread corrente.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.WindowsClientElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un comportamento dell'endpoint.|  
  
## Note  
 Le credenziali client sono usate per autenticare i client presso i servizi nei casi in cui non è richiesta l'autenticazione reciproca.  È inoltre possibile usare questa sezione di configurazione per specificare i certificati di servizio negli scenari in cui il client deve usare il certificato di un servizio per proteggere i messaggi inviati a un servizio.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)