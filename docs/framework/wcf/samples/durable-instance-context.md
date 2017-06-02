---
title: "Contesto dell&#39;istanza durevole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2994-5a2c-47c7-927a-c4cd273153df
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Contesto dell&#39;istanza durevole
In questo esempio viene illustrato come personalizzare il runtime di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per abilitare contesti dell'istanza durevoli.SQL Server 2005 viene utilizzato come archivio di backup \(in questo caso SQL Server 2005 Express\).Tuttavia, viene fornito anche un modo di accedere ai meccanismi di archiviazione personalizzati.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Questo esempio riguarda l'estensione del livello del canale e del livello del modello di servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].È pertanto necessario comprendere i concetti sottostanti prima di entrare nei dettagli dell'implementazione.  
  
 I contesti dell'istanza durevoli si trovano spesso in situazioni del mondo reale.Ad esempio, un'applicazione di carrello degli acquisti ha la possibilità di sospendere gli acquisti a metà strada e continuarli un altro giorno.Quando si visita il carrello degli acquisti il giorno successivo, il contesto originale viene ripristinato.È importante notare che l'applicazione di carrello degli acquisti \(sul server\) non mantiene l'istanza del carrello degli acquisti mentre si è disconnessi.Invece, lo stato viene salvato in un archivio durevole e viene utilizzato per generare una nuova istanza del contesto ripristinato.Pertanto l'istanza del servizio che può essere utile allo stesso contesto non corrisponde all'istanza precedente \(ovvero, non ha lo stesso indirizzo di memoria\).  
  
 Il contesto dell'istanza durevole è reso possibile da un piccolo protocollo che consente al client e al servizio di scambiare un ID del contesto.Questo ID del contesto viene creato sul client e trasmesso al servizio.Quando viene creata l'istanza del servizio, il runtime del servizio tenta di caricare lo stato salvato che corrisponde a questo ID del contesto da un'archiviazione permanente \(per impostazione predefinita corrisponde a un database SQL Server 2005\).Se non ci sono stati disponibili, la nuova istanza è dotata di uno stato predefinito.L'implementazione del servizio utilizza un attributo personalizzato per contrassegnare le operazioni che modificano il runtime del servizio, in modo che la fase di esecuzione possa salvare l'istanza del servizio dopo averle richiamate.  
  
 Dalla descrizione precedente è possibile individuare i due passaggi necessari per raggiungere l'obiettivo:  
  
1.  Modificare il messaggio che va in transito per portare l'ID del contesto.  
  
2.  Modificare il comportamento locale del servizio per implementare la logica dell'istanza personalizzata.  
  
 Poiché il primo passaggio influisce sul messaggio in transito, deve essere implementato come canale personalizzato e associato al livello del canale.Il secondo passaggio influisce solo sul comportamento locale del servizio e pertanto può essere implementato estendendo vari punti di estensibilità del servizio.Nelle prossime sezioni verranno illustrate tutte queste estensioni.  
  
## Canale InstanceContext durevole  
 La prima cosa da notare è l'estensione del livello del canale.Il primo passaggio per creare un canale personalizzato consiste nel decidere la struttura della comunicazione del canale.Poiché viene introdotto un nuovo protocollo di rete, è necessario che il canale funzioni con tutti gli altri canali dello stack di canali.È pertanto necessario che supporti tutti i modelli di scambio dei messaggi.Tuttavia, la funzionalità principale del canale rimane la stessa, indipendentemente dalla struttura della comunicazione.Più specificamente, deve scrivere l'ID del contesto ai messaggi dal client e leggere questo ID del contesto dai messaggi dal servizio, per poi passarlo ai livelli superiori.Per questa ragione, viene creata una classe `DurableInstanceContextChannelBase` che rappresenta la classe di base astratta per tutte le implementazioni dei canali del contesto dell'istanza durevole.Questa classe contiene le funzioni comuni di gestione del computer di stato e due membri protetti per applicare e leggere le informazioni di contesto a e da i messaggi.  
  
