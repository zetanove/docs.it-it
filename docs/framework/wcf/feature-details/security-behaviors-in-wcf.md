---
title: "Comportamenti di sicurezza in WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 513232c0-39fd-4409-bda6-5ebd5e0ea7b0
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# Comportamenti di sicurezza in WCF
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] i comportamenti modificano il funzionamento in fase di esecuzione a livello di servizio o di endpoint.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] comportamenti, vedere [Specifica del comportamento in fase di esecuzione del servizio](../../../../docs/framework/wcf/specifying-service-run-time-behavior.md). I *comportamenti di sicurezza* consentono di controllare le credenziali, le autenticazioni, le autorizzazioni e i registri di controllo.I comportamenti possono essere utilizzati tramite programmazione o mediante configurazione.In questo argomento viene descritto come configurare i comportamenti relativi alle funzioni di sicurezza elencati di seguito:  
  
-   [\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  
  
-   [\<credenzialiClient\>](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md).  
  
-   [\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md).  
  
-   [\<controlloSicurezzaServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md).  
  
-   [\<serviceMetadata\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md), che consente inoltre di specificare un endpoint protetto a cui i client possono accedere per ottenere metadati.  
  
## Impostazione delle credenziali tramite i comportamenti  
 Utilizzare l'[\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) e l'[\<credenzialiClient\>](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) per impostare i valori delle credenziali di un servizio o di un client.La configurazione dell'associazione sottostante determina se occorre impostare una credenziale.Ad esempio, se la modalità di sicurezza è impostata su `None`, né i client né i servizi si autenticano reciprocamente o richiedono alcun tipo di credenziale.  
  
 Se invece l'associazione del servizio richiede un tipo di credenziale client,è possibile che occorra utilizzare un comportamento per impostare i valori delle credenziali.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] tipi esistenti di credenziali, vedere [Selezione di un tipo di credenziale](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md). In alcuni casi, ad esempio quando si esegue l'autenticazione tramite le credenziali di Windows, l'ambiente determina automaticamente i valori effettivi delle credenziali. Pertanto, a meno che non si desideri specificare un insieme diverso di credenziali, in questo caso non è necessario eseguire l'impostazione manuale dei valori delle credenziali.  
  
 Tutte le credenziali di servizio si trovano nella [\<comportamentiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) sottoforma di elementi figlio.L'esempio seguente illustra un certificato utilizzato come credenziale di servizio.  
  
```  
<configuration>  
 <system.serviceModel>  
  <behaviors>  
   <serviceBehaviors>  
    <behavior name="ServiceBehavior1">  
     <serviceCredentials>  
      <serviceCertificate findValue="000000000000000000000000000"   
                          storeLocation="CurrentUser"  
      storeName="Root" x509FindType="FindByThumbprint" />  
     </serviceCredentials>  
    </behavior>  
   </serviceBehaviors>  
  </behaviors>  
 </system.serviceModel>  
</configuration>  
```  
  
## Credenziali di servizio  
 L'[\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) contiene quattro elementi figlio.Questi elementi e le relative modalità di utilizzo vengono descritti nelle sezioni seguenti.  
  
### Elemento \<serviceCertificate\>  
 Questo elemento consente di specificare il certificato X.509 utilizzato dai client per autenticare il servizio tramite la modalità di sicurezza Messaggio.L'identificazione digitale di un certificato rinnovato periodicamente viene aggiornata di conseguenza.In questo caso, poiché il certificato può essere rilasciato nuovamente con lo stesso nome del soggetto, utilizzare quest'ultimo come tipo `X509FindType`.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] utilizzo dell'elemento, vedere [Procedura: specificare valori di credenziali client](../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
### Elemento \<certificate\> di \<clientCertificate\>  
 Utilizzare l'elemento [\<certificato\>](../../../../docs/framework/configure-apps/file-schema/wcf/certificate-of-clientcertificate-element.md) quando il servizio deve disporre in anticipo del certificato del client per poter comunicare in modo sicuro con quest'ultimo.Questa esigenza si presenta quando si utilizza il modello di comunicazione duplex.Nel modello più comune di comunicazione richiesta\-risposta, il client include il proprio certificato nella richiesta e il servizio utilizza tale certificato per proteggere la risposta che invia al client.Il modello di comunicazione duplex, invece, non prevede né richieste né rispostee pertanto il servizio non può ricavare il certificato del client dalla comunicazione. Di conseguenza, per proteggere i messaggi inviati al client, il servizio deve disporre in anticipo del certificato del client.Questo certificato deve essere ottenuto mediante una modalità fuori banda e deve essere specificato tramite questo elemento.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] servizi duplex, vedere [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md).  
  
