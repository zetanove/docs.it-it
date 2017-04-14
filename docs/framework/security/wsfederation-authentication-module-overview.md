---
title: "Panoramica del modulo di autenticazione WSFederation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 02c4d5e8-f0a7-49ee-9cf5-3647578510ad
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Panoramica del modulo di autenticazione WSFederation
Communications foundation \(WIF\)identità Windows include il supporto per l'autenticazione organizzata in modo federativo nelle applicazioni ASP.NET mediante il modulo di autenticazione WS\- organizzato in modo federativo \(WS\-FAM\).  In questo argomento spiegherà in quale funziona organizzati in modo federativo di autenticazione e come utilizzarlo.  
  
### Panoramica di autenticazione organizzata in modo federativo  
 L'autenticazione organizzata in modo federativo consente a un servizio token di sicurezza \(STS\) in un dominio dell'attendibilità per fornire informazioni di autenticazione a un servizio token di sicurezza in un altro dominio dell'attendibilità quando esiste una relazione di trust tra i due domini.  Un esempio è illustrato nella figura seguente.  
  
 ![Scenario di autenticazione di federazione](../../../docs/framework/security/media/federatedauthentication.png "FederatedAuthentication")  
  
1.  Un client nel dominio dell'attendibilità di Fabrikam invia una richiesta a un'applicazione di \(RP\) del componente nel dominio dell'attendibilità Contoso.  
  
2.  Il RP reindirizza il client a un servizio token di sicurezza nel dominio dell'attendibilità Contoso.  Questo servizio token di sicurezza non contiene alcuna informazione del client.  
  
3.  Contoso servizio token di sicurezza reindirizza il client a un servizio token di sicurezza nel dominio dell'attendibilità di Fabrikam, con cui il dominio dell'attendibilità di Contoso ha una relazione di trust.  
  
4.  Fabrikam il servizio token di sicurezza verifica l'identità del client e genera un token di sicurezza in Contoso servizio token di sicurezza.  
  
5.  Contoso servizio token di sicurezza utilizza il token di Fabrikam per creare il relativo token che può essere utilizzato dal RP e lo invia al RP.  
  
6.  Il RP estrae le richieste del client dal token di sicurezza e viene presa una decisione di autorizzazione.  
  
### Tramite il modulo di autenticazione organizzato in modo federativo con ASP.NET  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WS\-FAM\) è un modulo HTTP che consente di aggiungere l'autenticazione organizzata in modo federativo a un'applicazione [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].  L'autenticazione organizzata in modo federativo della logica di autenticazione essere gestita dal servizio token di sicurezza consentendo di concentrarsi sulla logica di business di scrittura.  
  
 Configurare il WS\-FAM per specificare il servizio token di sicurezza in cui non è autenticato le richieste deve essere reindirizzati.  WIF consente di autenticare un utente in due modi:  
  
1.  Il reindirizzamento passivo: Quando un utente autenticato tenta di accedere a una risorsa protetta e si desidera riorientarli semplicemente a un servizio token di sicurezza senza richiedere una pagina di accesso, questo è il modo corretto.  Il servizio token di sicurezza verifica l'identità dell'utente e genera un token di sicurezza che contiene le richieste appropriate per tale utente.  Questa opzione richiede il WS\-FAM di aggiungere nella pipeline dei moduli HTTP.  È possibile utilizzare l'identità e di accesso da Visual Studio 2012 modificare il file di configurazione dell'applicazione per utilizzare il WS\-FAM e per organizzare in modo federativo con un servizio token di sicurezza.  Per ulteriori informazioni, vedere [Identity and Access Tool per Visual Studio 2012](../../../docs/framework/security/identity-and-access-tool-for-vs.md).  
  
