---
title: "&lt;customCookieHandler&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a03b153d-5ec6-4915-9031-6f0c3fd348be
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# &lt;customCookieHandler&gt;
Imposta il tipo di gestore di cookie personalizzati.  Può essere presente solo questo elemento se il `mode` attributo del `<cookieHandler>` elemento è "Custom".  Il tipo personalizzato deve essere derivato dal <xref:System.IdentityModel.Services.CookieHandler> classe.  
  
## Sintassi  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode=”Custom”>  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" >  
      </customCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Specifica un tipo personalizzato che deriva dal <xref:System.IdentityModel.Services.CookieHandler> classe.  Per ulteriori informazioni su come specificare il `type` di attributo, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<cookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|Consente di configurare il <xref:System.IdentityModel.Services.CookieHandler> che il <xref:System.IdentityModel.Services.SessionAuthenticationModule> viene utilizzata per leggere e scrivere i cookie.|  
  
## Note  
 Quando si specifica un gestore personalizzato cookie impostando il `mode` attributo del `<cookieHandler>` elemento "Personalizzato", è necessario specificare il tipo del gestore cookie personalizzato includendo un `<customCookieHandler>` elemento figlio che fa riferimento al tipo di gestore di cookie.  Questo elemento non può essere specificato quando il `mode` attributo è impostato su "Chunked" o "Default".  I gestori di cookie personalizzata devono derivare dal <xref:System.IdentityModel.Services.CookieHandler> classe.  
  
 Il `<customCookieHandler>` elemento è rappresentato dal <xref:System.IdentityModel.Configuration.CustomTypeElement> classe.  
  
## Esempio  
 Nell'esempio riportato di seguito consente di configurare il SAM per utilizzare un gestore di cookie personalizzati del tipo `MyNamespace.MyCustomCookieHandler`.  
  
```  
<cookieHandler mode="Custom">  
    <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
</cookieHandler>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Services.CookieHandler>