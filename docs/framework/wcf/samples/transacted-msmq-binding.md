---
title: "Associazioni MSMQ transazionali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 71f5cb8d-f1df-4e1e-b8a2-98e734a75c37
caps.latest.revision: 50
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 50
---
# Associazioni MSMQ transazionali
Questo esempio illustra come eseguire comunicazioni in coda transazionali utilizzando Accodamento messaggi \(MSMQ\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Nella comunicazione in coda, il client comunica al servizio utilizzando una coda.Più precisamente, il client invia messaggi a una coda.Il servizio riceve messaggi dalla coda.Di conseguenza, per comunicare mediante una coda, il servizio e il client non devono essere in esecuzione contemporaneamente.  
  
 Quando vengono utilizzate transazioni per inviare e ricevere messaggi, di fatto vi sono due transazioni distinte.Quando il client invia messaggi all'interno dell'ambito di una transazione, questa è locale per il client e il gestore delle code client.Quando il servizio riceve messaggi all'interno dell'ambito di una transazione, questa è locale per il servizio e il gestore delle code di destinazione.È molto importante ricordare che il client e il servizio non partecipano alla stessa transazione; essi utilizzano invece transazioni diverse per le operazioni con la coda, quali l'invio e la ricezione.  
  
 In questo esempio, il client invia un batch di messaggi al servizio dall'interno dell'ambito di una transazione.I messaggi inviati alla coda vengono quindi ricevuti dal servizio fra l'ambito della transazione definito dal servizio.  
  
 Il contratto del servizio è `IOrderProcessor`, come mostrato nel codice di esempio seguente.L'interfaccia definisce un servizio unidirezionale adatto per l'utilizzo con le code.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true)]  
    void SubmitPurchaseOrder(PurchaseOrder po);  
}  
```  
  
 Il comportamento del servizio definisce un comportamento dell'operazione con `TransactionScopeRequired` impostato su `true`.Questo assicura che lo stesso ambito della transazione che viene utilizzato per recuperare il messaggio dalla coda sia utilizzato da tutti i gestori di risorse ai quali accede il metodo.Garantisce anche che se il metodo genera un'eccezione, il messaggio viene restituito alla coda.Senza impostare questo comportamento dell'operazione, un canale in coda crea una transazione per leggere il messaggio dalla coda e ne esegue automaticamente il commit prima dell'invio in modo che se l'operazione non riesce, il messaggio va perduto.Lo scenario più comune per le operazioni del servizio è di inserirsi nella transazione che viene utilizzata per leggere il messaggio dalla coda, come dimostrato nel codice seguente.  
  
```  
  
 // This service class that implements the service contract.  
 // This added code writes output to the console window.  
 public class OrderProcessorService : IOrderProcessor  
 {  
     [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
     public void SubmitPurchaseOrder(PurchaseOrder po)  
     {  
         Orders.Add(po);  
         Console.WriteLine("Processing {0} ", po);  
     }  
  …  
}  
  
```  
  
 Il servizio è indipendente.Quando si utilizza il trasporto MSMQ, la coda utilizzata deve essere creata in anticipo.Questa operazione può essere eseguita manualmente o mediante il codice.In questo esempio, il servizio contiene il codice necessario per verificare l'esistenza della coda e crearla se necessario.Il nome della coda viene letto dal file di configurazione.L'indirizzo di base viene utilizzato da [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare il proxy per il servizio.  
  
```  
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Get the MSMQ queue name from appSettings in configuration.  
    string queueName = ConfigurationManager.AppSettings["queueName"];  
  
    // Create the transacted MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
  
    // Create a ServiceHost for the OrderProcessorService type.  
    using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
    {  
        // Open the ServiceHost to create listeners and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
  
        // Close the ServiceHost to shut down the service.  
        serviceHost.Close();  
    }  
}  
  
```  
  
 Il nome della coda MSMQ viene specificato in una sezione appSettings del file di configurazione, come mostra la configurazione di esempio seguente.  
  
```  
<appSettings>  
    <add key="queueName" value=".\private$\ServiceModelSamplesTransacted" />  
</appSettings>  
```  
  
> [!NOTE]
>  Il nome della coda utilizza un punto \(.\) per il computer locale e barre rovesciate come separatori all'interno del percorso quando la coda viene creata utilizzando <xref:System.Messaging>.L'endpoint [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizza l'indirizzo della coda con uno schema net.msmq, utilizza "localhost" per indicare il computer locale e barre nel percorso.  
  
 Il client crea un ambito di transazione.La comunicazione con la coda avviene all'interno dell'ambito della transazione, facendo in modo che venga trattata come unità atomica nella quale alla coda vengono inviati tutti i messaggi o nessuno.Il commit della transazione viene eseguito chiamando <xref:System.Transactions.TransactionScope.Complete%2A> nell'ambito della transazione.  
  
```  
// Create a client.  
OrderProcessorClient client = new OrderProcessorClient();  
  
