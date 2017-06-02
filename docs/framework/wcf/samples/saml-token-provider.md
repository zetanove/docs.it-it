---
title: "Provider di token SAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb16e5e2-4c8d-4f61-a479-9c965fcec80c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Provider di token SAML
Questo esempio dimostra come implementare un provider di token SAML client personalizzato.  Un provider di token in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è usato per fornire credenziali all'infrastruttura di sicurezza.  In generale, il provider di token esamina la destinazione ed emette credenziali adatte in modo che l'infrastruttura di sicurezza possa proteggere il messaggio.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene fornito con il provider di token di Gestione credenziali predefinito.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene anche fornito con un provider di token [!INCLUDE[infocard](../../../../includes/infocard-md.md)].  I provider di token personalizzati sono utili nei casi seguenti:  
  
-   Se è disponibile un archivio di credenziali con cui questi provider di token non sono in grado di operare.  
  
-   Se si vuole fornire un meccanismo personalizzato per la trasformazione delle credenziali dal punto in cui l'utente fornisce i dettagli a quello in cui il framework client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa le credenziali.  
  
-   Se si sta compilando un token personalizzato.  
  
 Questo esempio mostra come compilare un provider di token personalizzato che consente di usare un token SAML ottenuto dall'esterno del framework client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Per riassumere, questo esempio dimostra quanto segue.  
  
-   Come è possibile configurare un client con un provider personalizzato.  
  
-   Come è possibile passare un token SAML alle credenziali client personalizzate.  
  
-   Come viene fornito il token SAML al framework client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Come viene autenticato il servizio dal client mediante il certificato X.509 del server.  
  
 Il servizio espone due endpoint per comunicare con il servizio definito mediante il file di configurazione App.config.  Ciascun endpoint è costituito da un indirizzo, un binding e un contratto.  L'associazione è configurata con una classe `wsFederationHttpBinding` standard che usa la sicurezza del messaggio.  Un endpoint attende che il client si autentichi con un token SAML che usa una chiave di prova simmetrica mentre l'altro attende che il client si autentichi con un token SAML che usa una chiave di prova asimmetrica.  Il servizio configura anche il certificato del servizio usando il comportamento `serviceCredentials`.  Il comportamento `serviceCredentials` consente di configurare un certificato del servizio.  Un certificato del servizio viene usato da un client per autenticare il servizio e fornire protezione del messaggio.  La configurazione seguente fa riferimento al certificato "localhost" installato durante l'installazione dell'esempio come descritto nelle istruzioni fornite alla fine di questo argomento.  Il comportamento `serviceCredentials` consente anche di configurare certificati che sono attendibili per la firma di token SAML.  La configurazione seguente fa riferimento al certificato 'Alice' installato durante l'esempio.  
  
```  
<system.serviceModel>  
 <services>  
  <service   
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
   <host>  
    <baseAddresses>  
     <!-- configure base address provided by host -->  
     <add    
  baseAddress="http://localhost:8000/servicemodelsamples/service/" />  
    </baseAddresses>  
   </host>  
   <!-- use base address provided by host -->  
   <!-- Endpoint that expect SAML tokens with Symmetric proof keys -->  
   <endpoint address="calc/symm"  
             binding="wsFederationHttpBinding"  
             bindingConfiguration="Binding1"   
             contract="Microsoft.ServiceModel.Samples.ICalculator" />  
   <!-- Endpoint that expect SAML tokens with Asymmetric proof keys -->  
   <endpoint address="calc/asymm"  
             binding="wsFederationHttpBinding"  
             bindingConfiguration="Binding2"   
             contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  </service>  
 </services>  
  
 <bindings>  
  <wsFederationHttpBinding>  
   <!-- Binding that expect SAML tokens with Symmetric proof keys -->  
   <binding name="Binding1">  
    <security mode="Message">  
     <message negotiateServiceCredential ="false"   
              issuedKeyType="SymmetricKey"   
              issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"  />  
    </security>  
   </binding>  
   <!-- Binding that expect SAML tokens with Asymmetric proof keys -->  
   <binding name="Binding2">  
    <security mode="Message">  
     <message negotiateServiceCredential ="false"  
              issuedKeyType="AsymmetricKey"   
              issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"  />  
    </security>  
   </binding>          
  </wsFederationHttpBinding>  
 </bindings>  
  
 <behaviors>  
  <serviceBehaviors>  
   <behavior name="CalculatorServiceBehavior">  
    <!--   
    The serviceCredentials behavior allows one to define a service certificate.  
    A service certificate is used by a client to authenticate the service and provide message protection.  
    This configuration references the "localhost" certificate installed during the setup instructions.  
    -->  
    <serviceCredentials>  
     <!-- Set allowUntrustedRsaIssuers to true to allow self-signed, asymmetric key based SAML tokens -->  
     <issuedTokenAuthentication allowUntrustedRsaIssuers ="true" >  
      <!-- Add Alice to the list of certs trusted to issue SAML tokens -->  
      <knownCertificates>  
       <add storeLocation="LocalMachine"   
            storeName="TrustedPeople"   
            x509FindType="FindBySubjectName"   
            findValue="Alice"/>  
      </knownCertificates>  
     </issuedTokenAuthentication>  
     <serviceCertificate storeLocation="LocalMachine"  
                         storeName="My"  
                         x509FindType="FindBySubjectName"  
                         findValue="localhost"  />  
    </serviceCredentials>  
   </behavior>  
  </serviceBehaviors>  
 </behaviors>  
  
</system.serviceModel>  
```  
  
 I passaggi seguenti illustrano come sviluppare un provider di token SAML personalizzato e integrarlo nel framework di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
