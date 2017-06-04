---
title: "&lt;transport&gt; di &lt;ws2007HttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 692befa3-8b0b-4ec5-b601-755874e98eb0
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;transport&gt; di &lt;ws2007HttpBinding&gt;
Definisce le impostazioni di autenticazione per il trasporto HTTP.  
  
## Sintassi  
  
```  
  
transport clientCredentialType =   
       "Basic/Certificate/Digest/None/Ntlm/Windows"  
       proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
       realm="string"   
```  
  
## Tipo  
 <xref:System.ServiceModel.HttpTransportSecurity>  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`clientCredentialType`|Specifica la credenziale usata per autenticare il client presso il servizio.  L'attributo è di tipo <xref:System.ServiceModel.HttpClientCredentialType>.|  
|`proxyCredentialType`|Specifica la credenziale usata per autenticare il client presso un proxy di dominio.  L'attributo è di tipo <xref:System.ServiceModel.HttpProxyCredentialType>.|  
|`realm`|L'area di autenticazione per l'autenticazione di base o digest.  Il valore predefinito è una stringa vuota.<br /><br /> L'area di autenticazione specifica almeno il nome dell'host che esegue l'autenticazione.  Può inoltre specificare una raccolta di utenti aventi diritto di accesso.  Un utente può eseguire una query nell'area di autenticazione per determinare quale dei vari possibili nomi utente e password possono essere usati.|  
  
## Attributo clientCredentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|La sicurezza è disabilitata.|  
|Di base|Usa l'autenticazione di base.|  
|Digest|Usa l'autenticazione digest.|  
|Ntlm|Usa l'autenticazione NTLM come fallback con un dominio Windows.|  
|Windows|Usa l'autenticazione integrata di Windows.|  
|Certificato|Usa certificati X.509 per autenticare il client.|  
  
## Attributo proxyCredentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|La sicurezza è disabilitata.|  
|Di base|Usa l'autenticazione di base.|  
|Digest|Usa l'autenticazione digest.|  
|Ntlm|Usa NTLM come fallback con un dominio Windows.|  
|Windows|Usa l'autenticazione integrata di Windows.|  
|Certificato|Usa certificati X.509 per autenticare il client.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-ws2007httpbinding.md)|Rappresenta le funzionalità di sicurezza dell'elemento [\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md).|  
  
## Vedere anche  
 <xref:System.ServiceModel.HttpTransportSecurity>   
 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpTransportSecurityElement>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)