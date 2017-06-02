---
title: "Linee guida per la migrazione di un&#39;applicazione compilata con le versioni di WIF dalla 3.5 alla 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7a32fe6e-5f68-4693-9371-19411fa8063c
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# Linee guida per la migrazione di un&#39;applicazione compilata con le versioni di WIF dalla 3.5 alla 4.5
## Si applica a  
  
-   Foundation \(WIF\) 3,5 e 4,5 di identità di Microsoft® Windows®.  
  
## Panoramica  
 Communications foundation \(WIF\)identità Windows è stato originariamente rilasciato nel calendario di .NET framework 3.5 SP1.  Tale versione di WIF è denominato WIF 3,5.  È stata rilasciata come il runtime e SDK separati, nel modo che ogni computer in cui un'applicazione WIF\- abilitata ha funzionato doveva eseguire il runtime di WIF installare e gli sviluppatori hanno dovuto scaricare e installare il WIF SDK per ottenere i modelli e sugli strumenti di Visual Studio che hanno consentito lo sviluppo di applicazioni WIF\- abilitate.  A partire da .NET 4.5, WIF è stato completamente integrati in .NET Framework.  Del runtime distinte non sono più necessari e la gli strumenti di WIF può essere installata in Visual Studio 2012 utilizzando gestione di estensioni di Visual Studio.  Questa versione di WIF è denominato WIF 4,5.  
  
 L'integrazione di WIF in .NET motivo è necessario diverse modifiche nella superficie di WIF API.  WIF 4,5 include nuovi spazi dei nomi, alcune modifiche agli elementi di configurazione e la nuova gli strumenti di Visual Studio.  In questo argomento vengono fornite istruzioni che è possibile utilizzare per eseguire la migrazione di applicazioni sviluppate in WIF 3,5 \- WIF 4,5. Possono verificarsi situazioni in cui è necessario eseguire le applicazioni legacy compilati utilizzando WIF 3,5 nei computer che eseguono Windows 8 o Windows Server 2012.  In questo argomento vengono fornite indicazioni sull'attivazione WIF 3,5 per questi sistemi operativi.  
  
## Modifiche richieste per WIF 4,5  
 Questa sezione descrive le modifiche necessarie per eseguire la migrazione di un'applicazione di WIF WIF 3,5 a 4,5.  
  
### Modifiche dello spazio dei nomi e assembly  
 WIF In 3,5, tutte le classi di WIF erano contenute nell'assembly `Microsoft.IdentityModel` \(microsoft.identitymicrosoft.identitymodel.dll\).  WIF In 4,5, le classi di WIF sono state suddivise negli assembly seguenti: `mscorlib` \(mscorlib.dll\), `System.IdentityModel` \(System.IdentityModel.dll\), `System.IdentityModel.Services` \(System.IdentityModel.Services.dll\) e `System.ServiceModel` \(System.ServiceModel.dll\).  
  
 Tutte le classi di WIF 3,5 erano contenute in uno degli spazi dei nomi `Microsoft.IdentityModel` ; ad esempio, `Microsoft.IdentityModel`, `Microsoft.IdentityModel.Tokens`, `Microsoft.IdentityModel.Web`, e così via.  WIF In 4,5, le classi di WIF verranno estese negli [System.IdentityModel](http://go.microsoft.com/fwlink/?LinkId=272004) spazi dei nomi, lo spazio dei nomi <xref:System.Security.Claims?displayProperty=fullName> e lo spazio dei nomi <xref:System.ServiceModel.Security?displayProperty=fullName>.  Oltre alla riorganizzazione, le classi di tutto WIF 3,5 sono state rilasciate in WIF 4,5.  
  
 Nella tabella seguente sono illustrati alcuni degli spazi dei nomi più importanti di WIF 4,5 e il tipo di classi che contengono.  Per informazioni dettagliate su come eseguire il mapping di spazi dei nomi WIF tra 3,5 e 4,5 WIF e sugli spazi dei nomi e classi che sono stati rilasciati in WIF 4,5, vedere [Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md).  
  
|Spazio dei nomi di WIF 4,5|Descrizione|  
|--------------------------------|-----------------|  
|<xref:System.IdentityModel?displayProperty=fullName>|Contiene le classi che rappresentano le trasformazioni del cookie, i servizi token di sicurezza e i lettori specifici del dizionario XML.  Contiene le classi dai seguenti spazi dei nomi di WIF 3,5: `Microsoft.IdentityModel`, `Microsoft.IdentityModel.SecurityTokenService` e `Microsoft.IdentityModel.Threading`.|  
|<xref:System.Security.Claims?displayProperty=fullName>|Contiene le classi che rappresentano le richieste, le identità in base a requisiti, le entità di sicurezza basate richieste e altri elementi del modello di identità base richieste.  Contiene le classi dello spazio dei nomi `Microsoft.IdentityModel.Claims`.|  
|<xref:System.IdentityModel.Tokens?displayProperty=fullName>|Contiene le classi che rappresentano i token di sicurezza, i gestori del token di sicurezza e altri elementi del token di sicurezza.  Contiene le classi dai seguenti spazi dei nomi di WIF 3,5: `Microsoft.IdentityModel.Tokens`, `Microsoft.IdentityModel.Tokens.Saml11` e `Microsoft.IdentityModel.Tokens.Saml2`.|  
|<xref:System.IdentityModel.Services?displayProperty=fullName>|Contiene le classi utilizzate negli scenari passivi o di WS\- federazione\).  Contiene le classi dello spazio dei nomi `Microsoft.IdentityModel.Web`.|  
|<xref:System.ServiceModel.Security?displayProperty=fullName>|Le classi che rappresentano i contratti WCF, i canali, host del servizio e altri elementi utilizzati in scenari attivi \(WS\- di attendibilità\) sono ora presenti in questo spazio dei nomi.  WIF In 3,5, queste classi sono nello spazio dei nomi `Microsoft.IdentityModel.Protocols.WSTrust`.|  
  
