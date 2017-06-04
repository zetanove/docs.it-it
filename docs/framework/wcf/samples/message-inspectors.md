---
title: "Controlli messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9bd1f305-ad03-4dd7-971f-fa1014b97c9b
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Controlli messaggi
In questo esempio viene illustrato come implementare e configurare i controlli messaggi del client e del servizio.  
  
 Un controllo messaggi è un oggetto extensibility che può essere utilizzato nella fase di esecuzione del client e della distribuzione del modello del servizio a livello di programmazione o tramite configurazione e che può esaminare e modificare i messaggi dopo che sono stati ricevuti o prima che siano inviati.  
  
 Questo esempio implementa un meccanismo di convalida dei messaggi di base del client e del servizio che convalida i messaggi in arrivo confrontandoli con un set di documenti di XML Schema configurabili.Si noti che questo esempio non convalida i messaggi per ogni operazione.Si tratta di una semplificazione intenzionale.  
  
## Controllo messaggi  
 I controlli messaggi del client implementano l'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageInspector>, e i controlli messaggi del servizio implementano l'interfaccia <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector>.Le implementazioni possono essere combinate in una sola classe per formare un controllo messaggi che funzioni per entrambi lati.Questo esempio implementa questo controllo messaggi combinato.Il controllo viene generato tramite il passaggio di un set di schemi con cui vengono confrontati i messaggi in ingresso e in uscita e consente allo sviluppatore di specificare se i messaggi in ingresso o in uscita sono convalidati e se il controllo si trova in modalità client o di distribuzione, cosa che influisce sulla gestione degli errori illustrata in un secondo momento in questo argomento.  
  
```  
  
public class SchemaValidationMessageInspector : IClientMessageInspector, IDispatchMessageInspector  
{  
    XmlSchemaSet schemaSet;  
    bool validateRequest;  
    bool validateReply;  
    bool isClientSide;  
    [ThreadStatic]  
    bool isRequest;  
  
    public SchemaValidationMessageInspector(XmlSchemaSet schemaSet,  
         bool validateRequest, bool validateReply, bool isClientSide)  
    {  
        this.schemaSet = schemaSet;  
        this.validateReply = validateReply;  
        this.validateRequest = validateRequest;  
        this.isClientSide = isClientSide;  
    }  
```  
  
 Qualsiasi controllo messaggi del servizio \(dispatcher\) deve implementare i due metodi <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector><xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A> e <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%28System.ServiceModel.Channels.Message%40%2CSystem.Object%29>.  
  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A> viene richiamato dal dispatcher quando un messaggio è stato ricevuto, elaborato dallo stack di canali e assegnato a un servizio, ma prima che venga deserializzato e inviato a un'operazione.Se il messaggio in arrivo è crittografato, il messaggio arriva al controllo messaggi già decrittografato.Il metodo ottiene il messaggio `request` passato come un parametro di riferimento, il che significa che il messaggio potrà essere controllato, modificato o sostituito in base alla necessità.Il valore restituito può essere qualsiasi oggetto e può essere utilizzato come oggetto dello stato di correlazione che viene passato a <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%2A> quando il servizio restituisce una risposta al messaggio corrente.In questo esempio, <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A> delega l'esame \(la convalida\) del messaggio al metodo privato e locale `ValidateMessageBody` e non restituisce oggetti dello stato di correlazione.Questo metodo assicura che non passino messaggi non validi nel servizio.  
  
```  
object IDispatchMessageInspector.AfterReceiveRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel, System.ServiceModel.InstanceContext instanceContext)  
{  
    if (validateRequest)  
    {  
        // inspect the message. If a validation error occurs,  
        // the thrown fault exception bubbles up.  
        ValidateMessageBody(ref request, true);  
    }  
    return null;  
}  
```  
  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%28System.ServiceModel.Channels.Message%40%2CSystem.Object%29> viene richiamato ogni volta che una risposta è pronta per essere restituita a un client o, nel caso di messaggi unidirezionali, quando il messaggio in arrivo è stato elaborato.Questo consente alle estensioni di essere chiamate simmetricamente, indipendentemente da MEP.Come con <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>, il messaggio viene passato come un parametro di riferimento e può essere controllato, modificato o sostituito.La convalida del messaggio eseguita in questo esempio è delegata nuovamente al metodo `ValidMessageBody`, ma la gestione degli errori di convalida è leggermente diversa in questo caso.  
  
 Se si verifica un errore di convalida nel servizio, il metodo `ValidateMessageBody` genera eccezioni derivate da <xref:System.ServiceModel.FaultException>.In <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>, queste eccezioni possono essere inserite nell'infrastruttura del modello di servizi, dove vengono automaticamente trasformate in errori SOAP e inoltrate al client.In <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%2A>, le eccezioni <xref:System.ServiceModel.FaultException> non possono essere inserite nell'infrastruttura, perché la trasformazione di eccezioni d'errore generate dal servizio avviene prima che il controllo messaggi venga chiamato.Pertanto l'implementazione seguente rileva l'eccezione `ReplyValidationFault` nota e sostituisce il messaggio di risposta con un messaggio di errore esplicito.Questo metodo assicura che non vengano restituiti messaggi non validi dall'implementazione del servizio.  
  
