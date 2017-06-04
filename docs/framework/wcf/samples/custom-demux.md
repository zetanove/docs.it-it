---
title: "Demux personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc54065c-518e-4146-b24a-0fe00038bfa7
caps.latest.revision: 41
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 41
---
# Demux personalizzato
Questo esempio dimostra il mapping di intestazioni di messaggio MSMQ su diverse operazioni del servizio in modo che i servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che usano <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> non siano limitati all'uso di un'operazione del servizio come è dimostrato negli esempi [Accodamento messaggi in Windows Communication Foundation](../../../../docs/framework/wcf/samples/message-queuing-to-wcf.md) e [Da Windows Communication Foundation a Accodamento messaggi](../../../../docs/framework/wcf/samples/wcf-to-message-queuing.md).  
  
 Il servizio, in questo esempio è un'applicazione console indipendente che consente di osservare il servizio che riceve messaggi in coda.  
  
 Il contratto di servizio è `IOrderProcessor` e definisce un servizio unidirezionale adatto per l'uso con le code.  
  
```  
[ServiceContract]  
[KnownType(typeof(PurchaseOrder))]  
[KnownType(typeof(String))]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true, Name = "SubmitPurchaseOrder")]  
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);  
  
    [OperationContract(IsOneWay = true, Name = "CancelPurchaseOrder")]  
    void CancelPurchaseOrder(MsmqMessage<string> ponumber);  
}  
```  
  
 Un messaggio MSMQ non dispone di un'intestazione Action.  Non è possibile eseguire automaticamente il mapping di messaggi MSMQ diversi su contratti dell'operazione.  Pertanto, può essere presente un solo contratto dell'operazione.  Per superare questa limitazione il servizio implementa il metodo <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector.SelectOperation%2A> dell'interfaccia <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector>.  Il metodo <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector.SelectOperation%2A> consente al servizio di eseguire il mapping di una determinata intestazione del messaggio con una particolare operazione del servizio.  In questo esempio, l'intestazione dell'etichetta del messaggio è mappata sulle operazioni del servizio.  Il parametro `Name` del contratto dell'operazione determina quale operazione del servizio deve essere distribuita per una determinata etichetta del messaggio.  Ad esempio, se l'intestazione dell'etichetta del messaggio contiene "SubmitPurchaseOrder", viene richiamata l'operazione del servizio "SubmitPurchaseOrder".  
  
```  
public class OperationSelector : IDispatchOperationSelector  
{  
    public string SelectOperation(ref System.ServiceModel.Channels.Message message)  
    {  
        MsmqIntegrationMessageProperty property = MsmqIntegrationMessageProperty.Get(message);  
        return property.Label;  
    }  
}  
```  
  
 Il servizio deve implementare il metodo <xref:System.ServiceModel.Description.IContractBehavior.ApplyDispatchBehavior%28System.ServiceModel.Description.ContractDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%2CSystem.ServiceModel.Dispatcher.DispatchRuntime%29> dell'interfaccia <xref:System.ServiceModel.Description.IContractBehavior> come illustrato nel codice di esempio seguente.  Questo applica l'`OperationSelector` personalizzato al runtime di distribuzione del framework del servizio.  
  
```  
void IContractBehavior.ApplyDispatchBehavior(ContractDescription description, ServiceEndpoint endpoint, DispatchRuntime dispatch)  
{  
    dispatch.OperationSelector = new OperationSelector();  
}  
```  
  
 Prima di arrivare a OperationSelector, un messaggio deve passare attraverso il <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> del dispatcher.  Per impostazione predefinita un messaggio viene rifiutato se non è possibile trovare la relativa azione in alcun contratto implementato dal servizio.  Per evitare questo controllo, viene implementato un <xref:System.ServiceModel.Description.IEndpointBehavior> denominato `MatchAllFilterBehavior`, che consente il passaggio di tutti i messaggi attraverso il `ContractFilter` applicando <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> nel modo seguente.  
  