> [!IMPORTANT]
>  I seguenti spazi dei nomi `System.IdentityModel` contengono classi che implementano il modello basato su richieste di identità WCF: <xref:System.IdentityModel.Claims?displayProperty=fullName>, <xref:System.IdentityModel.Policy?displayProperty=fullName> e <xref:System.IdentityModel.Selectors?displayProperty=fullName>.  Il modello basato su richieste di identità WCF viene sostituito da WIF.  Non utilizzare le classi nei tre spazi dei nomi durante la compilazione di soluzioni basate su WIF.  
  
### Modifiche a causa di integrazione di .NET  
 WIF è integrato in .NET Framework.  La maggior parte delle classi di identità e principali di .NET ora derivano da <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> e <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>.  I risultati nelle seguenti modifiche in WIF 4,5:  
  
-   Le classi di WIF che rappresentano le richieste, le identità e le entità ora presenti nello spazio dei nomi <xref:System.Security.Claims?displayProperty=fullName>.  
  
    > [!IMPORTANT]
    >  Lo spazio dei nomi <xref:System.IdentityModel.Claims?displayProperty=fullName> contiene classi che rappresentano elementi al modello basato su richieste di identità WCF.  Molte di queste classi hanno nomi che corrispondono alle classi di WIF; ad esempio, `Claims`.  Non utilizzare queste classi per la compilazione di soluzioni basate su WIF.  
  
-   le classi di identità e principali di .NET ora derivano direttamente da <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> e <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>, che rappresentano a identità e alle entità in base a requisiti.  Per questo motivo, interfacce `IClaimsIdentity` di WIF 3,5 e `IClaimsPrincipal` più necessarie e non sono disponibili in WIF 4,5.  
  
-   Le classi di identità e dell'entità di Because.NET come <xref:System.Security.Principal.WindowsIdentity?displayProperty=fullName> e <xref:System.Security.Principal.WindowsPrincipal?displayProperty=fullName> ora derivano da <xref:System.Security.Claims.ClaimsIdentity> e <xref:System.Security.Claims.ClaimsPrincipal>, dispongono di funzionalità incorporate delle richieste.  Per questo motivo, le classi specifiche sull'oggetto principal e identity come `WindowsClaimsIdentity` e `WindowsClaimsPrincipal` che erano presenti in WIF 3,5 più necessarie e non in WIF 4,5.  
  
### Altre modifiche alle funzionalità di WIF  
 Oltre alle modifiche dello spazio dei nomi e le modifiche a causa di integrazione con .NET, le modifiche seguenti generali sulle funzionalità di WIF si verificano in WIF 4,5.  
  