2.  È possibile chiamare il metodo <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SignIn%2A?displayProperty=fullName> o il metodo <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectToIdentityProvider%2A> dal file code\-behind per il simbolo con segno nella pagina dell'applicazione di RP.  
  
 In passivo reindirizzare, le comunicazioni viene eseguito con la risposta\/reindirizzamento dal client \(in genere un browser.  È possibile aggiungere il WS\-FAM alla pipeline HTTP dell'applicazione, nei controlli per le richieste utente non autenticato e reindirizzare gli utenti al servizio token di sicurezza specificato.  
  
 Il WS\-FAM anche genera vari eventi che consentono di personalizzare la funzionalità in un'applicazione [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].  
  
### Come il funzionamento di WS\-FAM  
 Il WS\-FAM implementato nella classe <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>.  In genere, aggiungere il WS\-FAM alla pipeline HTTP dell'applicazione [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] RP.  Quando un utente autenticato tenta di accedere a una risorsa protetta, il RP restituisce una risposta HTTP negata l'autorizzazione "401".  Il WS\-FAM intercetta la risposta anziché lasciare che il client la ricezione, quindi reindirizza l'utente al servizio token di sicurezza specificato.  Il servizio token di sicurezza pubblica un token di sicurezza, che il WS\-FAM intercetta ancora.  Il WS\-FAM viene utilizzato il token per creare un'istanza <xref:System.Security.Claims.ClaimsPrincipal> per l'utente autenticato, che consente ai normali meccanismi dell'autorizzazione [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] per l'esecuzione.  
  
 Poiché HTTP è indipendente dallo stato, è necessario un modo per evitare di ripetere questo processo per ogni volta che l'utente tenta di accedere a una risorsa protetta.  A questo punto <xref:System.IdentityModel.Services.SessionAuthenticationModule> invio.  Quando il servizio token di sicurezza pubblica un token di sicurezza per l'utente, anche <xref:System.IdentityModel.Services.SessionAuthenticationModule> crea un token di sicurezza della sessione per l'utente e lo inserisce in un cookie.  Le richieste successive, <xref:System.IdentityModel.Services.SessionAuthenticationModule> intercetta i cookie e la utilizza per ricostruire <xref:System.Security.Claims.ClaimsPrincipal>dell'utente.  
  
 Il seguente diagramma mostra il flusso di informazioni globale in passivo reindirizzano il caso.  La richiesta viene reindirizzato automaticamente tramite il servizio token di sicurezza di stabilire le credenziali senza una pagina di accesso:  
  
 ![Diagramma di temporizzazione per accesso con reindirizzamento passivo](../../../docs/framework/security/media/signinusingpassiveredirect.png "SignInUsingPassiveRedirect")  
  
 Nel seguente diagramma più dettagli su ciò che si verifica quando l'utente è autenticato al servizio token di sicurezza e del relativo token di sicurezza vengono elaborati da <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>:  
  
 ![Temporizzazione per elaborazione token con reindirizzamento passivo](../../../docs/framework/security/media/signinusingpassiveredirect-tokenprocessing.png "SignInUsingPassiveRedirect\_TokenProcessing")  
  
 Nel seguente diagramma più dettagli su ciò che si verifica quando i token di sicurezza dall'utente sono stati serializzati nel cookie e vengono individuati da <xref:System.IdentityModel.Services.SessionAuthenticationModule>:  
  
 ![Diagramma di temporizzazione SAM con accesso mediante controlli](../../../docs/framework/security/media/signinusingconrols-sam.png "SignInUsingConrols\_SAM")  
  
### Eventi  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>, <xref:System.IdentityModel.Services.SessionAuthenticationModule> e la relativa classe padre, <xref:System.IdentityModel.Services.HttpModuleBase>, generano eventi alle varie fasi di elaborazione di una richiesta HTTP.  È possibile gestire questi eventi nel file `global.asax` dell'applicazione [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].  
  
-   L'infrastruttura ASP.NET richiama il metodo <xref:System.IdentityModel.Services.HttpModuleBase.Init%2A> del modulo per inizializzare il modulo.  
  
-   Viene generato l'evento <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated?displayProperty=fullName> all'infrastruttura ASP.NET chiama per la prima volta il metodo <xref:System.IdentityModel.Services.HttpModuleBase.Init%2A> su uno dei moduli dell'applicazione che derivano da <xref:System.IdentityModel.Services.HttpModuleBase>.  Questo metodo accede alla proprietà statica <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>, che determina la configurazione verrà caricato il file Web.config.  L'evento viene generato solo la prima volta questa proprietà viene eseguito.  L'oggetto <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> inizializzato dalla configurazione è accessibile tramite la proprietà <xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=fullName> in un gestore eventi.  È possibile utilizzare questo evento per modificare la configurazione prima che venga applicata a tutti i moduli.  È possibile aggiungere un gestore per questo evento nel metodo Application\_Start:  
  
    ```  
    void Application_Start(object sender, EventArgs e)  
    {  
        FederatedAuthentication.FederationConfigurationCreated += new EventHandler<FederationConfigurationCreatedEventArgs>(FederatedAuthentication_FederationConfigurationCreated);  
    }  
    ```  
  
     Ogni modulo eseguire l'override di <xref:System.IdentityModel.Services.HttpModuleBase.InitializeModule%2A?displayProperty=fullName> e metodi astratti <xref:System.IdentityModel.Services.HttpModuleBase.InitializePropertiesFromConfiguration%2A?displayProperty=fullName>.  Il primo di questi metodi aggiungere gestori per gli eventi ASP.NET della pipeline di interesse al modulo.  Nella maggior parte dei casi l'implementazione predefinita di un modulo.  Il secondo di questi metodi inizializza le proprietà del form dalla proprietà <xref:System.IdentityModel.Services.HttpModuleBase.FederationConfiguration%2A?displayProperty=fullName>. Si tratta di una copia della configurazione che è stata caricata in precedenza.\) Potrebbe essere necessario eseguire l'override di questo secondo metodo se si desidera supportare l'inizializzazione di nuove proprietà dalla configurazione delle classi che derivano da <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> o <xref:System.IdentityModel.Services.SessionAuthenticationModule>.  In questi casi è anche necessario derivare da oggetti appropriati di configurazione per supportare le proprietà aggiunte di configurazione; ad esempio, <xref:System.IdentityModel.Configuration.IdentityConfiguration>, <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration>, o <xref:System.IdentityModel.Services.Configuration.FederationConfiguration>.  
  
