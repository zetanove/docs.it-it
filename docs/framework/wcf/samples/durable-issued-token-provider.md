---
title: "Provider di token rilasciati in modo durevole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 76fb27f5-8787-4b6a-bf4c-99b4be1d2e8b
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Provider di token rilasciati in modo durevole
In questo esempio viene descritto come implementare un provider di token rilasciato da un client personalizzato.  
  
## Discussione  
 Un provider di token in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene utilizzato per fornire credenziali all'infrastruttura di sicurezza.In generale, il provider di token esamina la destinazione ed emette credenziali adatte in modo che l'infrastruttura di sicurezza possa salvaguardare il messaggio.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene fornito con un provider di token [!INCLUDE[infocard](../../../../includes/infocard-md.md)].I provider di token personalizzati sono utili nei casi seguenti:  
  
-   Se è disponibile un archivio di credenziali con cui il provider di token incluso non è in grado di operare.  
  
-   Se si desidera fornire un meccanismo personalizzato per la trasformazione delle credenziali dal punto in cui l'utente fornisce i dettagli a quello in cui il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le credenziali.  
  
-   Se si sta compilando un token personalizzato.  
  
 Questo esempio illustra come compilare un provider di token personalizzato che memorizza nella cache token rilasciati da un servizio token di protezione \(STS, Security Token Service\).  
  
 Per riassumere, questo esempio illustra quanto segue.  
  
-   Come è possibile configurare un client con un provider personalizzato.  
  
-   Come i token rilasciati possono essere memorizzati nella cache e forniti al client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Come viene autenticato il servizio dal client mediante il certificato X.509 del server.  
  
 L'esempio è costituito da un programma console del client \(Client.exe\), da un programma console del servizio token di sicurezza \(Securitytokenservice.exe\) e da un programma console del servizio \(Service.exe\).Il servizio implementa un contratto che definisce un modello di comunicazione request\/reply.Il contratto viene definito dall'interfaccia `ICalculator` che espone operazioni matematiche \(somma, sottrazione, moltiplicazione e divisione\).Il client riceve un token di protezione dal servizio token di protezione \(STS\), esegue richieste sincrone al servizio per un'operazione matematica specificata e il servizio risponde fornendo il risultato.L'attività del client è visibile nella finestra della console.  
  
> [!NOTE]
>  La procedura di configurazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Questo esempio espone il contratto ICalculator utilizzando [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).La configurazione di questa associazione nel client viene illustrata nel codice seguente.  
  
```  
<bindings>  <wsFederationHttpBinding>    <binding name="ServiceFed" >      <security mode ="Message">        <message issuedKeyType ="SymmetricKey" issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >          <issuer address ="http://localhost:8000/sts/windows" binding ="wsHttpBinding" />        </message>      </security>    </binding>  </wsFederationHttpBinding></bindings>  
```  
  
 Nell'elemento `security` di `wsFederationHttpBinding`, il valore `mode` configura quale modalità di sicurezza deve essere utilizzata.In questo esempio viene utilizzata la sicurezza dei messaggi; per tale motivo, l'elemento `message` di `wsFederationHttpBinding` viene specificato all'interno dell'elemento `security` di `wsFederationHttpBinding`.L'elemento `issuer` di `wsFederationHttpBinding` all'interno dell'elemento `message` di `wsFederationHttpBinding` specifica l'indirizzo e l'associazione per il servizio token di sicurezza che rilascia un token di sicurezza al client, in modo che quest'ultimo possa autenticarsi presso il servizio di calcolatrice.  
  
 La configurazione di quest'associazione sul servizio viene illustrata nel seguente codice.  
  
```  
<bindings>  <wsFederationHttpBinding>    <binding name="ServiceFed" >      <security mode ="Message">        <message issuedKeyType ="SymmetricKey" issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >          <issuerMetadata address ="http://localhost:8000/sts/mex" >            <identity>              <certificateReference storeLocation ="CurrentUser"                                     storeName="TrustedPeople"                                     x509FindType ="FindBySubjectDistinguishedName"                                     findValue ="CN=STS" />            </identity>          </issuerMetadata>        </message>      </security>    </binding>  </wsFederationHttpBinding></bindings>  
```  
  
 Nell'elemento `security` di `wsFederationHttpBinding`, il valore `mode` configura quale modalità di sicurezza deve essere utilizzata.In questo esempio viene utilizzata la sicurezza dei messaggi; per tale motivo, l'elemento `message` di `wsFederationHttpBinding` viene specificato all'interno dell'elemento `security` di `wsFederationHttpBinding`.L'elemento `issuerMetadata` di `wsFederationHttpBinding` all'interno dell'elemento `message` di `wsFederationHttpBinding` specifica l'indirizzo e l'identità di un endpoint che può essere utilizzato per recuperare metadati per il servizio token di sicurezza.  
  
 Il comportamento per il servizio viene illustrato nel codice seguente.  
  
