---
title: "Token personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e7fd8b38-c370-454f-ba3e-19759019f03d
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Token personalizzato
In questo esempio viene illustrato come aggiungere un'implementazione del token personalizzata in un'applicazione di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Nell'esempio viene usato un `CreditCardToken` per passare in modo protetto le informazioni sulle carte di credito del client al servizio.  Il token viene passato nell'intestazione del messaggio WS\-Security e viene firmato e crittografato usando l'elemento di associazione di sicurezza simmetrica, il corpo del messaggio e altre intestazioni del messaggio.  Questa operazione è utile nei casi in cui i token incorporati non sono sufficienti  In questo esempio viene illustrato come fornire un token di sicurezza personalizzato a un servizio, invece di usare uno dei token incorporati.  Il servizio implementa un contratto che definisce un modello di comunicazione richiesta\/risposta.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Per riassumere, questo esempio dimostra quanto segue.  
  
-   In che modo un client può passare un token di sicurezza personalizzato a un servizio.  
  
-   In che modo il servizio può usare e convalidare un token di sicurezza personalizzato.  
  
-   In che modo il codice del servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può ottenere le informazioni sui token di sicurezza ricevuti, compreso il token di sicurezza personalizzato.  
  
-   Come viene usato il certificato X.509 del server per proteggere la chiave simmetrica usata per crittografare il messaggio e la firma.  
  
## Autenticazione client tramite un token di sicurezza personalizzato  
 Il servizio espone un solo endpoint che viene creato a livello di programmazione usando le classi `BindingHelper` e `EchoServiceHost`.  L'endpoint è costituito da un indirizzo, un'associazione e un contratto.  L'associazione è configurata con un'associazione personalizzata usando `SymmetricSecurityBindingElement` e `HttpTransportBindingElement`.  Questo esempio imposta `SymmetricSecurityBindingElement` per usare un certificato X.509 del servizio per proteggere la chiave simmetrica durante la trasmissione e per passare un `CreditCardToken` personalizzato in un'intestazione del messaggio WS\-Security come token di sicurezza firmato e crittografato.  Il comportamento specifica le credenziali del servizio che devono essere usate per l'autenticazione del client e anche informazioni sul certificato X.509 del servizio.  
  
```  
public static class BindingHelper  
{  
    public static Binding CreateCreditCardBinding()  
    {  
        HttpTransportBindingElement httpTransport = new HttpTransportBindingElement();  
  
        // The message security binding element will be configured to require a credit card.  
        // The token that is encrypted with the service's certificate.   
        SymmetricSecurityBindingElement messageSecurity = new SymmetricSecurityBindingElement();  
        messageSecurity.EndpointSupportingTokenParameters.SignedEncrypted.Add(new CreditCardTokenParameters());  
        X509SecurityTokenParameters x509ProtectionParameters = new X509SecurityTokenParameters();  
        x509ProtectionParameters.InclusionMode = SecurityTokenInclusionMode.Never;  
        messageSecurity.ProtectionTokenParameters = x509ProtectionParameters;  
        return new CustomBinding(messageSecurity, httpTransport);  
    }  
}  
```  
  
 Per usare un token della carta di credito nel messaggio l'esempio usa credenziali del servizio personalizzate per fornire questa funzionalità.  La classe delle credenziali del servizio si trova nella classe `CreditCardServiceCredentials` e viene aggiunta alle raccolte di comportamenti dell'host del servizio nel metodo `EchoServiceHost.InitializeRuntime`.  
  