### Elemento \<authentication\> di \<clientCertificate\>  
 L'elemento [\<authentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) consente di personalizzare la modalità di autenticazione dei client.A tale scopo, l'attributo `CertificateValidationMode` può essere impostato su `None`, `ChainTrust`, `PeerOrChainTrust`, `PeerTrust` o `Custom`.Per impostazione predefinita, il livello è impostato su `ChainTrust`. Tale impostazione prevede che ogni certificato appartenga a una gerarchia di certificati che termina in un'*autorità radice* situata all'inizio della catena.Si tratta della modalità più sicura.Il livello può inoltre essere impostato su `PeerOrChainTrust`, a indicare che sia i certificati autocertificati \(trust peer\) sia i certificati appartenenti a una catena di trust sono ritenuti attendibili.Poiché i certificati autocertificati non devono essere acquistati da un'autorità attendibile, questo livello viene utilizzato in fase di sviluppo e di debug dei client e dei servizi.Quando si distribuisce un client è invece opportuno utilizzare il livello `ChainTrust`.Un altro livello disponibile è `Custom`.Quando si imposta il livello `Custom` è necessario impostare anche l'attributo `CustomCertificateValidatorType` sull'assembly e sul tipo utilizzati per convalidare il certificato.Per creare un validator personalizzato è necessario ereditare una classe dalla classe astratta <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  
  
### Elemento \<issuedTokenAuthentication\>  
 L'emissione di un token di autenticazione prevede tre fasi.Nella prima fase, un client che tenta di accedere a un servizio viene reindirizzato a un *servizio token di sicurezza* \(STS\).Nella seconda fase, il servizio token di sicurezza autentica il client, quindi rilascia a quest'ultimo un token, in genere un token SAML \(Security Assertions Markup Language\),che il client restituisce in seguito al servizio.Nella terza fase, il servizio ricerca nel token appena ricevuto i dati da utilizzare per autenticare il token stesso e, pertanto, il client.Affinché il token venga autenticato è necessario che il servizio riconosca il certificato utilizzato dal servizio token di sicurezza.L'elemento [\<autenticazioneTokenEmesso\>](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) rappresenta il repository dei certificati utilizzati dal servizio token di sicurezza.Per aggiungere certificati, utilizzare l'[\<certificatiNoti\>](../../../../docs/framework/configure-apps/file-schema/wcf/knowncertificates.md).Inserire un [\<aggiunta\>](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-knowncertificates.md) per ogni certificato, come illustrato nell'esempio seguente.  
  
```  
<issuedTokenAuthentication>  
   <knownCertificates>  
      <add findValue="www.contoso.com"   
           storeLocation="LocalMachine" storeName="My"   
           X509FindType="FindBySubjectName" />  
    </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
 Per impostazione predefinita, i certificati devono essere ottenuti da un servizio token di sicurezza.Questi certificati "riconosciuti" garantiscono che solo i client autorizzati siano in grado di accedere a un determinato servizio.  
  
 È necessario utilizzare la raccolta [\<allowedAudienceUris\>](../../../../docs/framework/configure-apps/file-schema/wcf/allowedaudienceuris.md) in un'applicazione federata che utilizza un *servizio token di sicurezza* \(STS\) che emette token di sicurezza `SamlSecurityToken`.Al momento del rilascio del token di sicurezza, è possibile che il servizio STS specifichi l'URI dei servizi Web per i quali è destinato il token di sicurezza mediante l'aggiunta di un oggetto `SamlAudienceRestrictionCondition` al token di sicurezza.Ciò consente all'autenticatore `SamlSecurityTokenAuthenticator` del servizio Web di destinazione di verificare che il token di sicurezza emesso sia associato a questo servizio Web specificando che questo controllo deve essere svolto mediante l'esecuzione delle operazioni seguenti:  
  
-   Impostare l'attributo `audienceUriMode` di [\<autenticazioneTokenEmesso\>](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) su `Always` o `BearerKeyOnly`.  
  
-   Specificare il set di URI validi aggiungendo gli URI a questa raccolta.A tale scopo, inserire un [\<aggiunta\>](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-allowedaudienceuris.md) per ogni URI  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] utilizzo di questo elemento di configurazione, vedere [Procedura: configurare le credenziali in un servizio federativo](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).  
  
#### Autenticazione degli utenti anonimi di CardSpace  
 Se si imposta in modo esplicito l'attributo `AllowUntrustedRsaIssuers` dell'elemento `<IssuedTokenAuthentication>` su `true`, qualsiasi client è in grado di presentare un token autocertificato firmato con una coppia di chiavi RSA arbitraria.L'autorità emittente è considerata *non attendibile*, in quanto alla chiave non è stato associato alcun dato di autorità emittente.Un utente di [!INCLUDE[infocard](../../../../includes/infocard-md.md)] può creare una scheda autocertificata contenente attestazioni autonome di identità.Questa funzionalità deve essere utilizzata con cautela.Per utilizzare questa funzionalità, considerare la chiave RSA pubblica come una password dotata di un maggior livello di sicurezza da memorizzare in un database insieme a un nome utente.Prima di consentire a un client di accedere al servizio, verificare la chiave pubblica RSA presentata dal client confrontandola con la chiave pubblica memorizzata associata al nome utente presentato.Ciò presuppone l'implementazione di un processo di registrazione in base al quale un utente può registrare il proprio nome utente e associarlo alla chiave pubblica RSA autocertificata.  
  
## Credenziali client  
 Le credenziali client sono utilizzate per autenticare i client presso i servizi nei casi in cui non è richiesta l'autenticazione reciproca.È possibile utilizzare questa sezione per specificare i certificati di servizio negli scenari in cui il client deve utilizzare il certificato di un servizio per proteggere i messaggi inviati a quest'ultimo.  
  
 È inoltre possibile configurare un client come parte di uno scenario federativo in modo che utilizzi i token emessi da un servizio token di sicurezza o da un'autorità emittente locale di token.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] scenari federativi, vedere [Federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).Tutte le credenziali client si trovano nella [\<comportamentiEndpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md), come mostrato nel codice seguente.  
  
```  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="EndpointBehavior1">  
   <clientCredentials>  
    <clientCertificate findValue="cn=www.contoso.com"     
        storeLocation="LocalMachine"  
        storeName="AuthRoot" x509FindType="FindBySubjectName" />  
    <serviceCertificate>  
     <defaultCertificate findValue="www.cohowinery.com"   
                    storeLocation="LocalMachine"  
                    storeName="Root" x509FindType="FindByIssuerName" />  
    <authentication revocationMode="Online"  
                    trustedStoreLocation="LocalMachine" />  
    </serviceCertificate>  
   </clientCredentials>  
  </behavior>  
 </endpointBehaviors>  
