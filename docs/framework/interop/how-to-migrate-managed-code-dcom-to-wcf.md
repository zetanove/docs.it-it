---
title: "Procedura: Eseguire la migrazione di codice gestito da DCOM a WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 52961ffc-d1c7-4f83-832c-786444b951ba
caps.latest.revision: 6
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: Eseguire la migrazione di codice gestito da DCOM a WCF
Windows Communication Foundation \(WCF\) è la scelta migliore e più sicura su Distributed Component Object Model \(DCOM\) per le chiamate di codice gestito tra i server e i client in un ambiente distribuito.  Questo articolo mostra come eseguire la migrazione del codice da DCOM a WCF per gli scenari seguenti.  
  
-   Il servizio remoto restituisce al client un oggetto in base al valore  
  
-   Il client invia al servizio remoto un oggetto in base al valore  
  
-   Il servizio remoto restituisce al client un oggetto in base al riferimento  
  
 Per motivi di sicurezza, l'invio di un oggetto in base al riferimento dal client al servizio non è consentito in WCF.  Uno scenario che richiede una conversazione tra il client e il server può essere realizzato in WCF usando un servizio duplex.  Per altre informazioni sui servizi duplex, vedere [Servizi duplex](../../../docs/framework/wcf/feature-details/duplex-services.md).  
  
 Per altri dettagli sulla creazione di servizi e client WCF per tali servizi, vedere [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md), [Progettazione e implementazione di servizi](../../../docs/framework/wcf/designing-and-implementing-services.md) e [Creazione di client](../../../docs/framework/wcf/building-clients.md).  
  
## Codice di esempio DCOM  
 Per questi scenari, le interfacce DCOM illustrate che usano WCF hanno la seguente struttura:  
  
```  
[ComVisible(true)]  
[Guid("AA9C4CDB-55EA-4413-90D2-843F1A49E6E6")]  
public interface IRemoteService  
{  
   Customer GetObjectByValue();  
   IRemoteObject GetObjectByReference();  
   void SendObjectByValue(Customer customer);  
}  
  
[ComVisible(true)]  
[Guid("A12C98DE-B6A1-463D-8C24-81E4BBC4351B")]  
public interface IRemoteObject  
{  
}  
  
public class Customer  
{  
}  
  
```  
  
## Il servizio restituisce un oggetto in base al valore  
 Per questo scenario, si effettua una chiamata a un servizio e il metodo restituisce un oggetto, che viene passato in base al valore dal server al client.  Questo scenario rappresenta la chiamata COM seguente:  
  
```  
public interface IRemoteService  
{  
    Customer GetObjectByValue();  
}  
```  
  
 In questo scenario, il client riceve una copia deserializzata di un oggetto dal servizio remoto.  Il client può interagire con questa copia locale senza chiamare nuovamente il servizio.  In altre parole, al client viene garantito che il servizio non verrà coinvolto in alcun modo quando verranno chiamati metodi sulla copia locale.  Poiché WCF restituisce sempre gli oggetti dal servizio in base al valore, la procedura seguente descrive come creare un normale servizio WCF.  
  
### Passaggio 1: Definire l'interfaccia del servizio WCF  
 Definire un'interfaccia pubblica per il servizio WCF e contrassegnarla con l'attributo \[<xref:System.ServiceModel.ServiceContractAttribute>\].  Contrassegnare i metodi che si desidera esporre ai client con l'attributo \[<xref:System.ServiceModel.OperationContractAttribute>\].  L'esempio seguente mostra l'uso di questi attributi per identificare l'interfaccia lato server e i metodi dell'interfaccia che possono essere chiamati da un client.  Il metodo usato per questo scenario viene visualizzato in grassetto.  
  
```  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Web;   
. . .  
[ServiceContract]  
public interface ICustomerManager  
{  
    [OperationContract]  
    void StoreCustomer(Customer customer);  
  
    [OperationContract]     
    Customer GetCustomer(string firstName, string lastName);   
  
}  
  
```  
  
### Passaggio 2: Definire il contratto dati  
 Successivamente, creare un contratto dati per il servizio, che descriverà come verranno scambiati i dati tra il servizio e i client.  Le classi descritte nel contratto dati devono essere contrassegnate con l'attributo \[<xref:System.Runtime.Serialization.DataContractAttribute>\].  Le singole proprietà o campi che devono essere visibili sia al client che al server devono essere contrassegnati con l'attributo \[<xref:System.Runtime.Serialization.DataMemberAttribute>\]. Per consentire i tipi derivati da una classe nel contratto dati, è necessario identificarli con l'attributo \[<xref:System.Runtime.Serialization.KnownTypeAttribute>\].  WCF serializzerà o deserializzerà solo i tipi nell'interfaccia del servizio e i tipi identificati come tipi noti.  Se si tenta di usare un tipo diverso da un tipo noto, si verificherà un'eccezione.  
  
 Per altre informazioni sui contratti dati, vedere [Contratti dati](../../../docs/framework/wcf/samples/data-contracts.md).  
  
