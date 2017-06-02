---
title: "Gestione dei messaggi non elaborabili in MSMQ 4,0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec8d59e3-9937-4391-bb8c-fdaaf2cbb73e
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Gestione dei messaggi non elaborabili in MSMQ 4,0
Questo esempio dimostra come eseguire la gestione dei messaggi non elaborabili in un servizio.  Questo esempio è basato sull'esempio [Associazioni MSMQ transazionali](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md).  In questo esempio viene usato l'oggetto `netMsmqBinding`.  Il servizio è un'applicazione console indipendente che consente di osservare il servizio che riceve messaggi in coda.  
  
 Nella comunicazione in coda, il client comunica al servizio usando una coda.  Più precisamente, il client invia messaggi a una coda.  Il servizio riceve messaggi dalla coda.  Di conseguenza, per comunicare mediante una coda il servizio e il client non devono essere in esecuzione contemporaneamente.  
  
 Un messaggio non elaborabile è un messaggio che viene letto ripetutamente da una coda quando il servizio che legge il messaggio è in grado di elaborarlo e quindi termina la transazione nella quale viene letto il messaggio.  In questi casi, il messaggio viene ritentato.  Teoricamente l'operazione può ripetersi all'infinito se c'è un problema con il messaggio.  Notare che questo può accadere solo quando si usano transazioni per leggere dalla coda e richiamare il funzionamento del servizio.  
  
 In base alla versione di MSMQ, NetMsmqBinding supporta dal rilevamento limitato fino a quello completo dei messaggi non elaborabili.  Dopo che il messaggio è stato rilevato come non elaborabile, è possibile gestirlo in alcuni modi.  Di nuovo, in base alla versione di MSMQ, NetMsmqBinding supporta dalla gestione limitata fino a quella completa dei messaggi non elaborabili.  
  
 Questo esempio illustra le funzioni dei messaggi non elaborabili limitate fornite nella piattaforma [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] e [!INCLUDE[wxp](../../../../includes/wxp-md.md)] e quelle complete fornite in [!INCLUDE[wv](../../../../includes/wv-md.md)].  In entrambi gli esempi, l'obiettivo è spostare il messaggio non elaborabile in un'altra coda che quindi può essere gestita da un servizio messaggi non elaborabili.  
  
## Esempio di gestione dei messaggi non elaborabili di MSMQ v4.0  
 In [!INCLUDE[wv](../../../../includes/wv-md.md)], MSMQ fornisce una funzionalità di coda secondaria non elaborabile che può essere usata per archiviare i messaggi non elaborabili.  Questo esempio dimostra la procedura consigliata per gestire i messaggi non elaborabili usando [!INCLUDE[wv](../../../../includes/wv-md.md)].  
  
 Il rilevamento dei messaggi non elaborabili in [!INCLUDE[wv](../../../../includes/wv-md.md)] è piuttosto sofisticato.  Il rilevamento è agevolato da 3 proprietà.  <xref:System.ServiceModel.MsmqBindingBase.ReceiveRetryCount%2A> è il numero di volte che un determinato messaggio viene riletto dalla coda e inviato all'applicazione per l'elaborazione.  Un messaggio viene riletto dalla coda quando è inserito di nuovo nella coda perché non può essere inviato all'applicazione o l'applicazione esegue il rollback della transazione nell'operazione del servizio.  <xref:System.ServiceModel.MsmqBindingBase.MaxRetryCycles%2A> è il numero di volte che il messaggio viene spostato nella coda di tentativi.  Quando viene raggiunto <xref:System.ServiceModel.MsmqBindingBase.ReceiveRetryCount%2A>, il messaggio viene spostato nella coda di tentativi.  La proprietà <xref:System.ServiceModel.MsmqBindingBase.RetryCycleDelay%2A> è l'intervallo di tempo dopo il quale il messaggio viene spostato dalla coda di tentativi alla coda principale.  <xref:System.ServiceModel.MsmqBindingBase.ReceiveRetryCount%2A> viene reimpostato su 0.  Viene eseguito un nuovo tentativo per il messaggio.  Se tutti i tentativi di leggere il messaggio non sono riusciti, il messaggio è contrassegnato come non elaborabile.  
  
 Una volta il messaggio è contrassegnato come non elaborabile, viene gestito in base alle impostazioni nell'enumerazione <xref:System.ServiceModel.MsmqBindingBase.ReceiveErrorHandling%2A>.  Per reiterare i valori possibili:  
  
