---
title: "Code di messaggi non recapitabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ff664f33-ad02-422c-9041-bab6d993f9cc
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# Code di messaggi non recapitabili
Questo esempio dimostra come gestire ed elaborare messaggi il cui recapito non è riuscito.  L'esempio è basato sull'esempio [Associazioni MSMQ transazionali](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md).  In questo esempio viene usata l'associazione `netMsmqBinding`.  Il servizio è un'applicazione console indipendente che consente di osservare il servizio che riceve messaggi in coda.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
> [!NOTE]
>  Questo esempio dimostra la coda di messaggi non recapitabili di ciascuna applicazione che è disponibile solo su [!INCLUDE[wv](../../../../includes/wv-md.md)].  L'esempio può essere modificato per usare le code a livello di sistema predefinite per MSMQ 3.0 su [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] e [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
 Nella comunicazione in coda, il client comunica al servizio usando una coda.  Più precisamente, il client invia messaggi a una coda.  Il servizio riceve messaggi dalla coda.  Di conseguenza, per comunicare mediante una coda il servizio e il client non devono essere in esecuzione contemporaneamente.  
  
 Poiché la comunicazione in coda può comportare una certa quantità di inattività, è possibile associare un valore di durata al messaggio per garantire che non venga recapitato all'applicazione se è stato superato il periodo.  Vi sono anche casi nei quali un'applicazione deve essere informata del mancato recapito di un messaggio.  In tutti di questi casi, quali la scadenza della durata del messaggio o il mancato recapito, il messaggio viene inserito in una coda di messaggi non recapitabili.  L'applicazione di invio può leggere quindi i messaggi nella coda di messaggi non recapitabili e adottare azioni correttive che vanno da nessuna azione alla correzione delle ragioni del mancato recapito e reinvio del messaggio.  
  
 La coda di messaggi non recapitabili nell'associazione `NetMsmqBinding` è espressa nelle proprietà seguenti:  
  
-   Proprietà <xref:System.ServiceModel.MsmqBindingBase.DeadLetterQueue%2A> per esprimere il tipo di coda di messaggi non recapitabili richiesta dal client.  L'enumerazione contiene i valori seguenti:  
  
-   `None`: non viene richiesta alcuna coda di messaggi non recapitabili dal client.  
  
-   `System`: viene usata la coda di messaggi non recapitabili di sistema per archiviare i messaggi non recapitati.  La coda di messaggi non recapitabili di sistema è condivisa da tutte le applicazioni in esecuzione nel computer.  
  
-   `Custom`: per archiviare i messaggi non recapitati viene usata una coda di messaggi non recapitabili personalizzata specificata usando la proprietà <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A>.  Questa funzionalità è disponibile solo in [!INCLUDE[wv](../../../../includes/wv-md.md)].  Viene usata quando l'applicazione deve usare la propria coda di messaggi non recapitabili invece di condividerla con altre applicazioni in esecuzione nello stesso computer.  
  
-   Proprietà <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A> per esprimere la coda specifica da usare come coda di messaggi non recapitabili.  Questa è disponibile solo in [!INCLUDE[wv](../../../../includes/wv-md.md)].  
  
 In questo esempio, il client invia un gruppo di messaggi al servizio dall'interno dell'ambito di una transazione e specifica un valore arbitrariamente basso per la "durata" di questi messaggi \(circa 2 secondi\).  Il client specifica anche una coda di messaggi non recapitabili personalizzata da usare per accodare i messaggi che sono scaduti.  
  
 L'applicazione client può leggere i messaggi nella coda di messaggi non recapitabili e ritentare l'invio del messaggio o correggere l'errore che ha causato l'inserimento del messaggio originale nella coda dei messaggi non recapitabili e inviare il messaggio.  Nell'esempio, il client visualizza un messaggio di errore.  
  
 Il contratto del servizio è `IOrderProcessor`, come mostrato nel codice di esempio seguente.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true)]  
    void SubmitPurchaseOrder(PurchaseOrder po);  
}  
  
```  
  
 Il codice del servizio nell'esempio è quello dell'[Associazioni MSMQ transazionali](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md).  
  
 La comunicazione con il servizio avviene all'interno dell'ambito di una transazione.  Il servizio legge messaggi dalla coda, esegue l'operazione e quindi visualizza i risultati dell'operazione.  L'applicazione crea anche una coda per i messaggi non recapitabili.  
  
```  
//The service contract is defined in generatedClient.cs, generated from the service by the svcutil tool.  
  