-   La classe `Microsoft.IdentityModel.ExceptionMapper`, che fornivano la funzionalità che consentiva di eseguire il mapping delle eccezioni errori SOAP specifici, viene rimossa.  
  
-   La superficie di eccezione è stata molto ridotta.  
  
-   Molte classi che il protocollo definito o costanti specifiche di WS\-\* è stata eliminata; ad esempio, la classe `Microsoft.IdentityModel.WSAddressing10Constants`, che definisce le costanti correlate a WS\-Addressing 1,0.  
  
-   I reclami il servizio token di Windows \(c2wts\) e le classi collegate nello spazio dei nomi `Microsoft.IdentityModel.WindowsTokenService` vengono rimossi.  
  
### Modifiche di configurazione di WIF  
 Molte delle modifiche nel file di configurazione sono state causate dagli aggiornamenti dello spazio dei nomi in WIF 4,5. Ad esempio, si consideri la seguente voce di WIF 3,5 nella sezione `<httpModules>` di aggiungere l'amministratore di autenticazione di WS\- federazione a un'applicazione:  
  
```  
<add name="WSFederationAuthenticationModule" type="Microsoft.IdentityModel.Web.WSFederationAuthenticationModule, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=abcd … 5678" />  
```  
  
 Questa voce è stata aggiornata in WIF 4,5 per includere nuovi spazi dei nomi e versione di assembly:  
  
```  
<add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcd … 5678"/>  
```  
  
 Nell'elenco enumera modifiche essenziali al file di configurazione per WIF 4,5.  
  
-   La sezione `<microsoft.identityModel>` è la sezione [\<system.identityModel\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md).  
  
-   L'elemento `<service>` è l'elemento [\<identityConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md).  
  
-   Una nuova sezione, [\<system.identityModel.services\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md), è stata aggiunta per specificare le impostazioni del comportamento del controllo negli scenari passivi o di WS\- federazione\).  
  
-   L'elemento [\<federationConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) e i relativi elementi figlio sono stati spostati dall'elemento `<service>` in WIF 3,5 al nuovo elemento `<system.identityModel.services>`.  
  