```  
class DurableInstanceContextChannelBase  
{  
  //…  
  protected void ApplyContext(Message message)  
  {  
    //…              
  }  
  protected string ReadContextId(Message message)  
  {  
    //…              
  }  
}  
```  
  
 Questi due metodi si avvalgono delle implementazioni `IContextManager` per scrivere e leggere l'ID del contesto a o da il messaggio.\(`IContextManager` è un'interfaccia personalizzata utilizzata per definire il contratto per tutti i gestori del contesto\). Il canale può includere l'ID del contesto in un'intestazione SOAP personalizzata o in un'intestazione HTTP del cookie.Ogni implementazione dei gestori di contesto eredita dalla classe `ContextManagerBase` che contiene le funzionalità comuni per tutti i gestori del contesto.Il metodo `GetContextId` in questa classe viene utilizzato per originare l'ID del contesto dal client.Quando un ID del contesto viene originato per la prima volta, questo metodo lo salva in un file di testo il cui nome è costituito dall'indirizzo endpoint remoto \(i caratteri del nome file non validi degli URI tipici sono sostituiti con il carattere @\).  
  
 In un secondo momento, quando l'ID del contesto è necessario allo stesso endpoint remoto, il metodo verifica se esiste un file appropriato.Se esiste, il metodo legge l'ID del contesto e termina.In caso contrario, restituisce un ID del contesto appena generato e lo salva in un file.Nella configurazione predefinita, questi file sono posizionati in una directory chiamata ContextStore che risiede nella directory temp dell'utente corrente.Questo percorso è tuttavia configurabile tramite l'elemento di associazione.  
  
 Il meccanismo utilizzato per trasportare l'ID del contesto è configurabile.Può essere scritto nell'intestazione HTTP del cookie o in un'intestazione SOAP personalizzata.Se si utilizza l'intestazione SOAP personalizzata, è possibile utilizzare questo protocollo con i protocolli non HTTP \(ad esempio, TCP o Named pipe\).Le due classi `MessageHeaderContextManager` e `HttpCookieContextManager` implementano queste due opzioni.  
  
 Entrambi scrivono l'ID del contesto nel messaggio in modo appropriato.Ad esempio, la classe `MessageHeaderContextManager` lo scrive in un'intestazione SOAP del metodo `WriteContext`.  
  
```  
public override void WriteContext(Message message)  
{  
  string contextId = this.GetContextId();  
  
  MessageHeader contextHeader =  
    MessageHeader.CreateHeader(DurableInstanceContextUtility.HeaderName,  
      DurableInstanceContextUtility.HeaderNamespace,  
      contextId,   
      true);  
  
  message.Headers.Add(contextHeader);  
}   
```  
  
 I metodi `ApplyContext` e `ReadContextId` della classe  `DurableInstanceContextChannelBase` richiamano rispettivamente `IContextManager.ReadContext` e `IContextManager.WriteContext`.Questi gestori del contesto non vengono creati direttamente dalla classe `DurableInstanceContextChannelBase`.Viene utilizzata la classe `ContextManagerFactory` per eseguire quel processo.  
  
```  
IContextManager contextManager =  
                ContextManagerFactory.CreateContextManager(contextType,   
                this.contextStoreLocation,   
                this.endpointAddress);  
```  
  
 Il metodo `ApplyContext` viene richiamato dai canali di invio.Inserisce l'ID del contesto nei messaggi in uscita.Il metodo `ReadContextId` viene richiamato dai canali di ricezione.Questo metodo assicura che l'ID del contesto sia disponibile nei messaggi in arrivo e lo aggiunge alla raccolta `Properties` della classe `Message`.Genera inoltre un'eccezione `CommunicationException` in caso di errore nella lettura dell'ID del contesto, facendo in modo che il canale venga interrotto.  
  
