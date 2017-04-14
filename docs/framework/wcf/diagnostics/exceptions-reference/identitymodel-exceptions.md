---
title: "Eccezioni IdentityModel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ef34497-8ff5-4621-b773-7731cc721231
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Eccezioni IdentityModel
In questo argomento vengono elencate tutte le eccezioni generate da IdentityModel.  
  
## Elenco delle eccezioni  
  
|Codice risorsa|Stringa corrente|  
|--------------------|----------------------|  
|ValueMustBeOf2Types|Il valore di questo argomento deve essere uguale a uno di questi due tipi.|  
|SAMLSubjectNameIdentifierRequiresNameValue|Il nome specificato per SamlNameIdentifier non può essere Null o di lunghezza 0.|  
|TraceCodeIssuanceTokenProviderEndSecurityNegotiation|L'IssuanceTokenProvider ha completato la negoziazione di sicurezza.|  
|TraceCodeSecurityNewServerSessionKeyIssued|Il server ha rilasciato una nuova chiave di sessione di sicurezza.|  
|SAMLAttributeMissingNameAttributeOnRead|Il nome per SamlAttribute in lettura è mancante o di lunghezza 0.|  
|UnknownICryptoType|L'implementazione ICrypto non è supportata.|  
|TraceCodeSecurityTokenProviderClosed|Il provider di token di sicurezza è stato chiuso.|  
|SAMLUnableToLoadAdvice|Impossibile caricare l'elemento \<saml:advice\>.|  
|SAMLAuthenticationStatementMissingAuthenticationMethodOnRead|Attributo "AuthenticationMethod" in lettura per un SamlAuthenticationStatement mancante o con lunghezza 0.|  
|UnsupportedTransformAlgorithm|Algoritmo di trasformazione o di canonizzazione non supportato.|  
|SAMLAudienceRestrictionShouldHaveOneAudience|SamlAudienceRestrictionCondition deve contenere almeno un valore Audience \(URI\).|  
|SAMLEvidenceShouldHaveOneAssertion|SamlEvidence deve fare riferimento ad almeno un SamlAssertion per ID o per riferimento.|  
|SAMLAudienceRestrictionInvalidAudienceValueOnRead|SamlAudienceRestrictionCondition in lettura con un valore mancante nell'elemento "Audience".|  
|X509ChainBuildFail|La creazione specifica della catena di certificati X.509 non è riuscita.Impossibile verificare una catena di trust del certificato utilizzato.Sostituire il certificato o modificare certificateValidationMode.|  
|XDCannotFindValueInDictionaryString|ID del valore specifico non trovato nella stringa del dizionario.|  
|TraceCodeImportSecurityChannelBindingEntry|Avvio di ImportChannelBinding di sicurezza.|  
|PrivateKeyExchangeNotSupported|La chiave privata non supporta KeySpec di scambio.|  
|TokenProviderUnableToGetToken|Il provider di token specifico non è stato in grado di fornire un token di sicurezza.|  
|SAMLEntityCannotBeNullOrEmpty|L'entità di SamlAssertion specifica non può essere Null o vuota.|  
|SAMLAssertionRequireOneStatement|SamlAssertion richiede almeno un'istruzione.Verificare di aver aggiunto almeno un SamlStatement al SamlAssertion che si sta creando.|  
|AESInvalidInputBlockSize|La dimensione di input deve essere un multiplo di byte specifici.|  
|AESCryptAcquireContextFailed|Impossibile acquisire il contesto CSP.|  
|SAMLAssertionRequireOneStatementOnRead|SamlAssertion in lettura non contiene alcun SamlStatement.SamlAssertion deve contenere almeno un SamlStatement.|  
|TraceCodeSecuritySessionClosedFaultReceived|La sessione di sicurezza client ha ricevuto un errore di sessione chiusa dal server.|  
|TraceCodeIssuanceTokenProviderRedirectApplied|L'IssuanceTokenProvider ha applicato un'intestazione di reindirizzamento.|  
|TraceCodeSecuritySessionClosedFaultSendFailure|Errore durante l'invio al client di un errore di sessione di sicurezza chiusa.|  
|ValueMustBeZero|Il valore di questo argomento deve essere 0.|  
|SAMLUnableToResolveSignatureKey|Impossibile risolvere il SecurityKeyIdentifier trovato nella firma di SamlAssertion.La firma di SamlAssertion non può essere convalidata per l'autorità emittente specifica.|  
|X509IsNotInTrustedStore|Il certificato X.509 specifico non è presente nell'archivio Persone attendibili.|  
|SAMLElementNotRecognized|L'elemento specifico non è supportato.|  
|SAMLAuthorizationDecisionStatementMissingResourceAttributeOnRead|Attributo "Resource" per SamlAuthorizationDecisionStatement in lettura mancante o con lunghezza 0.|  
|SamlTokenMissingSignature|SamlAssertion non è firmato.È possibile firmare SamlAssertions impostando SigningCredentials.|  
|ExpectedElementMissing|L'elemento previsto con lo spazio dei nomi specifico è mancante.|  
|NoKeyIdentifierClauseFound|In SecurityKeyIdentifier non è stata trovata nessuna clausola del tipo specifico.|  
|MissingPrivateKey|La chiave privata non è presente nel certificato X.509.|  
|UnexpectedEOFFromReader|Fine del file imprevista dal lettore XML.|  
|UnsupportedKeyDerivationAlgorithm|Algoritmo di derivazione della chiave specifico non supportato.|  
|TokenDoesNotSupportKeyIdentifierClauseCreation|Il token specifico non supporta la creazione della clausola dell'identificatore di chiave specifica.|  
|LastMessageNumberExceeded|Rilevata violazione del protocollo del numero di sequenza.|  
|SymmetricKeyLengthTooShort|La chiave simmetrica specificata è troppo corta.|  
|SAMLAuthorityBindingMissingAuthorityKindOnRead|SamlAuthorityBinding in lettura contenente un "AuthorityKind" mancante o di lunghezza 0.Questa operazione non è consentita.|  
|XmlTokenBufferIsEmpty|XmlTokenBuffer è vuoto.|  
|InvalidXmlQualifiedName|Era previsto un nome qualificato XML ma è stato trovato un nome non valido.|  
|SAMLAuthorityKindMissingName|XmlQualifiedName che rappresenta "AuthorityKind" in SamlAuthorityBinding non può essere Null o di lunghezza 0.|  
|AESCryptEncryptFailed|Impossibile crittografare i dati specifici.|  
|AuthorizationContextCreated|Creato contesto di autorizzazione con l'ID specifico.|  
|SamlSerializerUnableToReadSecurityKeyIdentifier|SamlSerializer non contiene un SecurityTokenSerializer in grado di leggere il SecurityKeyIdentifier.Se si utilizza un SecurityKeyIdentifier personalizzato, è necessario fornire un SecurityTokenSerializer personalizzato.|  
|TraceCodeIssuanceTokenProviderServiceTokenCacheFull|L'IssuanceTokenProvider ha ridotto la cache del token di servizio.|  
|TraceCodeSecurityTokenProviderOpened|Il provider del token di sicurezza è stato aperto.|  
|PublicKeyNotRSA|La chiave pubblica non è una chiave RSA.|  
|InvalidReaderState|Lo stato specifico non è valido per il lettore di input fornito.|  
|UnableToResolveReferenceUriForSignature|Impossibile risolvere l'URI specifico nella firma per calcolare il digest.|  
|EmptyBase64Attribute|È stato trovato un valore vuoto per il nome e lo spazio dei nomi dell'attributo Base64 richiesto.|  
|SAMLSubjectRequiresConfirmationMethodWhenConfirmationDataOrKeyInfoIsSpecified|SAML SubjectConfirmation deve disporre di un metodo Confirmation quando si specificano dati di conferma o KeyInfo.|  
|SAMLAudienceRestrictionShouldHaveOneAudienceOnRead|SamlAudienceRestrictionCondition in lettura deve contenere almeno un valore "Audience".Nessun valore trovato.|  
|TokenProviderUnableToRenewToken|Il provider di token specifico non è stato in grado di rinnovare il token di sicurezza.|  
|AESIVLengthNotSupported|Valore iniziale a bit specifico non supportato.Sono supportati solo valori iniziali a 128 bit.|  
|SAMLAuthorityBindingMissingAuthorityKind|SamlAuthorityBinding deve contenere un "AuthorityKind" non Null.|  
|TraceCodeSecuritySessionDemuxFailure|Il messaggio in arrivo non fa parte di una sessione di sicurezza esistente.|  
|TokenRenewalNotSupported|Il provider di token specifico non supporta il rinnovo del token.|  
|AtLeastOneReferenceRequired|Una firma deve contenere almeno un riferimento.|  
|SAMLSignatureAlreadyRead|La firma è già letta nell'asserzione SAML.|  
|AlgorithmAndPrivateKeyMisMatch|Mancata corrispondenza tra l'algoritmo specificato e la chiave privata.|  
|EmptyTransformChainNotSupported|Catena di trasformazioni vuota non supportata.|  
|SspiWrapperEncryptDecryptAssert1|SSPIWrapper::EncryptDecryptHelper&#124;'offset' fuori intervallo.|  
|SspiWrapperEncryptDecryptAssert2|SSPIWrapper::EncryptDecryptHelper&#124;'size' fuori intervallo.SecurityTokenManagerCannotCreateAuthenticatorForRequirement\=Il gestore del token di sicurezza non è in grado di creare un autenticatore del token per il requisito specifico.|  
|UnableToCreateKeyedHashAlgorithm|Impossibile creare un KeyedHashAlgorithm dal valore specifico per l'algoritmo di firma specifico.|  
|SAMLUnableToLoadAssertion|Impossibile caricare l'elemento \<saml:assertion\>.|  
|X509FindValueMismatchMulti|L'argomento findValue di X509FindType specifico deve essere uno dei 2 tipi di valori.L'argomento findValue è di un altro tipo.|  
|TraceCodeSecurityIdentityDeterminationSuccess|Identità determinata per un EndpointAddress.|  
|UndefinedUseOfPrefixAtElement|Nessuno spazio dei nomi definito per il prefisso specifico utilizzato nell'elemento.|  
|TraceCodeSecuritySessionResponderOperationFailure|Operazione sessione di sicurezza non riuscita nel server.|  
|CannotFindCert|Impossibile trovare il certificato X.509 utilizzando i criteri di ricerca specifici: StoreName, StoreLocation, FindType, FindValue.|  
|X509InvalidUsageTime|L'ora di utilizzo del certificato X.509 specifica non è valida.L'ora di utilizzo non è compresa tra NotBefore e NotAfter.|  
|TraceCodeSecurityIdentityDeterminationFailure|Impossibile determinare l'identità per un EndpointAddress.|  
|AsyncObjectAlreadyEnded|Il metodo End è già stato chiamato su questo oggetto risultato asincrono.|  
|ExternalDictionaryDoesNotContainAllRequiredStrings|Il dizionario esterno non contiene definizioni per tutte le stringhe richieste.La stringa specifica non è disponibile nel dizionario remoto.|  
|TraceCodeSecuritySessionKeyRenewalFaultReceived|La sessione di sicurezza client ha ricevuto un errore di rinnovo chiave dal server.|  
|SAMLActionNameRequired|La stringa che rappresenta SamlAction non può essere Null o di lunghezza 0.|  
|SignatureVerificationFailed|Impossibile verificare la firma.|  
|TraceCodeSecurityContextTokenCacheFull|La cache SecurityContextSecurityToken è piena.|  
|SAMLAssertionMissingMajorVersionAttributeOnRead|MajorVersion per SamlAssertion in lettura mancante o con lunghezza 0.|  
|SamlAttributeClaimRightShouldBePossessProperty|Per questo costruttore SamlAttribute il valore di Right dell'attestazione deve essere System.IdentityModel.Claims.Rights.PossessProperty.|  
|AuthorizationPolicyEvaluated|Valutato criterio con l'ID specifico.|  
|SAMLUnableToLoadCondtions|Impossibile caricare l'elemento \<saml:conditions\>.|  
|AESKeyLengthNotSupported|La chiave a bit specifica non è supportata.Sono supportate solo chiavi a 128, 192 e 256 bit.|  
|UserNameCannotBeEmpty|Il nome utente non può essere vuoto.|  
|AlgorithmAndPublicKeyMisMatch|Mancata corrispondenza tra l'algoritmo specificato e la chiave pubblica.|  
|SAMLUnableToLoadCondtion|Impossibile caricare l'elemento \<saml:conditions\>.|  
|SamlAssertionMissingSigningCredentials|SigningCredentials non impostato su SamlAssertion.Per SamlAssertions è necessaria una firma. Per procedere, impostare un valore SigningCredentials valido su SamlAssertion.|  
|SspiPayloadNotEncrypted|Dati binari non crittografati con il contesto di sicurezza SSPI.|  
|SAMLAuthorizationDecisionShouldHaveOneActionOnRead|SamlAuthorizationDecisionStatement in lettura non contenente alcun SamlAction.|  
|TraceCodeSecurityBindingSecureOutgoingMessageFailure|Il protocollo di sicurezza non è in grado di proteggere il messaggio in uscita.|  
|UndefinedUseOfPrefixAtAttribute|Nessuno spazio dei nomi definito per il prefisso specifico utilizzato nell'attributo specifico.|  
|NoInputIsSetForCanonicalization|Nessun input impostato per la scrittura di output in forma canonica.|  
|TraceCodeSecurityPendingServerSessionAdded|Al server viene aggiunta una sessione di sicurezza in sospeso.|  
|AsyncCallbackException|Un AsyncCallback ha generato un'eccezione.|  
|PrivateKeyNotRSA|La chiave privata non è una chiave RSA.|  
|TraceCodeSecurityClientSessionKeyRenewed|La sessione di sicurezza client ha rinnovato la chiave di sessione.|  
|SAMLAuthorizationDecisionStatementMissingDecisionAttributeOnRead|"Decision" per SamlAuthorizationDecisionStatement in lettura mancante o con lunghezza 0.|  
|SAMLAttributeNameAttributeRequired|Il nome specificato per SamlAttribute non può essere Null o di lunghezza 0.|  
|SamlSerializerRequiresExternalSerializers|SamlSerializer richiede un SecurityTokenSerializer per serializzare il SecurityKeyIdentifier presente nel token.|  
|UnableToResolveKeyReference|Il resolver del token non è in grado di risolvere il riferimento alla chiave di sicurezza specifica.|  
|UnsupportedKeyWrapAlgorithm|Algoritmo di incapsulamento della chiave specifico non supportato.|  
|SAMLAssertionMissingIssuerAttributeOnRead|"Issuer" per SamlAssertion in lettura mancante o con lunghezza 0.|  
|TraceCodeIssuanceTokenProviderUsingCachedToken|L'IssuanceTokenProvider ha utilizzato il token di servizio memorizzato nella cache.|  
|AESCryptGetKeyParamFailed|Impossibile ottenere il parametro della chiave specifico.|  
|InvalidNamespaceForEmptyPrefix|Spazio dei nomi non valido per il prefisso vuoto.|  
|AESCipherModeNotSupported|Modalità di crittografia specifica non supportata.Supportata solo CBC.|  
|ArgumentCannotBeEmptyString|L'argomento deve essere una stringa non vuota.|  
|SAMLAssertionMissingMinorVersionAttributeOnRead|MinorVersion per SamlAssertion in lettura mancante o con lunghezza 0.|  
|SpecifiedStringNotAvailableInDictionary|La stringa specificata non è una voce del dizionario corrente.|  
|KerberosApReqInvalidOrOutOfMemory|AP\-REQ non valido o memoria insufficiente.|  
|FailLogonUser|LogonUser non riuscito per l'utente specificato.Verificare che l'utente disponga di un account di Windows valido.|  
|ValueMustBeNonNegative|Il valore di questo argomento non deve essere negativo.|  
|X509ValidationFail|Convalida certificato X.509 specificata non riuscita.|  
|TraceCodeSecuritySessionRequestorOperationSuccess|Operazione sessione di sicurezza completata nel client.|  
|SAMLActionNameRequiredOnRead|Stringa letta per SamlAction mancante o con lunghezza 0.|  
|KerberosMultilegsNotSupported|L'identità è specificata come UPN.L'autenticazione di un servizio in esecuzione con un account utente che richiede l'autenticazione multifase Kerberos non è supportata.|  
|SAMLAssertionIdRequired|"assertionId" per SamlAssertion non può essere Null o vuoto.|  
|InvalidOperationForWriterState|Operazione specificata non valida nello stato XmlWriter specificato.|  
|CannotValidateSecurityTokenType|L'autenticatore del token di sicurezza specificato non può convalidare un token del tipo specificato.|  
|X509FindValueMismatch|Il tipo dell'argomento findValue di X509FindType specificato deve avere il valore specificato.L'argomento findValue è di un altro tipo.|  
|TraceCodeSecurityClientSessionCloseSent|Un messaggio di chiusura è stato inviato dalla sessione di sicurezza client.|  
|SuiteDoesNotAcceptAlgorithm|L'algoritmo specificato non è accettato per l'operazione specificata dalla suite di algoritmi specificata|  
|TraceCodeSecuritySessionRequestorOperationFailure|Operazione sessione di sicurezza client non riuscita.|  
|SAMLUnableToLoadStatement|Impossibile caricare un SamlStatement.|  
|InnerReaderMustBeAtElement|Il lettore interno deve essere sull'elemento.|  
|UnableToCreateTokenReference|Impossibile creare un riferimento a un token di sicurezza.|  
|TraceCodeSecurityBindingIncomingMessageVerified|Il protocollo di sicurezza ha verificato il messaggio in ingresso.|  
|ObjectIsReadOnly|L'oggetto è in sola lettura.|  
|TraceCodeSecurityClientSessionPreviousKeyDiscarded|La sessione di sicurezza client ha eliminato la chiave della sessione precedente.|  
|SAMLTokenTimeInvalid|SamlToken non compreso nel periodo di validità.L'ora corrente non è compresa tra l'ora di inizio validità e l'ora di scadenza del token.|  
|TraceCodeSecurityIdentityVerificationSuccess|Verifica identità completata.|  
|SigningTokenHasNoKeys|Il token di firma specificato non contiene chiavi.|  
|TraceCodeSecurityIdentityVerificationFailure|Verifica identità non riuscita.|  
|AESCryptImportKeyFailed|Impossibile importare il materiale della chiave.|  
|FailInitializeSecurityContext|InitializeSecurityContent non riuscito.Verificare che il nome dell'entità servizio sia corretto.|  
|TraceCodeStreamSecurityUpgradeAccepted|L'aggiornamento della protezione di flusso è stato accettato.|  
|SAMLAuthorityBindingRequiresLocation|L'attributo "Location" specificato in SamlAuthorityBinding non può essere Null o di lunghezza 0.|  
|PublicKeyNotDSA|La chiave pubblica non è una chiave DSA.|  
|ImpersonationLevelNotSupported|Le modalità di autenticazione che utilizzano Kerberos non supportano il livello di rappresentazione specificato.Specificare un'identificazione o un livello di rappresentazione validi.|  
|RequiredTargetNotSigned|L'elemento con l'ID specificato deve essere firmato.|  
|SAMLAuthenticationStatementMissingAuthenticationInstanceOnRead|Attributo "AuthenticationInstant" in lettura per SamlAuthenticationStatement mancante o con lunghezza 0.|  
|SAMLEvidenceShouldHaveOneAssertionOnRead|SamlEvidence in lettura non incorpora e non fa riferimento a un SamlAssertion.|  
|LengthOfArrayToConvertMustGreaterThanZero|La lunghezza della matrice per la conversione in un intero deve essere maggiore di 0.|  
|InvalidAsyncResult|AsyncResult non valido.|  
|TraceCodeIssuanceTokenProviderRemovedCachedToken|L'IssuanceTokenProvider ha rimosso il token di servizio scaduto.|  
|IncorrectUserNameFormat|Formato del nome utente non valido.Il formato del nome utente deve essere del tipo "nomeutente" o "dominio\\\\nomeutente".|  
|TraceCodeExportSecurityChannelBindingEntry|Avvio ExportChannelBinding di sicurezza.|  
|UnsupportedInputTypeForTransform|Tipo di input specificato non supportato per la trasformazione.|  
|CannotFindDocumentRoot|Impossibile trovare la radice del documento.|  
|XmlBufferQuotaExceeded|Le dimensioni necessarie per memorizzare nel buffer il contenuto XML hanno superato la quota di buffer.|  
|TraceCodeSecuritySessionClosedResponseSendFailure|Errore durante l'invio al client di una risposta di chiusura della sessione di sicurezza.|  
|UnableToResolveReferenceInSamlSignature|Impossibile risolvere il riferimento specificato nella firma SAML con AssertionID.|  
|SAMLSubjectRequiresNameIdentifierOrConfirmationMethod|SamlSubject richiede che venga specificato "NameIdentifier" o "ConfirmationMethod".Entrambi sono mancanti.|  
|SAMLAttributeMissingNamespaceAttributeOnRead|Spazio dei nomi mancante o con lunghezza 0 per SamlAttribute in lettura.|  
|SAMLSubjectConfirmationClauseMissingConfirmationMethodOnRead|Impossibile trovare "ConfirmationMethod" in SamlSubjectConfirmation in lettura.|  
|SecurityTokenRequirementHasInvalidTypeForProperty|Il requisito di token ha un tipo non previsto per la proprietà specificata.Il tipo di proprietà previsto ha un altro valore.|  
|TraceCodeNegotiationTokenProviderAttached|È stato allegato NegotiationTokenProvider.|  
|TraceCodeSpnegoClientNegotiationCompleted|SpnegoTokenProvider ha completato la negoziazione SSPI.|  
|SAMLUnableToLoadUnknownElement|Il SamlSerializer selezionato non è in grado di deserializzare l'elemento.Registrare un SamlSerializer personalizzato per deserializzare gli elementi personalizzati.|  
|CreateSequenceRefused|La richiesta di creazione sequenza è stata rifiutata dalla destinazione RM.|  
|TraceCodeSecuritySessionRedirectApplied|La sessione di sicurezza client è stata reindirizzata.|  
|SecurityTokenRequirementDoesNotContainProperty|Il requisito del token non contiene la proprietà specificata.|  
|SAMLAttributeValueCannotBeNull|Uno dei valori di attributo di SamlAttribute è Null.Quando si crea SamlAttribute, verificare che gli elenchi non siano Null.|  
|ValueMustBeGreaterThanZero|Il valore dell'argomento deve essere maggiore di zero.|  
|TraceCodeNegotiationAuthenticatorAttached|È stato allegato NegotiationTokenAuthenticator.|  
|ValueMustBePositive||  
|SAMLAuthorizationDecisionShouldHaveOneAction|SamlAuthorizationDecisionStatement deve avere almeno un SamlAction.|  
|TraceCodeSecurityTokenAuthenticatorClosed|L'autenticatore del token di sicurezza è stato chiuso.|  
|TraceCodeSecurityAuditWrittenSuccess|Il registro di controllo di sicurezza è scritto correttamente.|  
|PrivateKeyNotDSA|La chiave privata non è una chiave DSA.|  
|MessageNumberRollover|È stato superato il numero massimo di sequenza per questa sequenza.|  
|AESPaddingModeNotSupported|La modalità di padding specificata non è supportata.Sono supportate solo PKCS7 e ISO10126.|  
|SAMLSubjectRequiresNameIdentifierOrConfirmationMethodOnRead|Elementi necessari "NameIdentifier" e "ConfirmationMethod" non trovati per SamlSubject in lettura.|  
|TraceCodeSecurityAuditWrittenFailure|Errore durante la scrittura nel registro di controllo di sicurezza.|  
|UnsupportedCryptoAlgorithm|L'algoritmo di crittografia specificato non è supportato in questo contesto.|  
|SigningTokenHasNoKeysSupportingTheAlgorithmSuite|Il token di firma non ha chiavi che supportino la suite di algoritmi specificata.|  
|SAMLNameIdentifierMissingIdentifierValueOnRead|Stringa "Identifier" mancante per SamlNameIdentifier in lettura.|  
|SAMLSubjectStatementRequiresSubject|SAMLSubjectStatement richiede che venga specificato un SAMLSubject.|  
|TraceCodeSslClientCertMissing|Il client remoto SSL non è riuscito a fornire un certificato richiesto.|  
|SAMLTokenVersionNotSupported|La versione principale e la versione secondaria specificate non sono supportate.|  
|TraceCodeConfigurationIsReadOnly|La configurazione è in sola lettura.|  
|TraceCodeSecuritySessionRenewFaultSendFailure|Errore durante l'invio al client di un errore di rinnovo della chiave della sessione di sicurezza.|  
|TraceCodeSecurityInactiveSessionFaulted|Una sessione di sicurezza non attiva non è stata accettata dal server.|  
|SAMLUnableToLoadAttribute|Impossibile caricare un SamlAttribute.|  
|Psha1KeyLengthInvalid|La lunghezza della chiave PSHA1 specificata non è valida.|  
|KeyIdentifierCannotCreateKey|SecurityKeyIdentifier è privo di clausole che consentano la creazione di una chiave.|  
|X509IsInUntrustedStore|Il certificato X.509 specificato proviene da un archivio certificati non disponibile nell'elenco locale.|  
|UnexpectedXmlChildNode|Il nodo figlio XML specificato del tipo specificato non è previsto per l'elemento specificato.|  
|TokenDoesNotMeetKeySizeRequirements|I requisiti di dimensione della chiave per la suite di algoritmi specificata non sono soddisfatti dal token specificato.|  
|TraceCodeSecuritySessionRequestorStartOperation|L'operazione sessione di sicurezza è stata avviata nel client.|  
|InvalidHexString|Formato stringa esadecimale non valido.|  
|SamlAttributeClaimResourceShouldBeAString|Per questo costruttore SamlAttribute la risorsa dell'attestazione deve essere di tipo "string".|  
|SamlSigningTokenNotFound|Impossibile trovare il token con cui SamlAssertion è stato firmato.Verificare che il SecurityTokenResolver contenga il token con cui è stato firmato SamlAssertion.|  
|TraceCodeSecuritySpnToSidMappingFailure|Impossibile mappare ServicePrincipalName a un SecurityIdentifier.|  
|UnableToCreateSignatureFormatterFromAsymmetricCrypto|Impossibile creare un formattatore della firma per l'algoritmo specificato dalla crittografia asimmetrica specificata.|  
|TraceCodeSecurityServerSessionClosedFaultSent|Errore di sessione chiusa inviato al client dalla sessione di sicurezza del server.|  
|UnableToFindPrefix|Impossibile trovare il prefisso per il prefisso specificato utilizzato nell'elemento specificato.|  
|TraceCodeSecurityTokenAuthenticatorOpened|L'autenticatore del token di sicurezza è stato aperto.|  
|RequiredAttributeMissing|Nell'elemento specificato è richiesto l''attributo specificato.|  
|LocalIdCannotBeEmpty|LocalId non può essere vuoto.Specificare un "localId" valido.|  
|ValueMustBeInRange|Il valore dell'argomento deve essere compreso nell'intervallo specificato.|  
|TraceCodeIssuanceTokenProviderBeginSecurityNegotiation|L'IssuanceTokenProvider ha avviato una nuova negoziazione di sicurezza.|  
|InvalidNtMapping|Impossibile mappare il certificato X.509 specificato a un account di Windows.Necessario nome alternativo UPN.|  
|AESCryptSetKeyParamFailed|Impossibile impostare il parametro della chiave specificato.|  
|TraceCodeSecuritySessionClosedResponseReceived|La sessione di sicurezza client ha ricevuto una risposta di chiusura dal server.|  
|UnableToCreateSignatureDeformatterFromAsymmetricCrypto|Impossibile creare un deformattatore della firma per l'algoritmo specificato dalla crittografia asimmetrica specificata.|  
|TraceCodeIdentityModelAsyncCallbackThrewException|Eccezione generata da un cn callback asincrono.|  
|LengthMustBeGreaterThanZero|La lunghezza di questo argomento deve essere maggiore di 0.|  
|FoundMultipleCerts|Trovati più certificati X.509 utilizzando i criteri di ricerca specificati: StoreName, StoreLocation, FindType, FindValue.Fornire un valore di ricerca più specifico.|  
|AtLeastOneTransformRequired|L'elemento Transforms deve contenere almeno una trasformazione.|  
|SAMLTokenNotSerialized|Impossibile serializzare SamlAssertion in XML.Per ulteriori dettagli, vedere l'eccezione interna.|  
|TraceCodeSecurityBindingOutgoingMessageSecured|Il protocollo di sicurezza ha protetto il messaggio in uscita.|  
|KeyIdentifierClauseDoesNotSupportKeyCreation|Specificato SecurityKeyIdentifierClause che non supporta la creazione di chiavi.|  
|UnableToResolveTokenReference|Il resolver del token non è in grado di risolvere il riferimento al token specificato.|  
|UnsupportedEncryptionAlgorithm|L'algoritmo di crittografia specificato non è supportato.|  
|SamlSerializerUnableToWriteSecurityKeyIdentifier|SamlSerializer non contiene un SecurityTokenSerializer in grado di serializzare il SecurityKeyIdentifier specificato.Se si utilizza un SecurityKeyIdentifier personalizzato, è necessario fornire un SecurityTokenSerializer personalizzato.|  
|SAMLAttributeShouldHaveOneValue|Nessun valore di attributo trovato.Un attributo SamlAttribute deve avere almeno un valore di attributo.|  
|TraceCodeSecurityBindingVerifyIncomingMessageFailure|Il protocollo di sicurezza non è in grado di verificare il messaggio in ingresso.|  
|SamlSigningTokenMissing|SamlAssertion passato a SamlSecurityTokenAuthenticator non contiene un token di firma.|  
|NoPrivateKeyAvailable|Nessuna chiave privata disponibile.|  
|ValueMustBeOne|Il valore di questo argomento deve essere 1.|  
|TraceCodeSecurityPendingServerSessionRemoved|Una sessione di sicurezza in sospeso è stata attivata dal server.|  
|TraceCodeImportSecurityChannelBindingExit|ImportChannelBinding di sicurezza terminato.|  
|X509CertStoreLocationNotValid|StoreLocation deve essere LocalMachine o CurrentUser.|  
|SettingdMayBeModifiedOnlyWhenTheWriterIsInStartState|Le impostazioni dello scrittore possono essere modificate solo quando lo scrittore è in stato di avvio.|  
|ArgumentInvalidCertificate|Il certificato non è valido.|  
|DigestVerificationFailedForReference|Verifica digest non riuscita per il riferimento specificato.|  
|SAMLAuthorityBindingRequiresBinding|L'attributo "Binding" specificato in SamlAuthorityBinding non può essere Null o di lunghezza 0.|  
|AESInsufficientOutputBuffer|Il buffer di output deve essere maggiore dei byte specificati.|  
|SAMLAuthorityBindingMissingBindingOnRead|Attributo "Binding" per SamlAuthorityBinding in lettura mancante o di lunghezza 0.|  
|SAMLAuthorityBindingInvalidAuthorityKind|SamlAuthorityBinding in lettura ha un AuthorityKind non valido.Il formato di AuthorityKind deve essere un nome qualificato.|  
|ProvidedNetworkCredentialsForKerberosHasInvalidUserName|Le credenziali di rete specificate per il token Kerberos non dispongono di un nome utente valido.|  
|SSPIPackageNotSupported|Il pacchetto SSPI specificato non è supportato.|  
|TokenCancellationNotSupported|Il provider di token specificato non supporta la cancellazione dei token.|  
|UnboundPrefixInQName|Prefisso non associato utilizzato nel nome qualificato specificato.|  
|SAMLAuthorizationDecisionResourceRequired|La risorsa specificata in SamlAuthorizationDecisionStatement non può essere Null o di lunghezza 0.|  
|TraceCodeSecurityNegotiationProcessingFailure|Errore durante l'elaborazione della negoziazione di sicurezza del servizio.|  
|SAMLAssertionIssuerRequired|"Issuer" specificato per SamlAssertion non può essere Null o vuoto.|  
|UnableToCreateHashAlgorithmFromAsymmetricCrypto|Impossibile creare un HashAlgorithm per l'algoritmo specificato dalla crittografia asimmetrica specificata.|  
|SamlUnableToExtractSubjectKey|Impossibile risolvere il SecurityKeyIdentifier trovato nel SamlSubject in un SecurityToken.Il SecurityTokenResolver deve contenere un SecurityToken nel quale viene effettuata la risoluzione del SecurityKeyIdentifier.|  
|ChildNodeTypeMissing|L'elemento XML specificato non ha un figlio del tipo specificato.|  
|TraceCodeSecurityPendingServerSessionClosed|La sessione di sicurezza in sospeso è stata chiusa dal server.|  
|TraceCodeSecuritySessionCloseResponseSent|La sessione di sicurezza server ha inviato una risposta di chiusura al client.|  
|TraceCodeSecurityIdentityHostNameNormalizationFailure|Impossibile normalizzare la porzione HostName di un indirizzo endpoint.|  
|FailAcceptSecurityContext|AcceptSecurityContext non riuscito|  
|EmptyXmlElementError|L'elemento specificato non può essere vuoto.|  
|PrefixNotDefinedForNamespace|In questo contesto non è definito alcun prefisso per lo spazio dei nomi specificato e non può essere dichiarato.|  
|SAMLAuthorizationDecisionHasMoreThanOneEvidence|SamlAuthorizationDecisionStatement in lettura contiene più di un Evidence.Questa operazione non è consentita.|  
|SamlTokenAuthenticatorCanOnlyProcessSamlTokens|SamlSecurityTokenAuthenticator può elaborare solo SamlSecurityTokens.È stato ricevuto il SecurityTokenType specificato.|  
|SAMLAttributeStatementMissingAttributeOnRead|SamlAttributeStatement in lettura non contiene elementi "SamlAttribute".Questa operazione non è consentita.|  
|CouldNotFindNamespaceForPrefix|Impossibile cercare il prefisso specificato nello spazio dei nomi.|  
|TraceCodeExportSecurityChannelBindingExit|ExportChannelBinding di sicurezza terminato.|  
|AESCryptDecryptFailed|Impossibile decrittografare i dati specificati.|  
|SAMLAttributeNamespaceAttributeRequired|Lo spazio dei nomi specificato per SamlAttribute non può essere Null o di lunghezza 0.|  
|TraceCodeSpnegoServiceNegotiationCompleted|SpnegoTokenAuthenticator ha completato la negoziazione SSPI.|  
|TraceCodeSecurityServerSessionRenewalFaultSent|Errore di rinnovo chiave inviato al client dalla sessione di sicurezza del server.|  
|AlgorithmMismatchForTransform|Mancata corrispondenza nell'algoritmo per la trasformazione.|  
|UserNameAuthenticationFailed|L'autenticazione di nome utente\/password tramite il meccanismo specificato non è riuscita.L'utente non è autenticato.|  
|SamlInvalidSigningToken|SamlAssertion è stato firmato con un token non convalidato in conformità con il protocollo.Se si utilizzano certificati X.509, esaminare le semantiche di convalida.|  
|TraceCodeSecurityServerSessionKeyUpdated|Il server ha aggiornato la chiave di sessione di sicurezza.|  
|TraceCodeSecurityServerSessionCloseReceived|La sessione di sicurezza server ha ricevuto un messaggio di chiusura dal client.|  
|SAMLAuthenticationStatementMissingSubject|SamlAuthenticationStatement non dispone del SamlSubjectStatement necessario.|  
|UnexpectedEndOfFile|Fine del file imprevista.|  
|UnsupportedAlgorithmForCryptoOperation|L'algoritmo specificato non è supportato per l'operazione specificata.|  
|XmlLangAttributeMissing|Attributo xml:lang necessario mancante|  
|TraceCodeSecurityImpersonationSuccess|Rappresentazione protezione completata sul server.|  
|SAMLAuthorityBindingMissingLocationOnRead|Attributo "Location" per SamlAuthorityBinding in lettura mancante o di lunghezza 0.|  
|SAMLAttributeStatementMissingSubjectOnRead|Elemento "SamlSubject" mancante per SamlAttributeStatement.|  
|SAMLAuthorizationDecisionStatementMissingSubjectOnRead|Elemento "SamlSubject" mancante per SamlAuthorizationDecisionStatement in lettura.|  
|SAMLBadSchema|Durante la lettura di SamlAssertion è stato riscontrato che l'elemento specificato non è conforme allo schema.|  
|SAMLAssertionIDIsInvalid|"assertionId" specificato per SamlAssertion deve iniziare con una lettera o con '\_'.|  
|TraceCodeSecurityActiveServerSessionRemoved|Una sessione di sicurezza attiva è stata rimossa dal server.|  
|UnableToCreateKeyedHashAlgorithmFromSymmetricCrypto|Impossibile creare un keyedHashAlgorithm per l'algoritmo specificato dalla crittografia simmetrica specificata.|  
|SAMLAuthenticationStatementMissingAuthenticationMethod|L'attributo "AuthenticationMethod" specificato per un SamlAuthenticationStatement non può essere Null o di lunghezza 0.|  
|TraceCodeSecurityImpersonationFailure|Rappresentazione protezione non riuscita nel server.|  
|Predefinito|\(Predefinito\)|  
|UnsupportedNodeTypeInReader|Il tipo di nodo specificato con il nome specificato non è supportato.|