1.  Scrivere un provider di token SAML personalizzato.  
  
     L'esempio implementa un provider di token SAML personalizzato che restituisce un token di sicurezza basato su un'asserzione SAML fornita in fase di costruzione.  
  
     Per eseguire questa attività il provider di token personalizzato viene derivato dalla classe <xref:System.IdentityModel.Selectors.SecurityTokenProvider> ed esegue l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A>.  Questo metodo creare e restituisce un nuovo `SecurityToken`.  
  
    ```  
    protected override SecurityToken GetTokenCore(TimeSpan timeout)  
    {  
     // Create a SamlSecurityToken from the provided assertion  
     SamlSecurityToken samlToken = new SamlSecurityToken(assertion);  
  
     // Create a SecurityTokenSerializer that will be used to   
     // serialize the SamlSecurityToken  
     WSSecurityTokenSerializer ser = new WSSecurityTokenSerializer();  
     // Create a memory stream to write the serialized token into  
     // Use an initial size of 64Kb  
     MemoryStream s = new MemoryStream(UInt16.MaxValue);  
  
     // Create an XmlWriter over the stream  
     XmlWriter xw = XmlWriter.Create(s);  
  
     // Write the SamlSecurityToken into the stream  
     ser.WriteToken(xw, samlToken);  
  
     // Seek back to the beginning of the stream  
     s.Seek(0, SeekOrigin.Begin);  
  
     // Load the serialized token into a DOM  
     XmlDocument dom = new XmlDocument();  
     dom.Load(s);  
  
     // Create a KeyIdentifierClause for the SamlSecurityToken  
     SamlAssertionKeyIdentifierClause samlKeyIdentifierClause = samlToken.CreateKeyIdentifierClause<SamlAssertionKeyIdentifierClause>();  
  
    // Return a GenericXmlToken from the XML for the   
    // SamlSecurityToken, the proof token, the valid from and valid  
    // until times from the assertion and the key identifier clause  
    // created above  
    return new GenericXmlSecurityToken(dom.DocumentElement, proofToken, assertion.Conditions.NotBefore, assertion.Conditions.NotOnOrAfter, samlKeyIdentifierClause, samlKeyIdentifierClause, null);  
    }  
    ```  
  
