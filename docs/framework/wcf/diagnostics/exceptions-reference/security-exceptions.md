---
title: "Eccezioni di sicurezza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 76d5e5cd-e4f4-404f-9a5a-ec3522494ad8
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Eccezioni di sicurezza
Questo argomento elenca tutte le eccezioni di sicurezza.  
  
## Elenco delle eccezioni  
  
|Codice risorsa|Stringa di risorsa|  
|--------------------|------------------------|  
|AnonymousLogonsAreNotAllowed|Accesso anonimo non consentito dal servizio.|  
|AtLeastOneContractOperationRequestRequiresProtectionLevelNotSupportedByBinding|Il messaggio di richiesta deve essere protetto,come richiesto da un'operazione del contratto specificato.La protezione deve essere implementata dall'associazione indicata.|  
|AtLeastOneContractOperationResponseRequiresProtectionLevelNotSupportedByBinding|Il messaggio di risposta deve essere protetto,come richiesto da un'operazione del contratto specificato.La protezione deve essere implementata dall'associazione indicata.|  
|AtMostOnePrimarySignatureInReceiveSecurityHeader|In un'intestazione di sicurezza è consentita solo una firma primaria.|  
|BadContextTokenFaultReason|Il token del contesto di sicurezza è scaduto o non è valido.Il messaggio non è stato elaborato.|  
|BadEncryptionState|Stato di EncryptedData o EncryptedKey non valido per questa operazione.|  
|BasicHttpMessageSecurityRequiresCertificate|L'associazione BasicHttp richiede che BasicHttpBinding.Security.Message.ClientCredentialType sia equivalente al tipo di credenziali BasicHttpMessageCredentialType.Certificate per i messaggi protetti.Selezionare la protezione Transport o TransportWithMessageCredential per le credenziali UserName.|  
|BasicTokenCannotBeWrittenWithoutEncryption|Impossibile scrivere il token di base senza crittografia.|  
|BindingDoesNotSupportProtectionForRst|L'associazione specificata per il contratto indicato è configurata con SecureConversation, ma la modalità di autenticazione non è in grado di fornire l'integrità e la riservatezza basate su request\/reply necessarie per la negoziazione.|  
|BindingDoesNotSupportWindowsIdenityForImpersonation|L'operazione specificata del contratto richiede l'identità Windows per la rappresentazione automatica.L'associazione indicata per il contratto specificato non fornisce l'identità Windows che rappresenta il chiamante.|  
|CachedNegotiationStateQuotaReached|Il servizio non è in grado di memorizzare nella cache lo stato della negoziazione poiché è stata raggiunta la capacità specificata.Ritentare la richiesta.|  
|CacheQuotaReached|Impossibile aggiungere l'elemento.Vengono riportate le dimensioni massime della cache.|  
|CannotDetermineSPNBasedOnAddress|Il client non è in grado di determinare il nome dell'entità servizio in base all'identità contenuta nell'indirizzo di destinazione specificato per SspiNegotiation\/Kerberos.L'identità indirizzo di destinazione deve essere un'identità UPN \(ad esempio dominioacme\\nomeutentee\) o un'identità SPN \(ad esempio host\/nomecomputer\).|  
|CannotFindCert|Impossibile trovare il certificato X.509 utilizzando i criteri di ricerca specificati: StoreName, StoreLocation, FindType e FindValue.|  
|CannotFindCertForTarget|Impossibile trovare il certificato X.509 utilizzando i criteri di ricerca specificati per la destinazione indicata: StoreName, StoreLocation, FindType e FindValue.|  
|CannotFindCorrelationStateForApplyingSecurity|Impossibile trovare lo stato di correlazione allo scopo di applicare la protezione per la risposta nel risponditore.|  
|CannotFindNegotiationState|Impossibile trovare lo stato di negoziazione per il contesto specificato.|  
|CannotFindSecuritySession|Impossibile trovare la sessione di sicurezza con l'ID specificato.|  
|CannotImportProtectionLevelForContract|I criteri di importazione di un processo non sono in grado di importare un'associazione per il contratto specificato.I requisiti di protezione dell'associazione non sono compatibili con un'associazione già importata per il contratto.Occorre riconfigurare l'associazione.|  
|CannotImportSupportingTokensForOperationWithoutRequestAction|Impossibile completare l'importazione dei criteri di sicurezza.I criteri di sicurezza contengono i requisiti del token di supporto nell'ambito dell'operazione.La descrizione del contratto non specifica l'azione del messaggio di richiesta associato a questa operazione.|  
|CannotIssueRstTokenType|Impossibile emettere il token del tipo specificato.|  
|CannotObtainIssuedTokenKeySize|Impossibile determinare le dimensioni della chiave del token emesso.|  
|CannotPerformImpersonationOnUsernameToken|Rappresentazione impossibile utilizzando il token client.L'associazione specificata per il contratto indicato utilizza Username Security Token per l'autenticazione client con un provider di appartenenza registrato.Utilizzare un tipo diverso di token di sicurezza per il client.|  
|CannotPerformS4UImpersonationOnPlatform|L'associazione specificata per il contratto indicato supporta la rappresentazione solo su [!INCLUDE[ws2003](../../../../../includes/ws2003-md.md)] e le versioni più recenti di Windows.Utilizzare l'autenticazione SspiNegotiated e un'associazione con conversazione protetta in cui è stato attivato l'annullamento.|  
|CannotReadKeyIdentifier|Impossibile leggere l'identificatore KeyIdentifier dall'elemento specificato con lo spazio dei nomi indicato.|  
|CannotReadToken|Impossibile leggere il token dall'elemento specificato avente lo spazio dei nomi indicato per BinarySecretSecurityToken e il tipo di valore specificato.Se l'elemento deve essere valido, verificare che la protezione sia configurata per utilizzare un token avente il nome, lo spazio dei nomi e il tipo di valore specificati.|  
|CertificateUnsupportedForHttpTransportCredentialOnly|Autenticazione client basata sui certificati non supportata nella modalità di sicurezza TransportCredentialOnly.Selezionare la modalità di sicurezza del trasporto.|  
|ClaimTypeCannotBeEmpty|ClaimType non può essere una stringa vuota.|  
|ClientCertificateNotProvided|Non è stato fornito il certificato per il client.Il certificato può essere impostato su ClientCredentials o su ServiceCredentials.|  
|ClientCredentialTypeMustBeSpecifiedForMixedMode|ClientCredentialType.None non valido per la modalità di sicurezza TransportWithMessageCredential.Specificare un tipo di credenziale o utilizzare un altro tipo di modalità di sicurezza.|  
|ConfigurationSchemaInsuffientForSecurityBindingElementInstance|Lo schema di configurazione non è in grado di descrivere la configurazione non standard dell'elemento di associazione di sicurezza seguente.|  
|DerivedKeyTokenGenerationAndLengthTooHigh|La generazione e la lunghezza specificate della chiave derivata risultano in un offset di derivazione della chiave superiore all'offset massimo consentito.|  
|DnsIdentityCheckFailedForIncomingMessage|Impossibile completare il controllo di identità per il messaggio in ingresso.L'identità DNS specificata prevista dell'endpoint remotonon corrisponde all'attestazione DNS fornita dall'endpoint remoto.Se si tratta di un endpoint remoto legittimo, per risolvere il problema è possibile specificare esplicitamente l'identità DNS come proprietà Identity dell'indirizzo EndpointAddress durante la creazione del proxy del canale.|  
|DnsIdentityCheckFailedForOutgoingMessage|Impossibile completare il controllo di identità per il messaggio in uscita.L'identità DNS specificata prevista dell'endpoint remotonon corrisponde all'attestazione DNS fornita dall'endpoint remoto.Se si tratta di un endpoint remoto legittimo, per risolvere il problema è possibile specificare esplicitamente l'identità DNS come proprietà Identity dell'indirizzo EndpointAddress durante la creazione del proxy del canale.|  
|DuplicateIdInMessageToBeVerified|L'ID specificato è stato rilevato due volte nel messaggio fornito per la verifica.|  
|EmptyBase64Attribute|È stato trovato un valore vuoto per l'attributo Base 64 richiesto avente il nome e lo spazio dei nomi specificati.|  
|ExportOfBindingWithAsymmetricAndTransportSecurityNotSupported|Impossibile completare l'esportazione dei criteri di sicurezza.L'associazione contiene sia un AsymmetricSecurityBindingElement sia un elemento di associazione di trasporto protetto.L'esportazione dei criteri per tale associazione non è supportata.|  
|ExportOfBindingWithSymmetricAndTransportSecurityNotSupported|Impossibile completare l'esportazione dei criteri di sicurezza.L'associazione contiene sia un SymmetricSecurityBindingElement sia un elemento di associazione di trasporto protetto.L'esportazione dei criteri per tale associazione non è supportata.|  
|ExportOfBindingWithTransportSecurityBindingElementAndNoTransportSecurityNotSupported|Impossibile completare l'esportazione dei criteri di sicurezza.L'associazione contiene un elemento TransportSecurityBindingElement ma nessun elemento di associazione di trasporto che implementi l'interfaccia ITransportTokenAssertionProvider.L'esportazione dei criteri per tale associazione non è supportata.Verificare che l'elemento di associazione di trasporto dell'associazione implementi l'interfaccia ITransportTokenAssertionProvider.|  
|FoundMultipleCerts|Trovati più certificati X.509 utilizzando i criteri di ricerca specificati: StoreName, StoreLocation, FindType, FindValue.Fornire un valore di ricerca più specifico.|  
|FoundMultipleCertsForTarget|Trovati più certificati X.509 tramite i criteri di ricerca specificati per la destinazione indicata: StoreName, StoreLocation, FindType e FindValue.Fornire un valore di ricerca più specifico.|  
|HeaderDecryptionNotSupportedInWsSecurityJan2004|SecurityVersion.WSSecurityJan2004 non supporta la decrittografia delle intestazioni.Per decrittografare l'intero messaggio utilizzare SecurityVersion.WsSecurityXXX2005 e versioni successive oppure la protezione a livello di trasporto.|  
|IdentityCheckFailedForIncomingMessage|Impossibile completare il controllo di identità per il messaggio in ingresso.Viene specificata l'identità prevista per l'endpoint di destinazione.|  
|IdentityCheckFailedForOutgoingMessage|Impossibile completare il controllo di identità per il messaggio in uscita.Viene specificata l'identità prevista per l'endpoint di destinazione.|  
|IncorrectSpnOrUpnSpecified|Autenticazione Security Support Provider Interface \(SSPI\) non riuscita.Il server potrebbe non essere in esecuzione con l'account avente l'identità specificata.Se il server è in esecuzione con un account di servizio \(ad esempio Servizio di rete\), specificare il nome ServicePrincipalName dell'account come identità dell'elemento EndpointAddress del server.Se il server è in esecuzione con un account utente, specificare il nome UserPrincipalName dell'account come identità dell'elemento EndpointAddress del server.|  
|InvalidAttributeInSignedHeader|L'intestazione firmata specificata contiene l'attributo indicato,che tuttavia non corrisponde all'attributo previsto.|  
|InvalidCloseResponseAction|L'azione specificata ricevuta in una risposta di chiusura della sessione di sicurezza non è valida.|  
|InvalidQName|QName non valido.|  
|InvalidRenewResponseAction|L'azione specificata ricevuta in una risposta di rinnovo della sessione di sicurezza non è valida.|  
|InvalidSspiNegotiation|Negoziazione Security Support Provider Interface \(SSPI\) non riuscita.|  
|IssuerBindingNotPresentInTokenRequirement|Il gestore del token di sicurezza richiede che il requisito del token che descrive la conversazione protetta specifichi l'elemento di associazione di sicurezza bootstrap.Viene riportato il requisito del token.|  
|KeyLengthMustBeMultipleOfEight|La lunghezza di chiave specificata non è un multiplo di 8 per le chiavi simmetriche.|  
|LsaAuthorityNotContacted|Errore SSL interno. Per ulteriori dettagli, fare riferimento al codice di stato Win32.Controllare il certificato server per determinare se supporta lo scambio chiave.|  
|MaximumPolicyRedirectionsExceeded|È stato raggiunto il limite di recupero dei criteri ricorsivi.Verificare l'eventuale presenza di un ciclo nella catena del servizio federativo.|  
|MessagePartSpecificationMustBeImmutable|La specifica della parte del messaggio deve essere resa costante prima di poterla impostare.|  
|MissingCustomCertificateValidator|X509CertificateValidationMode.Custom richiede un elemento CustomCertificateValidator.Specificare la proprietà CustomCertificateValidator.|  
|MissingCustomUserNamePasswordValidator|UserNamePasswordValidationMode.Custom richiede un elemento CustomUserNamePasswordValidator.Specificare la proprietà CustomUserNamePasswordValidator.|  
|MissingMembershipProvider|UserNamePasswordValidationMode.MembershipProvider richiede un elemento MembershipProvider.Specificare la proprietà MembershipProvider.|  
|NoBinaryNegoToSend|Nessuna negoziazione binaria inviata all'altra parte.|  
|NoEncryptionPartsSpecified|Per i messaggi contenenti l'azione indicata non è stata specificata alcuna parte del messaggio di crittografia.|  
|NoKeyInfoInEncryptedItemToFindDecryptingToken|Valore KeyInfo non trovato nell'elemento crittografato per trovare il token di decrittografia.|  
|NonceLengthTooShort|Parametro nonce specificato troppo breve.La lunghezza minima richiesta per il parametro nonce è 4 byte.|  
|NoOutgoingEndpointAddressAvailableForDoingIdentityCheck|Nessun EndpointAddress in uscita disponibile per controllare l'identità di un messaggio da inviare.|  
|NoOutgoingEndpointAddressAvailableForDoingIdentityCheckOnReply|Nessun EndpointAddress in uscita disponibile per controllare l'identità di una risposta ricevuta.|  
|NoPartsOfMessageMatchedPartsToSign|Nessuna firma creata in quanto nessuna parte del messaggio corrispondeva alla specifica della parte del messaggio fornita.|  
|NoPrincipalSpecifiedInAuthorizationContext|Nessuna entità personalizzata specificata nel contesto di autorizzazione.|  
|NoSignatureAvailableInSecurityHeaderToDoReplayDetection|Nessuna firma disponibile nell'intestazione di sicurezza per fornire il parametro nonce per il rilevamento riproduzione.|  
|NoSignaturePartsSpecified|Per i messaggi contenenti l'azione indicata non è stata specificata alcuna parte del messaggio di firma.|  
|NoSigningTokenAvailableToDoIncomingIdentityCheck|Nessun token di firma disponibile per effettuare un controllo di identità in ingresso.|  
|NoTimestampAvailableInSecurityHeaderToDoReplayDetection|Nessun timestamp disponibile nell'intestazione di sicurezza per il rilevamento di attacchi di tipo replay.|  
|NoTransportTokenAssertionProvided|Errore expert criteri di sicurezza.L'asserzione del token di trasporto specificata del tipo specificato non è stata in grado di creare un'asserzione del token di trasporto per includere l'asserzione dei criteri di sicurezza sp:TransportBinding.|  
|OnlyOneOfEncryptedKeyOrSymmetricBindingCanBeSelected|Per il protocollo di sicurezza simmetrica può essere configurato un provider di token simmetrici e un autenticatore di token simmetrici oppure un provider di token asimmetrici.Non è possibile configurare entrambi le entità.|  
|OperationCannotBeDoneOnReceiverSideSecurityHeaders|Impossibile eseguire questa operazione sulle intestazioni di sicurezza del destinatario.|  
|OperationDoesNotAllowImpersonation|L'operazione di servizio specificata che appartiene al contratto avente il nome e lo spazio dei nomi indicati non consente la rappresentazione.|  
|PolicyRequiresConfidentialityWithoutIntegrity|I criteri di sicurezza dei messaggi per l'azione specificata richiedono riservatezza senza integrità.Tuttavia, questa combinazione di funzionalità non è supportata.|  
|PrimarySignatureIsRequiredToBeEncrypted|La firma primaria deve essere crittografata.|  
|PropertySettingErrorOnProtocolFactory|La proprietà richiesta specificata della protocol factory di sicurezza indicata non è impostata o presenta un valore non valido.|  
|ProtocolFactoryCouldNotCreateProtocol|La protocol factory non è in grado di creare un protocollo.|  
|PublicKeyNotRSA|La chiave pubblica non è una chiave RSA.|  
|RequiredMessagePartNotEncrypted|La parte del messaggio richiesta specificata non è crittografata.|  
|RequiredMessagePartNotEncryptedNs|La parte del messaggio richiesta specificata non è crittografata.|  
|RequiredMessagePartNotSigned|La parte del messaggio richiesta specificata non è firmata.|  
|RequiredMessagePartNotSignedNs|La parte del messaggio richiesta specificata non è firmata.|  
|RequiredSecurityHeaderElementNotSigned|L'elemento intestazione di sicurezza specificato avente l'ID indicato deve essere firmato.|  
|RequiredSecurityTokenNotEncrypted|Il token di sicurezza specificato con la modalità di associazione indicata deve essere crittografato.|  
|RequiredSecurityTokenNotSigned|Il token di sicurezza specificato con la modalità di associazione indicata deve essere firmato.|  
|RequiredSignatureMissing|La firma deve essere contenuta nell'intestazione di sicurezza.|  
|RequireNonCookieMode|L'associazione specificata con lo spazio dei nomi indicato è configurata per emettere token del contesto di sicurezza dei cookie.I servizi Integrazione COM\+ non supportano token del contesto di sicurezza dei cookie.|  
|RevertingPrivilegeFailed|Operazione di ripristino non riuscita. Viene riportata l'eccezione.|  
|RSTRAuthenticatorIncorrect|L'elemento CombinedHash della risposta RequestSecurityTokenResponse non è corretto.|  
|SecureConversationCancelNotAllowedFaultReason|Annullamento della conversazione protetta non consentito dall'associazione.|  
|SecureConversationDriverVersionDoesNotSupportSession|La versione SecureConversation configurata non supporta le sessioni.Utilizzare WSSecureConversationFeb2005 o versione successiva.|  
|SecureConversationRequiredByReliableSession|Impossibile stabilire una sessione affidabile senza una conversazione protetta.Attivare la conversazione protetta.|  
|SecurityAuditFailToLoadDll|Impossibile caricare la libreria di collegamento dinamico \(DLL, Dynamic Link Library\) specificata.|  
|SecurityAuditNotSupportedOnChannelFactory|Il comportamento SecurityAuditBehavior non è supportato nella channel factory.|  
|SecurityAuditPlatformNotSupported|Scrittura dei messaggi di controllo nel registro protezione non supportata dalla piattaforma corrente.Scrivere i messaggi di controllo nel registro applicazioni.|  
|SecurityBindingElementCannotBeExpressedInConfig|Criteri di sicurezza importati per l'endpoint.I criteri di sicurezza contengono requisiti che non possono essere rappresentati in una configurazione di Windows Communication Foundation.Verificare la presenza di un commento sui parametri SecurityBindingElement richiesti nel file di configurazione generato.Creare l'elemento di associazione corretto con il codice.La configurazione dell'associazione nel file di configurazione non è protetta.|  
|SecurityBindingSupportsOneWayOnly|L'elemento SecurityBinding dell'associazione specificata per il contratto indicato supporta solo l'operazione OneWay.|  
|SecurityContextDoesNotAllowImpersonation|Impossibile avviare la rappresentazione perché il contesto SecurityContext del ruolo UltimateReceiver del messaggio di richiesta contenente l'azione specificata non è associato a un'identità Windows.|  
|SecurityListenerClosing|Il listener non accetta nuove conversazioni protette perché è in fase di chiusura.|  
|SecurityListenerClosingFaultReason|Il server non accetta nuove conversazioni protette perché al momento è in fase di chiusura.Ritentare in un secondo momento.|  
|SecurityProtocolFactoryShouldBeSetBeforeThisOperation|Impostare la protocol factory di sicurezza prima di eseguire questa operazione.|  
|SecuritySessionAbortedFaultReason|Sessione di sicurezza interrotta.È possibile che per un intervallo di tempo eccessivo non sia stato ricevuto alcun messaggio nella sessione.|  
|SecuritySessionKeyIsStale|La chiave di sessione deve essere rinnovata per poter proteggere i messaggi dell'applicazione.|  
|SecuritySessionLimitReached|Impossibile creare una sessione di sicurezza.Ritentare in un secondo momento.|  
|SecuritySessionNotPending|Nessuna sessione di sicurezza in sospeso avente l'ID specificato.|  
|SecurityTokenParametersHasIncompatibleInclusionMode|L'associazione indicata è configurata con un parametro di token di sicurezza per cui è stata specificata una modalità di inclusione dei token di sicurezza incompatibile.Specificare una modalità di inclusione dei token di sicurezza alternativa.|  
|SecurityVersionDoesNotSupportEncryptedKeyBinding|L'associazione specificata per il contratto specificato è stata configurata con una versione di sicurezza incompatibile che non supporta riferimenti non associati a EncryptedKeys.Utilizzare la versione indicata o una versione successiva come versione di sicurezza dell'associazione.|  
|SecurityVersionDoesNotSupportSignatureConfirmation|La versione SecurityVersion specificata non supporta la conferma della firma.Utilizzare una versione SecurityVersion successiva.|  
|SecurityVersionDoesNotSupportThumbprintX509KeyIdentifierClause|L'associazione specificata per il contratto specificato è configurata per una versione di sicurezza che non supporta riferimenti esterni ai token X.509 che utilizzano il valore dell'identificazione personale del certificato.Utilizzare la versione indicata o una versione successiva come versione di sicurezza dell'associazione.|  
|SenderSideSupportingTokensMustSpecifySecurityTokenParameters|È necessario specificare i parametri token di sicurezza con i token di supporto per ogni messaggio.|  
|ServerCertificateNotProvided|Il destinatario non ha fornito il relativo certificato. Il certificato è richiesto dal protocollo TLS.Entrambe le parti devono disporre dell'accesso ai relativi certificati.|  
|SignatureConfirmationNotSupported|La versione SecurityVersion configurata non supporta la conferma della firma.Utilizzare WSSecurityXXX2005 o versione successiva.|  
|SignatureConfirmationRequiresRequestReply|La protocol factory deve supportare la protezione request\/reply per poter offrire la conferma della firma.|  
|SignatureNotExpected|Per questo messaggio non è prevista alcuna firma.|  
|SigningTokenHasNoKeys|Il token di firma specificato non contiene chiavi.Il token di sicurezza è utilizzato in un contesto in base al quale deve eseguire operazioni di crittografia, ma il token non contiene chiavi di crittografia.Il tipo di token non supporta le operazioni di crittografia o l'istanza token specifica non contiene chiavi di crittografia.Controllare la configurazione per verificare che i tipi di token per cui la crittografia non è consentita \(ad esempio UserNameSecurityToken\) non siano specificati in un contesto che richiede operazioni di crittografia \(ad esempio un token di supporto di verifica dell'autenticità\).|  
|SpnegoImpersonationLevelCannotBeSetToNone|L'interfaccia SSPI non supporta il livello Rappresentazione "Nessuno".Specificare il livello Identificazione, Rappresentazione o Delega.|  
|SslClientCertMustHavePrivateKey|Il certificato specificato deve avere una chiave privata.Il processo deve disporre dei diritti di accesso per la chiave privata.|  
|SslServerCertMustDoKeyExchange|Il certificato specificato deve avere una chiave privata capace di scambio chiave.Il processo deve disporre dei diritti di accesso per la chiave privata.|  
|StandardsManagerCannotWriteObject|Il serializzatore di token non è in grado di serializzare l'oggetto specificato.Se si tratta di un tipo personalizzato è necessario utilizzare un serializzatore personalizzato.|  
|TimeStampHasCreationAheadOfExpiry|Il timestamp di sicurezza non è valido in quanto specifica una data di creazione maggiore o uguale alla data di scadenza.|  
|TimeStampHasCreationTimeInFuture|Il timestamp di sicurezza non è valido in quanto specifica una data di creazione futura.Vengono riportati l'ora corrente e lo sfasamento consentito dei segnali di clock.|  
|TimeStampHasExpiryTimeInPast|Il timestamp di sicurezza non è aggiornato poiché specifica una data di scadenza già passata.Vengono riportati l'ora corrente e lo sfasamento consentito dei segnali di clock.|  
|TimeStampWasCreatedTooLongAgo|Il timestamp di sicurezza non è aggiornato poiché specifica una data di creazione già passata da molto tempo.Vengono riportati l'ora corrente, la durata massima del timestamp e lo sfasamento consentito dei segnali di clock.|  
|TokenProviderCannotGetTokensForTarget|Il provider di token non è in grado di ottenere token per la destinazione specificata.|  
|TooManyIssuedSecurityTokenParameters|Una parte della catena di sicurezza federativa contiene più elementi IssuedSecurityTokenParameters.Il sistema InfoCard supporta solo un elemento IssuedSecurityTokenParameters per ogni parte.|  
|TransportDoesNotProtectMessage|L'associazione specificata per il contratto specificato è configurata con una modalità di autenticazione che richiede l'integrità e riservatezza a livello di trasporto.Il trasporto non è tuttavia in grado di fornire integrità e riservatezza.|  
|TrustApr2004DoesNotSupportCertainIssuedTokens|WSTrustApr2004 non supporta il rilascio di certificati X.509 o EncryptedKeys.Utilizzare WsTrustFeb2005 o versione successiva.|  
|TrustDriverVersionDoesNotSupportSession|La versione Trust configurata non supporta le sessioni.Utilizzare WSTrustFeb2005 o superiore.|  
|UnableToCreateICryptoFromTokenForSignatureVerification|Impossibile creare un'interfaccia ICrypto dal token specificato per la verifica della firma.|  
|UnableToCreateSymmetricAlgorithmFromToken|Impossibile creare l'algoritmo simmetrico specificato a partire dal token.|  
|UnableToDeriveKeyFromKeyInfoClause|La clausola KeyInfo specificata è stata risolta nel token indicato, che non contiene una chiave simmetrica utilizzabile per la derivazione.|  
|UnableToFindTokenAuthenticator|Impossibile trovare un autenticatore del token per il tipo di token specificato.I token di tale tipo non possono essere accettati in base alle impostazioni di sicurezza correnti.|  
|UnableToLoadCertificateIdentity|Impossibile caricare l'identità del certificato X.509 specificata nella configurazione.|  
|UnexpectedEmptyElementExpectingClaim|L'elemento specificato dello spazio dei nomi indicato è vuoto e non specifica alcuna richiesta di identità valida.|  
|UnknownEncodingInBinarySecurityToken|Codifica non riconosciuta durante la lettura del token di sicurezza binario.|  
|UnsecuredMessageFaultReceived|L'altra parte ha ricevuto un errore non protetto o protetto in modo non corretto.Per il codice di errore e ulteriori dettagli, vedere l'eccezione FaultException interna.|  
|UnsupportedPasswordType|Il token nome utente specificato presenta un tipo di password non supportato.|  
|UnsupportedSecureConversationBootstrapProtectionRequirements|Impossibile importare i criteri di sicurezza.I requisiti di sicurezza per l'associazione bootstrap della conversazione protetta non sono supportati.I requisiti di sicurezza del bootstrap della conversazione protetta devono richiedere la firma e la crittografia sia della richiesta sia della risposta.|  
|UnsupportedSecurityPolicyAssertion|Rilevata un'asserzione di criteri di sicurezza non supportata durante l'importazione dei criteri di sicurezza specificata.|