```  
  
void IDispatchMessageInspector.BeforeSendReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
{  
    if (validateReply)  
    {  
        // Inspect the reply, catch a possible validation error   
        try  
        {  
            ValidateMessageBody(ref reply, false);  
        }  
        catch (ReplyValidationFault fault)  
        {  
            // if a validation error occurred, the message is replaced  
            // with the validation fault.  
            reply = Message.CreateMessage(reply.Version,   
                    fault.CreateMessageFault(), reply.Headers.Action);  
        }  
    }  
```  
  
 Il controllo messaggi del client è molto simile.I due metodi da implementare da <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> sono <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.AfterReceiveReply%2A> e <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A>.  
  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A> viene richiamato quando il messaggio è stato composto dall'applicazione client o dal formattatore dell'operazione.Come per i controlli messaggi del dispatcher, il messaggio può essere solo controllato o completamente sostituito.In questo esempio, l'ispettore delega allo stesso metodo di supporto locale `ValidateMessageBody` che viene utilizzato anche per i controlli messaggi della distribuzione.  
  
 La differenza di comportamento tra la convalida del client e quella del servizio \(come specificato nel costruttore\) è che la convalida del client genera eccezioni locali che vengono inserite nel codice utente perché si verificano localmente e non a causa di un errore del servizio.In genere, la regola è che i controlli dispatcher del servizio generano errori e che i controlli del client generano eccezioni.  
  
 Questa implementazione <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A> assicura che non vengano inviati messaggi non validi al servizio.  
  
```  
object IClientMessageInspector.BeforeSendRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel)  
{  
    if (validateRequest)  
    {  
        ValidateMessageBody(ref request, true);  
    }  
    return null;  
}  
```  
  
 L'implementazione `AfterReceiveReply` assicura che nessun messaggio non valido ricevuto dal servizio venga inoltrato al codice utente del client.  
  
```  
void IClientMessageInspector.AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
{  
    if (validateReply)  
    {  
        ValidateMessageBody(ref reply, false);  
    }  
}  
```  
  
 L'elemento essenziale di questo particolare controllo messaggi è il metodo `ValidateMessageBody`.Per eseguire il lavoro, esegue il wrapping di un <xref:System.Xml.XmlReader> di convalida sulla sottostruttura ad albero del contenuto del corpo del messaggio passato.Il lettore viene popolato con il set di schemi contenuti dal controllo messaggi e il callback di convalida viene impostato su un delegato che fa riferimento all'elemento `InspectionValidationHandler` definito insieme al metodo.Per eseguire la convalida, il messaggio viene letto e ne viene eseguito lo spooling in una memoria <xref:System.Xml.XmlDictionaryWriter> basata sul flusso.Se si verifica un errore di convalida o un avviso durante il processo, il metodo di callback viene richiamato.  
  
 Se non si verificano errori, viene costruito un nuovo messaggio che copia le proprietà e le intestazioni dal messaggio originale e utilizza l'InfoSet convalidato nel flusso di memoria, racchiuso in un <xref:System.Xml.XmlDictionaryReader> e aggiunto al messaggio sostitutivo.  
  