-   Il WS\-FAM genera l'evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SecurityTokenReceived> quando rileva un token di sicurezza pubblicato dal servizio token di sicurezza.  
  
-   Il WS\-FAM genera l'evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SecurityTokenValidated> dopo che ha convalidato il token.  
  
-   <xref:System.IdentityModel.Services.SessionAuthenticationModule> genera l'evento <xref:System.IdentityModel.Services.SessionAuthenticationModule.SessionSecurityTokenCreated> quando si crea un token di sicurezza della sessione per l'utente.  
  
-   <xref:System.IdentityModel.Services.SessionAuthenticationModule> genera l'evento <xref:System.IdentityModel.Services.SessionAuthenticationModule.SessionSecurityTokenReceived> quando rileva le richieste successive ai cookie contenenti il token di sicurezza della sessione.  
  
-   Prima che il WS\-FAM reindirizzare l'utente all'autorità, genera l'evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider>.  La WS\- federazione con la richiesta è disponibile tramite la proprietà <xref:System.IdentityModel.Services.RedirectingToIdentityProviderEventArgs.SignInRequestMessage%2A><xref:System.IdentityModel.Services.RedirectingToIdentityProviderEventArgs> passato nel caso.  È possibile scegliere per modificare la richiesta prima di inviare il termine dell'autorità.  
  
-   Il WS\-FAM genera l'evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SignedIn> ai cookie vengono scritti correttamente e l'utente viene firmato in.  
  
-   Il WS\-FAM genera l'evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SigningOut> una volta per sessione mentre la sessione viene chiusa giù per ciascun utente.  Non viene generato se la sessione viene chiusa giù sul lato client, ad esempio eliminazione di cookie di sessione\).  In un ambiente di SSO, il IP\-STS può richiedere ogni RP a firmare esterno, anche.  Anche questo genererà l'evento, con <xref:System.IdentityModel.Services.SigningOutEventArgs.IsIPInitiated%2A> impostare su `true`.  
  