```  
[DataContract]  
[KnownType(typeof(PremiumCustomer))]  
public class Customer  
{  
    [DataMember]  
    public string Firstname;  
    [DataMember]  
    public string Lastname;  
    [DataMember]  
    public Address DefaultDeliveryAddress;  
    [DataMember]  
    public Address DefaultBillingAddress;  
}  
 [DataContract]  
public class PremiumCustomer : Customer  
{  
    [DataMember]  
    public int AccountID;  
}  
  
 [DataContract]  
public class Address  
{  
    [DataMember]  
    public string Street;  
    [DataMember]  
    public string Zipcode;  
    [DataMember]  
    public string City;  
    [DataMember]  
    public string State;  
    [DataMember]  
    public string Country;  
}  
  
```  
  
### Passaggio 3: Implementare il servizio WCF  
 Successivamente, implementare la classe del servizio WCF, che implementa l'interfaccia definita nel passaggio precedente.  
  
```  
public class CustomerService: ICustomerManager    
{  
    public void StoreCustomer(Customer customer)  
    {  
        // write to a database  
    }  
    public Customer GetCustomer(string firstName, string lastName)  
    {  
        // read from a database  
    }  
}  
```  
  
### Passaggio 4: Configurare il servizio e il client  
 Per eseguire un servizio WCF, è necessario dichiarare un endpoint che esponga tale interfaccia del servizio in un URL specifico tramite un binding WCF specifico.  Un binding specifica i dettagli di trasporto, codifica e protocollo che permettono ai client e al server di comunicare.  In genere i binding si aggiungono ai file di configurazione del progetto del servizio \(web.config\).  Di seguito viene illustrata una voce di binding per il servizio di esempio:  
  
```  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Server.CustomerService">  
        <endpoint address="http://localhost:8083/CustomerManager"   
                  binding="basicHttpBinding"  
                  contract="Shared.ICustomerManager" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Successivamente, configurare il client in base alle informazioni di binding specificate dal servizio.  A tale scopo, aggiungere quanto segue al file di configurazione dell'applicazione \(app.config\) del client.  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="customermanager"   
                address="http://localhost:8083/CustomerManager"   
                binding="basicHttpBinding"   
                contract="Shared.ICustomerManager"/>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### Passaggio 5: Eseguire il servizio  
 Infine, è possibile ospitarlo in modo indipendente in un'applicazione console aggiungendo le righe seguenti all'app di servizio e avviando l'app.  Per altre informazioni su altri modi per ospitare un'applicazione di servizio WCF, vedere [Servizi host](../../../docs/framework/wcf/hosting-services.md).  
  
```  
ServiceHost customerServiceHost = new ServiceHost(typeof(CustomerService));  
customerServiceHost.Open();  
  
```  
  
### Passaggio 6: Chiamare il servizio dal client  
 Per chiamare il servizio dal client, è necessario creare una channel factory per il servizio e richiedere un canale che consentirà di chiamare il metodo `GetCustomer` direttamente dal client.  Il canale implementa l'interfaccia del servizio e gestisce automaticamente la logica di richiesta\/risposta sottostante.  Il valore restituito dalla chiamata del metodo è la copia deserializzata della risposta del servizio.  
  
```  
ChannelFactory<ICustomerManager> factory =   
     new ChannelFactory<ICustomerManager>("customermanager");  
ICustomerManager service = factory.CreateChannel();  
Customer customer = service.GetCustomer("Mary", "Smith");  
  
```  
  
## Il client invia al server un oggetto in base al valore  
 In questo scenario, il client invia un oggetto al server, in base al valore,  vale a dire che il server riceverà una copia deserializzata dell'oggetto.  Il server può chiamare i metodi su tale copia con la garanzia che non venga eseguito alcun callback nel codice client.  Come accennato in precedenza, i normali scambi di dati in WCF sono in base al valore.  Ciò garantisce che la chiamata di metodi su uno di questi oggetti venga eseguita solo in locale: non verrà richiamato codice sul client.  
  
 Questo scenario rappresenta la chiamata al metodo COM seguente:  
  
```  
public interface IRemoteService  
{  
    void SendObjectByValue(Customer customer);  
}  
  