//Client implementation code.  
class Client  
{  
    static void Main()  
    {  
        // Get MSMQ queue name from app settings in configuration  
        string deadLetterQueueName = ConfigurationManager.AppSettings["deadLetterQueueName"];  
  
        // Create the transacted MSMQ queue for storing dead message if necessary.  
        if (!MessageQueue.Exists(deadLetterQueueName))  
            MessageQueue.Create(deadLetterQueueName, true);  
  
        // Create a proxy with given client endpoint configuration  
        OrderProcessorClient client = new OrderProcessorClient("OrderProcessorEndpoint");  
  
        // Create the purchase order  
        PurchaseOrder po = new PurchaseOrder();  
        po.CustomerId = "somecustomer.com";  
        po.PONumber = Guid.NewGuid().ToString();  
  
        PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();  
        lineItem1.ProductId = "Blue Widget";  
        lineItem1.Quantity = 54;  
        lineItem1.UnitCost = 29.99F;  
  
        PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();  
        lineItem2.ProductId = "Red Widget";  
        lineItem2.Quantity = 890;  
        lineItem2.UnitCost = 45.89F;  
  
        po.orderLineItems = new PurchaseOrderLineItem[2];  
        po.orderLineItems[0] = lineItem1;  
        po.orderLineItems[1] = lineItem2;  
  
        //Create a transaction scope.  
        using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
        {  
            // Make a queued call to submit the purchase order  
            client.SubmitPurchaseOrder(po);  
            // Complete the transaction.  
            scope.Complete();  
        }  
  
        client.Close();  
  
        Console.WriteLine();  
        Console.WriteLine("Press <ENTER> to terminate client.");  
        Console.ReadLine();  
    }  
}  
```  
  
 La configurazione del client specifica una durata breve per il raggiungimento del servizio da parte del messaggio.  Se il messaggio non può essere trasmesso entro la durata specificata, scade e viene spostato nella coda di messaggi non recapitabili.  
  
> [!NOTE]
>  Per il client è possibile recapitare il messaggio alla coda del servizio entro il periodo specificato.  Per garantire di vedere il servizio dei messaggi non recapitabili in azione, è necessario eseguire il client prima di avviare il servizio.  Il messaggio scade e viene recapitato al servizio messaggi non recapitabili.  
  
 L'applicazione deve definire quale coda usare per i messaggi non recapitabili.  Se non viene specificata alcuna coda, per accodare i messaggi non recapitabili viene usata la coda di messaggi non recapitabili relativi a transazioni a livello di sistema.  In questo esempio, l'applicazione client specifica la propria coda di messaggi non recapitabili.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <appSettings>  
    <!-- use appSetting to configure MSMQ Dead Letter queue name -->  
    <add key="deadLetterQueueName" value=".\private$\ServiceModelSamplesOrdersAppDLQ"/>  
  </appSettings>  
  
  <system.serviceModel>  
    <client>  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint name="OrderProcessorEndpoint"  
                address="net.msmq://localhost/private/ServiceModelSamplesDeadLetter"   
                binding="netMsmqBinding"   
                bindingConfiguration="PerAppDLQBinding"   
                contract="IOrderProcessor" />  
    </client>  
  
    <bindings>  
      <netMsmqBinding>  
        <binding name="PerAppDLQBinding"  
                 deadLetterQueue="Custom"  
                 customDeadLetterQueue="net.msmq://localhost/private/ServiceModelSamplesOrdersAppDLQ"   
                 timeToLive="00:00:02"/>  
      </netMsmqBinding>  
    </bindings>  
  </system.serviceModel>  
  
</configuration>  
  
```  
  
 Il servizio di messaggi non recapitabili legge i messaggi dalla coda di messaggi non recapitabili.  Il servizio messaggi non recapitabili implementa il contratto `IOrderProcessor`.  La relativa implementazione tuttavia non ha lo scopo di elaborare ordini.  Il servizio messaggi non recapitabili è un servizio client e non ha funzionalità per elaborare ordini.  
  
> [!NOTE]
>  La coda di messaggi non recapitabili è una coda client ed è locale per il gestore delle code client.  
  
 L'implementazione del servizio messaggi non recapitabili verifica la ragione del mancato recapito di un messaggio e adotta misure correttive.  La ragione di un errore di messaggio viene acquisita in due enumerazioni, <xref:System.ServiceModel.Channels.MsmqMessageProperty.DeliveryFailure%2A> e <xref:System.ServiceModel.Channels.MsmqMessageProperty.DeliveryStatus%2A>.  È possibile recuperare la <xref:System.ServiceModel.Channels.MsmqMessageProperty> dal <xref:System.ServiceModel.OperationContext> come illustrato nel codice di esempio seguente:  
  
