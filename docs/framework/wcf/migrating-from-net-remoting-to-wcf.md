---
title: "Migrazione da .NET Remoting a WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 16902a42-ef80-40e9-8c4c-90e61ddfdfe5
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Migrazione da .NET Remoting a WCF
In questo articolo viene descritto come eseguire la migrazione di un'applicazione che usa Servizi remoti .NET per l'uso di Windows Communication Foundation \(WCF\).  Vengono confrontati concetti simili tra questi prodotti e quindi viene descritto come realizzare diversi scenari comuni di Servizi remoti .NET in WCF.  
  
 Servizi remoti .NET è un prodotto legacy supportato solo per la compatibilità con le versioni precedenti.  Non è sicuro in ambienti ad attendibilità mista poiché non è in grado di mantenere livelli di attendibilità distinti tra il client e il server.  Ad esempio, è consigliabile non esporre mai un endpoint Servizi remoti .NET a Internet o a client non attendibili.  Si consiglia di eseguire la migrazione delle applicazioni Servizi remoti .NET esistenti a tecnologie più recenti e sicure.  Se la progettazione dell'applicazione usa solo HTTP ed è RESTful, è consigliabile l'API Web ASP.NET.  Per altre informazioni, vedere l'API Web ASP.NET.  Se l'applicazione è basata su SOAP o richiede protocolli diversi da HTTP, come ad esempio TCP, è consigliabile WCF.  
  