// Create the purchase order.  
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
  
// Create a transaction scope.  
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
{  
    // Make a queued call to submit the purchase order.  
    client.SubmitPurchaseOrder(po);  
    // Complete the transaction.  
    scope.Complete();  
}  
  
// Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
  
Console.WriteLine();  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
```  
  
 Per verificare che le transazioni stiano funzionando, modificare il client impostando l'ambito della transazione come commento, come mostra il codice di esempio seguente, ricompilare la soluzione ed eseguire il client.  
  
```  
//scope.Complete();  
```  
  
 Poiché la transazione non è stata completata, i messaggi non vengono inviati alla coda.  
  
 Quando si esegue l'esempio, le attività del client e del servizio vengono visualizzate nelle finestre della console del servizio e del client.È possibile osservare il servizio che riceve i messaggi dal client.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.Notare che essendo utilizzato l'accodamento, non è necessario che client e servizio siano in esecuzione contemporaneamente.È possibile eseguire il client, arrestarlo e quindi avviare il servizio e riceve comunque i messaggi.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Processing Purchase Order: 7b31ce51-ae7c-4def-9b8b-617e4288eafd  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Se il servizio viene eseguito prima, verificherà la presenza della coda.Se la coda non è presente, il servizio ne creerà una.È possibile eseguire il servizio prima per creare la coda oppure è possibile crearne una tramite il gestore code MSMQ.Per creare una coda in Windows 2008, eseguire i passaggi riportati di seguito.  
  
    1.  Aprire Server Manager in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
    2.  Espandere la scheda **Funzionalità**.  
  
    3.  Fare clic con il pulsante destro del mouse su **Code private**, quindi scegliere **Nuova** **coda privata**.  
  
    4.  Selezionare la casella **Di transazione**.  
  
    5.  Immettere `ServiceModelSamplesTransacted` come nome della nuova coda.  
  
3.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
 Per impostazione predefinita, con l'associazione <xref:System.ServiceModel.NetMsmqBinding> la sicurezza del trasporto è abilitata.Nell'associazione sono presenti due proprietà importanti per la sicurezza del trasporto MSMQ: <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> e <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>.Per impostazione predefinita, la modalità di autenticazione è impostata su `Windows` e il livello di protezione è impostato su `Sign`.Affinché MSMQ fornisca la funzionalità di autenticazione e firma, è necessario che faccia parte di un dominio e che sia installata l'opzione di integrazione di Active Directory per MSMQ.Se si esegue questo esempio in un computer che non soddisfa questi criteri, si riceve un errore.  
  
### Per eseguire l'esempio in un computer appartenente a un gruppo di lavoro o privo di integrazione con Active Directory  
  
1.  Se il computer non appartiene a un dominio o non è installato con l'integrazione di Active Directory, disattivare la sicurezza del trasporto impostando la modalità di autenticazione e il livello di protezione su `None` come illustrato nel codice di configurazione seguente.  
  
    ```  
    <system.serviceModel>  
      <services>  
        <service name="Microsoft.ServiceModel.Samples.OrderProcessorService"  
                 behaviorConfiguration="OrderProcessorServiceBehavior">  
          <host>  
            <baseAddresses>  
              <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
            </baseAddresses>  
          </host>  
          <!-- Define NetMsmqEndpoint. -->  
          <endpoint  
              address="net.msmq://localhost/private/ServiceModelSamplesTransacted"  
              binding="netMsmqBinding"  
              bindingConfiguration="Binding1"  
           contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
          <!-- The mex endpoint is explosed at http://localhost:8000/ServiceModelSamples/service/mex. -->  
          <endpoint address="mex"  
                    binding="mexHttpBinding"  
                    contract="IMetadataExchange" />  
        </service>  
      </services>  
  
      <bindings>  
        <netMsmqBinding>  
          <binding name="Binding1">  
            <security mode="None" />  
          </binding>  
        </netMsmqBinding>  
      </bindings>  
  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="OrderProcessorServiceBehavior">  
              <serviceMetadata httpGetEnabled="True"/>  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
  
    ```  
  
2.  Verificare di modificare la configurazione nel server e nel client prima di eseguire l'esempio.  
  
    > [!NOTE]
    >  L'impostazione di `security``mode` su `None` è equivalente all'impostazione di <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> e della sicurezza di `Message` su `None`.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Transacted`  
  
## Vedere anche