```  
message.Properties.Add(DurableInstanceContextUtility.ContextIdProperty, contextId);  
```  
  
 Prima di procedere, è importante comprendere l'utilizzo della raccolta `Properties` nella classe `Message`.In genere, questa raccolta `Properties` viene utilizzata quando si passano dati dai livelli inferiore a quelli superiori dal livello del canale.In questo modo i dati desiderati possono essere forniti ai livelli superiori in modo coerente, indipendentemente dai dettagli del protocollo.In altre parole, il livello del canale può inviare e ricevere l'ID del contesto come intestazione SOAP o come intestazione HTTP del cookie.Ma non è necessario che i livelli superiori conoscano questi dettagli, perché il livello del canale rende disponibili queste informazioni nella raccolta `Properties`.  
  
 Una volta sistemata la classe `DurableInstanceContextChannelBase` tutte e dieci le interfacce necessarie \(IOutputChannel, IInputChannel, IOutputSessionChannel, IInputSessionChannel, IRequestChannel, IReplyChannel, IRequestSessionChannel, IReplySessionChannel, IDuplexChannel, IDuplexSessionChannel\) devono essere implementate.Queste interfacce presentano tutti i modelli di scambio di messaggi disponibili \(datagramma, simplex, duplex e le varianti con sessione\).Ognuna di queste implementazioni eredita la classe di base descritta precedentemente e chiama i metodi `ApplyContext` e `ReadContexId` in modo appropriato.Ad esempio, `DurableInstanceContextOutputChannel`, il quale implementa l'interfaccia IOutputChannel, chiama il metodo `ApplyContext` da ogni metodo che invia i messaggi.  
  
```  
public void Send(Message message, TimeSpan timeout)  
{  
    // Apply the context information before sending the message.  
    this.ApplyContext(message);  
    //…  
}   
```  
  
 Invece `DurableInstanceContextInputChannel`, il quale implementa l'interfaccia `IInputChannel`, chiama il metodo `ReadContextId` da ogni metodo che riceve i messaggi.  
  
```  
public Message Receive(TimeSpan timeout)  
{  
    //…  
      ReadContextId(message);  
      return message;  
}  
```  
  
 Tranne che in questi casi, queste implementazioni del canale delegano le chiamate al metodo al canale sottostante nello stack di canali.Tuttavia, le varianti con sessione hanno una logica di base per assicurarsi che l'ID del contesto venga inviato e letto solo per il primo messaggio che crea la sessione.  
  
```  
if (isFirstMessage)  
{  
//…  
    this.ApplyContext(message);  
    isFirstMessage = false;  
}  
```  
  
 Queste implementazioni del canale vengono quindi aggiunte appropriatamente al runtime del canale di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dalle classi `DurableInstanceContextBindingElement` e `DurableInstanceContextBindingElementSection`.Vedere la documentazione relativa agli esempi di canale [HttpCookieSession](../../../../docs/framework/wcf/samples/httpcookiesession.md) per ulteriori dettagli sugli elementi di associazione e le sezioni degli elementi di associazione.  
  
## Estensioni del livello del modello di servizio  
 Ora che l'ID del contesto è stato trasferito utilizzando il livello del canale, il comportamento del servizio può essere implementato per personalizzare la creazione di istanze.In questo esempio, viene utilizzata una gestione archivi per caricare e salvare lo stato a o da l'archivio permanente.Come spiegato in precedenza, questo esempio fornisce una gestione archivi che utilizza SQL Server 2005 come archivio di backup.È tuttavia possibile aggiungere meccanismi di archiviazione personalizzati a questa estensione.Per fare ciò, viene dichiarata un'interfaccia pubblica che deve essere implementata da tutte le gestioni archivi.  
  
```  
public interface IStorageManager  
{  
    object GetInstance(string contextId, Type type);  
    void SaveInstance(string contextId, object state);  
}  
```  
  
 La classe `SqlServerStorageManager` contiene l'implementazione `IStorageManager` predefinita.Nel metodo `SaveInstance` l'oggetto specificato viene serializzato utilizzando XmlSerializer e viene salvato nel database SQL Server.  
  
