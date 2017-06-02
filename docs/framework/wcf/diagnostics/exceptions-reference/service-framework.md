---
title: "Framework dei servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 75f60b87-f80e-4377-ba7c-8e6becaa2b28
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Framework dei servizi
In questo argomento vengono elencate tutte le eccezioni generate dai dati del framework dei servizi.  
  
## Elenco delle eccezioni  
  
|Codice risorsa|Stringa di risorsa|  
|--------------------|------------------------|  
|ABindingInstanceHasAlreadyBeenAssociatedTo1|Un'istanza dell'associazione è già stata associata per essere in attesa dell'URI specificato.Affinché due endpoint possano condividere lo stesso ListenUri, devono anche condividere la stessa istanza dell'oggetto di associazione.I due endpoint in conflitto sono stati specificati in chiamate AddServiceEndpoint\(\), in un file di configurazione o in una combinazione di AddServiceEndpoint\(\) e file di configurazione.|  
|AChannelServiceEndpointIsNull0|Un endpoint del servizio\/canale è nullo.|  
|AChannelServiceEndpointSContractSNameIsNull0|Il nome di un contratto di un endpoint del servizio\/canale è nullo o vuoto.|  
|AChannelServiceEndpointSContractSNamespace0|Lo spazio dei nomi di un contratto di un endpoint del servizio\/canale è nullo.|  
|BaseAddressCannotHaveFragment|Un indirizzo di base non può contenere un frammento URI.|  
|BaseAddressCannotHaveQuery|Un indirizzo di base non può contenere una stringa di query URI.|  
|BaseAddressCannotHaveUserInfo|Un indirizzo di base non può contenere una sezione di informazioni utente URI.|  
|BaseAddressDuplicateScheme|La raccolta contiene già un indirizzo con lo schema specificato.La raccolta può contenere al massimo un indirizzo per schema.|  
|BaseAddressMustBeAbsolute|È possibile utilizzare solo un URI assoluto come indirizzo di base.|  
|BindingDoesnTSupportAnyChannelTypes1|L'associazione specificata non supporta la creazione di alcun tipo di canale.Lo stack o l'ordine degli elementi di associazione in un'associazione personalizzata non è corretto.È richiesto un trasporto in fondo allo stack.L'ordine consigliato per gli elementi di associazione è: TransactionFlow, ReliableSession, Security, CompositeDuplex, OneWay, StreamSecurity, MessageEncoding, Transport.|  
|BindingDoesnTSupportDuplexButContractRequires1|Il contratto richiede la modalità duplex.L'associazione specificata non supporta tale modalità o non è configurata correttamente per supportarla.|  
|BindingDoesnTSupportOneWayButContractRequires1|Il contratto richiede la modalità unidirezionale.L'associazione specificata non supporta tale modalità o non è configurata correttamente per supportarla.|  
|BindingDoesnTSupportRequestReplyButContract1|Il contratto richiede la modalità request\/reply.L'associazione specificata non supporta tale modalità o non è configurata correttamente per supportarla.|  
|BindingDoesnTSupportSessionButContractRequires1|Il contratto richiede la modalità di sessione.L'associazione specificata non supporta tale modalità o non è configurata correttamente per supportarla.|  
|BindingDoesnTSupportTwoWayButContractRequires1|Il contratto richiede la modalità bidirezionale \(request\/reply o duplex\).L'associazione specificata non supporta tale modalità o non è configurata correttamente per supportarla.|  
|BindingRequirementsAttributeDisallowsQueuedDelivery1|DeliveryRequirementsAttribute non consente QueuedDelivery,ma l'associazione per l'endpoint con il contratto specificato lo supporta.|  
|BindingRequirementsAttributeRequiresQueuedDelivery1|DeliveryRequirementsAttribute richiede QueuedDelivery,ma l'associazione per l'endpoint con il contratto specificato non lo supporta o non è configurato correttamente per supportarlo.|  
|channelDoesNotHaveADuplexSession0|Il canale corrente non supporta la chiusura della sessione di outputpoiché il canale non implementa ISessionChannel\<IDuplexSession\>.|  
|ClientRuntimeRequiresFormatter0|L'elemento ClientOperation specificato richiede un formattatore, poiché SerializeRequest e DeserializeReply non sono entrambi False.|  
|CommunicationObjectAborted1|Impossibile utilizzare l'oggetto di comunicazione specificato per la comunicazione perché è stato interrotto.|  
|CommunicationObjectAbortedStack2|Impossibile utilizzare l'oggetto di comunicazione specificato per la comunicazione perché è stato interrotto: {1}|  
|CommunicationObjectBaseClassMethodNotCalled|L'oggetto di comunicazione specificato ha sostituito la funzione virtuale {1} ma non effettua una chiamata alla versione definita nella classe di base.|  
|ContractIsNotSelfConsistentItHasOneOrMore2|Il contratto specificato dispone di una o più operazioni IsTerminating o diverse da IsInitiating,ma la proprietà SessionMode non è impostata su SessionMode.Required.Gli attributi IsInitiating e IsTerminating possono essere utilizzati solo nel contesto di una sessione.|  
|CouldnTCreateChannelForChannelType2|È stato richiesto il tipo di canale specificato, ma l'associazione specificata non lo supporta o non è configurato correttamente per supportarlo.|  
|DispatchRuntimeRequiresFormatter0|L'elemento DispatchOperation specificato richiede un formattatore, poiché DeserializeRequest e SerializeReply non sono entrambi False.|  
|EndMethodsCannotBeDecoratedWithOperationContractAttribute|Quando si utilizza il modello di struttura IAsyncResult, il metodo End non può essere decorato con OperationContractAttribute.Solo il metodo Begin corrispondente può essere decorato con OperationContractAttribute.Tale attributo viene applicato alla coppia di metodi Begin\-End.|  
|EndpointListenerRequirementsCannotBeMetBy3|I requisiti ChannelDispatcher non possono essere soddisfatti da IChannelListener per l'associazione specificata perché il contratto richiede il supporto per uno dei tipi di canale specificati.Tuttavia, l'associazione supporta solo altri tipi di canale specificati.|  
|EndpointsMustHaveAValidBinding0|Gli endpoint devono presentare un'associazione valida.|  
|InvalidOrUnrecognizedAction|Impossibile elaborare il messaggio perché l'azione specificata non è valida o non è stata riconosciuta.|  
|MultipleMebesInParameters|Nei parametri BindingParameter di BindingContext è stato trovato più di un elemento MessageEncodingBindingElement.Le associazioni CustomBinding possono presentare al massimo un elemento MessageEncodingBindingElement.Rimuovere tutti gli elementi di questo tipo tranne uno.|  
|MultipleStreamUpgradeProvidersInParameters|Nei parametri BindingParameter di BindingContext è stato trovato più di un elemento IStreamUpgradeProviderElement.Le associazioni CustomBinding possono presentare al massimo un elemento IStreamUpgradeProviderElements.Rimuovere tutti gli elementi di questo tipo tranne uno.|  
|NoChannelBuilderAvailable|L'associazione non può essere utilizzata per creare una channel factory o un listener del canale perché non presenta alcun elemento TransportBindingElement.Ogni associazione deve contenere almeno un elemento di associazione che deriva da TransportBindingElement.|  
|NotAllBindingElementsBuilt|Alcuni elementi di questa associazione non sono stati utilizzati durante la compilazione della channel factory e del listener del canale.L'ordine degli elementi di associazione non è corretto.L'ordine consigliato per gli elementi di associazione è: TransactionFlow, ReliableSession, Security, CompositeDuplex, OneWay, StreamSecurity, MessageEncoding, Transport.Si noti che TransportBindingElement deve essere l'ultimo elemento.Gli elementi di associazione specificati non sono stati compilati.|  
|RuntimeRequiresInvoker0|DispatchOperation richiede Invoker.|  
|ServiceHasZeroAppEndpoints|Il servizio specificato ha zero endpoint di applicazione \(senza infrastruttura\).È possibile che non sia stato trovato alcun file di configurazione per l'applicazione, che non sia stato trovato alcun elemento del servizio corrispondente al nome del servizio nel file di configurazione oppure che non siano stati definiti endpoint nell'elemento del servizio.|  
|SFxActionMismatch|Azione non corrispondente. Impossibile creare un messaggio tipizzato.L'azione prevista specificata non corrisponde all'azione riscontrata.|  
|SFxAnonymousTypeNotSupported|La parte specificata del messaggio indicato non può essere esportata con RPC o codificata perché il relativo tipo è anonimo.|  
|SFxBadMetadataLocationNoAppropriateBaseAddress|L'URL fornito in ServiceMetadataBehavior tramite la proprietà ExternalMetadataLocation o l'attributo externalMetadataLocation nella sezione serviceMetadata del file di configurazione è un URL relativo e non esiste un indirizzo di base con cui risolverlo.|  
|SFxBadMetadataMustBePolicy|Occorre fornire un elemento dei criteri XmlElement avente lo spazio dei nomi e il nome specificati.L'elemento XmlElement fornito presenta lo spazio dei nomi e il nome specificati, ma non è un elemento dei criteri.|  
|SFxBodyObjectTypeCannotBeInherited|Il tipo specificato non può ereditare da nessuna classe diversa dall'oggetto da utilizzare come oggetto body nello stile RPC.|  
|SFxBodyObjectTypeCannotBeInterface|Il tipo specificato implementa l'interfaccia specificata, che tuttavia non è supportata per l'oggetto body nello stile RPC.|  
|SFxCallbackBehaviorAttributeOnlyOnDuplex|È possibile eseguire CallbackBehaviorAttribute solo come comportamento in un endpoint avente un contratto duplex.Il contratto specificato non è duplex e non contiene alcuna operazione di callback.|  
|SFxCallbackRequestReplyInOrder1|Impossibile ricevere la risposta da questa operazione fino al completamento dell'elaborazione del messaggio corrente.Se si desidera consentire l'elaborazione non ordinata dei messaggi, impostare ConcurrencyMode su Reentrant o su Multiple nell'elemento specificato.|  
|SfxCallbackTypeCannotBeNull|Per poter utilizzare il contratto specificato con DuplexChannelFactory, il contratto deve specificare un contratto di callback valido.Se il contratto non dispone di un contratto di callback, utilizzare ChannelFactory anziché DuplexChannelFactory.|  
|SFxCannotGetMetadataFromLocation|MetadataExchangeClient può ricevere metadati solo da MetadataLocation HTTP e HTTPS.Non può ricevere metadati dall'entità specificata.|  
|SFxCannotHttpGetMetadataFromAddress|MetadataExchangeClient può ricevere metadati da indirizzi HTTP o HTTPS solo quando utilizza MetadataExchangeClientMode HttpGet.Non può ricevere metadati dall'entità specificata.|  
|SFxCannotImportAsParameters\_Bare|Il sistema genera un contratto di messaggio perché l'operazione specificata non è RPC né incapsulata da documenti.|  
|SFxCannotImportAsParameters\_DifferentWrapperName|Il sistema genera un contratto di messaggio perché il nome wrapper specificato del messaggio indicato non corrisponde al valore predefinito.|  
|SFxCannotImportAsParameters\_DifferentWrapperNs|Il sistema genera un contratto di messaggio perché lo spazio dei nomi wrapper specificato del messaggio indicato non corrisponde al valore predefinito.|  
|SFxCannotImportAsParameters\_ElementIsNotNillable|Il sistema genera un contratto di messaggio perché il nome di elemento specificato appartenente allo spazio dei nomi indicato non è contrassegnato come nillable.|  
|SFxCannotImportAsParameters\_HeadersAreUnsupported|Il sistema genera un contratto di messaggio perché il messaggio specificato contiene intestazioni.|  
|SFxCannotImportAsParameters\_Message|Il sistema genera un contratto di messaggio perché l'operazione specificata contiene un argomento o un tipo restituito Message non tipizzato.|  
|SFxCannotImportAsParameters\_MessageHasProtectionLevel|Il sistema genera un contratto di messaggio perché il messaggio specificato richiede protezione.|  
|SFxCannotImportAsParameters\_NamespaceMismatch|Il sistema genera un contratto di messaggio perché lo spazio dei nomi specificato della parte del messaggio non corrisponde al valore predefinito.|  
|SFxCannotRequireBothSessionAndDatagram3|Uno dei contratti indicati specifica SessionMode.NotAllowed mentre l'altro contratto indicato specifica SessionMode.Required.Modificare uno dei valori SessionMode o specificare un indirizzo o un ListenURI diverso per ogni endpoint.|  
|SFxCannotSetExtensionsByIndex|L'impostazione delle estensioni per indice non è supportata in questa raccolta.Utilizzare il metodo InsertItem o RemoveItem.|  
|SFxChannelDispatcherDifferentHost0|ChannelDispatcher non associato al ServiceHost specificato.|  
|SFxChannelDispatcherMultipleHost0|Impossibile aggiungere un ChannelDispatcher a più di un ServiceHost.|  
|SFxChannelDispatcherNoHost0|Impossibile aprire ChannelDispatcher perché non è associato a un ServiceHost.|  
|SfxChannelFactoryDisposed|Impossibile aprire l'elemento ChannelFactory in quanto è stato eliminato.Creare nuovamente tale elemento prima di utilizzarlo.|  
|SFxChannelFactoryNoBinding|Impossibile aprire l'elemento ChannelFactory perché all'endpoint di tale elemento non è stata assegnata alcuna associazione.Specificare un'associazione utilizzando il costruttore o la proprietà dell'endpoint.|  
|SFxChannelTerminated0|È già stata richiamata nel canale un'operazione contrassegnata come IsTerminating, causando l'interruzione della connessione del canale.Impossibile richiamare altre operazioni nel canale.Ricreare il canale per continuare la comunicazione.|  
|SFxCloseTimedOut1|Si è verificato il timeout dell'operazione di chiusura ServiceHost dopo il periodo di tempo specificato.È possibile che un client non sia stato in grado di chiudere un canale con sessione entro l'intervallo di tempo previsto.È inoltre possibile che la durata consentita per l'operazione fosse una porzione di un timeout più lungo.|  
|SfxCloseTimedOutWaitingForDispatchToComplete|Durante l'attesa del completamento dell'invio del servizio si è verificato il timeout del processo di chiusura.|  
|SFxCodeGenIsNotAssignableFrom|Il valore specificato non può essere assegnato.|  
|SFxConfigChannelConfigurationNotFound|Impossibile trovare l'elemento di endpoint avente il nome e il contratto specificati nella sezione di configurazione client ServiceModel.|  
|SFxConflictingGlobalElement|L'elemento XML di primo livello avente il nome specificato dello spazio dei nomi indicato non può far riferimento al tipo specificatoin quanto fa già riferimento a un altro tipo.Utilizzare un nome di operazione diverso o MessageBodyAttribute per specificare un nome diverso per il messaggio o le parti di messaggio.|  
|SFxContractHasZeroInitiatingOperations|Un contratto deve contenere almeno un'operazione IsInitiating\=true.|  
|SFxContractHasZeroOperations|Un contratto deve contenere almeno un'operazione.|  
|SFxContractInheritanceRequiresInterfaces|La classe del servizio del tipo specificato definisce ed eredita allo stesso tempo un ServiceContract dal tipo indicato.L'eredità del contratto può essere soltanto utilizzata tra i tipi di interfaccia.Se una classe è contrassegnata con ServiceContractAttribute, deve essere l'unico tipo all'interno della gerarchia avente l'attributo ServiceContractAttribute.È consigliabile spostare l'attributo ServiceContractAttribute del tipo specificato in un'altra interfaccia implementata dal tipo specificato.|  
|SFxCreateDuplexChannel1|Il contratto di callback del contratto specificato non esiste o non definisce operazioni.Se non si tratta di un contratto duplex, è consigliabile utilizzare ChannelFactory invece di DuplexChannelFactory.|  
|SFxCreateDuplexChannelNoCallback|Impossibile chiamare l'overload CreateChannel in quest'istanza di DuplexChannelFactory,perché l'elemento DuplexChannelFactory non è stato inizializzato con un contesto InstanceContext.Chiamare l'overload CreateChannel che accetta un contesto InstanceContext.|  
|SFxCreateDuplexChannelNoCallback1|Impossibile chiamare l'overload CreateChannel in quest'istanza di DuplexChannelFactory,perché l'elemento DuplexChannelFactory è stato inizializzato con un tipo e non è stato fornito alcun contesto InstanceContext valido.Chiamare l'overload CreateChannel che accetta un contesto InstanceContext.|  
|SFxCreateDuplexChannelNoCallbackUserObject|Impossibile chiamare l'overload CreateChannel in quest'istanza di DuplexChannelFactory,perché il contesto InstanceContext fornito per l'elemento DuplexChannelFactory non contiene un UserObject valido.|  
|SFxCreateNonDuplexChannel1|ChannelFactory non supporta il contratto specificatoperché definisce un contratto di callback avente una o più operazioni.Utilizzare DuplexChannelFactory invece di ChannelFactory|  
|SFxCustomBindingNeedsTransport1|L'associazione CustomBinding dell'elemento ServiceEndpoint avente il contratto specificato non contiene alcun elemento TransportBindingElement.Ogni associazione deve contenere almeno un elemento di associazione che deriva da TransportBindingElement.|  
|SFxCustomBindingWithoutTransport|Impossibile calcolare lo schema per questa associazione personalizzata in quanto tale associazione non contiene alcun elemento TransportBindingElement.Ogni associazione deve contenere almeno un elemento di associazione che deriva da TransportBindingElement.|  
|SFxDataContractSerializerDoesNotSupportBareArray|L'elemento DataContractSerializer non supporta la raccolta specificata nell'elemento indicato.|  
|SFxDictionaryIsEmpty|Impossibile eseguire l'operazione perché il dizionario è vuoto.|  
|SFxDocEncodedNotSupported|Errore di reflection per l'elemento specificato.La codifica di documento non è supportata.Impostare "Use" su "Literal" oppure "Style" su "RPC".|  
|SFxDuplicateInitiatingActionAtSameVia|Il servizio ha più endpoint in attesa presso l'entità specificatache condividono la stessa azione di avvio indicata.Di conseguenza, poiché il dispatcher non sarà in grado di determinare l'endpoint corretto per la gestione del messaggio, i messaggi con questa azione verranno eliminati.|  
|SFXEndpointBehaviorUsedOnWrongSide|Impossibile utilizzare nel server il comportamento IEndpointBehavior specificato.Questo comportamento può essere applicato solo ai client.|  
|SFxEndpointNoMatchingScheme|Impossibile trovare l'indirizzo di base corrispondente allo schema specificato per l'endpoint avente l'associazione indicata.Gli schemi degli indirizzi di base registrati sono stati specificati.|  
|SFxErrorCreatingMtomReader|Si è verificato un errore durante la creazione di un lettore per il meccanismo di ottimizzazione della trasmissione dei messaggi.|  
|SFxErrorDeserializingFault|Il server ha restituito un errore SOAP non valido.Per ulteriori dettagli, vedere InnerException.|  
|SFxErrorDeserializingHeader|Si è verificato un errore durante la deserializzazione di una delle intestazioni del messaggio specificato.Per ulteriori dettagli, vedere InnerException.|  
|SFxErrorReflectingOnMethod3|Si è verificato un errore durante il caricamento dell'attributo specificato del metodo indicato appartenente al tipo specificato.Per ulteriori dettagli, vedere InnerException.|  
|SFxErrorReflectingOnParameter4|Si è verificato un errore durante il caricamento dell'attributo specificato del parametro indicato del metodo specificato appartenente al tipo indicato.Per ulteriori dettagli, vedere InnerException.|  
|SFxErrorReflectingOnType2|Si è verificato un errore durante il caricamento dell'attributo specificato appartenente al tipo indicato.Per ulteriori dettagli, vedere InnerException.|  
|SFxErrorSerializingBody|Si è verificato un errore durante la serializzazione del corpo del messaggio specificato.Per ulteriori dettagli, vedere InnerException.|  
|SFxErrorSerializingHeader|Si è verificato un errore durante la serializzazione di una delle intestazioni del messaggio specificato.Per ulteriori dettagli, vedere InnerException.|  
|SFxExpectedIMethodCallMessage|Errore interno.Il messaggio deve essere un elemento IMethodCallMessage valido.|  
|SFxExportMustHaveType|La parte specificata nell'operazione indicata non può essere esportata perché non contiene un tipo CLR valido.|  
|SFxHeaderNotUnderstood|Il messaggio non è stato elaborato.L'intestazione specificata appartenente allo spazio dei nomi indicato non è stata riconosciuta dal destinatario del messaggio.L'errore indica in genere che il mittente del messaggio ha attivato un protocollo di comunicazione che non può essere elaborato dal destinatario.Verificare che la configurazione dell'associazione del client sia coerente con quella del servizio.|  
|SFxHeadersAreNotSupportedInEncoded|Il messaggio specificato non deve avere intestazioni da utilizzare nello stile codificato RPC.|  
|SFxInconsistentWsdlOperationStyleInMessageParts|Tutte le parti del messaggio nell'operazione specificata devono contenere un tipo o un elemento.|  
|SFxInconsistentWsdlOperationStyleInOperationMessages|Lo stile specificato dedotto dai messaggi nell'operazione indicata non corrisponde allo stile previsto specificato tramite le associazioni.|  
|SFxInvalidCallbackIAsyncResult|IAsyncResult non è fornito oppure è del tipo errato.|  
|SFxInvalidMessageBody|OperationFormatter ha rilevato un corpo di messaggio non valido.Il nodo previsto di tipo "Element" nonché il nome e lo spazio dei nomi specificati per tale nodonon corrispondono a quelli rilevati.|  
|SFxInvalidMessageBodyEmptyMessage|OperationFormatter non può deserializzare alcuna informazione dal messaggio perché quest'ultimo è vuoto.|  
|SFxInvalidMessageBodyErrorDeserializingParameter|Si è verificato un errore durante la deserializzazione del parametro specificato.Per ulteriori informazioni, vedere InnerException.|  
|SFxInvalidMessageBodyErrorSerializingParameter|Si è verificato un errore durante la serializzazione del parametro specificato.Il messaggio InnerException è stato specificato.Per ulteriori dettagli, vedere InnerException.|  
|SFxInvalidMessageBodyUnexpectedNode|Durante la deserializzazione dei parametri è stato trovato il nodo imprevisto specificato appartenente allo spazio dei nomi specificato.|  
|SFxInvalidMessageContractSignature|L'operazione specificata ha un parametro o un tipo restituito con attributo MessageContractAttribute.Per rappresentare il messaggio di richiesta tramite un contratto messaggio, l'operazione deve avere un parametro singolo con attributo MessageContractAttribute.Per rappresentare il messaggio di risposta tramite un contratto messaggio, il valore restituito dall'operazione deve essere di un tipo con attributo MessageContractAttributee l'operazione non deve avere nessun parametro "out" o "ref".|  
|SFxInvalidReplyAction|Il messaggio di risposta in uscita per l'operazione contiene il valore di Action specificato, ma il contratto per tale operazione specifica un valore diverso di ReplyAction.Il valore di Action specificato nel messaggio deve corrispondere al valore di ReplyAction nel contratto, oppure il contratto dell'operazione deve specificare ReplyAction\='\*'.|  
|SFxInvalidRequestAction|Il messaggio di richiesta in uscita per l'operazione contiene il valore di Action specificato, ma il contratto per tale operazione specifica un valore diverso di RequestAction.Il valore di Action specificato nel messaggio deve corrispondere al valore di RequestAction nel contratto, oppure il contratto dell'operazione deve specificare RequestAction\='\*'.|  
|SFxInvalidStaticOverloadCalledForDuplexChannelFactory1|Impossibile utilizzare il metodo CreateChannel statico con il contratto specificato perché quest'ultimo definisce un contratto di callback.Utilizzare uno degli overload CreateChannel statici in DuplexChannelFactory\<TChannel\>.|  
|SFxInvalidStreamInRequest|Affinché la richiesta nell'operazione specificata possa essere un flusso, l'operazione deve avere un unico parametro di tipo Stream.|  
|SFxInvalidStreamInResponse|Affinché la risposta nell'operazione specificata possa essere un flusso, l'operazione deve avere un unico parametro out o valore restituito di tipo Stream.|  
|SFxInvalidStreamInTypedMessage|Per poter utilizzare i flussi con il modello di programmazione di contratto messaggio, il tipo specificato deve avere un unico membro MessageBody il cui tipo sia Stream.|  
|SFxInvalidUseOfPrimitiveOperationFormatter|Il parametro o il tipo restituito assegnato a PrimitiveOperationFormatter non è supportato da quest'ultimo.|  
|SFxMessageContractBaseTypeNotValid|Il tipo specificato definisce un MessageContract ma deriva da un tipo indicato che non definisce alcun MessageContract.Tutti gli oggetti nella gerarchia di eredità specificata devono definire un MessageContract.|  
|SFxMethodNotSupported1|Il metodo specificato non è supportato in questo oggetto.È possibile che il metodo non sia contrassegnato con OperationContractAttribute o che il tipo di interfaccia non sia contrassegnato con ServiceContractAttribute.|  
|SFxMethodNotSupportedByType2|Il tipo specificato di implementazione di ServiceHost non implementa il contratto di servizio indicato.|  
|SFxMethodNotSupportedOnCallback1|Il metodo callback specificato non è supportato.È possibile che il metodo non sia contrassegnato con OperationContractAttribute o che il relativo tipo di interfaccia non sia la destinazione del CallbackContract di ServiceContractAttribute.|  
|SFxMismatchedOperationParent|È possibile aggiungere DispatchOperation \(o ClientOperation\) solo al relativo DispatchRuntime \(o ClientRuntime\) padre.|  
|SFxNameCannotBeEmpty|La proprietà Name non può contenere una stringa vuota.|  
|SfxNoTypeSpecifiedForParameter|Impossibile generare l'operazione in quanto per il parametro non è stato specificato alcun tipo CLR.|  
|SFxOperationBehaviorAttributeOnlyOnServiceClass|OperationBehaviorAttribute può essere assegnato solo alla classe del servizio,non all'interfaccia ServiceContract.Il metodo specificato nel tipo indicato viola tale regola.|  
|SFxOperationContractOnNonServiceContract|Il metodo specificato è contrassegnato con OperationContractAttribute, ma il tipo di inclusione indicato non è contrassegnato con ServiceContractAttribute.OperationContractAttribute può essere utilizzato solo nei metodi nei tipi ServiceContractAttribute nei rispettivi tipi CallbackContract.|  
|SFxParameterCountMismatch|Il numero di argomenti forniti non corrisponde al numero di argomenti previsti.In particolare, il numero indicato di elementi dell'argomento specificato non corrisponde al numero di elementi indicato dell'argomento previsto.|  
|SFxPartNameMustBeUniqueInRpc|Il nome specificato della parte messaggio non è univoco in un messaggio RPC.|  
|SFxReplyActionMismatch3|È stato ricevuto un messaggio di risposta per l'operazione specificata con l'azione indicata.Tuttavia, il codice client richiede l'azione specificata.|  
|SFxRequestReplyNone|È stato ricevuto un messaggio con un'intestazione WS\-Addressing ReplyTo o FaultTo associata all'indirizzo "None".Tali valori non sono validi per le operazioni request\/reply.Utilizzare un'operazione unidirezionale o abilitare ManualAddressing se si desidera supportare i valori ReplyTo o FaultTo per "None".|  
|SFxRequestTimedOut1|L'operazione di richiesta non ha ricevuto una risposta entro il timeout configurato specificato.È possibile che la durata consentita per l'operazione fosse una porzione di un timeout più lungo.È possibile che il servizio stia ancora elaborando l'operazione o che il servizio non sia stato in grado di inviare un messaggio di risposta.|  
|SFxRequestTimedOut2|L'operazione di richiesta inviata alla destinazione specificata non ha ricevuto una risposta entro il timeout configurato indicato.È possibile che la durata consentita per l'operazione fosse una porzione di un timeout più lungo.È possibile che il servizio stia ancora elaborando l'operazione o che il servizio non sia stato in grado di inviare un messaggio di risposta.|  
|SFxSchemaDoesNotContainType|Lo schema avente lo spazio dei nomi di destinazione specificato non contiene un tipo avente il nome indicato.|  
|SfxServiceContractAttributeNotFound|Al tipo di contratto specificato non è stato assegnato un attributo ServiceContractAttribute.Per definire un contratto valido, il tipo specificato deve avere l'attributo ServiceContractAttribute.Il tipo può essere un'interfaccia di contratto o una classe di servizio.|  
|SFxServiceContractGeneratorConfigRequired|Per generare le informazioni di configurazione utilizzando il metodo GenerateServiceEndpoint, l'istanza ServiceContractGenerator deve essere stata inizializzata con un oggetto Configuration valido.|  
|SFxServiceHostBaseCannotAddEndpointAfterOpen|Gli endpoint non possono essere aggiunti quando ServiceHost si trova in uno degli stati seguenti:<br /><br /> -   Aperto<br />-   Non riuscito<br />-   Interrotto<br />-   Chiuso|  
|SFxServiceHostBaseCannotAddEndpointWithoutDescription|Impossibile aggiungere gli endpoint prima dell'inizializzazione della proprietà Description.|  
|SFxServiceMetadataBehaviorNoHttpBaseAddress|La proprietà HttpGetEnabled di ServiceMetadataBehavior è impostata su True e la proprietà HttpGetUrl è un indirizzo relativo, ma non è disponibile alcun indirizzo HTTP di base.Specificare un indirizzo HTTP di base o impostare HttpGetUrl su un indirizzo assoluto.|  
|SFxServiceMetadataBehaviorNoHttpsBaseAddress|La proprietà HttpsGetEnabled di ServiceMetadataBehavior è impostata su True e la proprietà HttpsGetUrl è un indirizzo relativo, ma non è disponibile alcun indirizzo HTTPS di base.Specificare un indirizzo HTTPS di base o impostare HttpsGetUrl su un indirizzo assoluto.|  
|SFxServiceMetadataBehaviorUrlMustBeHttpOrRelative|L'URL di comportamento deve essere un URI relativo o un URI assoluto avente lo schema specificato.L'URL specificato è un URI assoluto avente lo schema specificato.|  
|SFxStreamRequestMessageClosed|Il messaggio contenente il flusso è stato chiuso.Non è possibile accedere ai flussi di richiesta dopo la restituzione dell'operazione del servizio.|  
|SFxStreamResponseMessageClosed|Il messaggio contenente il flusso è stato chiuso.|  
|SFxTerminateRequestProcessingException|Un'estensione della pipeline dell'operazione deve interrompere l'elaborazione di questo messaggio.|  
|SFxTerminatingOperationAlreadyCalled1|Il canale non è in grado di inviare altri messaggi in quanto è stata chiamata l'operazione IsTerminating.|  
|SFxThrottleLimitMustBeGreaterThanZero0|Il limite di velocità deve essere maggiore di zero.Per disattivare tale limite, impostare il valore su Int32.MaxValue.|  
|SFxTypedOrUntypedMessageCannotBeMixedWithVoidInRpc|Quando si utilizza lo stile codificato rpc, non è possibile utilizzare i tipi di contratto messaggio o il tipo System.ServiceModel.Channels.Message se l'operazione non ha parametri o il valore restituito è vuoto.Aggiungere un tipo di contratto messaggio vuoto come parametro o tipo restituito all'operazione.|  
|SFxUserCodeThrewException|L'operazione utente specificata ha generato un'eccezione non gestita nel codice utente.Se si tratta di un problema ricorrente, potrebbe indicare un errore nell'implementazione del metodo specificato.|  
|SfxUseTypedMessageForCustomAttributes|Impossibile eseguire il mapping del parametro specificato al parametro dell'operazione poiché quest'ultimo richiede attributi aggiuntivi.|  
|SFxVersionMismatchInOperationContextAndMessage2|Impossibile aggiungere intestazioni in uscita al messaggio in quanto l'elemento MessageVersion del contesto OperationContext.Current non corrisponde alla versione dell'intestazione del messaggio in fase di elaborazione.|  
|SFxWellKnownNonSingleton0|Per poter utilizzare uno dei costruttori ServiceHost che accettano un'istanza del servizio, l'elemento InstanceContextMode del servizio deve essere impostato su InstanceContextMode.Single.È possibile configurarlo tramite ServiceBehaviorAttribute.In alternativa, è consigliabile utilizzare i costruttori ServiceHost che accettano un argomento Type.|  
|SFxWrapperTypeHasMultipleNamespaces|Impossibile proiettare il tipo wrapper per il messaggio specificato come tipo di contratto dati in quanto presenta più spazi dei nomi.Utilizzare XmlSerializer.|  
|UriMustBeAbsolute|L'URI deve essere assoluto.|