```  
  
 Questo scenario usa lo stesso contratto dati e la stessa interfaccia di servizio del primo esempio.  Anche i client e il servizio verranno configurati nello stesso modo.  In questo esempio, viene creato un canale per inviare l'oggetto ed eseguirlo nello stesso modo.  Per questo esempio, tuttavia, si creerà un client che chiama il servizio, passando un oggetto in base al valore.  Il metodo di servizio che verrà chiamato dal client nel contratto di servizio viene visualizzato in grassetto:  
  
```  
[ServiceContract]  
public interface ICustomerManager  
{  
    [OperationContract]  
        void StoreCustomer(Customer customer);  
  
    [OperationContract]  
    Customer GetCustomer(string firstName, string lastName);  
}  
  
```  
  
### Aggiungere il codice al client che invia un oggetto in base al valore  
 Il codice seguente mostra come il client crea un nuovo oggetto Customer in base al valore, crea un canale per comunicare con il servizio `ICustomerManager` e gli invia l'oggetto Customer.  
  
 L'oggetto Customer verrà serializzato e inviato al servizio, dove sarà deserializzato dal servizio in una nuova copia di tale oggetto.  I metodi chiamati dal servizio su questo oggetto verranno eseguiti solo localmente nel server. È importante notare che questo codice illustra l'invio di un tipo derivato \(`PremiumCustomer`\).  Per il contratto di servizio è previsto un oggetto `Customer`, ma il contratto dati di servizio usa l'attributo \[<xref:System.Runtime.Serialization.KnownTypeAttribute>\] per indicare che è consentito anche `PremiumCustomer`.  In WCF i tentativi di serializzare o deserializzare qualsiasi altro tipo tramite questa interfaccia di servizio avranno esito negativo.  
  
```  
PremiumCustomer customer = new PremiumCustomer();  
customer.Firstname = "John";  
customer.Lastname = "Doe";  
customer.DefaultBillingAddress = new Address();  
customer.DefaultBillingAddress.Street = "One Microsoft Way";  
customer.DefaultDeliveryAddress = customer.DefaultBillingAddress;  
customer.AccountID = 42;  
  
ChannelFactory<ICustomerManager> factory =  
   new ChannelFactory<ICustomerManager>("customermanager");  
ICustomerManager customerManager = factory.CreateChannel();  
customerManager.StoreCustomer(customer);  
```  
  
## Il servizio restituisce un oggetto in base al riferimento  
 Per questo scenario, l'app client effettua una chiamata al servizio remoto e il metodo restituisce un oggetto, che viene passato in base al riferimento dal servizio al client.  
  
 Come accennato in precedenza, i servizi WCF restituiscono sempre un oggetto in base al valore.  Tuttavia, è possibile ottenere un risultato simile usando la classe <xref:System.ServiceModel.EndpointAddress10>.  <xref:System.ServiceModel.EndpointAddress10> è un oggetto serializzabile in base al valore che può essere usato dal client per ottenere un oggetto in base al riferimento con sessione sul server.  
  
 Il comportamento dell'oggetto in base al riferimento in WCF illustrato in questo scenario è diverso da quello in DCOM.  In DCOM, il server può restituire direttamente al client un oggetto in base al riferimento e il client può chiamare i metodi dell'oggetto, che vengono eseguiti nel server.  In WCF, tuttavia, l'oggetto restituito è sempre in base al valore.  Il client deve accettare tale oggetto in base al valore, rappresentato da <xref:System.ServiceModel.EndpointAddress10>, e usarlo per creare il proprio oggetto in base al riferimento con sessione.  Le chiamate al metodo client sull'oggetto con sessione vengono eseguite sul server. In altre parole, questo oggetto in base al riferimento in WCF è un normale servizio WCF configurato con sessione.  
  
 In WCF una sessione è un modo per correlare più messaggi inviati tra due endpoint.  Ciò significa che, una volta che un client ottiene una connessione al servizio, verrà stabilita una sessione tra il client e il server.  Il client userà una singola istanza univoca dell'oggetto sul lato server per tutte le proprie interazioni all'interno di questa singola sessione.  I contratti WCF con sessione sono simili ai modelli di richiesta\/risposta di rete orientati alla connessione.  
  
 Questo scenario è rappresentato dal metodo DCOM seguente.  
  
```  
public interface IRemoteService  
{  
    IRemoteObject GetObjectByReference();  
}  
```  
  
### Passaggio 1: Definire l'interfaccia e l'implementazione del servizio WCF con sessione  
 Innanzitutto definire un'interfaccia del servizio WCF contenente l'oggetto con sessione.  
  
 In questo codice, l'oggetto con sessione è contrassegnato con l'attributo `ServiceContract`, che lo identifica come normale interfaccia del servizio WCF.  Inoltre, la proprietà <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> viene impostata in modo da indicare che sarà un servizio con sessione.  
  
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
  
 Nel codice seguente viene illustrata l'implementazione del servizio.  
  
 Il servizio viene contrassegnato con l'attributo \[ServiceBehavior\] e la proprietà InstanceContextMode viene impostata su InstanceContextMode.PerSessions per indicare che per ogni sessione deve essere creata un'istanza univoca di questo tipo.  
  
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
  
### Passaggio 2: Definire il servizio factory WCF per l'oggetto con sessione  
 Il servizio che crea l'oggetto con sessione deve essere definito e implementato.  A tale scopo, osservare il codice indicato di seguito.  Questo codice crea un altro servizio WCF che restituisce un oggetto <xref:System.ServiceModel.EndpointAddress10>.  Si tratta di una forma serializzabile di endpoint che può essere usata per creare l'oggetto con sessione.  
  
```  
[ServiceContract]  
    public interface ISessionBoundFactory  
    {  
        [OperationContract]  
        EndpointAddress10 GetInstanceAddress();  
    }  
  