> [!NOTE]
>  Non utilizzare la proprietà <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> durante un evento generato da <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> o <xref:System.IdentityModel.Services.SessionAuthenticationModule>.  Perché <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> viene impostato dopo il processo di autenticazione, mentre gli eventi vengono generati durante il processo di autenticazione.  
  
### Configurazione di autenticazione organizzata in modo federativo  
 I WS\-FAM e il SAM vengono configurati dall'elemento [\<federationConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md).  L'elemento figlio [\<wsFederation\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/wsfederation.md) configura i valori predefiniti per le proprietà di WS\-FAM; ad esempio <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.Issuer%2A> e la proprietà <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.Realm%2A>. \(Questi valori possono essere modificati in base alla richiesta di fornire gestori per alcuni eventi di WS\-FAM; ad esempio, <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider>\). Il gestore del cookie utilizzato dal SAM è configurato tramite l'elemento [\<cookieHandler\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md) figlio.  WIF fornisce un gestore predefinito del cookie implementato nella classe <xref:System.IdentityModel.Services.ChunkedCookieHandler> che possono avere dimensioni del blocco impostata dall'elemento [\<chunkedCookieHandler\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/chunkedcookiehandler.md).  L'elemento `<federationConfiguration>` fa riferimento <xref:System.IdentityModel.Configuration.IdentityConfiguration>, che fornisce la configurazione per altri componenti di WIF utilizzate nell'applicazione, ad esempio <xref:System.Security.Claims.ClaimsAuthenticationManager> e <xref:System.Security.Claims.ClaimsAuthorizationManager>.  La configurazione di identità è possibile fare riferimento in modo esplicito specificando un elemento denominato [\<identityConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) nell'attributo `identityConfigurationName` dell'elemento `<federationConfiguration>`.  Se la configurazione di identità non viene fatto riferimento in modo esplicito, la configurazione predefinita di identità verrà utilizzata.  
  
 Il codice XML seguente viene illustrata una configurazione di un'applicazione di \(RP\) del componente di ASP.NET.  Le sezioni di configurazione <xref:System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection> e <xref:System.IdentityModel.Configuration.SystemIdentityModelSection> vengono aggiunti all'elemento `<configSections>`.  Il SAM e i WS\-FAM vengono aggiunti ai moduli HTTP nell'elemento`<modules>` \/ `<system.webServer>`.  Infine componenti di WIF vengono configurate in `<system.identityModel>`\/`<identityConfiguration>` e `<system.identityModel.services>`\/elementi`<federationConfiguration>`.  Questa configurazione specifica il gestore bloccato cookie poiché è il gestore predefinito del cookie e non esiste un tipo di gestore del cookie specificato nell'elemento `<cookieHandler>`.  
  
> [!WARNING]
>  Nell'esempio seguente, entrambi l'attributo `requireHttps` di `<wsFederation>` e l'attributo `requireSsl` dell'elemento `<cookieHandler>` sono `false`.  Ciò offre una potenziale minaccia alla sicurezza.  Nella produzione, entrambi questi valori devono essere `true`impostato.  
  
```  
<configuration>  
  <configSections>  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
  </configSections>  
  
  ...  
  
  <system.webServer>  
    <modules>  
      <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
    </modules>  
  </system.webServer>  
  
  <system.identityModel>  
    <identityConfiguration>  
      <audienceUris>  
        <add value="http://localhost:50969/" />  
      </audienceUris>  
      <certificateValidation certificateValidationMode="None" />  
      <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
        <trustedIssuers>  
          <add thumbprint="9B74CB2F320F7AAFC156E1252270B1DC01EF40D0" name="LocalSTS" />  
        </trustedIssuers>  
      </issuerNameRegistry>  
    </identityConfiguration>  
  </system.identityModel>  
  <system.identityModel.services>  
    <federationConfiguration>  
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:15839/wsFederationSTS/Issue" realm="http://localhost:50969/" reply="http://localhost:50969/" requireHttps="false" />  
      <cookieHandler requireSsl="false" />  
    </federationConfiguration>  
  </system.identityModel.services>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Services.SessionAuthenticationModule>   
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>   
 [\<federationConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)