```  
class EchoServiceHost : ServiceHost  
{  
    string creditCardFile;  
  
    public EchoServiceHost(parameters Uri[] addresses)  
        : base(typeof(EchoService), addresses)  
    {  
        creditCardFile = ConfigurationManager.AppSettings["creditCardFile"];  
        if (string.IsNullOrEmpty(creditCardFile))  
        {  
            throw new ConfigurationErrorsException("creditCardFile not specified in service config");  
        }  
  
        creditCardFile = String.Format("{0}\\{1}", System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath, creditCardFile);  
  
    }  
  
    override protected void InitializeRuntime()  
    {  
        // Create a credit card service credentials and add it to the behaviors.  
        CreditCardServiceCredentials serviceCredentials = new CreditCardServiceCredentials(this.creditCardFile);  
        serviceCredentials.ServiceCertificate.SetCertificate("CN=localhost", StoreLocation.LocalMachine, StoreName.My);  
        this.Description.Behaviors.Remove((typeof(ServiceCredentials)));  
        this.Description.Behaviors.Add(serviceCredentials);  
  
        // Register a credit card binding for the endpoint.  
        Binding creditCardBinding = BindingHelper.CreateCreditCardBinding();  
        this.AddServiceEndpoint(typeof(IEchoService), creditCardBinding, string.Empty);  
  
        base.InitializeRuntime();  
    }  
}  
  
```  
  
 L'endpoint del client viene configurato in modo simile all'endpoint del servizio.  Il client usa la stessa classe `BindingHelper` per creare un'associazione.  Il resto dell'installazione è situato nella classe `Client`.  Il client imposta inoltre le informazioni contenute nel `CreditCardToken` e le informazioni sul certificato X.509 del servizio nel codice di impostazione aggiungendo un'istanza `CreditCardClientCredentials` con i dati appropriati alla raccolta di comportamenti dell'endpoint.  L'esempio usa il certificato X.509 con il nome del soggetto impostato su `CN=localhost` come certificato del servizio.  
  
```  
Binding creditCardBinding = BindingHelper.CreateCreditCardBinding();  
EndpointAddress serviceAddress = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
  
// Create a client with given client endpoint configuration  
channelFactory =   
new ChannelFactory<IEchoService>(creditCardBinding, serviceAddress);  
  
// configure the credit card credentials on the channel factory   
CreditCardClientCredentials credentials =   
      new CreditCardClientCredentials(  
      new CreditCardInfo(creditCardNumber, issuer, expirationTime));  
// configure the service certificate on the credentials  
credentials.ServiceCertificate.SetDefaultCertificate(  
      "CN=localhost", StoreLocation.LocalMachine, StoreName.My);  
  
// replace ClientCredentials with CreditCardClientCredentials  
channelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));  
channelFactory.Endpoint.Behaviors.Add(credentials);  
  
client = channelFactory.CreateChannel();  
  
Console.WriteLine("Echo service returned: {0}", client.Echo());  
  
((IChannel)client).Close();  
channelFactory.Close();  
```  
  
## Implementazione del token di sicurezza personalizzato  
 Per abilitare un token di sicurezza personalizzato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], creare una rappresentazione dell'oggetto del token di sicurezza personalizzato.  Nell'esempio la rappresentazione si trova nella classe `CreditCardToken`.  La rappresentazione dell'oggetto contiene tutte le informazioni del token di sicurezza pertinenti e fornisce un elenco di chiavi di sicurezza contenute nel token di sicurezza.  In questo caso, il token di sicurezza della carta di credito non contiene chiavi di sicurezza.  
  
 La prossima sezione descrive le operazioni da eseguire per consentire la trasmissione in rete di un token personalizzato e il suo utilizzo da parte di un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
```  
class CreditCardToken : SecurityToken  
{  
    CreditCardInfo cardInfo;  
    DateTime effectiveTime = DateTime.UtcNow;  
    string id;  
    ReadOnlyCollection<SecurityKey> securityKeys;  
  
    public CreditCardToken(CreditCardInfo cardInfo) : this(cardInfo, Guid.NewGuid().ToString()) { }  
  
    public CreditCardToken(CreditCardInfo cardInfo, string id)  
    {  
        if (cardInfo == null)  
            throw new ArgumentNullException("cardInfo");  
  
        if (id == null)  
            throw new ArgumentNullException("id");  
  
        this.cardInfo = cardInfo;  
        this.id = id;  
  
        // The credit card token is not capable of any cryptography.  
        this.securityKeys = new ReadOnlyCollection<SecurityKey>(new List<SecurityKey>());  
    }  
  
    public CreditCardInfo CardInfo { get { return this.cardInfo; } }  
  
    public override ReadOnlyCollection<SecurityKey> SecurityKeys { get { return this.securityKeys; } }  
  
    public override DateTime ValidFrom { get { return this.effectiveTime; } }  
    public override DateTime ValidTo { get { return this.cardInfo.ExpirationDate; } }  
    public override string Id { get { return this.id; } }  
}  
  
```  
  
