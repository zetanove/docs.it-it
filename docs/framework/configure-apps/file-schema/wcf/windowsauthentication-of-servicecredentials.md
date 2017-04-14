---
title: "&lt;windowsAuthentication&gt; di &lt;serviceCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e0709473-0997-4de3-8f49-783527309a48
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;windowsAuthentication&gt; di &lt;serviceCredentials&gt;
Specifica le impostazioni della credenziale di un servizio Windows.  
  
## Sintassi  
  
```  
  
<windowsAuthentication  
      allowAnonymousLogons="Boolean"  
      includeWindowsGroups="Boolean" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`includeWindowsGroups`|Attributo booleano facoltativo che specifica se il sistema include gruppi Windows nel contesto di sicurezza.  Il valore predefinito è `true`.<br /><br /> L'impostazione di questo attributo su `true` determina un effetto sulle prestazioni in quanto comporta un'espansione completa del gruppo.  Impostare questo attributo su `false` se non è necessario stabilire l'elenco di gruppi a cui appartiene un utente.|  
|`allowAnonymousLogons`|Attributo booleano facoltativo che specifica se sono consentiti chiamanti anonimi, non autenticati.  Il valore predefinito è `false`.<br /><br /> Quando l'attributo `clientCredentialType` di un'associazione è impostato su `Windows`, il sistema non consente i chiamanti anonimi.  Questo significa che l'accesso al sistema è consentito solo ai chiamanti autenticati del dominio o del gruppo di lavoro.  È possibile eseguire l'override di questo comportamento usando questo attributo.<br /><br /> Usare questa impostazione con estrema cautela.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.|  
  
## Note  
 Usare questo elemento per specificare se consentire l'accesso a utenti di Windows anonimi mediante l'impostazione dell'attributo `allowAnonymousLogons`.  È inoltre possibile specificare se includere le informazioni sul gruppo al quale appartengono gli utenti in AuthorizationContext mediante l'impostazione dell'attributo `includeWindowsGroups`.  Se l'attributo viene impostato su `true` \(impostazione predefinita\), il servizio sarà in grado di determinare i gruppi di Windows ai quali appartiene il client.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WindowsServiceElement>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.WindowsAuthentication%2A>   
 <xref:System.ServiceModel.Description.ServiceCredentials.WindowsAuthentication%2A>   
 <xref:System.ServiceModel.Security.WindowsServiceCredential>