```  
XmlSerializer serializer = new XmlSerializer(state.GetType());  
string data;  
  
using (StringWriter writer = new StringWriter(CultureInfo.InvariantCulture))  
{  
    serializer.Serialize(writer, state);  
    data = writer.ToString();  
}  
  
using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
{  
    connection.Open();  
  
    string update = @"UPDATE Instances SET Instance = @instance WHERE ContextId = @contextId";  
  
    using (SqlCommand command = new SqlCommand(update, connection))  
    {  
        command.Parameters.Add("@instance", SqlDbType.VarChar, 2147483647).Value = data;  
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;  
  
        int rows = command.ExecuteNonQuery();  
  
        if (rows == 0)  
        {  
            string insert = @"INSERT INTO Instances(ContextId, Instance) VALUES(@contextId, @instance)";  
            command.CommandText = insert;  
            command.ExecuteNonQuery();  
        }  
    }  
}  
```  
  
 Nel metodo `GetInstance` i dati serializzati vengono letti per un ID del contesto specificato e l'oggetto costruito da questo contesto viene restituito al chiamante.  
  
```  
object data;  
using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
{  
    connection.Open();  
  
    string select = "SELECT Instance FROM Instances WHERE ContextId = @contextId";  
    using (SqlCommand command = new SqlCommand(select, connection))  
    {  
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;  
        data = command.ExecuteScalar();  
    }  
}  
  
if (data != null)  
{  
    XmlSerializer serializer = new XmlSerializer(type);  
    using (StringReader reader = new StringReader((string)data))  
    {  
        object instance = serializer.Deserialize(reader);  
        return instance;  
    }  
}  
```  
  
 Non è necessario che gli utenti di queste gestioni archivi creino direttamente un'istanza.Possono utilizzare la classe `StorageManagerFactory` che astrae dai dettagli della creazione della gestione archivi.Questa classe ha uno membro statico, `GetStorageManager`, che crea un'istanza di un tipo di gestione archivi specificato.Se il parametro di tipo è `null`, questo metodo crea un'istanza della classe `SqlServerStorageManager` predefinita e la restituisce.Convalida inoltre il tipo specificato per assicurarsi che implementi l'interfaccia `IStorageManager`.  
  
```  
public static IStorageManager GetStorageManager(Type storageManagerType)  
{  
IStorageManager storageManager = null;  
  
if (storageManagerType == null)  
{  
    return new SqlServerStorageManager();  
}  
else  
{  
    object obj = Activator.CreateInstance(storageManagerType);  
  
    // Throw if the specified storage manager type does not  
    // implement IStorageManager.  
    if (obj is IStorageManager)  
    {  
        storageManager = (IStorageManager)obj;  
    }  
    else  
    {  
        throw new InvalidOperationException(  
                  ResourceHelper.GetString("ExInvalidStorageManager"));  
    }  
  
    return storageManager;  
}                  
}   
```  
  
 L'infrastruttura necessaria per leggere e scrivere istanze dall'archiviazione permanente è implementata.È ora necessario eseguire i passaggi necessari per modificare il comportamento del servizio.  
  
 Come primo passaggio di questo processo è necessario salvare l'ID del contesto che è stato trasferito sul InstanceContext attuale utilizzando il livello del canale.InstanceContext è un componente di runtime che fa da collegamento tra il dispatcher [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e l'istanza del servizio.Può essere utilizzato per fornire stati e comportamenti aggiuntivi all'istanza del servizio.È essenziale, perché nella comunicazione con sessione l'ID del contesto viene inviato solo con il primo messaggio.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di estendere il componente del runtime InstanceContext aggiungendo un nuovo stato e un nuovo comportamento tramite il modello di oggetti estensibili.Questo modello viene utilizzato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per estendere le classi del runtime esistenti con nuove funzionalità oppure per aggiungere nuove funzionalità di stato a un oggetto.Esistono tre interfacce nel modello di oggetti estensibili: IExtensibleObject\<T\>, IExtension\<T\>e IExtensionCollection\<T\>:  
  