2.  Scrivere il gestore di token di sicurezza personalizzato.  
  
     La classe <xref:System.IdentityModel.Selectors.SecurityTokenManager> viene usata per creare <xref:System.IdentityModel.Selectors.SecurityTokenProvider> per il <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> specifico che viene passato nel metodo `CreateSecurityTokenProvider`.  Viene inoltre usato un gestore del token di sicurezza per creare autenticatori del token e serializzatori del token, che però non sono trattati in questo esempio.  In questo esempio il gestore del token di sicurezza personalizzato eredita dalla classe <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> ed esegue l'override del metodo `CreateSecurityTokenProvider` per restituire il provider di token SAML personalizzato quando i requisiti del token passati indicano che il token SAML è richiesto.  Se la classe delle credenziali client \(vedere il passaggio 3\) non ha specificato un'asserzione, il gestore del token di sicurezza crea un'istanza appropriata.  
  
    ```  
    public class SamlSecurityTokenManager :  
     ClientCredentialsSecurityTokenManager  
    {  
     SamlClientCredentials samlClientCredentials;  
  
     public SamlSecurityTokenManager ( SamlClientCredentials samlClientCredentials)  
      : base(samlClientCredentials)  
     {  
      // Store the creating client credentials  
      this.samlClientCredentials = samlClientCredentials;  
     }  
  
     public override SecurityTokenProvider CreateSecurityTokenProvider ( SecurityTokenRequirement tokenRequirement )  
     {  
      // If token requirement matches SAML token return the   
      // custom SAML token provider  
      if (tokenRequirement.TokenType == SecurityTokenTypes.Saml ||  
          tokenRequirement.TokenType == "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1")  
      {  
       // Retrieve the SAML assertion and proof token from the   
       // client credentials  
       SamlAssertion assertion = this.samlClientCredentials.Assertion;  
       SecurityToken prooftoken = this.samlClientCredentials.ProofToken;  
  
       // If either the assertion of proof token is null...  
       if (assertion == null || prooftoken == null)  
       {  
        // ...get the SecurityBindingElement and then the   
        // specified algorithm suite  
        SecurityBindingElement sbe = null;  
        SecurityAlgorithmSuite sas = null;  
  
        if ( tokenRequirement.TryGetProperty<SecurityBindingElement> ( "http://schemas.microsoft.com/ws/2006/05/servicemodel/securitytokenrequirement/SecurityBindingElement", out sbe))  
        {  
         sas = sbe.DefaultAlgorithmSuite;  
        }  
  
        // If the token requirement is for a SymmetricKey based token..  
        if (tokenRequirement.KeyType == SecurityKeyType.SymmetricKey)  
        {  
         // Create a symmetric proof token  
         prooftoken = SamlUtilities.CreateSymmetricProofToken ( tokenRequirement.KeySize );  
         // and a corresponding assertion based on the claims specified in the client credentials  
         assertion = SamlUtilities.CreateSymmetricKeyBasedAssertion ( this.samlClientCredentials.Claims, new X509SecurityToken ( samlClientCredentials.ClientCertificate.Certificate ), new X509SecurityToken ( samlClientCredentials.ServiceCertificate.DefaultCertificate ), (BinarySecretSecurityToken)prooftoken, sas);  
        }  
        // otherwise...  
        else  
        {  
         // Create an asymmetric proof token  
         prooftoken = SamlUtilities.CreateAsymmetricProofToken();  
         // and a corresponding assertion based on the claims   
         // specified in the client credentials  
         assertion = SamlUtilities.CreateAsymmetricKeyBasedAssertion ( this.samlClientCredentials.Claims, prooftoken, sas );  
        }  
       }  
  
       // Create a SamlSecurityTokenProvider based on the assertion and proof token  
       return new SamlSecurityTokenProvider(assertion, prooftoken);  
      }  
      // otherwise use base implementation  
      else  
      {  
       return base.CreateSecurityTokenProvider(tokenRequirement);  
      }  
    }  
  
    ```  
  
3.  Scrivere una credenziale client personalizzata.  
  
     La classe delle credenziali client viene  usata per rappresentare le credenziali configurate per il proxy client e crea un gestore del token di sicurezza usato per ottenere gli autenticatori del token, i provider di token e il serializzatore di token.  
  
    ```  
    public class SamlClientCredentials : ClientCredentials  
    {  
     ClaimSet claims;  
     SamlAssertion assertion;  
     SecurityToken proofToken;  
  
     public SamlClientCredentials() : base()  
     {  
      // Set SupportInteractive to false to suppress Cardspace UI  
      base.SupportInteractive = false;  
     }  
  
     protected SamlClientCredentials(SamlClientCredentials other) : base ( other )  
     {  
      // Just do reference copy given sample nature  
      this.assertion = other.assertion;  
      this.claims = other.claims;  
      this.proofToken = other.proofToken;  
     }  
  
     public SamlAssertion Assertion { get { return assertion; } set { assertion = value; } }  
  
     public SecurityToken ProofToken { get { return proofToken; } set { proofToken = value; } }  
     public ClaimSet Claims { get { return claims; } set { claims = value; } }  
  
     protected override ClientCredentials CloneCore()  
     {  
      return new SamlClientCredentials(this);  
     }  
  
     public override SecurityTokenManager CreateSecurityTokenManager()  
     {  
      // return custom security token manager  
      return new SamlSecurityTokenManager(this);  
     }  
    }  
    ```  
  
4.  Configurare il client per l'uso della credenziale client personalizzata.  
  
     L'esempio elimina la classe della credenziale client predefinita e fornisce la nuova classe della credenziale client così il client possa usare la credenziale client personalizzata.  
  
    ```  
    // Create new credentials class  
    SamlClientCredentials samlCC = new SamlClientCredentials();  
  
    // Set the client certificate. This is the cert that will be used to sign the SAML token in the symmetric proof key case  
    samlCC.ClientCertificate.SetCertificate(StoreLocation.CurrentUser, StoreName.My, X509FindType.FindBySubjectName, "Alice");  
  
    // Set the service certificate. This is the cert that will be used to encrypt the proof key in the symmetric proof key case  
    samlCC.ServiceCertificate.SetDefaultCertificate(StoreLocation.CurrentUser, StoreName.TrustedPeople, X509FindType.FindBySubjectName, "localhost");  
  
    // Create some claims to put in the SAML assertion  
    IList<Claim> claims = new List<Claim>();  
    claims.Add(Claim.CreateNameClaim(samlCC.ClientCertificate.Certificate.Subject));  
    ClaimSet claimset = new DefaultClaimSet(claims);  
    samlCC.Claims = claimset;  
  
    // set new credentials  
    client.ChannelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));  
    client.ChannelFactory.Endpoint.Behaviors.Add(samlCC);  
    ```  
  
 Nel servizio, vengono visualizzate le richieste associate al chiamante.  Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.  Premere INVIO nella finestra del client per arrestare il client.  
  