## Recupero del token della carta di credito personalizzato a e da il messaggio  
 I serializzatori di token di sicurezza in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono responsabili per la creazione di una rappresentazione dell'oggetto dei token di sicurezza dal XML nel messaggio e della creazione di un modulo XML dei token di sicurezza.  Sono inoltre responsabili per altre funzionalità, ad esempio per la lettura e la scrittura degli identificatori di chiave che puntano ai token di sicurezza, ma in questo esempio viene usata solo la funzionalità relativa al token di sicurezza.  Per abilitare un token personalizzato è necessario implementare un serializzatore del token di sicurezza.  In questo esempio viene usata la classe `CreditCardSecurityTokenSerializer` a questo scopo.  
  
 Nel servizio, il serializzatore personalizzato legge il modulo XML del token personalizzato e lo usa per creare la rappresentazione dell'oggetto del token personalizzato.  
  
 Nel client, la classe `CreditCardSecurityTokenSerializer` scrive le informazioni contenute nella rappresentazione dell'oggetto del token di sicurezza nel writer XML.  
  
```  
public class CreditCardSecurityTokenSerializer : WSSecurityTokenSerializer  
{  
    public CreditCardSecurityTokenSerializer(SecurityTokenVersion version) : base() { }  
  
    protected override bool CanReadTokenCore(XmlReader reader)  
    {  
        XmlDictionaryReader localReader = XmlDictionaryReader.CreateDictionaryReader(reader);  
  
        if (reader == null) throw new ArgumentNullException("reader");  
  
        if (reader.IsStartElement(Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace))  
            return true;  
  
        return base.CanReadTokenCore(reader);  
    }  
  
    protected override SecurityToken ReadTokenCore(XmlReader reader, SecurityTokenResolver tokenResolver)  
    {  
        if (reader == null) throw new ArgumentNullException("reader");  
  
        if (reader.IsStartElement(Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace))  
        {  
            string id = reader.GetAttribute(Constants.Id, Constants.WsUtilityNamespace);  
  
            reader.ReadStartElement();  
  
            // Read the credit card number.  
            string creditCardNumber = reader.ReadElementString(Constants.CreditCardNumberElementName, Constants.CreditCardTokenNamespace);  
  
            // Read the expiration date.  
            string expirationTimeString = reader.ReadElementString(Constants.CreditCardExpirationElementName, Constants.CreditCardTokenNamespace);  
            DateTime expirationTime = XmlConvert.ToDateTime(expirationTimeString, XmlDateTimeSerializationMode.Utc);  
  
            // Read the issuer of the credit card.  
            string creditCardIssuer = reader.ReadElementString(Constants.CreditCardIssuerElementName, Constants.CreditCardTokenNamespace);  
            reader.ReadEndElement();  
  
            CreditCardInfo cardInfo = new CreditCardInfo(creditCardNumber, creditCardIssuer, expirationTime);  
  
            return new CreditCardToken(cardInfo, id);  
        }  
        else  
        {  
            return WSSecurityTokenSerializer.DefaultInstance.ReadToken(reader, tokenResolver);  
        }  
    }  
  
    protected override bool CanWriteTokenCore(SecurityToken token)  
    {  
        if (token is CreditCardToken)  
            return true;  
  
        else  
            return base.CanWriteTokenCore(token);  
    }  
  
    protected override void WriteTokenCore(XmlWriter writer, SecurityToken token)  
    {  
        if (writer == null) { throw new ArgumentNullException("writer"); }  
        if (token == null) { throw new ArgumentNullException("token"); }  
  
        CreditCardToken c = token as CreditCardToken;  
        if (c != null)  
        {  
            writer.WriteStartElement(Constants.CreditCardTokenPrefix, Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace);  
            writer.WriteAttributeString(Constants.WsUtilityPrefix, Constants.Id, Constants.WsUtilityNamespace, token.Id);  
            writer.WriteElementString(Constants.CreditCardNumberElementName, Constants.CreditCardTokenNamespace, c.CardInfo.CardNumber);  
            writer.WriteElementString(Constants.CreditCardExpirationElementName, Constants.CreditCardTokenNamespace, XmlConvert.ToString(c.CardInfo.ExpirationDate, XmlDateTimeSerializationMode.Utc));  
            writer.WriteElementString(Constants.CreditCardIssuerElementName, Constants.CreditCardTokenNamespace, c.CardInfo.CardIssuer);  
            writer.WriteEndElement();  
            writer.Flush();  
        }  
        else  
        {  
            base.WriteTokenCore(writer, token);  
        }  
    }  
}  
```  
  
