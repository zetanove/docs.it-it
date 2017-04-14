---
title: "&lt;claimsAuthenticationManager&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d30a450-6d13-4671-81a8-77e0204500c5
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;claimsAuthenticationManager&gt;
Registra un amministratore di autenticazione delle richieste per le richieste in arrivo.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthenticationManager type=xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthenticationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Specifica un tipo personalizzato che deriva dalla classe di <xref:System.Security.Claims.ClaimsAuthenticationManager> .  per ulteriori informazioni su come specificare l'attributo di `type` , vedere .|  
  
### Elementi figlio  
 Se non c " è attributo di `type` , o se i riferimenti dell' attributo di `type` la classe di <xref:System.Security.Claims.ClaimsAuthenticationManager> , l'elemento di `<claimsAuthenticationManager>` non accetta gli elementi figlio; tuttavia, le classi derivate da <xref:System.Security.Claims.ClaimsAuthenticationManager> possono definire gli elementi di configurazione figlio.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni dell' identità del livello di servizio.|  
  
## Note  
 Il comportamento predefinito fornito con gli echi della classe di <xref:System.Security.Claims.ClaimsAuthenticationManager> le richieste in arrivo.  Se nessun attributo su `type` viene specificato o se l'attributo di `type` specifica la classe di <xref:System.Security.Claims.ClaimsAuthenticationManager> , l'elemento di `<claimsAuthenticationManager>` non accetta gli elementi figlio.  È possibile specificare l'attributo di `type` per registrare un tipo derivato dalla classe di <xref:System.Security.Claims.ClaimsAuthenticationManager> per implementare il comportamento personalizzato.  Le classi derivate possono supportare la configurazione dagli elementi figlio dell' elemento di `<claimsAuthenticationManager>` eseguendo l'override del metodo di <xref:System.Security.Claims.ClaimsAuthenticationManager.LoadCustomConfiguration%2A> per gestire tali elementi.  Lo schema definito per gli elementi figlio dipende fino alla finestra di progettazione della classe.  
  
 gli insiemi di elementi di `<claimsAuthenticationManager>` la proprietà di <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthenticationManager%2A?displayProperty=fullName> .  
  
## Esempio  
  
```  
<system.identityModel>  
    <identityConfiguration name=”MyIdentity”>  
      <claimsAuthenticationManager type="MyNamespace.CustomClaimsAuthenticationManager, MyAssembly"/>          
    </identityConfiguration>  
</microsoft.identityModel>  
```