```  
  
void ValidateMessageBody(ref System.ServiceModel.Channels.Message message, bool isRequest)  
{  
    if (!message.IsFault)  
    {  
        XmlDictionaryReaderQuotas quotas =   
                new XmlDictionaryReaderQuotas();  
        XmlReader bodyReader =   
            message.GetReaderAtBodyContents().ReadSubtree();  
        XmlReaderSettings wrapperSettings =   
                              new XmlReaderSettings();  
        wrapperSettings.CloseInput = true;  
        wrapperSettings.Schemas = schemaSet;  
        wrapperSettings.ValidationFlags =   
                                XmlSchemaValidationFlags.None;  
        wrapperSettings.ValidationType = ValidationType.Schema;  
        wrapperSettings.ValidationEventHandler += new   
           ValidationEventHandler(InspectionValidationHandler);  
        XmlReader wrappedReader = XmlReader.Create(bodyReader,   
                                            wrapperSettings);  
  
        // pull body into a memory backed writer to validate  
        this.isRequest = isRequest;  
        MemoryStream memStream = new MemoryStream();  
        XmlDictionaryWriter xdw =  
              XmlDictionaryWriter.CreateBinaryWriter(memStream);  
        xdw.WriteNode(wrappedReader, false);  
        xdw.Flush(); memStream.Position = 0;  
        XmlDictionaryReader xdr =   
        XmlDictionaryReader.CreateBinaryReader(memStream, quotas);  
  
        // reconstruct the message with the validated body  
        Message replacedMessage =   
            Message.CreateMessage(message.Version, null, xdr);  
        replacedMessage.Headers.CopyHeadersFrom(message.Headers);  
        replacedMessage.Properties.CopyProperties(message.Properties);  
        message = replacedMessage;  
    }  
}  
```  
  
 Il metodo `InspectionValidationHandler` viene chiamato dal <xref:System.Xml.XmlReader> di convalida ogni volta che si verifica un errore o un avviso di convalida.L'implementazione seguente funziona solo con gli errori e ignora tutti gli avvisi.  
  
 A prima vista. potrebbe sembrare possibile inserire un <xref:System.Xml.XmlReader> di convalida nel messaggio insieme al controllo messaggi e lasciare che la convalida si verifichi automaticamente quando viene elaborato il messaggio e senza memorizzarlo nel buffer.Tuttavia, ciò significa che questo callback genera le eccezioni di convalida da qualche parte nell'infrastruttura del modello del servizio o nel codice utente quando vengono rilevati nodi XML non validi, risultando in un comportamento imprevedibile.Memorizzando il messaggio nel buffer, si protegge completamente il codice utente dai messaggi non validi.  
  
 Come illustrato precedentemente, le eccezioni generate dal gestore sono diverse per il client e per il servizio.Nel servizio, le eccezioni derivano da <xref:System.ServiceModel.FaultException>, mentre nel client che le eccezioni sono normali eccezioni personalizzate.  
  
```  
        void InspectionValidationHandler(object sender, ValidationEventArgs e)  
{  
    if (e.Severity == XmlSeverityType.Error)  
    {  
        // We are treating client and service side validation errors  
        // differently here. Client side errors cause exceptions  
        // and are thrown straight up to the user code. Service side  
        // validations cause faults.  
        if (isClientSide)  
        {  
            if (isRequest)  
            {  
                throw new RequestClientValidationException(e.Message);  
            }  
            else  
            {  
                throw new ReplyClientValidationException(e.Message);  
            }  
        }  
        else  
        {  
            if (isRequest)  
            {  
                // this fault is caught by the ServiceModel   
                // infrastructure and turned into a fault reply.  
                throw new RequestValidationFault(e.Message);  
             }  
             else  
             {  
                // this fault is caught and turned into a fault message  
                // in BeforeSendReply in this class  
                throw new ReplyValidationFault(e.Message);  
              }  
          }  
      }  
    }  
```  
  
## Comportamento  
 I controlli messaggi sono estensioni alla fase di esecuzione del client o della distribuzione.Tali estensioni sono configurate utilizzando i *comportamenti*.Un comportamento è una classe che modifica il comportamento della fase di esecuzione del modello del servizio modificando la configurazione predefinita o aggiungendole estensioni \(ad esempio controlli messaggi\).  
  
 La classe `SchemaValidationBehavior` seguente rappresenta il comportamento utilizzato per aggiungere il controllo messaggi di questo esempio alla fase di esecuzione del client o della distribuzione.L'implementazione è piuttosto semplice in entrambi casi.In <xref:System.ServiceModel.Description.IEndpointBehavior.ApplyClientBehavior%2A> e <xref:System.ServiceModel.Description.IEndpointBehavior.ApplyDispatchBehavior%2A>, il controllo messaggi viene creato e aggiunto alla raccolta <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> della rispettiva fase di esecuzione.  
  