```  
public void ApplyDispatchBehavior(ServiceEndpoint serviceEndpoint, EndpointDispatcher endpointDispatcher)  
{  
    endpointDispatcher.ContractFilter = new MatchAllMessageFilter();  
}  
```  
  
 Quando il servizio riceve un messaggio, l'operazione del servizio appropriata viene distribuita usando le informazioni fornite dall'intestazione dell'etichetta.  Il corpo del messaggio viene deserializzato in un oggetto `PurchaseOrder`, come illustrato nel codice di esempio seguente.  
  
```  
[OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
public void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg)  
{  
    PurchaseOrder po = (PurchaseOrder)msg.Body;  
    Random statusIndexer = new Random();  
    po.Status = (OrderStates)statusIndexer.Next(3);  
    Console.WriteLine("Processing {0} ", po);  
}  
```  
  
 Il servizio è indipendente.  Quando si usa MSMQ, la coda usata deve essere creata in anticipo.  Questa operazione può essere eseguita manualmente o mediante il codice.  In questo esempio, il servizio contiene il codice necessario per verificare l'esistenza della coda e la crea se necessario.  Il nome della coda viene letto dal file di configurazione.  
  
```  
public static void Main()  
{  
    // Get MSMQ queue name from app settings in configuration  
    string queueName = ConfigurationManager.AppSettings["orderQueueName"];  
  
    // Create the transacted MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
  
    // Create a ServiceHost for the CalculatorService type.  
    using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
    {                 
        ServiceEndpoint endpoint = serviceHost.Description.Endpoints[0];  
        endpoint.Behaviors.Add(new MatchAllFilterBehavior());  
  
        //Open the ServiceHost to create listeners and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.ReadLine();  
  
        // Close the ServiceHost to shutdown the service.  
        serviceHost.Close();  
    }  
}  
```  
  
 Il nome della coda MSMQ è specificato in una sezione appSettings del file di configurazione.  
  
> [!NOTE]
>  Nel nome della coda viene usato un punto \(.\) per il computer locale e il separatore barra rovesciata nel percorso.  Nell'indirizzo dell'endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene specificato uno schema msmq.formatname e viene usato "localhost" per il computer locale.  Di seguito viene indicato lo schema di un indirizzo di coda formattato correttamente in base alle linee guida sull'indirizzamento dei nomi del formato MSMQ.  
  
```  
<appSettings>  
    <!-- Use appSetting to configure the MSMQ queue name. -->  
    <add key="queueName" value=".\private$\Orders" />  
</appSettings>  
  
```  
  
> [!NOTE]
>  Questo esempio richiede l'installazione di [Accodamento messaggi](http://go.microsoft.com/fwlink/?LinkId=95143).  
  
 Avviare il servizio ed eseguire il client.  
  
 Sul client viene visualizzato l'output seguente.  
  
```  
Placed the order:Purchase Order: 28fc457a-1a56-4fe0-9dde-156965c21ed6  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
Canceled the Order: 28fc457a-1a56-4fe0-9dde-156965c21ed6  
Press <ENTER> to terminate client.  
```  
  
 Nel servizio deve essere visualizzato l'output seguente.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
Processing Purchase Order: 28fc457a-1a56-4fe0-9dde-156965c21ed6  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Shipped  
Purchase Order 28fc457a-1a56-4fe0-9dde-156965c21ed6 is canceled  
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
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### Per eseguire l'esempio tra più computer  
  
1.  Copiare i file del programma servizio dalla cartella \\service\\bin\\, presente nella cartella specifica del linguaggio, nel computer del servizio.  
  
2.  Copiare i file del programma client dalla cartella \\client\\bin\\, presente nella cartella specifica del linguaggio, nel computer client.  
  
3.  Nel file Client.exe.config modificare orderQueueName per specificare il nome del computer del servizio anziché ".".  
  
4.  Sul computer del servizio eseguire Service.exe da un prompt dei comandi.  
  
5.  Sul computer client avviare Client.exe da un prompt dei comandi.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\CustomDemux`  
  
## Vedere anche  
 [Accodamento in WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)   
 [Accodamento messaggi](http://go.microsoft.com/fwlink/?LinkId=95143)