```  
public void SubmitPurchaseOrder(PurchaseOrder po)  
{  
    Console.WriteLine("Submitting purchase order did not succed ", po);  
    MsmqMessageProperty mqProp =   
                  OperationContext.Current.IncomingMessageProperties[  
                  MsmqMessageProperty.Name] as MsmqMessageProperty;  
    Console.WriteLine("Message Delivery Status: {0} ",   
                                                mqProp.DeliveryStatus);  
    Console.WriteLine("Message Delivery Failure: {0}",   
                                               mqProp.DeliveryFailure);  
    Console.WriteLine();  
    ….  
}  
  
```  
  
 I messaggi nella coda di messaggi non recapitabili sono indirizzati al servizio che sta elaborando il messaggio.  Di conseguenza, quando il servizio messaggi non recapitabili legge messaggi dalla coda, il livello canale di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] trova la mancata corrispondenza negli endpoint e non distribuisce il messaggio.  In questo caso, il messaggio è indirizzato al servizio di elaborazione ordini ma viene ricevuto dal servizio messaggi non recapitabili.  Per ricevere un messaggio indirizzato a un altro endpoint, in `ServiceBehavior` viene specificato un filtro degli indirizzi con il quale confrontare qualsiasi indirizzo.  Questo è necessario per elaborare correttamente i messaggi che vengono letti dalla coda di messaggi non recapitabili.  
  
 In questo esempio, il servizio messaggi non recapitabili reinvia il messaggio se la ragione dell'errore è che il messaggio è scaduto.  Per tutte le altre ragioni, visualizza l'errore di recapito, come illustrato nel codice di esempio seguente:  
  
```  
// Service class that implements the service contract.  
// Added code to write output to the console window.  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.Single, ConcurrencyMode=ConcurrencyMode.Single, AddressFilterMode=AddressFilterMode.Any)]  
public class PurchaseOrderDLQService : IOrderProcessor  
{  
    OrderProcessorClient orderProcessorService;  
    public PurchaseOrderDLQService()  
    {  
        orderProcessorService = new OrderProcessorClient("OrderProcessorEndpoint");  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public void SubmitPurchaseOrder(PurchaseOrder po)  
    {  
        Console.WriteLine("Submitting purchase order did not succeed ", po);  
        MsmqMessageProperty mqProp = OperationContext.Current.IncomingMessageProperties[MsmqMessageProperty.Name] as MsmqMessageProperty;  
  
        Console.WriteLine("Message Delivery Status: {0} ", mqProp.DeliveryStatus);  
        Console.WriteLine("Message Delivery Failure: {0}", mqProp.DeliveryFailure);  
        Console.WriteLine();  
  
        // resend the message if timed out  
        if (mqProp.DeliveryFailure == DeliveryFailure.ReachQueueTimeout ||  
            mqProp.DeliveryFailure == DeliveryFailure.ReceiveTimeout)  
        {  
            // re-send  
            Console.WriteLine("Purchase order Time To Live expired");  
            Console.WriteLine("Trying to resend the message");  
  
            // reuse the same transaction used to read the message from dlq to enqueue the message to app. queue  
            orderProcessorService.SubmitPurchaseOrder(po);  
            Console.WriteLine("Purchase order resent");  
        }  
    }  
  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
        // Create a ServiceHost for the PurchaseOrderDLQService type.  
        using (ServiceHost serviceHost = new ServiceHost(typeof(PurchaseOrderDLQService)))  
        {  
            // Open the ServiceHostBase to create listeners and start listening for messages.  
            serviceHost.Open();  
  
            // The service can now be accessed.  
            Console.WriteLine("The dead letter service is ready.");  
            Console.WriteLine("Press <ENTER> to terminate service.");  
            Console.WriteLine();  
            Console.ReadLine();  
        }  
    }  
}   
```  
  
 Nell'esempio seguente viene illustrata la configurazione per un messaggio non recapitabile.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.PurchaseOrderDLQService">  
        <!-- Define NetMsmqEndpoint in this case, DLQ end point to read messages-->  
        <endpoint address="net.msmq://localhost/private/ServiceModelSamplesOrdersAppDLQ"  
                  binding="netMsmqBinding"  
                  bindingConfiguration="DefaultBinding"   
                  contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
      </service>  
    </services>  
  
    <client>  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint name="OrderProcessorEndpoint"  
                 address="net.msmq://localhost/private/ServiceModelSamplesDeadLetter"   
                 binding="netMsmqBinding"   
                 bindingConfiguration="SystemDLQBinding"   
                 contract="IOrderProcessor" />  
    </client>  
  
    <bindings>  
      <netMsmqBinding>  
        <binding name="DefaultBinding" />  
        <binding name="SystemDLQBinding"  
                 deadLetterQueue="System"/>  
      </netMsmqBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Nell'esempio, per visualizzare il funzionamento della coda di messaggi non recapitabili per ciascuna applicazione è necessario eseguire 3 file eseguibili: il client, il servizio e un servizio messaggi non recapitabili che legge dalla coda di messaggi non recapitabili di ciascuna applicazione e reinvia il messaggio al servizio.  Tutte sono applicazioni console con output in finestre di console.  
  