-   Fault \(impostazione predefinita\): per determinare l'errore del listener e anche dell'host del servizio.  
  
-   Drop: per rilasciare il messaggio.  
  
-   Move: per spostare il messaggio nella coda secondaria di messaggi non elaborabili.  Questo valore è disponibile solo in [!INCLUDE[wv](../../../../includes/wv-md.md)].  
  
-   Reject: per rifiutare il messaggio, rispedendolo alla coda di messaggi non recapitabili del mittente.  Questo valore è disponibile solo in [!INCLUDE[wv](../../../../includes/wv-md.md)].  
  
 Nell'esempio viene mostrato l'uso della disposizione `Move` per il messaggio non elaborabile.  `Move` determina lo spostamento del messaggio nella coda secondaria non elaborabile.  
  
 Il contratto di servizio è `IOrderProcessor`che definisce un servizio unidirezionale adatto per l'uso con le code.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true)]  
    void SubmitPurchaseOrder(PurchaseOrder po);  
}  
  
```  
  
 L'operazione del servizio visualizza un messaggio indicante che l'ordine è in fase di elaborazione.  Per dimostrare la funzionalità dei messaggi non elaborabili l'operazione del servizio `SubmitPurchaseOrder` genera un'eccezione per eseguire il rollback della transazione in una chiamata casuale del servizio.  Questo fa in modo che il messaggio venga rimesso nella coda.  Eventualmente il messaggio viene contrassegnato come non elaborabile.  La configurazione è impostata per spostare il messaggio non elaborabile nella coda secondaria non elaborabile.  
  
```  
  
// Service class that implements the service contract.  
// Added code to write output to the console window.  
public class OrderProcessorService : IOrderProcessor  
{  
    static Random r = new Random(137);  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public void SubmitPurchaseOrder(PurchaseOrder po)  
    {  
  
        int randomNumber = r.Next(10);  
  
        if (randomNumber % 2 == 0)  
        {  
            Orders.Add(po);  
            Console.WriteLine("Processing {0} ", po);  
        }  
        else  
        {  
            Console.WriteLine("Aborting transaction, cannot process purchase order: " + po.PONumber);  
            Console.WriteLine();  
            throw new Exception("Cannot process purchase order: " + po.PONumber);  
        }  
    }  
  
    public static void OnServiceFaulted(object sender, EventArgs e)   
    {  
        Console.WriteLine("Service Faulted");  
    }  
  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
        // Get MSMQ queue name from app settings in configuration.  
        string queueName = ConfigurationManager.AppSettings["queueName"];  
  
        // Create the transacted MSMQ queue if necessary.  
        if (!System.Messaging.MessageQueue.Exists(queueName))  
            System.Messaging.MessageQueue.Create(queueName, true);  
  
        // Get the base address that is used to listen for WS-MetaDataExchange requests.  
        // This is useful to generate a proxy for the client.  
        string baseAddress = ConfigurationManager.AppSettings["baseAddress"];  
  
        // Create a ServiceHost for the OrderProcessorService type.  
        ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService), new Uri(baseAddress));  
  
        // Hook on to the service host faulted events.  
        serviceHost.Faulted += new EventHandler(OnServiceFaulted);  
  
        // Open the ServiceHostBase to create listeners and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
  
        if(serviceHost.State != CommunicationState.Faulted) {  
            serviceHost.Close();  
        }  
  
    }  
}  
```  
  
 La configurazione del servizio comprende le seguenti proprietà dei messaggi non elaborabili: `receiveRetryCount`, `maxRetryCycles`, `retryCycleDelay` e `receiveErrorHandling` come è illustrato nel file di configurazione seguente.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <appSettings>  
    <!-- Use appSetting to configure MSMQ queue name. -->  
    <add key="queueName" value=".\private$\ServiceModelSamplesPoison" />  
    <add key="baseAddress" value="http://localhost:8000/orderProcessor/poisonSample"/>  
  </appSettings>  
  <system.serviceModel>  
    <services>  
      <service   
              name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
        <!-- Define NetMsmqEndpoint -->  
        <endpoint address="net.msmq://localhost/private/ServiceModelSamplesPoison"  
                  binding="netMsmqBinding"  
                  bindingConfiguration="PoisonBinding"   
                  contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
      </service>  
    </services>  
  
    <bindings>  
      <netMsmqBinding>  
        <binding name="PoisonBinding"   
                 receiveRetryCount="0"  
                 maxRetryCycles="1"  
                 retryCycleDelay="00:00:05"                        
                 receiveErrorHandling="Move">  
        </binding>  
      </netMsmqBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
```  
  
