---
title: "&lt;remove&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4058e2f1-7db4-4d1a-84dd-1b52836f2ae6
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;remove&gt;
Rimuove il gestore del token di protezione specificato dall'insieme del gestore del token.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <remove type=xs:string >  
      </remove>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Il nome del tipo CLR del token gestore da rimuovere.  Per ulteriori informazioni su come specificare il `type` di attributo, vedere [Custom Type References](http://msdn.microsoft.com/it-it/7286d2e3-c63d-49fd-abdc-ce2705f22c24).  Obbligatorio.|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|Specifica un insieme di gestori di token di protezione che sono registrati con l'endpoint.|  
  
## Esempio  
 Il file XML riportato di seguito viene illustrato come utilizzare il `<add>` e `<remove>` gli elementi per sostituire il gestore predefinito del token di sessione con un gestore del token di sessione personalizzato.  Da cui proviene il file XML di `ClaimsAwareWebFarm` campione.  
  
```  
<securityTokenHandlers>  
  <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
  <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
</securityTokenHandlers>  
```