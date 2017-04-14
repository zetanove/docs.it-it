---
title: "&lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4712a888-f154-4395-8887-ef14a88a6497
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;add&gt;
Aggiunge il gestore del token di protezione specificato all'insieme di gestore del token.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type=xs:string>  
        <optionalConfigurationElement>  
        </optionalConfigurationElement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Il nome del tipo CLR del token gestore da aggiungere.  Per ulteriori informazioni su come specificare il `type` di attributo, vedere [Custom Type References](http://msdn.microsoft.com/it-it/7286d2e3-c63d-49fd-abdc-ce2705f22c24).|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<samlSecurityTokenRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/samlsecuritytokenrequirement.md)|Fornisce la configurazione per il <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> classe, il <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> classe o una classe derivata di una di queste classi.|  
|[\<sessionTokenRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessiontokenrequirement.md)|Fornisce la configurazione per il <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> classe o le classi derivate.|  
|[\<userNameSecurityTokenHandlerRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/usernamesecuritytokenhandlerrequirement.md)|Fornisce la configurazione per il <xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler> classe o le classi derivate.|  
|[\<x509SecurityTokenHandlerRequirement\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/x509securitytokenhandlerrequirement.md)|Fornisce la configurazione facoltativa per il <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler> classe o le classi derivate.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlers.md)|Specifica un insieme di gestori di token di protezione che sono registrati con l'endpoint.|  
  
## Note  
 Il `<add>` elemento può accettare un solo elemento figlio che specifica la configurazione per il gestore del token.  Ciò dipende se fare riferimento alla classe del gestore tramite il `type` attributo del `<add>` elemento fornisce il supporto per questa funzionalità.  Le classi del gestore di token che forniscono questa funzionalità devono esporre un costruttore che accetta un <xref:System.Xml.XmlElement> oggetto.  
  
```  
public class CustomTokenHandler : Microsoft.IdentityModel.Tokens.SecurityTokenHandler  
{  
    public CustomTokenHandler( XmlElement customConfig )  
    {  
    }  
}  
```  
  
 Molte delle classi di gestore del token di protezione incorporata offrono questa funzionalità.  These classes are <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, <xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>, and <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>.  
  
> [!IMPORTANT]
>  L'insieme di gestore del token può contenere solo un singolo gestore di un tipo.  Ciò significa, ad esempio, che se si desidera aggiungere un gestore che deriva dal <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> classe all'insieme, è necessario rimuovere il <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>, che è presente per impostazione predefinita, dall'insieme.  È possibile utilizzare la [\<remove\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/remove.md) elemento per rimuovere un singolo gestore dal insieme o utilizzare il [\<clear\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/clear.md) elemento da rimuovere tutti i gestori dall'insieme.  
  
 Le impostazioni specificate in un gestore di ignorare le impostazioni equivalenti specificate nell'insieme di gestore del token nel [\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) elemento e quelli specificati a livello di servizio sotto il [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento.  
  
## Esempio  
 Il file XML riportato di seguito viene illustrato come utilizzare il `<add>` e `<remove>` gli elementi per sostituire il gestore predefinito del token di sessione con un gestore del token di sessione personalizzato.  Da cui proviene il file XML di `ClaimsAwareWebFarm` campione.  
  
```  
<securityTokenHandlers>  
  <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
  <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
</securityTokenHandlers>  
```