-   L'interfaccia IExtensibleObject\<T\> viene implementata dagli oggetti che consentono le estensioni che personalizzano le proprie funzionalità.  
  
-   L'interfaccia IExtension\<T\> viene implementata dagli oggetti che sono estensioni di classi di tipo T.  
  
-   L'interfaccia IExtensionCollection\<T\> è una raccolta di IExtensions che consente di recuperare IExtensions in base al tipo.  
  
 È pertanto necessario creare una classe InstanceContextExtension che implementi l'interfaccia IExtension e definisca lo stato necessario per salvare l'ID del contesto.Questa classe fornisce inoltre lo stato per memorizzare la gestione archivi utilizzata.Una volta salvato il nuovo stato, non sarà possibile modificarlo.Lo stato viene pertanto fornito e salvato nell'istanza che viene generata in quel momento e vi si potrà accedere soltanto utilizzando le proprietà di sola lettura.  
  
```  
// Constructor  
public DurableInstanceContextExtension(string contextId,   
            IStorageManager storageManager)  
{  
    this.contextId = contextId;  
    this.storageManager = storageManager;              
}  
  
// Read only properties  
public string ContextId  
{  
    get { return this.contextId; }  
}  
  
public IStorageManager StorageManager  
{  
    get { return this.storageManager; }              
}   
```  
  
 La classe InstanceContextInitializer implementa l'interfaccia IInstanceContextInitializer e aggiunge l'estensione del contesto di istanza alla raccolta di estensioni dell'InstanceContext che viene generata.  
  
```  
public void Initialize(InstanceContext instanceContext, Message message)  
{  
    string contextId =   
  (string)message.Properties[DurableInstanceContextUtility.ContextIdProperty];  
  
    DurableInstanceContextExtension extension =  
                new DurableInstanceContextExtension(contextId,   
                     storageManager);  
    instanceContext.Extensions.Add(extension);  
}  
```  
  
 Come descritto precedentemente, l'ID del contesto viene letto dalla raccolta `Properties` della classe `Message` e passato al costruttore della classe dell'estensione.Questo dimostra che le informazioni possono essere scambiate tra i livelli in modo coerente.  
  
 Il successivo passaggio consiste nell'eseguire l'override del processo di creazione dell'istanza di servizio.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente l'implementazione dei comportamenti di creazione di istanze personalizzati e di associarli al runtime utilizzando l'interfaccia IInstanceProvider.La nuova classe `InstanceProvider` viene implementata per eseguire quel processo.Il tipo di servizio previsto dal provider di istanze viene accettato nel costruttore.In un secondo momento viene utilizzato per creare nuove istanze.Nell'implementazione `GetInstance` un'istanza di una gestione archivi viene creata cercando un'istanza persistente.Se restituisce `null`, viene creata una nuova istanza del tipo di servizio e viene restituita al chiamante.  
  
```  
public object GetInstance(InstanceContext instanceContext, Message message)  
{  
    object instance = null;  
  
    DurableInstanceContextExtension extension =  
    instanceContext.Extensions.Find<DurableInstanceContextExtension>();  
  
    string contextId = extension.ContextId;  
    IStorageManager storageManager = extension.StorageManager;              
  
    instance = storageManager.GetInstance(contextId, serviceType);          
  
    if (instance == null)  
    {  
        instance = Activator.CreateInstance(serviceType);  
    }  
  
    return instance;  
}  
```  
  
 Il successivo passaggio consiste nell'installare le classi `InstanceContextExtension`,  `InstanceContextInitializer` e `InstanceProvider` nel runtime del modello di servizi.È possibile utilizzare un attributo personalizzato per contrassegnare le classi di implementazione del servizio perché installino il comportamento.`DurableInstanceContextAttribute` contiene l'implementazione per questo attributo e implementa l'interfaccia `IServiceBehavior` per estendere l'intero runtime del servizio.  
  
 Questa classe è dotata di una proprietà che accetta il tipo della gestione archivi da utilizzare.In questo modo l'implementazione consente agli utenti di specificare la propria implementazione `IStorageManager` come parametro di questo attributo.  
  
 Nell'implementazione `ApplyDispatchBehavior` viene verificato il `InstanceContextMode` dell'attributo `ServiceBehavior` attuale.Se questa proprietà è impostata su Singleton, non è possibile abilitare la creazione di istanze durevoli e viene generata un'eccezione `InvalidOperationException` per notificare l'host.  
  