```  
public class SchemaValidationBehavior : IEndpointBehavior  
{  
    XmlSchemaSet schemaSet;   
    bool validateRequest;   
    bool validateReply;  
  
    public SchemaValidationBehavior(XmlSchemaSet schemaSet, bool   
                           inspectRequest, bool inspectReply)  
    {  
        this.schemaSet = schemaSet;  
        this.validateReply = inspectReply;  
        this.validateRequest = inspectRequest;  
    }  
    #region IEndpointBehavior Members  
  
    public void AddBindingParameters(ServiceEndpoint endpoint,   
       System.ServiceModel.Channels.BindingParameterCollection   
                                            bindingParameters)  
    {  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint,   
            System.ServiceModel.Dispatcher.ClientRuntime clientRuntime)  
    {  
        SchemaValidationMessageInspector inspector =   
           new SchemaValidationMessageInspector(schemaSet,   
                      validateRequest, validateReply, true);  
            clientRuntime.MessageInspectors.Add(inspector);  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint,   
         System.ServiceModel.Dispatcher.EndpointDispatcher   
                                          endpointDispatcher)  
    {  
        SchemaValidationMessageInspector inspector =   
           new SchemaValidationMessageInspector(schemaSet,   
                        validateRequest, validateReply, false);  
   endpointDispatcher.DispatchRuntime.MessageInspectors.Add(inspector);  
    }  
  
   public void Validate(ServiceEndpoint endpoint)  
   {  
   }  
  
    #endregion  
}  
```  
  