```  
  
#### Elemento \<clientCertifictate\>  
 Questo elemento consente di impostare il certificato utilizzato per autenticare il client.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: specificare valori di credenziali client](../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
#### \<httpDigest\>  
 Questa funzionalità deve essere abilitata con Active Directory in Windows e Internet Information Services \(IIS\).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Autenticazione digest in IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88443).  
  
#### Elemento \<issuedToken\>  
 L'[\<tokenEmesso\>](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md) contiene gli elementi utilizzati per configurare un'autorità emittente locale di token oppure i comportamenti utilizzati in un servizio token di sicurezza.Per istruzioni su come configurare un client affinché utilizzi un'autorità emittente locale, vedere [Procedura: configurare un emittente locale](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
#### \<localIssuerAddress\>  
 Specifica l'indirizzo predefinito di un servizio token di sicurezza.Questo elemento viene utilizzato quando l'associazione <xref:System.ServiceModel.WSFederationHttpBinding> non fornisce alcun URL per il servizio token di sicurezza oppure quando l'indirizzo dell'autorità emittente di un'associazione federativa è http:\/\/schemas.microsoft.com\/2005\/12\/ServiceModel\/Addressing\/Anonymous o `null`.In questi casi le credenziali <xref:System.ServiceModel.Description.ClientCredentials> devono essere configurate con l'indirizzo dell'autorità emittente locale e con l'associazione da utilizzare per comunicare con tale autorità emittente.  
  
#### \<issuerChannelBehaviors\>  
 L'[\<issuerChannelBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/issuerchannelbehaviors-element.md) consente di aggiungere i comportamenti client di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzati per comunicare con un servizio token di sicurezza.I comportamenti client vengono definiti nella sezione [\<comportamentiEndpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md).Per utilizzare un comportamento definito, aggiungere un elemento \<`add`\> all'elemento `<issuerChannelBehaviors>` con due attributi.Impostare l'indirizzo `issuerAddress` sull'URL del servizio token di sicurezza, quindi impostare l'attributo `behaviorConfiguration` sul nome del comportamento di endpoint definito, come mostrato nell'esempio seguente.  
  
```  
<clientCredentials>  
   <issuedToken>  
      <issuerChannelBehaviors>  
         <add issuerAddress="http://www.contoso.com"  
               behaviorConfiguration="clientBehavior1" />     