## Come creare classi di provider di token e di autenticatori del token  
 Le credenziali del client e del servizio sono responsabili per fornire l'istanza del gestore del token di sicurezza.  L'istanza del gestore del token di sicurezza viene usato per ottenere i provider di token, gli autenticatori del token e i serializzatori di token.  
  
 Il provider di token crea una rappresentazione dell'oggetto del token in base alle informazioni contenute nelle credenziali del client o del servizio.  La rappresentazione dell'oggetto del token viene quindi scritta nel messaggio usando il serializzatore di token \(descritto nella sezione precedente\).  
  
 L'autenticatore del token convalida i token che arrivano nel messaggio.  La rappresentazione dell'oggetto del token in arrivo viene creata dal serializzatore di token.  Questa rappresentazione dell'oggetto viene quindi passata all'autenticatore del token per la convalida.  Una volta convalidato correttamente il token, l'autenticatore del token restituisce una raccolta di oggetti `IAuthorizationPolicy` che rappresentano le informazioni contenute nel token.  Queste informazioni vengono usate in un secondo momento durante l'elaborazione del messaggio per prendere decisioni di autorizzazione e fornire attestazioni per l'applicazione.  In questo esempio, l'autenticatore del token della carta di credito usa `CreditCardTokenAuthorizationPolicy` a questo scopo.  
  
 Il serializzatore di token ha la responsabilità di ottenere la rappresentazione dell'oggetto del token alla e dalla rete.  Questa operazione viene descritta nella sezione precedente.  
  
 In questo esempio, si usa un provider di token solo nel client e un autenticatore del token solo nel servizio, per trasmettere un token della carta di credito solo nella direzione dal client al servizio.  
  
 Nel client la funzionalità si trova nelle classi `CreditCardClientCrendentials`, `CreditCardClientCredentialsSecurityTokenManager` e `CreditCardTokenProvider`.  
  
 Nel servizio, la funzionalità si trova nelle classi `CreditCardServiceCredentials`, `CreditCardServiceCredentialsSecurityTokenManager`, `CreditCardTokenAuthenticator` e `CreditCardTokenAuthorizationPolicy`.  
  