> [!NOTE]
>  Questo particolare comportamento non funge anche da attributo e pertanto non può essere aggiunto in modo dichiarativo a un tipo di contratto di un tipo di servizio.Si tratta di una decisione presa a livello di programmazione perché la raccolta di schemi non può essere caricata in una dichiarazione di attributo e fare riferimento a un ulteriore percorso di configurazione \(per esempio alle impostazioni dell'applicazione\) in questo attributo significa creare un elemento di configurazione non coerente con il resto della configurazione del modello del servizio.Pertanto, questo comportamento può essere aggiunto soltanto in modo imperativo tramite codice o tramite una configurazione del modello del servizio.  
  
## Aggiunta del controllo messaggi tramite configurazione  
 Per configurare un comportamento personalizzato in un endpoint nel file di configurazione dell'applicazione, il modello del servizio richiede agli implementatori di creare un *elemento di estensione* di configurazione rappresentato da una classe derivata da <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>.Questa estensione deve essere quindi aggiunta alla sezione di configurazione del modello del servizio per le estensioni come illustrato per le seguenti estensioni in questo argomento.  
  
```  
<system.serviceModel>  
…  
   <extensions>  
      <behaviorExtensions>  
        <add name="schemaValidator" type="Microsoft.ServiceModel.Samples.SchemaValidationBehaviorExtensionElement, MessageInspectors, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
      </behaviorExtensions>  
    </extensions>  
…  
</system.serviceModel>  
```  
  
 Le estensioni possono essere aggiunte all'applicazione o al file di configurazione ASP.NET, che rappresenta la scelta più comune, oppure nel file di configurazione del computer.  
  
 Quando l'estensione viene aggiunta a un ambito di configurazione, il comportamento può essere aggiunto a una configurazione di comportamento come illustrato nel codice seguente.Le configurazioni di comportamento sono elementi riutilizzabili che possono essere applicati a più endpoint, in base alle necessità.Poiché il comportamento da configurare in questa situazione implementa <xref:System.ServiceModel.Description.IEndpointBehavior>, è valido solo nella rispettiva sezione di configurazione del file di configurazione.  
  
```  
<system.serviceModel>  
   <behaviors>  
      …  
     <endpointBehaviors>  
        <behavior name="HelloServiceEndpointBehavior">  
          <schemaValidator validateRequest="True" validateReply="True">  
            <schemas>  
              <add location="messages.xsd" />    
            </schemas>  
          </schemaValidator>  
        </behavior>  
      </endpointBehaviors>  
      …  
    </behaviors>  
</system.serviceModel>  
```  
  
 L'elemento `<schemaValidator>` che configura il controllo messaggi si bassa sulla classe `SchemaValidationBehaviorExtensionElement`.La classe espone due proprietà pubbliche booleane denominate `ValidateRequest` e `ValidateReply`.Entrambi queste proprietà sono contrassegnate da un <xref:System.Configuration.ConfigurationPropertyAttribute>.Questo attributo rappresenta il collegamento tra le proprietà del codice e gli attributi XML che possono essere visualizzati nell'elemento di configurazione XML precedente.La classe è inoltre dotata di una proprietà `Schemas` che è contrassegnata ulteriormente da <xref:System.Configuration.ConfigurationCollectionAttribute> ed è del tipo `SchemaCollection`, che fa parte di questo esempio ma è stato omesso da questo documento per motivi di brevità.Questa proprietà, con la raccolta e la classe di elementi della raccolta `SchemaConfigElement` si basa sull'elemento `<schemas>` presente nel frammento di configurazione precedente e consente di aggiungere una raccolta di schemi al set di convalida.  
  
 Il metodo `CreateBehavior` sottoposto a override trasforma i dati di configurazione in un oggetto di comportamento quando la fase di esecuzione valuta i dati di configurazione mentre compila un client o un endpoint.  
  
```  
public class SchemaValidationBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public SchemaValidationBehaviorExtensionElement()  
    {  
    }  
  
    public override Type BehaviorType   
    {   
        get  
        {  
            return typeof(SchemaValidationBehavior);  
        }   
    }  
  
    protected override object CreateBehavior()  
    {  
        XmlSchemaSet schemaSet = new XmlSchemaSet();  
        foreach (SchemaConfigElement schemaCfg in this.Schemas)  
        {  
            Uri baseSchema = new   
                Uri(AppDomain.CurrentDomain.BaseDirectory);  
            string location = new   
                Uri(baseSchema,schemaCfg.Location).ToString();  
            XmlSchema schema =   
                XmlSchema.Read(new XmlTextReader(location), null);  
            schemaSet.Add(schema);  
        }  
     return new   
     SchemaValidationBehavior(schemaSet,ValidateRequest,ValidateReply);  
    }  
  
[ConfigurationProperty("validateRequest",DefaultValue=false,IsRequired=false)]  
public bool ValidateRequest  
{  
    get { return (bool)base["validateRequest"]; }  
    set { base["validateRequest"] = value; }  
}  
  
[ConfigurationProperty("validateReply", DefaultValue = false, IsRequired = false)]  
        public bool ValidateReply  
        {  
            get { return (bool)base["validateReply"]; }  
            set { base["validateReply"] = value; }  
        }  
  
     //Declare the Schema collection property.  
     //Note: the "IsDefaultCollection = false" instructs   
     //.NET Framework to build a nested section of   
     //the kind <Schema> ...</Schema>.  
    [ConfigurationProperty("schemas", IsDefaultCollection = true)]  
    [ConfigurationCollection(typeof(SchemasCollection),  
        AddItemName = "add",  
        ClearItemsName = "clear",  
        RemoveItemName = "remove")]  
    public SchemasCollection Schemas  
    {  
        get  
        {  
            SchemasCollection SchemasCollection =  
            (SchemasCollection)base["schemas"];  
            return SchemasCollection;  
        }  
    }  
}  
```  
  
## Aggiunta di controlli messaggi in modo imperativo  
 I comportamenti possono essere aggiunti facilmente alla fase di esecuzione del client e o del servizio utilizzando il codice imperativo, ma non utilizzando attributi \(funzione non supportata in questo esempio per la ragione sopra citata\) e configurazione.In questo esempio, questa operazione viene eseguita nell'applicazione client per testare il controllo messaggi del client.La classe `GenericClient` deriva da <xref:System.ServiceModel.ClientBase%601>, che espone la configurazione dell'endpoint al codice utente.Prima che il client venga aperto in modo implicito, la configurazione dell'endpoint può essere modificata, ad esempio aggiungendo i comportamenti come illustrato nel codice seguente.L'aggiunta del comportamento al servizio è praticamente equivalente alla tecnica per client illustrata e deve essere eseguita prima che l'host del servizio venga aperto.  
  
```  
try  
{  
    Console.WriteLine("*** Call 'Hello' with generic client, with client behavior");  
    GenericClient client = new GenericClient();  
  
    // Configure client programmatically, adding behavior  
    XmlSchema schema = XmlSchema.Read(new StreamReader("messages.xsd"),   
                                                          null);  
    XmlSchemaSet schemaSet = new XmlSchemaSet();  
    schemaSet.Add(schema);  
    client.Endpoint.Behaviors.Add(new   
                SchemaValidationBehavior(schemaSet, true, true));  
  
    Console.WriteLine("--- Sending valid client request:");  
    GenericCallValid(client, helloAction);  
    Console.WriteLine("--- Sending invalid client request:");  
    GenericCallInvalid(client, helloAction);  
  
    client.Close();  
}  
catch (Exception e)  
{  
    DumpException(e);  
}  
  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\MessageInspectors`  
  
## Vedere anche