> [!NOTE]
>  Poiché viene usato l'accodamento, non è necessario che client e servizio siano in esecuzione contemporaneamente.  È possibile eseguire il client, arrestarlo e quindi avviare il servizio e riceve comunque i messaggi.  È necessario avviare il servizio e arrestarlo per consentire la creazione della coda.  
  
 Quando viene seguito, il client visualizza il messaggio.  
  
```  
Press <ENTER> to terminate client.  
```  
  
 Il client ha tentato di inviare il messaggio ma con un breve timeout, il messaggio è scaduto e ora si trova nella coda di messaggi non recapitabili di ciascuna applicazione.  
  
 Viene quindi eseguito il servizio messaggi non recapitabili che legge il messaggio, visualizza il codice di errore e reinvia il messaggio al servizio.  
  
```  
The dead letter service is ready.  
Press <ENTER> to terminate service.  
  
Submitting purchase order did not succeed  
Message Delivery Status: InDoubt  
Message Delivery Failure: ReachQueueTimeout  
  
Purchase order Time To Live expired  
Trying to resend the message  
Purchase order resent  
  
```  
  
 Il servizio viene avviato e quindi legge il messaggio reinviato e lo elabora.  
  
```  
  
The service is ready.  
Press <ENTER> to terminate service.  
  
Processing Purchase Order: 97897eff-f926-4057-a32b-af8fb11b9bf9  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Se il servizio viene eseguito prima, verificherà la presenza della coda.  Se la coda non è presente, il servizio ne creerà una.  È possibile eseguire il servizio prima per creare la coda oppure è possibile crearne una tramite il gestore code MSMQ.  Per creare una coda in Windows 2008, eseguire i passaggi riportati di seguito.  
  
    1.  Aprire Server Manager in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
    2.  Espandere la scheda **Funzionalità**.  
  
    3.  Fare clic con il pulsante destro del mouse su **Code private**, quindi scegliere **Nuova** **coda privata**.  
  
    4.  Selezionare la casella **Di transazione**.  
  
    5.  Immettere `ServiceModelSamplesTransacted` come nome della nuova coda.  
  
3.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio in una configurazione singola o tra più computer, modificare i nomi della coda in modo appropriato, sostituendo localhost con il nome completo del computer e seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### Per eseguire l'esempio in un computer appartenente a un gruppo di lavoro  
  
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
  
     Verificare che l'endpoint sia associato al binding impostando l'attributo `bindingConfiguration`.  
  
2.  Assicurarsi di modificare la configurazione in DeadLetterService, sul server e sul client prima che di eseguire l'esempio.  
  
    > [!NOTE]
    >  L'impostazione di `security mode` su `None` è equivalente all'impostazione di `MsmqAuthenticationMode`, `MsmqProtectionLevel` e della sicurezza `Message` su `None`.  
  
## Commenti  
 Per impostazione predefinita con il trasporto dell'associazione `netMsmqBinding` è abilitata la sicurezza.  Il tipo di sicurezza del trasporto è determinato da due proprietà, `MsmqAuthenticationMode` e `MsmqProtectionLevel`.  Per impostazione predefinita, la modalità di autenticazione è impostata su `Windows` e il livello di protezione è impostato su `Sign`.  Affinché MSMQ fornisca la funzionalità di autenticazione e firma, deve appartenere a un dominio.  Se si esegue questo esempio in un computer che non appartiene a un dominio, si riceve l'errore seguente: "Il certificato interno del servizio di accodamento messaggi non esiste".  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\DeadLetter`  
  
## Vedere anche