## File batch di installazione  
 Il file batch Setup.bat incluso con questo esempio consente di configurare il server con il certificato attinente per eseguire un'applicazione indipendente che richiede sicurezza server basata su certificato.  Questo file batch deve essere modificato per funzionare tra computer diversi o nel caso in cui non sia ospitato.  
  
 Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.  
  
-   Creazione del certificato server:  
  
     Le righe seguenti del file batch Setup.bat creano il certificato server da usare.  La variabile `%SERVER_NAME%` specifica il nome del server.  Modificare questa variabile per specificare nome del server.  Il valore predefinito in questo file batch è localhost.  
  
     Il certificato viene memorizzato nell'archivio personale nel percorso di archivio LocalMachine.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss My -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
-   Installazione del certificato server nell'archivio certificati attendibile del client:  
  
     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client.  Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.  Se è già disponibile un certificato impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r LocalMachine -s TrustedPeople  
    ```  
  
-   Creazione del certificato emittente:  
  
     Le righe seguenti del file batch Setup.bat creano il certificato emittente da usare.  La variabile `%USER_NAME%` specifica il nome dell'emittente.  Modificare questa variabile per specificare nome dell'emittente.  Il valore predefinito in questo file batch è Alice.  
  
     Il certificato viene memorizzato nell'archivio personale nel percorso di archivio LocalUser.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr CurrentUser -ss My -a sha1 -n CN=%USER_NAME% -sky exchange -pe  
    ```  
  
-   Installazione del certificato emittente nell'archivio certificati attendibile del server:  
  
     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client.  Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.  Se è già disponibile un certificato che impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio della popolazione dell'archivio certificati server con il certificato emittente  non è necessario.  
  
    ```  
    certmgr.exe -add -r CurrentUser -s My -c -n %USER_NAME% -r LocalMachine -s TrustedPeople  
  
    ```  
  
#### Per impostare e compilare l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
> [!NOTE]
>  Se si usa Svcutil.exe per rigenerare la configurazione di questo esempio, assicurarsi di modificare il nome dell'endpoint nella configurazione client in modo che corrisponda al codice client.  
  
#### Per eseguire l'esempio nello stesso computer  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.  In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  La variabile di ambiente PATH impostata nel prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] punta alla directory che contiene file eseguibili richiesti dallo script Setup.bat.  
  
2.  Avviare Service.exe da service\\bin.  
  
3.  Avviare Client.exe da \\client\\bin.  L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
4.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio per i file binari del servizio.  
  
2.  Copiare i file di programma del servizio nella directory del servizio sul computer relativo.  Copiare i file Setup.bat e Cleanup.bat nel computer del servizio.  
  
3.  È necessario disporre di un certificato server con il nome del soggetto che contiene il nome di dominio completo del computer.  Il file Service.exe.config deve essere aggiornato per riflettere il nome del nuovo certificato.  È possibile creare il certificato server modificando il file batch Setup.bat.  Si noti che è necessario eseguire il file setup.bat in un prompt dei comandi di Visual Studio aperto con privilegi di amministratore.  È necessario impostare la variabile `%SERVER_NAME%` sul nome host completo del computer usato per ospitare il servizio.  
  
4.  Copiare il certificato server nell'archivio CurrentUser\-TrustedPeople del client.  Questo passaggio non è necessario quando il certificato server è emesso da un'autorità emittente client attendibile.  
  
5.  Nel file Service.exe.config sul computer del servizio modificare il valore dell'indirizzo di base per specificare un nome del computer completo anziché localhost.  
  
6.  Sul computer del servizio eseguire Service.exe da un prompt dei comandi.  
  
7.  Copiare i file del programma client dalla cartella \\client\\bin\\, presente nella cartella specifica del linguaggio, nel computer client.  
  
8.  Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.  
  
9. Sul computer client avviare `Client.exe` da una finestra del prompt dei comandi.  
  
10. Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire la pulizia dopo l'esempio  
  
1.  Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
## Vedere anche