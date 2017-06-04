---
title: "Novit&#224; di Windows Identity Foundation 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b381f04-593b-471f-bd33-0362be1aade5
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# Novit&#224; di Windows Identity Foundation 4.5
La prima versione di Windows Identity Foundation \(WIF\) è stata rilasciata come download autonomo ed è nota come WIF 3.5 perché è stata introdotta nello stesso periodo di .NET 3.5 SP1.  Con .NET 4.5 WIF è diventato parte di .NET Framework.  La disponibilità delle classi di WIF direttamente nel framework stesso consente una maggiore integrazione dell'identità basata sulle attestazioni nella piattaforma .NET, semplificando così l'utilizzo delle attestazioni.  Le applicazioni scritte per WIF 3.5 devono essere modificate per poter usufruire del nuovo modello; per informazioni, vedere [Linee guida per la migrazione di un'applicazione compilata con le versioni di WIF dalla 3.5 alla 4.5](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md).  
  
 Di seguito sono descritti alcuni elementi di rilievo delle principali modifiche.  
  
## WIF fa ora parte di .NET Framework  
 Le classi di WIF sono ora estese tra vari assembly, i principali dei quali sono `mscorlib`, `System.IdentityModel`, `System.IdentityModel.Services` e `System.ServiceModel`.  Analogamente, le classi di WIF sono distribuite in diversi spazi dei nomi: <xref:System.Security.Claims?displayProperty=fullName>, diversi spazi dei nomi [System.IdentityModel](http://go.microsoft.com/fwlink/?LinkId=272004) e <xref:System.ServiceModel.Security?displayProperty=fullName>.  Lo spazio dei nomi <xref:System.Security.Claims?displayProperty=fullName> contiene le nuove classi <xref:System.Security.Claims.ClaimsPrincipal> e <xref:System.Security.Claims.ClaimsIdentity> \(vedere sotto\).  Tutte le entità in .NET ora derivano da <xref:System.Security.Claims.ClaimsPrincipal>.  Per informazioni dettagliate sugli spazi dei nomi di WIF e sui tipi di classi in essi contenute, vedere [Riferimento per le API di WPF](../../../docs/framework/security/wif-api-reference.md).  Per informazioni sulla corrispondenza degli spazi dei nomi tra WIF 3.5 e WIF 4.5, vedere [Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md).  
  
## Nuovi modello attestazioni e oggetto entità  
 Le attestazioni sono il nucleo fondamentale di .NET Framework 4.5. Le classi attestazione di base \(<xref:System.Security.Claims.Claim>, <xref:System.Security.Claims.ClaimsIdentity>, <xref:System.Security.Claims.ClaimsPrincipal>, <xref:System.Security.Claims.ClaimTypes> e <xref:System.Security.Claims.ClaimValueTypes>\) risiedono tutte direttamente in `mscorlib` nello spazio dei nomi <xref:System.Security.Claims?displayProperty=fullName>.  Non è più necessario utilizzare le interfacce per inserire le attestazioni nel sistema di identità .NET: <xref:System.Security.Principal.WindowsPrincipal>, <xref:System.Security.Principal.GenericPrincipal> e <xref:System.Web.Security.RolePrincipal> ora ereditano da <xref:System.Security.Claims.ClaimsPrincipal>; <xref:System.Security.Principal.WindowsIdentity>, <xref:System.Security.Principal.GenericIdentity> e <xref:System.Web.Security.FormsIdentity> ora ereditano da <xref:System.Security.Claims.ClaimsIdentity>.  In breve, ogni classe di entità consente ora di soddisfare le attestazioni.  Le interfacce e le classi di integrazione di WIF 3.5\(`WindowsClaimsIdentity`, `WindowsClaimsPrincipal`, `IClaimsPrincipal`, `IClaimsIdentity`\) sono state quindi rimosse.  Inoltre, la classe <xref:System.Security.Claims.ClaimsIdentity> ora espone i metodi che semplificano l'esecuzione di query sulla raccolta delle attestazioni di identità.  
  
## Modifiche all'esperienza di WIF 4.5 con Visual Studio  
  
-   La funzionalità di Visual Studio **Aggiungi riferimento STS …** \(utilità della riga di comando FedUtil\) è stata rimossa; al suo posto è possibile utilizzare la nuova estensione di Visual Studio **Identity and Access Tool for Visual Studio 2012**.  Ciò consente di attuare una federazione con un STS esistente o di utilizzare LocalSTS per eseguire i test delle soluzioni.  Una volta installata l'estensione, è possibile fare clic con il pulsante destro del mouse sul progetto e cercare **Identity and Access** nel menu di scelta rapida.  
  
-   I modelli ASP.NET e STS non sono più disponibili in quanto le attestazioni possono essere utilizzate direttamente nei modelli di progetto esistenti per ASP.NET, siti Web e WCF.  
  
-   I controlli nello spazio dei nomi `Microsoft.IdentityModel.Web.Controls` \(`SignInControl`, `FederatedPassiveSignInControl` e `FederatedPassiveSignInStatus`\) non sono disponibili in WIF 4.5.  
  
## Modifiche all'API di WIF 4.5  
  
-   In generale, le classi correlate alle attestazioni si trovano nello spazio dei nomi <xref:System.Security.Claims?displayProperty=fullName>; le classi correlate a WCF, i contratti di servizio, i canali, le channel factory e gli host di servizio che sono utilizzati per gli scenari WS\-Trust, si trovano in <xref:System.ServiceModel.Security?displayProperty=fullName>; tutte le altre classi di WIF sono distribuite tra i vari spazi dei nomi [System.IdentityModel](http://go.microsoft.com/fwlink/?LinkId=272004), incluse, ad esempio, le classi che rappresentano elementi WS\-\* e SAML, gestori di token e classi correlate e le classi utilizzate negli scenari di WS\-Federation.  Per ulteriori informazioni, vedere [Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md) e [Riferimento per le API di WPF](../../../docs/framework/security/wif-api-reference.md).  
  
-   La chiave del computer è stata abilitata per l'utilizzo nei cookie di sessione per gli scenari di web farm.  Per ulteriori informazioni, vedere [WIF e Web farm](../../../docs/framework/security/wif-and-web-farms.md).  
  
-   WIF deve ora essere configurato in modo dichiarativo sotto gli elementi [\<system.identityModel\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) e [\<system.identityModel.services\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md).  Per ulteriori informazioni sulla configurazione di WIF, vedere [Guida di riferimento per la configurazione di WIF](../../../docs/framework/security/wif-configuration-reference.md).  
  
## Altre modifiche o funzionalità significative di .NET determinate dall'integrazione di WIF in .NET  
  
-   In .NET Framework è stata integrata la possibilità di eseguire autorizzazioni basate su attestazioni \(CBAC\).  È possibile configurare un oggetto <xref:System.Security.Claims.ClaimsAuthorizationManager> e utilizzare le classi <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> e <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> per eseguire controlli di accesso imperativi e dichiarativi nel codice.  CBAC fornisce maggiore flessibilità e maggiore granularità rispetto ai tradizionali controlli dell'accesso basato su ruoli \(RBAC\).  Consente inoltre una maggiore separazione dei criteri di autorizzazioni dalla logica di business poiché la logica di business può basare il controllo dell'accesso su un'attestazione specifica o su un set di attestazioni e i criteri di autorizzazione per tali attestazioni possono essere configurati in modo dichiarativo sotto l'elemento [\<claimsAuthorizationManager\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md).  
  
## Modifiche a WCF come conseguenza dell'integrazione di WIF:  
  
-   Il modello di identità basato sulle attestazioni di WCF è stato sostituito da WIF.  Ciò significa che le classi negli spazi dei nomi <xref:System.IdentityModel.Claims?displayProperty=fullName>, <xref:System.IdentityModel.Policy?displayProperty=fullName> e <xref:System.IdentityModel.Selectors?displayProperty=fullName> devono essere eliminate a favore dell'utilizzo delle classi di WIF.  
  
-   WIF viene ora abilitato su un servizio WCF tramite la specifica dell'attributo `useIdentityConfiguration` nell'elemento `<system.serviceModel>`\/`<behaviors>`\/`<serviceBehaviors>`\/`<serviceCredentials>` come nel file XML seguente:  
  
    ```xml  
    <serviceCredentials useIdentityConfiguration="true">  
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->  
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />  
    </serviceCredentials>  
    ```  
  
     Quando si utilizza **Identity and Access Tool for Visual Studio 2012** \(tornare a **Modifiche all'esperienza con Visual Studio**\), tramite questo strumento viene automaticamente aggiunto un elemento `<serviceCredentials>` con l'attributo `useIdentityConfiguration` impostato sul file di configurazione.  Vengono inoltre aggiunti un elemento [\<system.identityModel\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) corrispondente che contiene le impostazioni di configurazione di WIF, un'associazione e altre impostazioni necessarie per delocalizzare l'autenticazione al servizio STS scelto.  
  
## Vedere anche  
 [Linee guida per la migrazione di un'applicazione compilata con le versioni di WIF dalla 3.5 alla 4.5](../../../docs/framework/security/guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)   
 [Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)   
 [Riferimento per le API di WPF](../../../docs/framework/security/wif-api-reference.md)   
 [Guida di riferimento per la configurazione di WIF](../../../docs/framework/security/wif-configuration-reference.md)