-   [Confronto tra Servizi remoti .NET e WCF](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Compare_Top)  
  
    -   [Confronto dell'implementazione server](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Server_Comp)  
  
    -   [Confronto dell'implementazione client](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Client_Comp)  
  
    -   [Uso della serializzazione](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Serialization_Usage)  
  
    -   [Funzionalità di gestione delle eccezioni](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Exception_Handling)  
  
    -   [Considerazioni sulla sicurezza](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Security_Considerations)  
  
-   [Migrazione a WCF](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Migrating_Top)  
  
    -   [Perché eseguire la migrazione da Servizi remoti .NET a WCF?](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Why_Migrate)  
  
    -   [Suggerimenti sulla migrazione](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Migration_Recommendations)  
  
    -   [Scenari di migrazione](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Migration_Scenarios)  
  
-   [Riepilogo](../../../docs/framework/wcf/migrating-from-net-remoting-to-wcf.md#Summary)  
  
<a name="Compare_Top"></a>   
## Confronto tra Servizi remoti .NET e WCF  
 In questa sezione vengono confrontati i componenti di base di Servizi remoti .NET con gli equivalenti di WCF.  Questi componenti di base verranno usati in un secondo momento per creare alcuni scenari client\-server comuni in WCF. Nella tabella seguente sono riepilogate le principali analogie e differenze tra Servizi remoti .NET e WCF.  
  
||Servizi remoti .NET|WCF|  
|-|-------------------------|---------|  
|Tipo di server|Sottoclasse MarshalByRefObject|Contrassegno con l'attributo \[ServiceContract\]|  
|Operazioni di servizio|Metodi pubblici nel tipo di server|Contrassegno con l'attributo \[OperationContract\]|  
|Serializzazione|ISerializable o \[Serializable\]|DataContractSerializer o XmlSerializer|  
|Oggetti passati|In base al valore o in base al riferimento|Solo in base al valore|  
|Errori\/eccezioni|Qualsiasi eccezione serializzabile|FaultContract\<TDetail\>|  
|Oggetti proxy client|Proxy trasparenti fortemente tipizzati vengono creati automaticamente da MarshalByRefObjects|Proxy fortemente tipizzati vengono generati su richiesta usando ChannelFactory\<TChannel\>|  
|Piattaforma richiesta|Sia il client che il server devono usare un sistema operativo Microsoft e .NET|Multipiattaforma|  
|Formato dei messaggi|Private|Standard di settore \(SOAP, WS\-\* e così via\)|  
  
<a name="Server_Comp"></a>   
### Confronto dell'implementazione server  
  
#### Creazione di un server in Servizi remoti .NET  
 I tipi di server di Servizi remoti .NET devono derivare da MarshalByRefObject e definire i metodi che il client può chiamare, nel modo seguente:  
  
```  
public class RemotingServer : MarshalByRefObject  
{  
    public Customer GetCustomer(int customerId) { … }  
}  
```  
  
 I metodi pubblici di questo tipo di server diventano il contratto pubblico disponibile per i client.  Non vi è alcuna separazione tra l'interfaccia pubblica del server e la relativa implementazione: un solo tipo le gestisce entrambe.  
  
 Dopo aver definito il tipo di server, questo può essere reso disponibile ai client, come nell'esempio seguente:  
  
```  
TcpChannel channel = new TcpChannel(8080);  
ChannelServices.RegisterChannel(channel, ensureSecurity : true);  
RemotingConfiguration.RegisterWellKnownServiceType(  
    typeof(RemotingServer),   
    "RemotingServer",   
    WellKnownObjectMode.Singleton);  
Console.WriteLine("RemotingServer is running.  Press ENTER to terminate...");  
Console.ReadLine();  
  
```  
  
 Esistono diversi modi per rendere disponibile il tipo di Servizi remoti .NET come server, incluso l'uso di file di configurazione.  Questo è solo un esempio.  
  
#### Creazione di un server in WCF  
 Il passaggio equivalente in WCF prevede la creazione di due tipi: il "contratto di servizio" pubblico e l'implementazione concreta.  Il primo viene dichiarato come un'interfaccia contrassegnata con \[ServiceContract\].  I metodi disponibili per i client sono contrassegnati con \[OperationContract\]:  
  
```  
[ServiceContract]  
public interface IWCFServer  
{  
    [OperationContract]  
    Customer GetCustomer(int customerId);  
}  
  
```  
  
 L'implementazione del server è definita in una classe concreta distinta, come nell'esempio seguente:  
  
```  
public class WCFServer : IWCFServer  
{  
    public Customer GetCustomer(int customerId) { … }  
}  
```  
  
 Dopo aver definito questi tipi, il server WCF può essere reso disponibile ai client, come nell'esempio seguente:  
  
```  
NetTcpBinding binding = new NetTcpBinding();  
Uri baseAddress = new Uri("net.tcp://localhost:8000/wcfserver");  
  
using (ServiceHost serviceHost = new ServiceHost(typeof(WCFServer), baseAddress))  
{  
    serviceHost.AddServiceEndpoint(typeof(IWCFServer), binding, baseAddress);  
    serviceHost.Open();  
  
    Console.WriteLine(String.Format("The WCF server is ready at {0}.",  
                                    baseAddress));  
    Console.WriteLine("Press <ENTER> to terminate service...");  
    Console.WriteLine();  
    Console.ReadLine();  
}  
  
```  
  
> [!NOTE]
>  Viene usato TCP in entrambi gli esempi per mantenerli quanto più simili possibile.  Per esempi relativi all'uso di HTTP, fare riferimento alle procedure dettagliate per gli scenari, disponibili più avanti in questo argomento.  
  
 Esistono diversi modi per configurare e ospitare servizi WCF.  Questo è solo un esempio, basato su un approccio "self\-hosted".  Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Procedura: definire il contratto di servizio](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)  
  
-   [Configurazione dei servizi tramite file di configurazione](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)  
  
-   [Servizi host](../../../docs/framework/wcf/hosting-services.md)  
  
<a name="Client_Comp"></a>   
### Confronto dell'implementazione client  
  
#### Creazione di un client in Servizi remoti .NET  
 Una volta che è stato reso disponibile un oggetto server Servizi remoti .NET, questo può essere usato dai client, come nell'esempio seguente:  
  
```  
TcpChannel channel = new TcpChannel();  
ChannelServices.RegisterChannel(channel, ensureSecurity : true);  
RemotingServer server = (RemotingServer)Activator.GetObject(  
                            typeof(RemotingServer),   
                            "tcp://localhost:8080/RemotingServer");  
  
RemotingCustomer customer = server.GetCustomer(42);  
Console.WriteLine(String.Format("Customer {0} {1} received.",   
                                 customer.FirstName, customer.LastName));  
```  
  
 L'istanza RemotingServer restituita da Activator.GetObject\(\) è denominata "proxy trasparente". Implementa l'API pubblica per il tipo RemotingServer sul client, ma tutti i metodi chiamano l'oggetto server in esecuzione in un altro processo o computer.  
  
#### Creazione di un client in WCF  
 Il passaggio equivalente in WCF prevede l'uso di una channel factory per creare il proxy in modo esplicito.  Analogamente a Servizi remoti .NET, l'oggetto proxy può essere usato per richiamare operazioni sul server, come nell'esempio seguente:  
  
```  
NetTcpBinding binding = new NetTcpBinding();  
String url = "net.tcp://localhost:8000/wcfserver";  
EndpointAddress address = new EndpointAddress(url);  
ChannelFactory<IWCFServer> channelFactory =   
    new ChannelFactory<IWCFServer>(binding, address);  
IWCFServer server = channelFactory.CreateChannel();  
  
Customer customer = server.GetCustomer(42);  
Console.WriteLine(String.Format("  Customer {0} {1} received.",  
                    customer.FirstName, customer.LastName));  
```  
  
 In questo esempio viene illustrata la programmazione a livello di canale perché è molto simile all'esempio relativo a Servizi remoti .NET.  In Visual Studio è inoltre disponibile l'approccio **Aggiungi riferimento al servizio**, che genera codice per semplificare la programmazione del client.  Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Programmazione a livello di canale client](../../../docs/framework/wcf/extending/client-channel-level-programming.md)  
  
-   [How to: Add, Update, or Remove a Service Reference](../Topic/How%20to:%20Add,%20Update,%20or%20Remove%20a%20Service%20Reference.md)  
  
<a name="Serialization_Usage"></a>   
### Uso della serializzazione  
 Sia Servizi remoti .NET che WCF usano la serializzazione per l'invio di oggetti tra il client e il server, ma vi sono tre importanti differenze:  
  
1.  Vengono usati serializzatori e convenzioni differenti per indicare gli elementi da serializzare.  
  
2.  Servizi remoti .NET supporta la serializzazione "in base al riferimento", che consente l'accesso a proprietà o metodi su un livello per l'esecuzione di codice su un altro livello, ovvero attraverso i limiti di sicurezza.  Questa funzionalità espone vulnerabilità di sicurezza e rappresenta uno dei motivi principali per cui gli endpoint Servizi remoti .NET non devono mai essere esposti a client non attendibili.  
  
3.  La serializzazione usata da Servizi remoti .NET è di tipo opt\-out \(vengono esclusi in modo esplicito gli elementi da non serializzare\), mentre la serializzazione di WCF è di tipo opt\-in \(vengono contrassegnati in modo esplicito i membri da serializzare\).  
  
#### Serializzazione in Servizi remoti .NET  
 Servizi remoti .NET supporta due modi per serializzare e deserializzare gli oggetti tra client e server:  
  
-   *In base al valore*. I valori dell'oggetto vengono serializzati attraverso i limiti del livello e viene creata una nuova istanza dell'oggetto su un altro livello.  Tutte le chiamate a metodi o proprietà della nuova istanza sono in esecuzione solo in locale e non influiscono sull'oggetto o sul livello originale.  
  
-   *In base al riferimento*. Uno speciale "riferimento all'oggetto" viene serializzato attraverso i limiti del livello.  Quando un livello interagisce con metodi o proprietà di tale oggetto, comunica con l'oggetto originale nel livello originale.  Il flusso degli oggetti in base al riferimento può avvenire in entrambe le direzioni: dal server al client o dal client al server.  
  
 I tipi in base al valore in Servizi remoti .NET sono contrassegnati con l'attributo \[Serializable\] o implementano ISerializable, come nell'esempio seguente:  
  
```  
[Serializable]  
public class RemotingCustomer  
{  
    public string FirstName { get; set; }  
    public string LastName { get; set; }  
    public int CustomerId { get; set; }  
}  
```  
  
 I tipi in base al riferimento derivano dalla classe MarshalByRefObject, come nell'esempio seguente:  
  
```  
public class RemotingCustomerReference : MarshalByRefObject  
{  
    public string FirstName { get; set; }  
    public string LastName { get; set; }  
    public int CustomerId { get; set; }  
}  
```  
  
 È estremamente importante comprendere le implicazioni degli oggetti in base al riferimento di Servizi remoti .NET.  Se un livello \(client o server\) invia un oggetto in base al riferimento all'altro livello, tutte le chiamate di metodi vengono eseguite nel livello proprietario dell'oggetto.  Ad esempio, un client che esegue la chiamata di metodi su un oggetto in base al riferimento restituito dal server eseguirà il codice sul server.  Analogamente, un server che esegue la chiamata di metodi su un oggetto in base al riferimento fornito dal client eseguirà il codice sul client.  Per questo motivo, l'uso di Servizi remoti .NET è consigliabile solo all'interno di ambienti completamente attendibili.  L'esposizione di un endpoint Servizi remoti .NET pubblico a client non attendibili renderà vulnerabile agli attacchi un server Servizi remoti .NET.  
  
#### Serializzazione in WCF  
 WCF supporta solo la serializzazione in base al valore.  Il modo più comune per definire un tipo per lo scambio tra client e server è simile a quello riportato nell'esempio seguente:  
  
```  
[DataContract]  
public class WCFCustomer  
{  
    [DataMember]  
    public string FirstName { get; set; }  
  
    [DataMember]  
    public string LastName { get; set; }  
  
    [DataMember]  
    public int CustomerId { get; set; }  
}  
```  
  
 L'attributo \[DataContract\] identifica questo tipo come serializzabile e deserializzabile tra client e server.  L'attributo \[DataMember\] identifica le singole proprietà o i singoli campi da serializzare.  
  
 Quando WCF invia un oggetto tra i livelli, serializza solo i valori e crea una nuova istanza dell'oggetto nell'altro livello.  Tutte le interazioni con i valori dell'oggetto avvengono solo in locale: non comunicano con l'altro livello come nel caso degli oggetti in base al riferimento di Servizi remoti .NET.  Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Serializzazione e deserializzazione](../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)  
  