```  
    public class CreditCardClientCredentials : ClientCredentials  
    {  
        CreditCardInfo creditCardInfo;  
  
        public CreditCardClientCredentials(CreditCardInfo creditCardInfo)  
            : base()  
        {  
            if (creditCardInfo == null)  
                throw new ArgumentNullException("creditCardInfo");  
  
            this.creditCardInfo = creditCardInfo;  
        }  
  
        public CreditCardInfo CreditCardInfo  
        {  
            get { return this.creditCardInfo; }  
        }  
  
        protected override ClientCredentials CloneCore()  
        {  
            return new CreditCardClientCredentials(this.creditCardInfo);  
        }  
  
        public override SecurityTokenManager CreateSecurityTokenManager()  
        {  
            return new CreditCardClientCredentialsSecurityTokenManager(this);  
        }  
    }  
  
public class CreditCardClientCredentialsSecurityTokenManager : ClientCredentialsSecurityTokenManager  
    {  
        CreditCardClientCredentials creditCardClientCredentials;  
  
        public CreditCardClientCredentialsSecurityTokenManager(CreditCardClientCredentials creditCardClientCredentials)  
            : base (creditCardClientCredentials)  
        {  
            this.creditCardClientCredentials = creditCardClientCredentials;  
        }  
  
        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)  
        {  
            // handle this token for Custom  
            if (tokenRequirement.TokenType == Constants.CreditCardTokenType)  
                return new CreditCardTokenProvider(this.creditCardClientCredentials.CreditCardInfo);  
            // return server cert  
            else if (tokenRequirement is InitiatorServiceModelSecurityTokenRequirement)  
            {  
                if (tokenRequirement.TokenType == SecurityTokenTypes.X509Certificate)  
                {  
                    return new X509SecurityTokenProvider(creditCardClientCredentials.ServiceCertificate.DefaultCertificate);  
                }  
            }  
  
            return base.CreateSecurityTokenProvider(tokenRequirement);  
        }  
  
        public override SecurityTokenSerializer CreateSecurityTokenSerializer(SecurityTokenVersion version)  
        {  
  
            return new CreditCardSecurityTokenSerializer(version);  
        }  
  
    }  
  
    class CreditCardTokenProvider : SecurityTokenProvider  
    {  
        CreditCardInfo creditCardInfo;  
  
        public CreditCardTokenProvider(CreditCardInfo creditCardInfo) : base()  
        {  
            if (creditCardInfo == null)  
            {  
                throw new ArgumentNullException("creditCardInfo");  
            }  
            this.creditCardInfo = creditCardInfo;  
        }  
  
        protected override SecurityToken GetTokenCore(TimeSpan timeout)  
        {  
            SecurityToken result = new CreditCardToken(this.creditCardInfo);  
            return result;  
        }  
    }  
  
public class CreditCardServiceCredentials : ServiceCredentials  
    {  
        string creditCardFile;  
  
        public CreditCardServiceCredentials(string creditCardFile)  
            : base()  
        {   
            if (creditCardFile == null)  
                throw new ArgumentNullException("creditCardFile");  
  
            this.creditCardFile = creditCardFile;  
        }  
  
        public string CreditCardDataFile  
        {  
            get { return this.creditCardFile; }  
        }  
  
        protected override ServiceCredentials CloneCore()  
        {  
            return new CreditCardServiceCredentials(this.creditCardFile);  
        }  
  
        public override SecurityTokenManager CreateSecurityTokenManager()  
        {  
            return new CreditCardServiceCredentialsSecurityTokenManager(this);  
        }  
    }  
  
public class CreditCardServiceCredentialsSecurityTokenManager : ServiceCredentialsSecurityTokenManager  
{  
        CreditCardServiceCredentials creditCardServiceCredentials;  
  
        public CreditCardServiceCredentialsSecurityTokenManager(CreditCardServiceCredentials creditCardServiceCredentials)  
            : base(creditCardServiceCredentials)  
        {  
            this.creditCardServiceCredentials = creditCardServiceCredentials;  
        }  
  
        public override SecurityTokenAuthenticator CreateSecurityTokenAuthenticator(SecurityTokenRequirement tokenRequirement, out SecurityTokenResolver outOfBandTokenResolver)  
        {  
            if (tokenRequirement.TokenType == Constants.CreditCardTokenType)  
            {  
                outOfBandTokenResolver = null;  
                return new CreditCardTokenAuthenticator(creditCardServiceCredentials.CreditCardDataFile);  
            }  
  
            return base.CreateSecurityTokenAuthenticator(tokenRequirement, out outOfBandTokenResolver);  
        }  
  
        public override SecurityTokenSerializer CreateSecurityTokenSerializer(SecurityTokenVersion version)  
        {  
            return new CreditCardSecurityTokenSerializer(version);  
        }  
    }  
  
    class CreditCardTokenAuthenticator : SecurityTokenAuthenticator  
    {  
        string creditCardsFile;  
        public CreditCardTokenAuthenticator(string creditCardsFile)  
        {  
            this.creditCardsFile = creditCardsFile;  
        }  
  
        protected override bool CanValidateTokenCore(SecurityToken token)  
        {  
            return (token is CreditCardToken);  
        }  
  
        protected override ReadOnlyCollection<IAuthorizationPolicy> ValidateTokenCore(SecurityToken token)  
        {  
            CreditCardToken creditCardToken = token as CreditCardToken;  
  
            if (creditCardToken.CardInfo.ExpirationDate < DateTime.UtcNow)  
                throw new SecurityTokenValidationException("The credit card has expired");  
            if (!IsCardNumberAndExpirationValid(creditCardToken.CardInfo))  
                throw new SecurityTokenValidationException("Unknown or invalid credit card");  
  
            // the credit card token has only 1 claim - the card number. The issuer for the claim is the  
            // credit card issuer  
  
            DefaultClaimSet cardIssuerClaimSet = new DefaultClaimSet(new Claim(ClaimTypes.Name, creditCardToken.CardInfo.CardIssuer, Rights.PossessProperty));  
            DefaultClaimSet cardClaimSet = new DefaultClaimSet(cardIssuerClaimSet, new Claim(Constants.CreditCardNumberClaim, creditCardToken.CardInfo.CardNumber, Rights.PossessProperty));  
            List<IAuthorizationPolicy> policies = new List<IAuthorizationPolicy>(1);  
            policies.Add(new CreditCardTokenAuthorizationPolicy(cardClaimSet));  
            return policies.AsReadOnly();  
        }  
  
        /// <summary>  
        /// Helper method to check if a given credit card entry is present in the User DB  
        /// </summary>  
        private bool IsCardNumberAndExpirationValid(CreditCardInfo cardInfo)  
        {  
            try  
            {  
                using (StreamReader myStreamReader = new StreamReader(this.creditCardsFile))  
                {  
                    string line = "";  
                    while ((line = myStreamReader.ReadLine()) != null)  
                    {  
                        string[] splitEntry = line.Split('#');  
                        if (splitEntry[0] == cardInfo.CardNumber)  
                        {  
                            string expirationDateString = splitEntry[1].Trim();  
                            DateTime expirationDateOnFile = DateTime.Parse(expirationDateString, System.Globalization.DateTimeFormatInfo.InvariantInfo, System.Globalization.DateTimeStyles.AdjustToUniversal);  
                            if (cardInfo.ExpirationDate == expirationDateOnFile)  
                            {  
                                string issuer = splitEntry[2];  
                                return issuer.Equals(cardInfo.CardIssuer, StringComparison.InvariantCultureIgnoreCase);  
                            }  
                            else  
                            {  
                                return false;  
                            }  
                        }  
                    }  
                    return false;  
                }  
            }  
            catch (Exception e)  
            {  
                throw new Exception("BookStoreService: Error while retrieving credit card information from User DB " + e.ToString());  
            }  
        }  
    }  
  
    public class CreditCardTokenAuthorizationPolicy : IAuthorizationPolicy  
    {  
        string id;  
        ClaimSet issuer;  
        IEnumerable<ClaimSet> issuedClaimSets;  
  
        public CreditCardTokenAuthorizationPolicy(ClaimSet issuedClaims)  
        {  
            if (issuedClaims == null)  
                throw new ArgumentNullException("issuedClaims");  
            this.issuer = issuedClaims.Issuer;  
            this.issuedClaimSets = new ClaimSet[] { issuedClaims };  
            this.id = Guid.NewGuid().ToString();  
        }  
  
        public ClaimSet Issuer { get { return this.issuer; } }  
  
        public string Id { get { return this.id; } }  
  
        public bool Evaluate(EvaluationContext context, ref object state)  
        {  
            foreach (ClaimSet issuance in this.issuedClaimSets)  
            {  
                context.AddClaimSet(this, issuance);  
            }  
  
            return true;  
        }  
    }  
  
```  
  