```  
ServiceBehaviorAttribute serviceBehavior =  
    serviceDescription.Behaviors.Find<ServiceBehaviorAttribute>();  
  
if (serviceBehavior != null &&  
     serviceBehavior.InstanceContextMode == InstanceContextMode.Single)  
{  
    throw new InvalidOperationException(  
       ResourceHelper.GetString("ExSingeltonInstancingNotSupported"));  
}  
```  
  
 Dopodiché le istanze della gestione archivi, dell'inizializzatore del contesto dell'istanza e del provider di istanze vengono  creati e installati nel `DispatchRuntime` creato per ogni endpoint.  
  
```  
IStorageManager storageManager =   
    StorageManagerFactory.GetStorageManager(storageManagerType);  
  
InstanceContextInitializer contextInitializer =  
    new InstanceContextInitializer(storageManager);  
  
InstanceProvider instanceProvider =  
    new InstanceProvider(description.ServiceType);  
  
foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)  
{  
    ChannelDispatcher cd = cdb as ChannelDispatcher;  
  
    if (cd != null)  
    {  
        foreach (EndpointDispatcher ed in cd.Endpoints)  
        {  
            ed.DispatchRuntime.InstanceContextInitializers.Add(contextInitializer);  
            ed.DispatchRuntime.InstanceProvider = instanceProvider;  
        }  
    }  
}  
```  
  
 Per riassumere, questo esempio ha prodotto un canale che abilita il protocollo di rete personalizzato per lo scambio di ID del contesto personalizzati e sovrascrive il comportamento di istanza predefinito per caricare le istanze dall'archivio permanente.  
  
 Rimane da trovare un modo per salvare l'istanza del servizio nell'archivio permanente.Come illustrato precedentemente, esiste già la funzionalità necessaria per salvare lo stato in un'implementazione `IStorageManager`.Ora è necessario integrare questa funzionalità con il runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].È necessario un altro attributo applicabile ai metodi della classe di implementazione del servizio.Questo attributo va applicato ai metodi che modificano lo stato dell'istanza del servizio.  
  
 La classe `SaveStateAttribute` implementa questa funzionalità.Implementa inoltre la classe `IOperationBehavior` per modificare il runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per ogni operazione.Quando un metodo è contrassegnato da questo attributo, il runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiama il metodo `ApplyBehavior` mentre viene generato l'elemento  `DispatchOperation` appropriato.In questa implementazione del metodo c'è una sola riga di codice:  
  
```  
dispatch.Invoker = new OperationInvoker(dispatch.Invoker);  
```  
  
 Questa istruzione crea un'istanza di tipo `OperationInvoker` e la assegna alla proprietà `Invoker` dell'elemento `DispatchOperation` che viene generato.La classe `OperationInvoker` è un wrapper per l'invoker dell'operazione predefinita creato per `DispatchOperation`.Questa classe implementa l'interfaccia `IOperationInvoker`.Nell'implementazione del metodo `Invoke` la chiamata al metodo effettiva viene delegata all'invoker dell'operazione interna.Tuttavia, prima di restituire i risultati la gestione archivi in `InstanceContext` viene utilizzata per salvare l'istanza del servizio.  
  