```  
<behavior name ="ServiceBehavior" >  <serviceDebug includeExceptionDetailInFaults ="true"/>  <serviceMetadata httpGetEnabled ="true"/>  <serviceCredentials>    <issuedTokenAuthentication>      <knownCertificates>        <add storeLocation ="LocalMachine"             storeName="TrustedPeople"             x509FindType="FindBySubjectDistinguishedName"             findValue="CN=STS" />      </knownCertificates>    </issuedTokenAuthentication>    <serviceCertificate storeLocation ="LocalMachine"                        storeName ="My"                        x509FindType ="FindBySubjectDistinguishedName"                        findValue ="CN=localhost"/>  </serviceCredentials></behavior>  
```  
  
 L'elemento `issuedTokenAuthentication` all'interno dell'elemento `serviceCredentials` consente al servizio di specificare i vincoli nei token che i client possono presentare durante l'autenticazione.Questa configurazione specifica che i token firmati da un certificato il cui nome di soggetto è CN\=STS possono essere accettati dal servizio.  
  
 Il servizio token di sicurezza espone un solo endpoint utilizzando l'elemento wsHttpBinding standard.Il servizio token di sicurezza risponde alle richieste di token dei client e, se il client si autentica utilizzando un account di Windows, emette un token che contiene il nome utente del client come attestazione nel token emesso.Come parte del processo di creazione del token, il servizio token di protezione firma il token utilizzando la chiave privata associata al certificato CN\=STS .Crea, inoltre, una chiave simmetrica e la crittografa utilizzando la chiave pubblica associata al certificato CN\=localhost.Nel restituire il token al client, il servizio token di protezione restituisce anche la chiave simmetrica.Il client presenta il token emesso al servizio di calcolatrice e dimostra che conosce la chiave simmetrica firmando il messaggio con quella chiave.  
  
## Credenziali client e servizio token di protezione personalizzati  
 I passaggi seguenti illustrano come sviluppare un provider di token personalizzato in grado di memorizzare nella cache i token rilasciati e come integrarlo nella sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
#### Per sviluppare un provider di token personalizzato  
  
1.  Scrivere un provider di token personalizzato.  
  
     L'esempio implementa un provider di token personalizzato che restituisce un token di sicurezza recuperato da una cache.  
  
     Per eseguire questa attività il provider di token personalizzato deriva dalla classe <xref:System.IdentityModel.Selectors.SecurityTokenProvider> ed esegue l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A>.Questo metodo tenta di ottenere un token dalla cache o, se non è possibile trovare un token nella cache, recupera un token dal provider sottostante e quindi lo memorizza nella cache.In entrambi i casi, il metodo restituisce `SecurityToken`.  
  
    ```  
    protected override SecurityToken GetTokenCore(TimeSpan timeout)  
    {  
      GenericXmlSecurityToken token;  
      if (!this.cache.TryGetToken(target, issuer, out token))  
      {  
        token = (GenericXmlSecurityToken) this.innerTokenProvider.GetToken(timeout);  
        this.cache.AddToken(token, target, issuer);  
      }  
      return token;  
    }  
    ```  
  
2.  Scrivere il gestore di token di protezione personalizzato.  
  
     La classe <xref:System.IdentityModel.Selectors.SecurityTokenManager> viene utilizzata per creare un <xref:System.IdentityModel.Selectors.SecurityTokenProvider> per un <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> specifico che viene passato nel metodo `CreateSecurityTokenProvider`.Viene inoltre utilizzato un gestore del token di sicurezza per creare autenticatori del token e serializzatori del token, che però non vengono presi in esame in questo esempio.Nell'esempio, il gestore del token di sicurezza eredita dalla classe <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> ed esegue l'override del metodo `CreateSecurityTokenProvider` per restituire il provider di token personalizzato quando i requisiti del token passati indicano che viene richiesto un token emesso.  
  
    ```  
    class DurableIssuedTokenClientCredentialsTokenManager :  
     ClientCredentialsSecurityTokenManager  
    {  
      IssuedTokenCache cache;  
  
      public DurableIssuedTokenClientCredentialsTokenManager ( DurableIssuedTokenClientCredentials creds ): base(creds)  
      {  
        this.cache = creds.IssuedTokenCache;  
      }  
  
      public override SecurityTokenProvider CreateSecurityTokenProvider ( SecurityTokenRequirement tokenRequirement )  
      {  
        if (IsIssuedSecurityTokenRequirement(tokenRequirement))  
        {  
          return new DurableIssuedSecurityTokenProvider ((IssuedSecurityTokenProvider)base.CreateSecurityTokenProvider( tokenRequirement), this.cache);  
        }  
        Else  
        {  
          return base.CreateSecurityTokenProvider(tokenRequirement);  
        }  
      }  
    }  
    ```  
  