## Visualizzazione delle informazioni sul chiamante  
 Per visualizzare le informazioni sul chiamante, usare `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` come illustrato nell'esempio di codice seguente.  `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` contiene attestazioni di autorizzazione associate al chiamante corrente.  Le attestazioni vengono fornite dalla classe `CreditCardToken` nella raccolta `AuthorizationPolicies`.  
  
```  
bool TryGetStringClaimValue(ClaimSet claimSet, string claimType, out string claimValue)  
{  
    claimValue = null;  
    IEnumerable<Claim> matchingClaims = claimSet.FindClaims(claimType,  
        Rights.PossessProperty);  
    if (matchingClaims == null)  
        return false;  
    IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();  
    enumerator.MoveNext();  
    claimValue = (enumerator.Current.Resource == null) ? null :   
        enumerator.Current.Resource.ToString();  
    return true;  
}  
  
string GetCallerCreditCardNumber()  
{  
     foreach (ClaimSet claimSet in   
         ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)  
     {  
         string creditCardNumber = null;  
         if (TryGetStringClaimValue(claimSet,   
             Constants.CreditCardNumberClaim, out creditCardNumber))  
             {  
                 string issuer;  
                 if (!TryGetStringClaimValue(claimSet.Issuer,  
                        ClaimTypes.Name, out issuer))  
                 {  
                     issuer = "Unknown";  
                 }  
                 return String.Format(  
                   "Credit card '{0}' issued by '{1}'",   
                   creditCardNumber, issuer);  
        }  
    }  
    return "Credit card is not known";  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.  Premere INVIO nella finestra del client per arrestare il client.  
  
## File batch di installazione  
 Il file batch Setup.bat incluso con questo esempio consente di configurare il server con i certificati attinenti per eseguire l'applicazione ospitata da IIS che richiede la sicurezza server basata su certificato.  Questo file batch deve essere modificato per funzionare tra computer diversi o nel caso in cui non sia ospitato.  
  
 Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.  
  
-   Creazione del certificato server:  
  
     Le righe seguenti del file batch `Setup.bat` creano il certificato server da usare.  La variabile `%SERVER_NAME%`  specifica il nome del server.  Modificare questa variabile per specificare nome del server.  Il valore predefinito in questo file batch è localhost.  Se si modifica la variabile `%SERVER_NAME%`, è necessario sostituire tutte le istanze di localhost nei file Client.cs e Service.cs con il nome del server che si usa nello script Setup.bat.  
  
     Il certificato viene memorizzato nell'archivio personale nel percorso di archivio `LocalMachine`.  Il certificato viene archiviato nell'archivio LocalMachine per i servizi ospitati su IIS.  Per i servizi indipendenti, è necessario modificare il file batch per archiviare il certificato del client nel percorso dell'archivio CurrentUser sostituendo la stringa LocalMachine con CurrentUser.  
  
    ```  
  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
  
    ```  
  
-   Installazione del certificato server nell'archivio certificati attendibili del client:  
  
     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client.  Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.  Se è già disponibile un certificato con radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio del popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
  
    echo ************  
    echo copying server cert to client's TrustedPeople store  
    echo ************  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
  
    ```  
  