-   [Serializzazione in Windows Communication Foundation](http://msdn.microsoft.com/magazine/cc163569.aspx)  
  
<a name="Exception_Handling"></a>   
### Funzionalità di gestione delle eccezioni  
  
#### Eccezioni in Servizi remoti .NET  
 Le eccezioni generate da un server Servizi remoti .NET vengono serializzate, inviate al client e generate in locale sul client come qualsiasi altra eccezione.  È possibile creare eccezioni personalizzate assegnando una sottoclasse al tipo Exception e contrassegnandolo con \[Serializable\].  La maggior parte delle eccezioni del framework sono già contrassegnate in questo modo, pertanto possono essere generate dal server, serializzate e generate nuovamente sul client.  Benché questa progettazione sia utile in fase di sviluppo, è possibile che informazioni sul lato server vengano inavvertitamente rivelate al client.  Questo è uno dei diversi motivi per cui Servizi remoti .NET deve essere usato solo in ambienti completamente attendibili.  
  
#### Eccezioni ed errori in WCF  
 WCF non consente la restituzione di tipi di eccezione arbitrari dal server al client, poiché ciò potrebbe causare la divulgazione accidentale di informazioni.  Se un'operazione del servizio genera un'eccezione imprevista, questo determina la generazione di una FaultException generica sul client.  Tale eccezione non include informazioni sul motivo del problema o sulla posizione in cui si è verificato e per alcune applicazioni è sufficiente.  Le applicazioni che devono comunicare al client informazioni più dettagliate sugli errori possono eseguire questa operazione definendo un contratto di errore.  
  
 A tale scopo, creare innanzitutto un tipo \[DataContract\] per fornire le informazioni sull'errore.  
  
```  
[DataContract]  
public class CustomerServiceFault  
{  
    [DataMember]  
    public string ErrorMessage { get; set; }  
  
    [DataMember]  
    public int CustomerId {get;set;}  
}  
```  
  
 Specificare il contratto di errore da usare per ogni operazione del servizio.  
  
```  
[ServiceContract]  
public interface IWCFServer  
{  
    [OperationContract]  
    [FaultContract(typeof(CustomerServiceFault))]  
    Customer GetCustomer(int customerId);  
}  
```  
  
 Il server segnala le condizioni di errore generando una FaultException.  
  
```  
throw new FaultException<CustomerServiceFault>(  
    new CustomerServiceFault() {   
        CustomerId = customerId,   
        ErrorMessage = "Illegal customer Id"   
    });  
```  
  
 Ogni volta che il client effettua una richiesta al server, può intercettare gli errori come normali eccezioni.  
  
```  
try  
{  
    Customer customer = server.GetCustomer(-1);  
}  
catch (FaultException<CustomerServiceFault> fault)  
{  
    Console.WriteLine(String.Format("Fault received: {0}",  
    fault.Detail.ErrorMessage));  
}  
  
```  
  
 Per altre informazioni sui contratti di errore, vedere <xref:System.ServiceModel.FaultException>.  
  
<a name="Security_Considerations"></a>   
### Considerazioni sulla sicurezza  
  
#### Sicurezza in Servizi remoti .NET  
 Alcuni canali di Servizi remoti .NET supportano funzionalità di sicurezza quali l'autenticazione e la crittografia a livello di canale \(IPC e TCP\).  Il canale HTTP si basa su Internet Information Services \(IIS\) sia per l'autenticazione che per la crittografia.  Nonostante questo supporto, è necessario considerare Servizi remoti .NET un protocollo di comunicazione non sicuro e usarlo solo all'interno di ambienti completamente attendibili.  Non esporre mai un endpoint Servizi remoti .NET pubblico a Internet o a client non attendibili.  
  
#### Sicurezza in WCF  
 WCF è stato progettato tenendo conto della sicurezza, in parte per risolvere i tipi di vulnerabilità che sono presenti in Servizi remoti .NET.  WCF garantisce la sicurezza sia a livello di trasporto che di messaggi e offre numerose opzioni per l'autenticazione, l'autorizzazione, la crittografia e così via.  Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Sicurezza](../../../docs/framework/wcf/feature-details/security.md)  
  
