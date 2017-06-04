---
title: "Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a092d98c-444d-4336-a644-63c2e11e96c8
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5
A partire da .NET 4,5, Windows communications foundation \(WIF\) l'identità di Windows è stato completamente integrati in .NET Framework.  Le modifiche di nomi generati questa integrazione e un determinato consolidamento degli spazi dei nomi di WIF e l'api si verificano.  In questo argomento vengono fornite alcune indicazioni e un mapping generale tra gli spazi dei nomi di WIF 3,5 e gli spazi dei nomi di WIF 4,5.  Non devono essere ritenute esaustive, bensì fornisce alcune informazioni generali su sono disponibili le classi di informazioni WIF 3,5 in WIF 4,5.  Per informazioni più dettagliate sulle differenze tra WIF 3,5 e WIF 4,5, vedere [Novità di Windows Identity Foundation 4.5](../../../docs/framework/security/whats-new-in-wif.md).  Per informazioni su come eseguire la migrazione di applicazioni sviluppate in WIF 3,5 \- WIF 4,5, vedere [Linee guida per la migrazione di un'applicazione compilata con le versioni di WIF dalla 3.5 alla 4.5](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md).  
  
## Mapping dello spazio dei nomi di WIF 3,5 e 4,5 di WIF  
 Le classi di WIF, raccolte negli spazi dei nomi `Microsoft.IdentityModel` in WIF 3,5, verranno distribuiti tra i seguenti spazi dei nomi: `System.Security.Claims`, `System.ServiceModel.Security`e gli spazi dei nomi `System.IdentityModel` in WIF 4,5.  Anche gli spazi dei nomi di tutto WIF 3,5 sono stati consolidati o rilasciato stati completamente in WIF 4,5.  
  
> [!IMPORTANT]
>  I seguenti spazi dei nomi `System.IdentityModel` contengono classi che implementano il modello basato su richieste di identità WCF: <xref:System.IdentityModel.Claims?displayProperty=fullName>, <xref:System.IdentityModel.Policy?displayProperty=fullName>e <xref:System.IdentityModel.Selectors?displayProperty=fullName>.  Il modello basato su richieste di identità WCF viene sostituito da WIF.  Non utilizzare le classi nei tre spazi dei nomi durante la compilazione delle soluzioni basate su WIF.  
  
 Nella tabella seguente vengono fornite informazioni sulla posizione delle classi di WIF 3,5 sono disponibili in WIF 4,5.  
  
||||  
|-|-|-|  
|**Spazio dei nomi di WIF 3,5**|**Spazio dei nomi di WIF 4,5**|**Commenti**|  
|`Microsoft.IdentityModel`|<xref:System.IdentityModel?displayProperty=fullName>|-   La maggior parte delle classi che rappresentano le costanti non vengono implementate.<br />-   Classi utilizzate per compilare servizi token di sicurezza sono state spostate da `Microsoft.IdentityModel.SecurityTokenService` a <xref:System.IdentityModel?displayProperty=fullName>.<br />-   Le classi in `Microsoft.IdentityModel.Threading` sono state spostate in <xref:System.IdentityModel?displayProperty=fullName>.<br />-   Le classi `MruSecurityTokenCache` e `ExceptionMapper` non vengono implementate.|  
|`Microsoft.IdentityModel.Claims`|<xref:System.Security.Claims?displayProperty=fullName>|-   Le interfacce `IClaimsIdentity` e `IClaimsPrincipal` non vengono distribuite in WIF 4,5.  Anziché <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName> e <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> sono ora le classi di base da cui la maggior parte delle classi dell'oggetto principal e identity di.NET derivano.  Ciò significa che non è necessaria alcuna delle esigenze specifiche principale e classi di identità come `Microsoft.IdentityModel.Claims.WindowsClaimsPrincipal` e `Microsoft.IdentityModel.Claims.WindowsClaimsIdentity` in WIF 4,5, nell'utilizzo <xref:System.Security.Principal.WindowsPrincipal?displayProperty=fullName> e in <xref:System.Security.Principal.WindowsIdentity?displayProperty=fullName> anziché.  Lo stesso vale per altro per le altre richieste specifiche principale e le classi di identità esistenti in WIF 3,5.<br />-   La classe `Microsoft.IdentityModel.Claims.ClaimsCollection` non viene implementata in WIF 4,5.  Viceversa, le raccolte delle richieste vengono esposte come raccolte enumerabili di tipo <xref:System.Security.Claims.Claim?displayProperty=fullName>.<br />-   <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName> e <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> fornisce metodi che ora completamente supportano LINQ.|  
|`Microsoft.IdentityModel.Configuration`|<xref:System.IdentityModel.Configuration?displayProperty=fullName>|Alcuni elementi e classi hanno subito importanti di nome e alcuni sono stati rilasciati in WIF 4,5; ad esempio `Microsoft.IdentityModel.Configuraiton.ServiceConfiguration` è <xref:System.IdentityModel.Configuration.IdentityConfiguration?displayProperty=fullName>.|  
|`Microsoft.IdentityModel.Protocols`|<xref:System.IdentityModel.Services?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Protocols.WSFederation`|<xref:System.IdentityModel.Services?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Protocols.WSFederation.Metadata`|<xref:System.IdentityModel.Metadata?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Protocols.WSIdentity`|Non implementato in WIF 4,5|In WIF 3,5 contiene le classi per supportare CardSpace, non implementato in WIF 4,5.|  
|`Microsoft.IdentityModel.Protocols.WSTrust`|Divisione tra <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName> e gli spazi dei nomi <xref:System.ServiceModel.Security?displayProperty=fullName>.|Le classi che rappresenta gli elementi di WS\- Attendibilità nello spazio dei nomi <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName> ; ad esempio, la classe <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken>.  Le classi che rappresentano i contratti relativi ai servizi di servizi WCF, host del servizio e i canali che consentono a un servizio WCF per comunicare mediante il protocollo di WS\- Attendibilità nello spazio dei nomi <xref:System.ServiceModel.Security?displayProperty=fullName> ; ad esempio, la classe <xref:System.ServiceModel.Security.WSTrustServiceHost>.|  
|`Microsoft.IdentityModel.Protocols.WSTrust.Bindings`|Non implementato in WIF 4,5|\-|  
|`Microsoft.IdentityModel.Protocols.XmlEncryption`|Non implementato in WIF 4,5|Classi contenute che rappresentano le costanti di crittografia XML in WIF 3,5.  Queste costanti non vengono distribuite in WIF 4,5.|  
|`Microsoft.IdentityModel.Protocols.XmlSignature`|<xref:System.IdentityModel?displayProperty=fullName>|La classe e le classi `EnvelopingSignature` che rappresentano le costanti non vengono implementate.|  
|`Microsoft.IdentityModel.SecurityTokenService`|Divisione tra <xref:System.IdentityModel?displayProperty=fullName>, <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName>e gli spazi dei nomi <xref:System.IdentityModel.Tokens?displayProperty=fullName>.|\-|  
|`Microsoft.IdentityModel.Threading`|<xref:System.IdentityModel?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Tokens`|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Tokens.Saml11`|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Tokens.Saml2`|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Web`|<xref:System.IdentityModel.Services?displayProperty=fullName>|\-|  
|`Microsoft.IdentityModel.Web.Configuration`|<xref:System.IdentityModel.Services.Configuration?displayProperty=fullName>|Le classi che forniscono la configurazione per scenari passivi \(WS\- Federazione\) in gran parte sono state spostate in <xref:System.IdentityModel.Services.Configuration?displayProperty=fullName>; tuttavia, alcune di queste classi sono in <xref:System.IdentityModel.Services?displayProperty=fullName>.|  
|`Microsoft.IdentityModel.Web.Controls`|Non implementato in WIF 4,5|Le classi in `Microsoft.IdentityModel.Web.Controls` implementata il passivo organizzato in modo federativo con segno nel controllo, che non esiste in WIF 4,5.|  
|`Microsoft.IdentityModel.WindowsTokenService`|Non implementato in WIF 4,5|\-|  
  
## Vedere anche  
 [Novità di Windows Identity Foundation 4.5](../../../docs/framework/security/whats-new-in-wif.md)   
 [Linee guida per la migrazione di un'applicazione compilata con le versioni di WIF dalla 3.5 alla 4.5](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)