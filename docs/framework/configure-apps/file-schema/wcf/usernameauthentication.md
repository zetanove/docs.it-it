---
title: "&lt;autenticazioneNomeUtente&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24d8b398-770f-418f-ba23-c4325419cfa6
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;autenticazioneNomeUtente&gt;
Specifica le credenziali di un servizio in base a nome utente e password.  
  
## Sintassi  
  
```  
  
<userNameAuthentication  
   cacheLogonTokenLifetime="TimeSpan"  
   cacheLogonTokens="Boolean"   
   customUserNamePasswordValidatorType="String"  
   includeWindowsGroups="Boolean"   
   maxCacheLogonTokens="Integer"  
   membershipProviderName="String"  
   userNamePasswordValidationMode="Windows/MembershipProvider/Custom" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`cacheLogonTokenLifetime`|<xref:System.Timespan> specifica il periodo massimo di tempo durante il quale un token è memorizzato nella cache.  L'impostazione predefinita è 00:15:00.|  
|`cacheLogonTokens`|Valore booleano che specifica se i token di accesso vengono memorizzati nella cache.  Il valore predefinito è `false`.|  
|`customUserNamePasswordValidatorType`|Stringa che specifica il tipo di convalida personalizzata della password nome utente da usare.  Il valore predefinito è una stringa vuota.|  
|`includeWindowsGroups`|Valore booleano che specifica se i gruppi di Windows sono inclusi nel contesto di sicurezza.  Il valore predefinito è `true`.<br /><br /> L'impostazione di questo attributo su `true` determina un effetto sulle prestazioni in quanto comporta un'espansione completa del gruppo.  Impostare questa proprietà su `false` se non è necessario stabilire l'elenco di gruppi a cui appartiene un utente.|  
|`maxCacheLogonTokens`|Numero intero che specifica il numero massimo di token di accesso da memorizzare nella cache.  Questo valore deve essere maggiore di zero.  Il valore predefinito è 128.|  
|`membershipProviderName`|Quando l'attributo `clientCredentialType` di un'associazione viene impostato su `username`, viene eseguito il mapping del nome utente sugli account di Windows.  È possibile eseguire l'override di questo comportamento usando questo attributo, il quale è una stringa che contiene il nome del valore <xref:System.Web.Security.MembershipProvider> che fornisce il meccanismo di convalida della password appropriato.|  
|`userNamePasswordValidationMode`|Specifica il modo in cui viene convalidata la password del nome utente.  I valori validi sono:<br /><br /> -   Windows<br />-   MembershipProvider<br />-   Personalizza<br /><br /> L'impostazione predefinita è Windows.  L'attributo è di tipo <xref:System.ServiceModel.Security.UserNamePasswordValidationMode>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.|  
  
## Note  
 Se nessuna delle associazioni usate da un servizio viene configurata per l'autenticazione basata su nome utente\/password, gli attributi rilevanti per questo elemento vengono ignorate.  Tali attributi includono `customUserNamePasswordValidatorType`, `includeWindowsGroups`, `membershipProviderName` e `userNamePasswordValidationMode`.  
  
 Se nessuna delle associazioni usate da un servizio viene configurata per usare l'autenticazione di Windows per nome utente\/password, le impostazioni relative alla memorizzazione nella cache dei token di accesso vengono ignorate.  Tali impostazioni includono `cacheLogonTokenLifetime`, `cacheLogonTokens` e `maxCacheLogonTokens`.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.UserNameServiceElement>   
 <xref:System.ServiceModel.Description.ServiceCredentials.UserNameAuthentication%2A>   
 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.UserNameAuthentication%2A>