## Elaborazione dei messaggi dalla coda di messaggi non elaborabili  
 Il servizio messaggi non elaborabili legge i messaggi dalla coda finale di messaggi non elaborabili e li elabora.  
  
 I messaggi nella coda di messaggi non elaborabili sono indirizzati al servizio che sta elaborando il messaggio, il quale può essere diverso dall'endpoint del servizio messaggi non elaborabili.  Pertanto, quando il servizio messaggi non elaborabili legge messaggi dalla coda, il livello del canale di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trova la mancata corrispondenza negli endpoint e non invia il messaggio.  In questo caso, il messaggio è indirizzato al servizio di elaborazione ordini ma viene ricevuto dal servizio messaggi non elaborabili.  Per continuare a ricevere il messaggio anche se è indirizzato a un endpoint diverso, è necessario aggiungere un `ServiceBehavior` per filtrare gli indirizzi nei quali il criterio di corrispondenza è qualsiasi endpoint del servizio al quale il messaggio è indirizzato.  Questo è necessario per elaborare correttamente i messaggi che vengono letti dalla coda di messaggi non elaborabili.  
  
 L'implementazione stessa del servizio messaggi non elaborabili è molto simile all'implementazione del servizio.  Implementa il contratto ed elabora gli ordini.  Di seguito è riportato l'esempio di codice completo:  
  
```  
// Service class that implements the service contract.  
// Added code to write output to the console window.  
[ServiceBehavior(AddressFilterMode=AddressFilterMode.Any)]  
public class OrderProcessorService : IOrderProcessor  
{  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public void SubmitPurchaseOrder(PurchaseOrder po)  
    {  
        Orders.Add(po);  
        Console.WriteLine("Processing {0} ", po);  
    }  
  
    public static void OnServiceFaulted(object sender, EventArgs e)   
    {  
        Console.WriteLine("Service Faulted...exiting app");  
        Environment.Exit(1);  
    }  
  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
  
        // Create a ServiceHost for the OrderProcessorService type.  
        ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService));  
  
        // Hook on to the service host faulted events.  
        serviceHost.Faulted += new EventHandler(OnServiceFaulted);  
  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The poison message service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
  
        // Close the ServiceHostBase to shutdown the service.  
        if(serviceHost.State != CommunicationState.Faulted)  
        {  
            serviceHost.Close();  
        }  
    }  
  
```  
  
 Diversamente dal servizio di elaborazione ordini che legge i messaggi dalla coda degli ordini, il servizio messaggi non elaborabili legge i messaggi dalla coda secondaria non elaborabile.  La coda non elaborabile è una coda secondaria della coda principale, denominata "non elaborabile" ed è generata automaticamente da MSMQ.  Per accedervi, fornire il nome della coda principale seguito da un "," e il nome della coda secondaria, in questo caso \-"poison", come illustrato nella configurazione di esempio seguente.  
  
> [!NOTE]
>  Nell'esempio per MSMQ v3.0, il nome della coda non elaborabile non è una coda secondaria, ma la coda nella quale viene spostato il messaggio.  
  
```  
  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
        <!-- Define NetMsmqEndpoint -->  
        <endpoint address="net.msmq://localhost/private/ServiceModelSamplesPoison;poison"  
                  binding="netMsmqBinding"  
                  contract="Microsoft.ServiceModel.Samples.IOrderProcessor" >  
        </endpoint>  
      </service>  
    </services>  
  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Quando si esegue l'esempio, le attività del client, del servizio e del servizio messaggi non elaborabili vengono visualizzate nelle finestre della console.  È possibile osservare il servizio che riceve i messaggi dal client.  Premere INVIO in ciascuna finestra della console per arrestare i servizi.  
  
 Il servizio avvia l'esecuzione, elaborando gli ordini e in modo casuale inizia a terminare l'elaborazione.  Se il messaggio indica che ha elaborato l'ordine, è possibile eseguire di nuovo il client per inviare un altro messaggio finché non si nota che il servizio ha effettivamente terminato un messaggio.  In base alle impostazioni dei messaggi non elaborabili configurate, l'elaborazione del messaggio viene tentata una volta prima che questo venga rimosso dalla coda finale non elaborabile.  
  
```  
  