```  
object result = innerOperationInvoker.Invoke(instance,  
    inputs, out outputs);  
  
// Save the instance using the storage manager saved in the   
// current InstanceContext.  
InstanceContextExtension extension =  
    OperationContext.Current.InstanceContext.Extensions.Find<InstanceContextExtension>();  
  
extension.StorageManager.SaveInstance(extension.ContextId, instance);  
return result;  
```  
  
## Utilizzo dell'estensione  
 Le estensioni del livello del canale e del livello del modello di servizio sono state completate e possono essere utilizzate nelle applicazioni di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].È necessario che i servizi aggiungano il canale allo stack di canali utilizzando un'associazione personalizzata e che contrassegnino quindi le classi di implementazione del servizio con gli attributi appropriati.  
  
```  
[DurableInstanceContext]  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
public class ShoppingCart : IShoppingCart  
{  
//…  
     [SaveState]  
     public int AddItem(string item)  
     {  
         //…  
     }  
//…  
 }  
```  
  
 È necessario che le applicazioni client aggiungano DurableInstanceContextChannel allo stack di canali utilizzando un'associazione personalizzata.Per configurare in modo dichiarativo il canale nel file di configurazione la sezione dell'elemento di associazione deve essere aggiunta alla raccolta delle estensioni degli elementi di associazione.  
  
```  
<system.serviceModel>  
 <extensions>  
   <bindingElementExtensions>  
     <add name="durableInstanceContext"  
type="Microsoft.ServiceModel.Samples.DurableInstanceContextBindingElementSection, DurableInstanceContextExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
   </bindingElementExtensions>  
 </extensions>  
```  
  
 È ora possibile utilizzare l'elemento di associazione con un'associazione personalizzata, proprio come gli altri elementi di associazione standard:  
  
```  
<bindings>  
 <customBinding>  
   <binding name="TextOverHttp">  
     <durableInstanceContext contextType="HttpCookie"/>             
     <reliableSession />  
     <textMessageEncoding />  
     <httpTransport />  
   </binding>  
 </customBinding>  
</bindings>  
```  
  
## Conclusione  
 In questo esempio viene illustrato come creare un canale del protocollo personalizzato e come personalizzare il comportamento del servizio per abilitarlo.  
  
 L'estensione può essere ulteriormente migliorata consentendo agli utenti di specificare l'implementazione `IStorageManager` utilizzando una sezione di configurazione.In questo modo è possibile modificare l'archivio di backup senza ricompilare il codice del servizio.  
  
 È inoltre possibile tentare di implementare una classe \(ad esempio, `StateBag`\) che incapsuli lo stato dell'istanza.Quella classe è responsabile di salvare in modo permanente lo stato quando viene modificato.In questo modo è possibile evitare di utilizzare l'attributo `SaveState` ed eseguire più accuratamente il lavoro di archiviazione permanente \(ad esempio, è possibile salvare in modo permanente lo stato solo quando viene davvero modificato piuttosto che salvarlo ogni volta che viene chiamato un metodo con l'attributo `SaveState`\).  
  
 Quando si esegue l'esempio, viene visualizzato l'output seguente:Il client aggiunge due elementi al carrello degli acquisti e ottiene l'elenco di elementi nel carrello degli acquisti dal servizio.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
```  
Enter the name of the product: apples  
Enter the name of the product: bananas  
  
Shopping cart currently contains the following items.  
apples  
bananas  
Press ENTER to shut down client  
```  
  
> [!NOTE]
>  La ricompilazione del servizio si sovrascrive il file di database.Per osservare lo stato salvato in modo permanente in più esecuzioni dell'esempio, assicurarsi di non ricompilare l'esempio tra esecuzioni.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito la  [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!NOTE]
>  È necessario che SQL Server 2005 o SQL Express 2005 siano in esecuzione per eseguire questo esempio.Se è in esecuzione SQL Server 2005, è necessario modificare la configurazione della stringa di connessione del servizio.Quando si esegue tra più computer, SQL Server è necessario solo nel server.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Durable`  
  
## Vedere anche