3.  Scrivere una credenziale client personalizzata.  
  
     La classe delle credenziali di un client viene utilizzata per rappresentare le credenziali configurate per il proxy client e crea il gestore del token di protezione utilizzato per ottenere gli autenticatori del token, i provider di token e i serializzatori di token.  
  
    ```  
    public class DurableIssuedTokenClientCredentials : ClientCredentials  
    {  
      IssuedTokenCache cache;  
  
      public DurableIssuedTokenClientCredentials() : base()  
      {  
      }  
  
      DurableIssuedTokenClientCredentials ( DurableIssuedTokenClientCredentials other) : base(other)  
      {  
        this.cache = other.cache;  
      }  
  
      public IssuedTokenCache IssuedTokenCache  
      {  
        Get  
        {  
          return this.cache;  
        }  
        Set  
        {  
          this.cache = value;  
        }  
      }  
  
      protected override ClientCredentials CloneCore()  
      {  
        return new DurableIssuedTokenClientCredentials(this);  
      }  
  
      public override SecurityTokenManager CreateSecurityTokenManager()  
      {  
        return new DurableIssuedTokenClientCredentialsTokenManager ((DurableIssuedTokenClientCredentials)this.Clone());  
      }  
    }  
    ```  
  
4.  Implementare la cache del token.L'implementazione di esempio utilizza una classe di base astratta tramite la quale utenti di una cache del token specificata interagiscono con la cache.  
  
    ```  
    public abstract class IssuedTokenCache  
    {  
      public abstract void AddToken ( GenericXmlSecurityToken token, EndpointAddress target, EndpointAddress issuer);  
      public abstract bool TryGetToken(EndpointAddress target, EndpointAddress issuer, out GenericXmlSecurityToken cachedToken);  
    }  
    Configure the client to use the custom client credential.  
    ```  
  
     L'esempio elimina la classe della credenziale client predefinita e fornisce la nuova classe della credenziale client affinché il client possa utilizzare la credenziale client personalizzata.  
  
    ```  
    clientFactory.Endpoint.Behaviors.Remove<ClientCredentials>();  
    DurableIssuedTokenClientCredentials durableCreds = new DurableIssuedTokenClientCredentials();  
    durableCreds.IssuedTokenCache = cache;  
    durableCreds.ServiceCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.PeerOrChainTrust;  
    clientFactory.Endpoint.Behaviors.Add(durableCreds);  
    ```  
  
## Esecuzione dell'esempio  
 Per eseguire l'esempio seguire le istruzioni seguenti.Quando si esegue l'esempio, la richiesta per il token di protezione viene visualizzata nella finestra della console del servizio token di protezione.Le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console del client e in quella del servizio.Premere INVIO in una delle finestre della console per arrestare l'applicazione.  
  
## File batch Setup.cmd  
 Il file batch Setup.cmd incluso in questo esempio consente di configurare il server e il servizio token di sicurezza con i relativi certificati per eseguire un'applicazione indipendente.Il file batch crea due certificati, entrambi nell'archivio certificati di CurrentUser\/TrustedPeople.Il primo certificato ha un nome soggetto di CN\=STS e viene utilizzato dal servizio token di protezione per firmare i token di protezione emessi al client.Il secondo certificato ha un nome soggetto di CN\=localhost e viene utilizzato dal servizio token di sicurezza per crittografare una chiave privata in modo che il servizio sia in grado di decrittografarla.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Eseguire il file Setup.cmd per creare i certificati richiesti.  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).Assicurarsi che tutti i progetti nella soluzione siano stati generati  \(Shared, RSTRSTR, Service, SecurityTokenService e Client\).  
  
3.  Assicurarsi che Service.exe e SecurityTokenService.exe siano entrambi in esecuzione con privilegi di amministratore.  
  
4.  Eseguire Client.exe.  
  
#### Per eseguire la pulizia dopo l'esempio  
  
1.  Eseguire Cleanup.cmd nella cartella degli esempi una volta completato l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Security\DurableIssuedTokenProvider`  
  
## Vedere anche