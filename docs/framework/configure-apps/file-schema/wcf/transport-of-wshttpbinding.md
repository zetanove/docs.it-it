---
title: "&lt;transport&gt; di &lt;wsHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21e38acf-450a-4bda-82b6-de305e1f7cd8
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# &lt;transport&gt; di &lt;wsHttpBinding&gt;
Definisce le impostazioni di autenticazione per il trasporto HTTP.  
  
## Sintassi  
  
```  
  
<wsHttpBinding>  
    <binding>  
        <security mode=”None|Transport|TransportWithMessageCredential|TransportCredentialOnly”>  
            <transport  
            clientCredentialType="Basic|Certificate|Digest|None|Ntlm|Windows"  
            proxyCredentialType="Basic|Digest|None|Ntlm|Windows"  
            realm="string" />  
                <extendedProtectionPolicy policyEnforcement=”Never|WhenSupported|Always” protectionScenario=”TransportSelected|TrustedProxy”>  
                    <customServiceNames></customServiceNames>  
                </extendedProtecutionPolicy>  
            </transport>  
        </security>  
    </binding>  
</wsHttpBinding>  
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
|`realm`|Stringa che specifica l'area di autenticazione per l'autenticazione di base o digest.  Il valore predefinito è una stringa vuota.<br /><br /> L'area di autenticazione specifica almeno il nome dell'host che esegue l'autenticazione.  Può inoltre specificare una raccolta di utenti aventi diritto di accesso.  Un utente può eseguire una query nell'area di autenticazione per verificare i nomi utente e le password da usare tra quelli possibili.|  
|`policyEnforcement`|Questa enumerazione specifica il momento in cui deve essere applicato l'oggetto <xref:System.Security.Authentication.ExtendedProtectionPolicy>.<br /><br /> 1.  Never – I criteri non vengono mai applicati e la protezione estesa è disabilitata.<br />2.  WhenSupported – I criteri vengono applicati solo se il client supporta la protezione estesa.<br />3.  Always \- I criteri vengono sempre applicati.  L'autenticazione dei client che non supportano la protezione estesa avrà esito negativo.|  
  
## Attributo clientCredentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`None`|La sicurezza è disabilitata.|  
|`Basic`|Usa l'autenticazione di base.|  
|`Digest`|Usa l'autenticazione digest.|  
|`Ntlm`|Usa l'autenticazione NTLM come fallback con un dominio Windows.|  
|`Windows`|Usa l'autenticazione integrata di Windows.|  
|`Certificate`|Usa certificati X.509 per autenticare il client.|  
  
## Attributo proxyCredentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`None`|La sicurezza è disabilitata.|  
|`Basic`|Usa l'autenticazione di base.|  
|`Digest`|Usa l'autenticazione digest.|  
|`Ntlm`|Usa NTLM come fallback con un dominio Windows.|  
|`Windows`|Usa l'autenticazione integrata di Windows.|  
|`Certificate`|Usa certificati X.509 per autenticare il client.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)|Rappresenta le funzionalità di sicurezza di [\<wsHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).|  
  
## Vedere anche  
 <xref:System.ServiceModel.HttpTransportSecurity>   
 <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)