-   Diversi elementi che possono essere specificati a livello di servizio direttamente sotto l'elemento `<service>` in WIF 3,5 sono stati limitati a essere specificato sotto l'elemento [\<securityTokenHandlerConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md). \(Possono comunque essere specificati nell'elemento [\<identityConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) in WIF 4,5 per compatibilità con le versioni precedenti\).  
  
 Per un elenco completo degli elementi di configurazione di WIF 4,5, vedere [Schema di configurazione di WIF](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/index.md).  
  
### Modifiche degli strumenti di Visual Studio  
 WIF Il 3,5 SDK ha fornito un'utilità di federazione autonoma, FedUtil.exe \(FedUtil\), utilizzabili per delocalizzare la gestione di identità nelle applicazioni WIF\- attivate in un servizio token di sicurezza \(STS\).  Questo strumento è stato aggiunto le impostazioni di WIF al file di configurazione dell'applicazione per abilitare l'applicazione ottenere i token di sicurezza da uno o più servizio token di sicurezza ed è stato sorto in Visual Studio tramite il pulsante **Aggiungi riferimento a servizio STS**.  FedUtil non fornisce con WIF 4,5. Invece, WIF 4,5 supporta una nuova estensione di Visual Studio denominata lo strumento di accesso e di identità per Visual Studio 2012 che è possibile utilizzare per modificare il file di configurazione dell'applicazione e le impostazioni di WIF richieste per delocalizzare la gestione di identità a un servizio token di sicurezza.  L'identità e di accesso implementa anche un STS Locale denominato servizio token di sicurezza che è possibile utilizzare per testare le applicazioni WIF\- abilitate.  In molti casi, questa funzionalità previene di dover compilare custom servizio token di sicurezza che era spesso necessaria in WIF 3,5 da verificare le soluzioni in fase di sviluppo.  Per questo motivo, i modelli di servizio token di sicurezza non sono più supportati in Visual Studio 2012; tuttavia, le classi che supportano lo sviluppo di servizio token di sicurezza ancora disponibili in WIF 4,5.  
  
 È possibile configurare l'identità e di accesso dalle estensioni e aggiornate l'amministratore in Visual Studio o è possibile scaricarlo dalla seguente pagina nel sito web MSDN code gallery: [Strumento di accesso e di identità per Visual Studio 2012 nella raccolta di codice](http://go.microsoft.com/fwlink/?LinkID=245849).  Le modifiche degli strumenti di Visual Studio sono riepilogate nell'elenco seguente:  
  
-   La funzionalità di riferimento al servizio aggiunta di servizio token di sicurezza viene rimossa.  La sostituzione è lo strumento di accesso e di identità.  
  
-   I modelli di Visual Studio servizio token di sicurezza vengono rimossi.  È possibile utilizzare il locale servizio token di sicurezza disponibili tramite lo strumento di accesso e di identità per verificare le soluzioni di identità che si sviluppano con WIF.  La configurazione locali servizio token di sicurezza possono essere modificato per personalizzare le richieste che serve.  
  
-   L'utilità di federazione autonoma \(FedUtil\) non è disponibile in WIF 4,5. È possibile utilizzare l'identità e di accesso per modificare i file di configurazione per delocalizzare la gestione di identità a un servizio token di sicurezza.  
  
 Per ulteriori informazioni sull'identità e sullo strumento di accesso, vedere [Identity and Access Tool per Visual Studio 2012](../../../docs/framework/security/identity-and-access-tool-for-vs.md)  
  
<a name="BKMK_ToolingChanges"></a>   
### Scenari passivi o di WS\- federazione\):  
  
-   Le classi che supportano scenari passivi sono state spostate nello spazio dei nomi <xref:System.IdentityModel.Services?displayProperty=fullName>.  In queste classi di WIF 3,5 sono nello spazio dei nomi `Microsoft.IdentityModel.Web`.  
  
-   Le classi nello spazio dei nomi `Microsoft.IdentityModel.Web.Configuration` sono state spostate in <xref:System.IdentityModel.Services.Configuration?displayProperty=fullName>.  Queste classi rappresentano oggetti specifici della configurazione negli scenari passivi.  
  
-   `FederatedPasssiveSignInControl` non è più supportato; tutte le classi nello spazio dei nomi `Microsoft.IdentityModel.Web.Controls` sono state rimosse da WIF 4,5.  
  
-   La funzionalità del segno \(first\-in del modulo autenticazione di WS\- federazione \(<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>\) è diverso da WIF 3,5.  Per ulteriori informazioni sul funzionamento del segno \(first\-in in WIF 4,5, vedere l'argomento relativo alle classi <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>.  
  
### Scenario attivo \(WCF\/WS\-Trust\):  
  
-   Lo spazio dei nomi `Microsoft.IdentityModel.Protocols.WSTrust` è stato suddiviso principalmente in due spazi dei nomi in WIF 4,5. Le classi che rappresentano elementi specifici del protocollo di WS\- attendibilità sono ora in <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName>.  Incluse le classi come <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken>.  Le classi che rappresentano i contratti di servizio, i canali, host del servizio e altri elementi che sono inclusi in utilizzare ws\-trust nelle applicazioni WCF sono state spostate in <xref:System.ServiceModel.Security?displayProperty=fullName>; ad esempio, l'interfaccia <xref:System.ServiceModel.Security.IWSTrust13AsyncContract>.  
  
-   La configurazione di un'applicazione WCF utilizzare WIF notevolmente è stato semplificato.  In `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement` doveva essere aggiunto come estensione del comportamento e questa funzionalità è stata quindi utilizzata per incuneare WIF nel comportamento del servizio specificando un elemento `<federatedServiceHostConfiguration>`.  WIF 4,5 è stato integrato \(IDE\) sono strettamente con il WCF.  Ora si abilita WIF in un servizio WCF specificando l'attributo `useIdentityConfiguration` da `<system.serviceModel>``<behaviors>`\/\/\/`<serviceBehaviors>` elemento`<serviceCredentials>` come nel seguente codice XML:  
  
    ```xml  
    <serviceCredentials useIdentityConfiguration="true">  
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->  
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />  
    </serviceCredentials>  
    ```  
  
-   WIF 4,5 Nel certificato del servizio utilizzato da un servizio WCF \(attivo\) deve essere specificato nell'host del servizio.  Nella configurazione, è possibile procedere con `<system.serviceModel>``<behaviors>`\/\/\/`<serviceBehaviors>``<serviceCredentials>`\/elemento`<serviceCertificate>` come illustrato nell'esempio precedente.  WIF 3,5 Nel certificato del servizio può essere specificato tramite l'elemento figlio `<serviceCertificate>` di elemento di `<service>` WIF.  Questa funzionalità non è presente in WIF 4,5; specificare l'elemento `<serviceCertificate>` sotto l'elemento `<serviceCredentials>`.  
  
-   Le classi utilizzate per incuneare WIF 3,5 in WCF più.  Sono incluse le seguenti classi nello spazio dei nomi `Microsoft.IdentityModel.Tokens` : `FederatedSecurityTokenManager`, `FederatedServiceCredentials` e `IdentityModelServiceAuthorizationManager`che la classe `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement`.  
  
## Abilitare WIF 3,5 in Windows 8  
 Poiché WIF 4,5 fa parte di .NET 4.5, viene abilitata automaticamente nei computer che eseguono Windows 8 e Windows Server 2012 e le applicazioni che sono compilati utilizzando WIF 4,5 funzionano in Windows 8 o Windows Server 2012 per impostazione predefinita.  Tuttavia, potrebbe essere necessario eseguire le applicazioni sviluppate tramite WIF 3,5 in un computer che esegue Windows 8 o Windows Server 2012.  In questo caso, è necessario abilitare WIF 3,5 nel computer di destinazione.  Su computer con Windows 8, è possibile utilizzare assistenza dell'immagine di distribuzione e lo strumento di gestione \(DISM\).  In un server 2012 dei computer con Windows, è possibile utilizzare lo strumento di DISM oppure utilizzare il cmdlet di Windows PowerShell `Add-WindowsFeature`.  In entrambi i casi, i controlli appropriati possono essere richiamati dalla riga di comando o dall'ambiente di Windows PowerShell.  
  
 I controlli seguenti viene illustrato come utilizzare lo strumento di DISM dalla riga di comando o dall'ambiente di Windows PowerShell.  Per impostazione predefinita, il modulo di DISM PowerShell è incluso in Windows 8 e Windows Server 2012 e non deve essere incluso.  Per ulteriori informazioni su l DISM con Windows PowerShell, vedere [Come utilizzare DISM in Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=254419).  
  
 Per abilitare WIF 3,5 utilizzando DISM:  
  
```  
dism /online /enable-feature:windows-identity-foundation  
```  
  
 Per disabilitare WIF 3,5 utilizzando DISM:  
  
```  
dism /online /disable-feature:windows-identity-foundation  
```  
  
 Per controllare le funzionalità abilitate o disabilitate tramite DISM:  
  
```  
dism /online /get-features  
```  
  
 In alternativa, nei computer che eseguono Windows Server 2012, è possibile abilitare WIF 3,5 utilizzando il cmdlet di Windows PowerShell `Add-WindowsFeature`.  A tale scopo dalla riga di comando, è possibile immettere il comando seguente:  
  
```  
powershell "add-windowsfeature windows-identity-foundation"  
```  
  
 Nell'ambiente di Windows PowerShell, è possibile direttamente il comando:  
  
```  
add-windowsfeature windows-identity-foundation  
```  
  
> [!NOTE]
>  Poiché molte delle classi in WIF 3,5 e 4,5 in WIF condivisioni gli stessi nomi, quando si utilizza la raccolta sia WIF 3,5 che WIF 4,5, sicure ai nomi di classe completo di utilizzo o agli alias dello spazio dei nomi di utilizzo distinguere tra le classi in WIF 3,5 e in WIF 4,5.  
  
## Vedere anche  
 [Schema di configurazione di WIF](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/index.md)   
 [Mapping dello spazio dei nomi tra WIF 3.5 e WIF 4.5](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)   
 [Novità di Windows Identity Foundation 4.5](../../../docs/framework/security/whats-new-in-wif.md)   
 [Identity and Access Tool per Visual Studio 2012](../../../docs/framework/security/identity-and-access-tool-for-vs.md)