```  
  
#### Elemento \<serviceCertificate\>  
 Utilizzare questo elemento per controllare l'autenticazione dei certificati di servizio.  
  
 L'elemento [\<certificatoPredefinito\>](../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md) può contenere un solo certificato da utilizzare quando il servizio non specifica alcun certificato.  
  
 Utilizzare l'elemento [\<certificatiConAmbito\>](../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md) e l'[\<aggiunta\>](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md) per impostare i certificati di servizio associati a servizi specifici.L'elemento `<add>` contiene l'attributo `targetUri` utilizzato per associare il certificato al servizio.  
  
 L'elemento [\<autenticazione\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) specifica il livello di attendibilità utilizzato per autenticare i certificati.Per impostazione predefinita, il livello è impostato su "ChainTrust". Tale impostazione prevede che ogni certificato appartenga a una gerarchia di certificati che termina in un'autorità di certificazione attendibile situata all'inizio della catena.Si tratta della modalità più sicura.Il livello può inoltre essere impostato su "PeerOrChainTrust" per indicare che sia i certificati autocertificati \(trust peer\) che quelli appartenenti a una catena di trust sono ritenuti attendibili.Poiché i certificati autocertificati non devono essere acquistati da un'autorità attendibile, questo livello viene utilizzato in fase di sviluppo e di debug dei client e dei servizi.Quando si distribuisce un client è invece opportuno utilizzare il livello "ChainTrust".Il livello può inoltre essere impostato su "Custom" o "None". Quando si imposta il livello "Custom" è necessario impostare anche l'attributo `CustomCertificateValidatorType` sull'assembly e sul tipo utilizzati per convalidare il certificato.Per creare un validator personalizzato è necessario ereditare una classe dalla classe astratta <xref:System.IdentityModel.Selectors.X509CertificateValidator>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: creare un servizio che usa un validator del certificato personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
 L'elemento [\<autenticazione\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) contiene un attributo `RevocationMode` che specifica la modalità per la revoca dei certificati.L'impostazione predefinita è "online" e indica che i certificati vengono contrassegnati automaticamente per la revoca.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
## ServiceAuthorization  
 L'elemento [\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) contiene elementi che influiscono su autorizzazioni, provider del ruolo personalizzati e rappresentazioni.  
  
 La classe <xref:System.Security.Permissions.PrincipalPermissionAttribute> viene applicata a un metodo di servizio.Questo attributo specifica i gruppi di utenti da utilizzare quando si autorizza l'utilizzo di un metodo protetto.Il valore predefinito è "UseWindowsGroups" e specifica che la ricerca degli ID che tentano di accedere a una determinata risorsa viene eseguita nei gruppi di Windows, ad esempio "Administrators" o "Users".È inoltre possibile specificare "UseAspNetRoles" per utilizzare un provider del ruoli personalizzato configurato nell'elemento \<`system.web` \> come illustrato nel codice seguente.  
  
```  
<system.web>  
  <membership defaultProvider="SqlProvider"   
   userIsOnlineTimeWindow="15">  
     <providers>  
       <clear />  
       <add   
          name="SqlProvider"   
          type="System.Web.Security.SqlMembershipProvider"   
          connectionStringName="SqlConn"  
          applicationName="MembershipProvider"  
          enablePasswordRetrieval="false"  
          enablePasswordReset="false"  
          requiresQuestionAndAnswer="false"  
          requiresUniqueEmail="true"  
          passwordFormat="Hashed" />  
     </providers>  
   </membership>  
  <!-- Other configuration code not shown.-->  
</system.web>  
```  
  
 Nell'esempio di codice seguente viene illustrato l'utilizzo di un elemento `roleProviderName` con l'attributo `principalPermissionMode`.  
  
```  
<behaviors>  
 <behavior name="ServiceBehaviour">          
  <serviceAuthorization principalPermissionMode ="UseAspNetRoles"   
                        roleProviderName ="SqlProvider" />  
</behavior>   
   <!-- Other configuration code not shown. -->  
</behaviors>  
```  
  
## Configurazione dei controlli di sicurezza  
 Utilizzare l'[\<controlloSicurezzaServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) per  specificare il log in cui scrivere e i tipi di evento da registrare.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
```  
<system.serviceModel>  
<serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceSecurityAudit auditLogLocation="Application"   
             suppressAuditFailure="true"  
             serviceAuthorizationAuditLevel="Success"   
             messageAuthenticationAuditLevel="Success" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## Scambio protetto di metadati  
 L'esportazione e l'invio di metadati ai client risulta particolarmente utile per gli sviluppatori di servizi e client, in quanto consente il download di codice client e di configurazione.Per ridurre l'esposizione di un servizio agli utenti malintenzionati, questo trasferimento può essere protetto mediante il meccanismo HTTPS \(ovvero SSL su HTTP\).A tale scopo, è anzitutto necessario associare un certificato X.509 adatto a una porta specifica del computer che ospita il servizio.\([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).\) Quindi, è necessario aggiungere un [\<serviceMetadata\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md) nella configurazione del servizio e impostare l'attributo `HttpsGetEnabled` su `true`.Infine, come mostrato nell'esempio seguente, è necessario impostare l'attributo `HttpsGetUrl` sull'URL dell'endpoint dei metadati del servizio.  
  
```  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## Vedere anche  
 [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)   
 [Sicurezza e protezione](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)