The service is ready.  
Press <ENTER> to terminate service.  
  
Processing Purchase Order: 0f063b71-93e0-42a1-aa3b-bca6c7a89546  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
Processing Purchase Order: 5ef9a4fa-5a30-4175-b455-2fb1396095fa  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
Aborting transaction, cannot process purchase order: 23e0b991-fbf9-4438-a0e2-20adf93a4f89  
```  
  
 Avviare il servizio messaggi non elaborabili per leggere il messaggio non elaborabile dalla coda non elaborabile.  In questo esempio, il servizio messaggi non elaborabili legge il messaggio e lo elabora.  È possibile osservare che l'ordine di acquisto terminato e impostato come non elaborabile viene letto dal servizio messaggi non elaborabili.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Processing Purchase Order: 23e0b991-fbf9-4438-a0e2-20adf93a4f89  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Se il servizio viene eseguito prima, verificherà la presenza della coda.  Se la coda non è presente, il servizio ne creerà una.  È possibile eseguire il servizio prima per creare la coda oppure è possibile crearne una tramite il gestore code MSMQ.  Per creare una coda in Windows 2008, eseguire i passaggi riportati di seguito.  
  
    1.  Aprire Server Manager in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
    2.  Espandere la scheda **Funzionalità**.  
  
    3.  Fare clic con il pulsante destro del mouse su **Code private**, quindi scegliere **Nuova** **coda privata**.  
  
    4.  Selezionare la casella **Di transazione**.  
  
    5.  Immettere `ServiceModelSamplesTransacted` come nome della nuova coda.  
  
3.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio in una configurazione singola o tra più computer, modificare i nomi della coda per riflettere il nome host effettivo anziché localhost e seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
 Per impostazione predefinita con il trasporto dell'associazione `netMsmqBinding` è abilitata la sicurezza.  Il tipo di sicurezza del trasporto è determinato da due proprietà, `MsmqAuthenticationMode` e `MsmqProtectionLevel`.  Per impostazione predefinita, la modalità di autenticazione è impostata su `Windows` e il livello di protezione è impostato su `Sign`.  Affinché MSMQ fornisca la funzionalità di autenticazione e firma, deve appartenere a un dominio.  Se si esegue questo esempio in un computer che non appartiene a un dominio, si riceve l'errore seguente: "Il certificato interno del servizio di accodamento messaggi non esiste".  
  
#### Per eseguire l'esempio in un computer appartenente a un gruppo di lavoro  
  
1.  Se il computer non appartiene a un dominio, disattivare la sicurezza del trasporto impostando la modalità di autenticazione e livello di protezione su `None` come illustrato nella configurazione di esempio seguente:  
  
    ```  
    <bindings>  
        <netMsmqBinding>  
            <binding name="TransactedBinding">  
                <security mode="None"/>  
            </binding>  
        </netMsmqBinding>  
    </bindings>  
    ```  
  
     Verificare che l'endpoint sia associato al binding impostando l'attributo bindingConfiguration dell'endpoint.  
  
2.  Assicurarsi di modificare la configurazione in PoisonMessageServer, sul server e sul client prima che di eseguire l'esempio.  
  
    > [!NOTE]
    >  L'impostazione di `security mode` su `None` è equivalente all'impostazione di `MsmqAuthenticationMode`, `MsmqProtectionLevel` e della sicurezza `Message` su `None`.  
  
3.  Affinché Metadata Exchange funzioni, registriamo un URL con associazione HTTP.  Ciò richiede che il servizio venga eseguito in una finestra di comando elevata.  In caso contrario, si ottiene un'eccezione quale: Eccezione non gestita: System.ServiceModel.AddressAccessDeniedException: HTTP non ha potuto registrare l'URL http:\/\/\+:8000\/ServiceModelSamples\/service\/.  Il processo non dispone dei diritti di accesso su questo spazio dei nomi \(vedere http:\/\/go.microsoft.com\/fwlink\/?LinkId\=70353 per dettagli\).  \-\-\-\> System.Net.HttpListenerException: Accesso negato.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Poison\MSMQ4`  
  
## Vedere anche