```  
  
 Di seguito è riportata l'implementazione di questo servizio.  Questa implementazione mantiene una channel factory singleton per creare oggetti con sessione.  Quando viene chiamato `GetInstanceAddress`, questo crea un canale e un oggetto <xref:System.ServiceModel.EndpointAddress10> che fa riferimento all'indirizzo remoto associato a questo canale.  <xref:System.ServiceModel.EndpointAddress10> è un tipo di dati che può essere restituito al client in base al valore.  
  
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
  
### Passaggio 3: Configurare e avviare i servizi WCF  
 Per ospitare questi servizi, sarà necessario aggiungere quanto segue al file di configurazione del server \(Web.config\).  
  
1.  Aggiungere una sezione `<client>` che descrive l'endpoint per l'oggetto con sessione.  In questo scenario, il server funge anche da client e deve essere configurato per abilitare questa opzione.  
  
2.  Nella sezione `<services>` dichiarare gli endpoint di servizio per la factory e l'oggetto con sessione.  Ciò consente al client di comunicare con gli endpoint di servizio, di acquisire <xref:System.ServiceModel.EndpointAddress10> e di creare il canale con sessione.  
  
 Di seguito viene riportato un file di configurazione di esempio con queste impostazioni:  
  
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
  
 Aggiungere le seguenti righe a un'applicazione console, per ospitare il servizio in modo indipendente, e avviare l'app.  
  
```  
ServiceHost factoryHost = new ServiceHost(typeof(SessionBoundFactory));  
factoryHost.Open();  
  
ServiceHost sessionBoundServiceHost = new ServiceHost(  
typeof(MySessionBoundObject));  
sessionBoundServiceHost.Open();  
```  
  
### Passaggio 4: Configurare il client e chiamare il servizio  
 Configurare il client per comunicare con i servizi WCF, creando le seguenti voci nel file di configurazione dell'applicazione \(app.config\) del progetto.  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
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
  
 Per chiamare il servizio, aggiungere il codice al client per eseguire le operazioni seguenti:  
  
1.  Creare un canale per il servizio `ISessionBoundFactory`.  
  
2.  Usare il canale per richiamare il servizio `ISessionBoundFactory` e ottenere un oggetto <xref:System.ServiceModel.EndpointAddress10>.  
  
3.  Usare <xref:System.ServiceModel.EndpointAddress10> per creare un canale in modo da ottenere un oggetto con sessione.  
  
4.  Chiamare i metodi `SetCurrentValue` e `GetCurrentValue` per dimostrare che l'istanza dell'oggetto usata in più chiamate è sempre la stessa.  
  
```  
ChannelFactory<ISessionBoundFactory> factory =  
        new ChannelFactory<ISessionBoundFactory>("factory");  
  
ISessionBoundFactory sessionBoundFactory = factory.CreateChannel();  
  
EndpointAddress10 address = sessionBoundFactory.GetInstanceAddress();  
  
ChannelFactory<ISessionBoundObject> sessionBoundObjectFactory =  
    new ChannelFactory<ISessionBoundObject>(  
        new NetTcpBinding(),  
        address.ToEndpointAddress());  
  
ISessionBoundObject sessionBoundObject =  
        sessionBoundObjectFactory.CreateChannel();  
  
sessionBoundObject.SetCurrentValue("Hello");  
if (sessionBoundObject.GetCurrentValue() == "Hello")  
{  
    Console.WriteLine("Session-full instance management works as expected");  
}  
```  
  
## Vedere anche  
 [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Progettazione e implementazione di servizi](../../../docs/framework/wcf/designing-and-implementing-services.md)   
 [Creazione di client](../../../docs/framework/wcf/building-clients.md)   
 [Servizi duplex](../../../docs/framework/wcf/feature-details/duplex-services.md)