-   Per abilitare l'accesso alla chiave privata del certificato dal servizio ospitato su IIS, è necessario concedere le autorizzazioni alla chiave privata appropriate all'account utente con cui viene eseguito il processo ospitato da IIS.  Questa operazione viene eseguita negli ultimi passaggi dello script Setup.bat.  
  
    ```  
    echo ************  
    echo setting privileges on server certificates  
    echo ************  
    for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i  
    set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
    (ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
    iisreset  
    ```  
  
> [!NOTE]
>  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  La variabile di ambiente PATH impostata nel prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] punta alla directory che contiene file eseguibili richiesti dallo script Setup.bat.  
  
#### Per impostare e compilare l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
#### Per eseguire l'esempio nello stesso computer  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.  In questo modo vengono installati tutti i certificati richiesti per l'esecuzione dell'esempio. Verificare che percorso includa la cartella in cui è presente Makecert.exe.  
  
> [!NOTE]
>  Assicurarsi di rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio.  Negli altri esempi relativi alla sicurezza vengono usati gli stessi certificati.  
  
1.  Avviare Client.exe dalla directory client\\bin.  L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
2.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio per i file binari del servizio.  
  
2.  Copiare i file di programma del servizio nella directory del servizio sul computer relativo.  Ricordarsi di copiare CreditCardFile.txt. In caso contrario l'autenticatore della carta di credito non può convalidare le informazioni della carta di credito inviate dal client.  Copiare i file Setup.bat e Cleanup.bat nel computer del servizio.  
  
3.  È necessario disporre di un certificato server con il nome del soggetto che contiene il nome di dominio completo del computer.  È possibile crearne uno usando Setup.bat se si modifica la variabile `%SERVER_NAME%` con il nome host completo del computer sul quale è ospitato il servizio.  Si noti che è necessario eseguire il file Setup.bat in un prompt dei comandi di Visual Studio aperto con privilegi di amministratore.  
  
4.  Copiare il certificato server nell'archivio CurrentUser\-TrustedPeople del client.  Questo passaggio è necessario solo se il certificato server non è emesso da un'autorità emittente attendibile.  
  
5.  Nel file EchoServiceHost.cs modificare il valore del nome del soggetto del certificato per specificare un nome del computer completo anziché localhost.  
  
6.  Copiare i file del programma client dalla cartella \\client\\bin\\, presente nella cartella specifica del linguaggio, nel computer client.  
  
7.  Nel file Client.cs modificare il valore dell'indirizzo dell'endpoint affinché corrisponda al nuovo indirizzo del servizio.  
  
8.  Nel file Client.cs modificare il nome del soggetto del certificato X.509 del servizio affinché corrisponda al nome del computer completo dell'host remoto anziché localhost.  
  
9. Sul computer client avviare Client.exe da una finestra del prompt dei comandi.  
  
10. Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire la pulizia dopo l'esempio  
  
1.  Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
## Vedere anche