-   [WCF Security Guidance](http://wcfsecurity.codeplex.com/)  
  
<a name="Migrating_Top"></a>   
## Migrazione a WCF  
  
<a name="Why_Migrate"></a>   
### Perché eseguire la migrazione da Servizi remoti .NET a WCF?  
  
-   **Servizi remoti .NET è un prodotto legacy.** Come descritto in [Servizi remoti .NET](http://msdn.microsoft.com/library/vstudio/72x4h507\(v=vs.100\).aspx), viene considerato un prodotto legacy e non è consigliato per le nuove attività di sviluppo.  Per le applicazioni nuove ed esistenti sono consigliati WCF o l'API Web ASP.NET.  
  
-   **WCF usa standard multipiattaforma.** WCF è stato progettato tenendo conto dell'interoperabilità tra le piattaforme e supporta numerosi standard di settore \(SOAP, WS\-Security, WS\-Trust e così via\).  Un servizio WCF può interagire con client in esecuzione in sistemi operativi diversi da Windows.  Servizi remoti .NET è stato progettato principalmente per gli ambienti in cui sia le applicazioni client che quelle server vengono eseguite tramite .NET Framework in un sistema operativo Windows.  
  
-   **WCF dispone di funzionalità di sicurezza incorporate.** WCF è stato progettato prestando particolare attenzione alla sicurezza e offre numerose opzioni per l'autenticazione, la sicurezza a livello di trasporto, la sicurezza a livello di messaggi e così via.  Servizi remoti .NET è stato progettato per semplificare l'interoperabilità tra le applicazioni, ma non per garantire la sicurezza in ambienti non attendibili.  WCF è stato progettato per l'uso sia in ambienti attendibili che non attendibili.  
  
<a name="Migration_Recommendations"></a>   
### Suggerimenti sulla migrazione  
 Di seguito sono riportate le procedure consigliate per la migrazione da Servizi remoti .NET a WCF:  
  
-   **Creare il contratto di servizio.** Definire i tipi di interfaccia di servizio e contrassegnarli con l'attributo \[ServiceContract\]. Contrassegnare tutti i metodi che i client saranno autorizzati a chiamare con \[OperationContract\].  
  
-   **Creare il contratto dati.** Definire i tipi di dati che verranno scambiati tra il server e il client e contrassegnarli con l'attributo \[DataContract\].  Contrassegnare tutti i campi e le proprietà che il client sarà autorizzato a usare con \[DataMember\].  
  
-   **Creare il contratto di errore \(facoltativo\).** Creare i tipi che verranno scambiati tra il server e il client quando si verificano errori.  Contrassegnare questi tipi con \[DataContract\] e \[DataMember\] per renderli serializzabili.  Contrassegnare inoltre con \[FaultContract\] tutte le operazioni di servizio contrassegnate con \[OperationContract\] per indicare quali errori possono restituire.  
  
-   **Configurare e ospitare il servizio.** Dopo aver creato il contratto di servizio, il passaggio successivo consiste nel configurare un'associazione per esporre il servizio in un endpoint.  Per altre informazioni, vedere [Endpoint: indirizzi, associazioni e contratti](../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md).  
  
 Una volta che è stata eseguita la migrazione a WCF di un'applicazione Servizi remoti .NET, è comunque importante rimuovere le dipendenze da Servizi remoti .NET.  Questo garantisce che eventuali vulnerabilità di Servizi remoti .NET vengano rimosse dall'applicazione.  Tali passaggi sono:  
  
-   **Interrompere l'uso di MarshalByRefObject.** Il tipo MarshalByRefObject esiste solo per Servizi remoti .NET e non viene usato da WCF.  Tutti i tipi di applicazioni che usano la sottoclasse MarshalByRefObject devono essere rimossi o modificati.  Il tipo MarshalByRefObject esiste solo per Servizi remoti .NET e non viene usato da WCF.  Tutti i tipi di applicazioni che usano la sottoclasse MarshalByRefObject devono essere rimossi o modificati.  
  
-   **Interrompere l'uso di \[Serializable\] e ISerializable.** L'attributo \[Serializable\] e l'interfaccia ISerializable erano originariamente concepiti per la serializzazione di tipi all'interno di ambienti attendibili e vengono usati da Servizi remoti .NET.  La serializzazione di WCF si basa sui tipi contrassegnati con \[DataContract\] e \[DataMember\].  I tipi di dati usati da un'applicazione devono essere modificati in modo da usare \[DataContract\] invece di ISerializable o \[Serializable\].  L'attributo \[Serializable\] e l'interfaccia ISerializable erano originariamente concepiti per la serializzazione di tipi all'interno di ambienti attendibili e vengono usati da Servizi remoti .NET.  La serializzazione di WCF si basa sui tipi contrassegnati con \[DataContract\] e \[DataMember\].  I tipi di dati usati da un'applicazione devono essere modificati in modo da usare \[DataContract\] invece di ISerializable o \[Serializable\].  
  
<a name="Migration_Scenarios"></a>   
### Scenari di migrazione  
 Verrà ora descritto come realizzare in WCF i seguenti scenari comuni di Servizi remoti .NET:  
  
1.  Il server restituisce al client un oggetto in base al valore  
  
2.  Il server restituisce al client un oggetto in base al riferimento  
  
3.  Il client invia al server un oggetto in base al valore  
  
> [!NOTE]
>  L'invio di un oggetto in base al riferimento dal client al server non è consentito in WCF.  
  
 Ai fini dei presenti scenari, si presuppone che le interfacce di base per Servizi remoti .NET siano analoghe a quelle illustrate nel seguente esempio.  L'implementazione di Servizi remoti .NET non è importante in questo caso, perché si vuole solo illustrare come usare WCF per implementare una funzionalità equivalente.  
  
```  
public class RemotingServer : MarshalByRefObject  
{  
    // Demonstrates server returning object by-value  
    public Customer GetCustomer(int customerId) {…}  
  
    // Demonstrates server returning object by-reference  
    public CustomerReference GetCustomerReference(int customerId) {…}  
  
    // Demonstrates client passing object to server by-value  
    public bool UpdateCustomer(Customer customer) {…}  
}  
  
```  
  
#### Scenario 1: il server restituisce un oggetto in base al valore  
 In questo scenario viene illustrato un server che restituisce al client un oggetto in base al valore.  Poiché WCF restituisce sempre gli oggetti dal server in base al valore, la procedura seguente descrive semplicemente come compilare un normale servizio WCF.  
  
1.  Per iniziare, definire un'interfaccia pubblica per il servizio WCF e contrassegnarla con l'attributo \[ServiceContract\].  Viene usato \[OperationContract\] per identificare i metodi sul lato server che verranno chiamati dal client.  
  
    ```  
    [ServiceContract]  
    public interface ICustomerService  
    {  
        [OperationContract]  
        Customer GetCustomer(int customerId);  
  
        [OperationContract]  
        bool UpdateCustomer(Customer customer);  
    }  
    ```  
  
2.  Il passaggio successivo consiste nel creare il contratto dati per questo servizio.  Tale operazione viene eseguita creando classi \(non interfacce\) contrassegnate con l'attributo \[DataContract\].  Le singole proprietà o i singoli campi che devono essere visibili sia per il client che per il server sono contrassegnati con \[DataMember\].  Se si vuole che i tipi derivati siano consentiti, è necessario usare l'attributo \[KnownType\] per identificarli.  Gli unici tipi di cui WCF consentirà la serializzazione o la deserializzazione per questo servizio sono quelli nell'interfaccia del servizio e questi "tipi noti".  Ogni tentativo di scambiare qualsiasi altro tipo non incluso in questo elenco verrà rifiutato.  
  
    ```  
    [DataContract]  
    [KnownType(typeof(PremiumCustomer))]  
    public class Customer  
    {  
        [DataMember]  
        public string FirstName { get; set; }  
  
        [DataMember]  
        public string LastName { get; set; }  
  
        [DataMember]  
        public int CustomerId { get; set; }  
    }  
  
    [DataContract]  
    public class PremiumCustomer : Customer   
    {  
        [DataMember]  
        public int AccountId { get; set; }  
    }  
    ```  
  
3.  È quindi necessario fornire l'implementazione per l'interfaccia del servizio.  
  
    ```  
    public class CustomerService : ICustomerService  
    {  
        public Customer GetCustomer(int customerId)  
        {  
            // read from database  
        }  
  
        public bool UpdateCustomer(Customer customer)  
        {  
            // write to database  
        }  
    }  
    ```  
  
4.  Per eseguire il servizio WCF, è necessario dichiarare un endpoint che esponga tale interfaccia del servizio in un URL specifico tramite un'associazione WCF specifica.  Questa operazione viene in genere eseguita aggiungendo le sezioni seguenti al file web.config del progetto server.  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name="Server.CustomerService">  
            <endpoint address="http://localhost:8083/CustomerService"  
                      binding="basicHttpBinding"  
                      contract="Shared.ICustomerService" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
5.  Il servizio WCF può quindi essere avviato con il codice seguente:  
  
    ```  
    ServiceHost customerServiceHost = new ServiceHost(typeof(CustomerService));  
        customerServiceHost.Open();  
    ```  
  
     Quando questo ServiceHost viene avviato, usa il file web.config per stabilire il contratto, l'associazione e l'endpoint appropriati.  Per altre informazioni sui file di configurazione, vedere [Configurazione dei servizi tramite file di configurazione](../../../docs/framework/wcf/configuring-services-using-configuration-files.md).  Questo tipo di avvio del server è noto come self\-hosting.  Per altre informazioni sulle altre opzioni di hosting dei servizi WCF, vedere [Servizi host](../../../docs/framework/wcf/hosting-services.md).  
  
6.  Il file app.config del progetto client deve dichiarare le informazioni di associazione corrispondenti per l'endpoint del servizio.  Il modo più semplice per eseguire questa operazione in Visual Studio consiste nell'usare il comando **Aggiungi riferimento al servizio**, che aggiorna automaticamente il file app.config.  In alternativa, è possibile apportare le stesse modifiche manualmente.  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint name="customerservice"  
                    address="http://localhost:8083/CustomerService"  
                    binding="basicHttpBinding"  
                    contract="Shared.ICustomerService"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     Per altre informazioni sull'uso di **Aggiungi riferimento al servizio**, vedere [How to: Add, Update, or Remove a Service Reference](../Topic/How%20to:%20Add,%20Update,%20or%20Remove%20a%20Service%20Reference.md).  
  
7.  A questo punto è possibile chiamare il servizio WCF dal client.  È possibile eseguire tale operazione creando una channel factory per il servizio, richiedendole un canale e chiamando direttamente il metodo desiderato su tale canale.  Ciò è possibile perché il canale implementa l'interfaccia del servizio e gestisce automaticamente la logica di richiesta\/risposta sottostante.  Il valore restituito dalla chiamata del metodo è la copia deserializzata della risposta del server.  
  
    ```  
    ChannelFactory<ICustomerService> factory =  
        new ChannelFactory<ICustomerService>("customerservice");  
    ICustomerService service = factory.CreateChannel();  
    Customer customer = service.GetCustomer(42);  
    Console.WriteLine(String.Format("  Customer {0} {1} received.",  
            customer.FirstName, customer.LastName));  
    ```  
  
 Gli oggetti restituiti da WCF dal server al client sono sempre in base al valore.  Gli oggetti sono copie deserializzate dei dati inviati dal server.  Il client può chiamare metodi su queste copie locali senza rischiare di richiamare codice server tramite callback.  
  
#### Scenario 2: il server restituisce un oggetto in base al riferimento  
 In questo scenario viene illustrato un server che fornisce al client un oggetto in base al riferimento.  In Servizi remoti .NET questa operazione viene gestita automaticamente per qualsiasi tipo derivato da MarshalByRefObject, che è serializzato in base al riferimento.  Un esempio di questo scenario consiste nel consentire a più client di disporre di oggetti con sessione indipendenti sul lato server.  Come accennato in precedenza, gli oggetti restituiti da un servizio WCF sono sempre in base al valore, pertanto non esiste un equivalente diretto di un oggetto in base al riferimento. Tuttavia, è possibile ottenere un risultato analogo a una semantica in base al riferimento usando un oggetto <xref:System.ServiceModel.EndpointAddress10>.  Questo è un oggetto serializzabile in base al valore che può essere usato dal client per ottenere un oggetto in base al riferimento con sessione sul server.  Ciò rende possibile lo scenario relativo a più client con oggetti con sessione indipendenti sul lato server.  
  
1.  Innanzitutto, è necessario definire un contratto di servizio WCF che corrisponde all'oggetto con sessione stesso.  
  
    ```  
    [ServiceContract(SessionMode = SessionMode.Allowed)]  
        public interface ISessionBoundObject  
        {  
            [OperationContract]  
            string GetCurrentValue();  
  
            [OperationContract]  
            void SetCurrentValue(string value);  
        }  
    ```  
  
    > [!TIP]
    >  Si noti che l'oggetto con sessione è contrassegnato con \[ServiceContract\], che lo rende una normale interfaccia del servizio WCF.  L'impostazione della proprietà SessionMode indica che sarà un servizio con sessione.  In WCF una sessione è un modo per correlare più messaggi inviati tra due endpoint.  Ciò significa che, una volta che un client ottiene una connessione al servizio, verrà stabilita una sessione tra il client e il server.  Il client userà una singola istanza univoca dell'oggetto sul lato server per tutte le proprie interazioni all'interno di questa singola sessione.  
  
2.  È quindi necessario fornire l'implementazione di questa interfaccia del servizio.  Denotandola con \[ServiceBehavior\] e impostando InstanceContextMode, è possibile indicare a WCF che si vuole usare un'istanza univoca di questo tipo per ciascuna sessione.  
  
    ```  
    [ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
        public class MySessionBoundObject : ISessionBoundObject  
        {  
            private string _value;  
  
            public string GetCurrentValue()  
            {  
                return _value;  
            }  
  
            public void SetCurrentValue(string val)  
            {  
                _value = val;  
            }  
  
        }  
    ```  
  
3.  A questo punto è necessario un modo per ottenere un'istanza di questo oggetto con sessione.  A tale scopo, è possibile creare un'altra interfaccia di servizio WCF che restituisce un oggetto EndpointAddress10.  Si tratta di una forma serializzabile di un endpoint che il client può usare per creare l'oggetto con sessione.  
  
    ```  
    [ServiceContract]  
        public interface ISessionBoundFactory  
        {  
            [OperationContract]  
            EndpointAddress10 GetInstanceAddress();  
        }  
    ```  
  
     È quindi possibile implementare il servizio WCF:  
  
    ```  
    public class SessionBoundFactory : ISessionBoundFactory  
        {  
            public static ChannelFactory<ISessionBoundObject> _factory =   
                new ChannelFactory<ISessionBoundObject>("sessionbound");  
  
            public SessionBoundFactory()  
            {  
            }  
  
            public EndpointAddress10 GetInstanceAddress()  
            {  
                IClientChannel channel = (IClientChannel)_factory.CreateChannel();  
                return EndpointAddress10.FromEndpointAddress(channel.RemoteAddress);  
            }  
        }  
    ```  
  
     Questa implementazione mantiene una channel factory singleton per creare oggetti con sessione.  Quando viene chiamato GetInstanceAddress\(\), questo crea un canale e un oggetto EndpointAddress10 che fa riferimento in modo efficace all'indirizzo remoto associato a questo canale.  EndpointAddress10 è semplicemente un tipo di dati che può essere restituito al client in base al valore.  
  
4.  È necessario modificare il file di configurazione del server eseguendo le due operazioni seguenti, come illustrato nell'esempio riportato di seguito:  
  
    1.  Dichiarare una sezione \<client\> che descrive l'endpoint per l'oggetto con sessione.  Questa operazione è necessaria perché il server opera anche come client in questa situazione.  
  
    2.  Dichiarare gli endpoint per la factory e l'oggetto con sessione.  Ciò è necessario per consentire al client di comunicare con gli endpoint del servizio per acquisire l'EndpointAddress10 e per creare il canale con sessione.  
  
    ```  
    <configuration>  
      <system.serviceModel>  
         <client>  
          <endpoint name="sessionbound"  
                    address="net.tcp://localhost:8081/SessionBoundObject"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundObject"/>  
        </client>  
  
        <services>  
          <service name="Server.CustomerService">  
            <endpoint address="http://localhost:8083/CustomerService"  
                      binding="basicHttpBinding"  
                      contract="Shared.ICustomerService" />  
          </service>  
          <service name="Server.MySessionBoundObject">  
            <endpoint address="net.tcp://localhost:8081/SessionBoundObject"  
                      binding="netTcpBinding"  
                      contract="Shared.ISessionBoundObject" />  
          </service>  
          <service name="Server.SessionBoundFactory">  
            <endpoint address="net.tcp://localhost:8081/SessionBoundFactory"  
                      binding="netTcpBinding"  
                      contract="Shared.ISessionBoundFactory" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     È quindi possibile avviare questi servizi:  
  
    ```  
    ServiceHost factoryHost = new ServiceHost(typeof(SessionBoundFactory));  
    factoryHost.Open();  
  
    ServiceHost sessionHost = new ServiceHost(typeof(MySessionBoundObject));  
    sessionHost.Open();  
    ```  
  
5.  Il client può essere configurato dichiarando questi stessi endpoint nel file app.config del progetto.  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint name="customerservice"  
                    address="http://localhost:8083/CustomerService"  
                    binding="basicHttpBinding"  
                    contract="Shared.ICustomerService"/>  
          <endpoint name="sessionbound"  
                    address="net.tcp://localhost:8081/SessionBoundObject"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundObject"/>  
          <endpoint name="factory"  
                    address="net.tcp://localhost:8081/SessionBoundFactory"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundFactory"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
6.  Per creare e usare questo oggetto con sessione, il client deve eseguire le operazioni seguenti:  
  
    1.  Creare un canale per il servizio ISessionBoundFactory.  
  
    2.  Usare tale canale per richiamare il servizio in modo da ottenere un EndpointAddress10.  
  
    3.  Usare l'EndpointAddress10 per creare un canale in modo da ottenere un oggetto con sessione.  
  
    4.  Interagire con l'oggetto con sessione per verificare che rimanga la stessa istanza fra diverse chiamate.  
  
    ```  
    ChannelFactory<ISessionBoundFactory> channelFactory =   
        new ChannelFactory<ISessionBoundFactory>("factory");  
    ISessionBoundFactory sessionFactory = channelFactory.CreateChannel();  
  
    EndpointAddress10 address1 = sessionFactory.GetInstanceAddress();  
    EndpointAddress10 address2 = sessionFactory.GetInstanceAddress();  
  
    ChannelFactory<ISessionBoundObject> sessionObjectFactory1 =   
        new ChannelFactory<ISessionBoundObject>(new NetTcpBinding(),   
                                                address1.ToEndpointAddress());  
    ChannelFactory<ISessionBoundObject> sessionObjectFactory2 =   
        new ChannelFactory<ISessionBoundObject>(new NetTcpBinding(),   
                                                address2.ToEndpointAddress());  
  
    ISessionBoundObject sessionInstance1 = sessionObjectFactory1.CreateChannel();  
    ISessionBoundObject sessionInstance2 = sessionObjectFactory2.CreateChannel();  
  
    sessionInstance1.SetCurrentValue("Hello");  
    sessionInstance2.SetCurrentValue("World");  
  
    if (sessionInstance1.GetCurrentValue() == "Hello" &&  
        sessionInstance2.GetCurrentValue() == "World")  
    {  
        Console.WriteLine("sessionful server object works as expected");  
    }  
    ```  
  
 WCF restituisce sempre oggetti in base al valore, ma è possibile supportare l'equivalente di una semantica in base al riferimento mediante l'uso di EndpointAddress10.  Ciò consente al client di richiedere un'istanza del servizio WCF con sessione, dopodiché può interagire con tale istanza come qualsiasi altro servizio WCF.  
  
#### Scenario 3: il client invia al server un'istanza in base al valore  
 In questo scenario viene illustrato un client che invia al server un'istanza di oggetto non primitiva in base al valore.  Poiché WCF invia solo oggetti in base al valore, in questo scenario viene illustrato il normale uso di WCF.  
  
1.  Usare lo stesso servizio WCF dello scenario 1.  
  
2.  Usare il client per creare un nuovo oggetto in base al valore \(Customer\), creare un canale per comunicare con il servizio ICustomerService e inviare l'oggetto a tale canale.  
  
    ```  
    ChannelFactory<ICustomerService> factory =  
        new ChannelFactory<ICustomerService>("customerservice");  
    ICustomerService service = factory.CreateChannel();  
    PremiumCustomer customer = new PremiumCustomer {   
    FirstName = "Bob",   
    LastName = "Jones",   
    CustomerId = 43,   
    AccountId = 99};  
    bool success = service.UpdateCustomer(customer);  
    Console.WriteLine(String.Format("  Server returned {0}.", success));  
    ```  
  
     L'oggetto Customer verrà serializzato e inviato al server, dove sarà deserializzato in una nuova copia di tale oggetto.  
  
    > [!NOTE]
    >  Questo codice illustra inoltre l'invio di un tipo derivato \(PremiumCustomer\).  L'interfaccia del servizio prevede un oggetto Customer, ma l'attributo \[KnownType\] nella classe Customer indicava che anche PremiumCustomer era consentito.  In WCF qualunque tentativo di serializzare o deserializzare qualsiasi altro tipo tramite questa interfaccia di servizio non riuscirà.  
  
 I normali scambi di dati in WCF sono in base al valore.  Ciò garantisce che la chiamata di metodi su uno di questi oggetti di dati venga eseguita solo in locale: non verrà richiamato codice su un altro livello.  Benché sia possibile ottenere un risultato simile alla restituzione di oggetti in base al riferimento *dal* server, non è possibile per un client passare *al* server un oggetto in base al riferimento.  Uno scenario che richiede una conversazione tra il client e il server può essere realizzato in WCF usando un servizio duplex.  Per altre informazioni, vedere [Servizi duplex](../../../docs/framework/wcf/feature-details/duplex-services.md).  
  
<a name="Summary"></a>   
## Riepilogo  
 Servizi remoti .NET è un framework di comunicazione destinato all'uso solo all'interno di ambienti completamente attendibili.  Si tratta di un prodotto legacy e supportato solo per la compatibilità con le versioni precedenti.  Non deve essere usato per creare nuove applicazioni.  Al contrario, WCF è stato progettato prestando particolare attenzione alla sicurezza ed è consigliato per le applicazioni nuove ed esistenti.  Microsoft consiglia di eseguire la migrazione delle applicazioni Servizi remoti .NET esistenti per l'uso di WCF o dell'API Web ASP.NET.