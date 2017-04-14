---
title: "Comunicazione bidirezionale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb64192d-b3ea-4e02-9fb3-46a508d26c60
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Comunicazione bidirezionale
Questo esempio dimostra come eseguire comunicazioni transazionali bidirezionali in coda su MSQM.  In questo esempio viene usata l'associazione `netMsmqBinding`.  In questo caso, il servizio è un'applicazione console indipendente che consente di osservare il servizio che riceve messaggi in coda.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Questo esempio è basato sull'[Associazioni MSMQ transazionali](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md).  
  
 Nella comunicazione in coda, il client comunica al servizio usando una coda.  Il client invia messaggi a una coda e il servizio riceve i messaggi dalla coda.  Di conseguenza, per comunicare mediante una coda il servizio e il client non devono essere in esecuzione contemporaneamente.  
  
 Questo esempio dimostra la comunicazione bidirezionale usando le code.  Il client invia ordini di acquisto alla coda dall'interno dell'ambito di una transazione.  Il servizio riceve gli ordini, elabora l'ordine e quindi richiama il client con lo stato dell'ordine dalla coda all'interno dell'ambito di una transazione.  Per facilitare la comunicazione bidirezionale il client e il servizio usano entrambi code per accodare gli ordini di acquisto e lo stato degli ordini.  
  
 Il contratto di servizio `IOrderProcessor` definisce operazioni del servizio bidirezionale che sono adeguate all'accodamento.  L'operazione del servizio include l'endpoint di risposta al qual e inviare gli stati degli ordini  L'endpoint di risposta è URI della coda alla quale restituire lo stato dell'ordine per il client.  L'applicazione di elaborazione degli ordini implementa questo contratto.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true)]  
    void SubmitPurchaseOrder(PurchaseOrder po, string   
                                  reportOrderStatusTo);  
}  
  
```  
  
 Il contratto di risposta per inviare lo stato dell'ordine è specificato dal client.  Il client implementa il contratto dello stato dell'ordine.  Il servizio usa il proxy generato di questo contratto per restituire lo stato dell'ordine al client.  
  
```  
[ServiceContract]  
public interface IOrderStatus  
{  
    [OperationContract(IsOneWay = true)]  
    void OrderStatus(string poNumber, string status);  
}  
```  
  
 L'operazione del servizio elabora l'ordine di acquisto inviato.  <xref:System.ServiceModel.OperationBehaviorAttribute> viene applicato all'operazione del servizio per specificare l'inserimento automatico nell'elenco in una transazione usata per ricevere il messaggio dalla coda e il completamento automatico delle transazioni al completamento dell'operazione del servizio.  La classe `Orders` incapsula la funzionalità di elaborazione degli ordini.  In questo caso, aggiunge l'ordine di acquisto a un dizionario.  La transazione che l'operazione del servizio ha inserito nell'elenco è disponibile per le operazioni nella classe `Orders`.  
  
 L'operazione del servizio, oltre a elaborare l'ordine di acquisto inviato risponde al client in merito allo stato dell'ordine.  
  
```  
[OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
public void SubmitPurchaseOrder(PurchaseOrder po, string reportOrderStatusTo)  
{  
    Orders.Add(po);  
    Console.WriteLine("Processing {0} ", po);  
    Console.WriteLine("Sending back order status information");  
    NetMsmqBinding msmqCallbackBinding = new NetMsmqBinding("ClientCallbackBinding");  
    OrderStatusClient client = new OrderStatusClient(msmqCallbackBinding, new EndpointAddress(reportOrderStatusTo));  
  
    // Please note that the same transaction that is used to dequeue the purchase order is used  
    // to send back order status.  
    using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
    {  
        client.OrderStatus(po.PONumber, po.Status);  
        scope.Complete();  
    }  
    //Close the client.  
    client.Close();  
}  
```  
  
 Il nome della coda MSMQ è specificato in una sezione appSettings del file di configurazione.  L'endpoint per il servizio è definito nella sezione System.ServiceModel del file di configurazione.  
  
> [!NOTE]
>  Il nome della coda MSMQ e l'indirizzo endpoint usano convenzioni di indirizzamento leggermente diverse.  Nel nome della coda MSMQ viene usato un punto \(.\) per il computer locale e il separatore barra rovesciata nel percorso.  Nell'indirizzo dell'endpoint di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene specificato uno schema net.msmq:, viene usato "localhost" per il computer locale e barre nel percorso.  Per leggere da una coda ospitata sul computer remoto, sostituire "." e "localhost" con il nome computer remoto.  
  
 Il servizio è indipendente.  Quando si usa il trasporto MSMQ, la coda usata deve essere creata in anticipo.  Questa operazione può essere eseguita manualmente o mediante il codice.  In questo esempio, il servizio verifica l'esistenza della coda e la crea se necessario.  Il nome della coda viene letto dal file di configurazione.  L'indirizzo di base viene usato da [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare il proxy per il servizio.  
  
```  
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Get MSMQ queue name from appSettings in configuration.  
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
    }  
}  
```  
  
 Il client crea una transazione.  La comunicazione con la coda avviene all'interno dell'ambito della transazione, facendo in modo che venga trattata come unità atomica nella quale tutti i messaggi riescono o meno.  
  
```  
// Create a ServiceHost for the OrderStatus service type.  
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderStatusService)))  
{  
  
    // Open the ServiceHostBase to create listeners and start listening for order status messages.  
    serviceHost.Open();  
  
    // Create the purchase order.  
    ...  
  
    // Create a client with given client endpoint configuration.  
    OrderProcessorClient client = new OrderProcessorClient("OrderProcessorEndpoint");  
  
    //Create a transaction scope.  
    using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
    {  
        string hostName = Dns.GetHostName();  
  
        // Make a queued call to submit the purchase order.  
        client.SubmitPurchaseOrder(po, "net.msmq://" + hostName + "/private/ServiceModelSamplesTwo-way/OrderStatus");  
  
        // Complete the transaction.  
        scope.Complete();  
    }  
  
    //Close down the client.  
    client.Close();  
  
    Console.WriteLine();  
    Console.WriteLine("Press <ENTER> to terminate client.");  
    Console.ReadLine();  
  
    // Close the ServiceHost to shutdown the service.  
    serviceHost.Close();  
}  
  
```  
  
 Il codice client implementa il contratto `IOrderStatus` per ricevere lo stato dell'ordine dal servizio.  In questo caso, stampa lo stato dell'ordine.  
  
```  
[ServiceBehavior]  
public class OrderStatusService : IOrderStatus  
{  
    [OperationBehavior(TransactionAutoComplete = true,   
                        TransactionScopeRequired = true)]  
    public void OrderStatus(string poNumber, string status)  
    {  
        Console.WriteLine("Status of order {0}:{1} ", poNumber ,   
                                                           status);  
    }  
}  
  
```  
  
 La coda dello stato degli ordini viene creata nel metodo `Main`.  La configurazione del client comprende la configurazione del servizio di stato degli ordini per ospitare il servizio di stato degli ordini, come illustrato nella configurazione di esempio seguente.  
  
```  
<appSettings>  
  <!-- Use appSetting to configure MSMQ queue name. -->  
  <add key="queueName" value=".\private$\ServiceModelSamplesTwo-way/OrderStatus" />  
</appSettings>  
  
<system.serviceModel>  
  
  <services>  
    <service   
       name="Microsoft.ServiceModel.Samples.OrderStatusService">  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderStatus"  
                binding="netMsmqBinding"  
                contract="Microsoft.ServiceModel.Samples.IOrderStatus" />  
    </service>  
  </services>  
  
  <client>  
    <!-- Define NetMsmqEndpoint -->  
    <endpoint name="OrderProcessorEndpoint"  
              address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderProcessor"   
              binding="netMsmqBinding"   
              contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
  </client>  
  
</system.serviceModel>  
  
```  
  
 Quando si esegue l'esempio, le attività del client e del servizio vengono visualizzate nelle finestre della console del servizio e del client.  È possibile osservare il servizio che riceve i messaggi dal client.  Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
 Il servizio visualizza le informazioni dell'ordine di acquisto e indica che restituisce lo stato dell'ordine alla coda di stato degli ordini.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Processing Purchase Order: 124a1f69-3699-4b16-9bcc-43147a8756fc  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
  
Sending back order status information  
```  
  
 Il client visualizza le informazioni sullo stato dell'ordine inviate dal servizio.  
  
```  
Press <ENTER> to terminate client.  
Status of order 124a1f69-3699-4b16-9bcc-43147a8756fc:Pending  
  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
    > [!NOTE]
    >  Se si usa Svcutil.exe per rigenerare la configurazione di questo esempio, assicurarsi di modificare i nomi degli endpoint nella configurazione client in modo che corrisponda al codice client.  
  
 Per impostazione predefinita con l'associazione <xref:System.ServiceModel.NetMsmqBinding>, la sicurezza del trasporto è abilitata.  Sono disponibili due proprietà di rilievo per la sicurezza del trasporto MSMQ, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> e <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>`.` Per impostazione predefinita, la modalità di autenticazione è impostata su `Windows` e il livello di protezione è impostato su `Sign`.  Affinché MSMQ fornisca la funzionalità di autenticazione e firma, è necessario che faccia parte di un dominio e che sia installata l'opzione di integrazione di Active Directory per MSMQ.  Se si esegue questo esempio in un computer che non soddisfà questi criteri si riceve un errore.  
  
### Per eseguire l'esempio in un computer appartenente a un gruppo di lavoro o privo di integrazione con Active Directory  
  
1.  Se il computer non appartiene a un dominio o non è installato con l'integrazione di Active Directory, disattivare la sicurezza del trasporto impostando la modalità di autenticazione e il livello di protezione su `None` come illustrato nella configurazione di esempio seguente:  
  
    ```  
    <configuration>  
  
      <appSettings>  
        <!-- Use appSetting to configure MSMQ queue name. -->  
        <add key="queueName" value=".\private$\ServiceModelSamplesTwo-way/OrderProcessor" />  
      </appSettings>  
  
      <system.serviceModel>  
        <services>  
          <service   
              name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
            <!-- Define NetMsmqEndpoint -->  
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderProcessor"  
                      binding="netMsmqBinding"  
                      bindingConfiguration="TransactedBinding"   
                      contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
          </service>  
        </services>  
  
        <bindings>  
          <netMsmqBinding>  
            <binding name="TransactedBinding" >  
             <security mode="None" />  
            </binding>  
          </netMsmqBinding>  
        </bindings>  
  
      </system.serviceModel>  
  
    </configuration>  
  
    ```  
  
2.  La disattivazione della sicurezza per una configurazione client genera quanto segue:  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <appSettings>  
        <!-- Use appSetting to configure MSMQ queue name. -->  
        <add key="queueName" value=".\private$\ServiceModelSamplesTwo-way/OrderStatus" />  
      </appSettings>  
  
      <system.serviceModel>  
  
        <services>  
          <service   
             name="Microsoft.ServiceModel.Samples.OrderStatusService">  
            <!-- Define NetMsmqEndpoint -->  
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderStatus"  
                      binding="netMsmqBinding"  
                      bindingConfiguration="TransactedBinding" contract="Microsoft.ServiceModel.Samples.IOrderStatus" />  
          </service>  
        </services>  
  
        <client>  
          <!-- Define NetMsmqEndpoint -->  
          <endpoint name="OrderProcessorEndpoint"  
                    address="net.msmq://localhost/private/ServiceModelSamplesTwo-way/OrderProcessor"   
                    binding="netMsmqBinding"   
                    bindingConfiguration="TransactedBinding"  
                    contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
        </client>  
  
        <bindings>  
          <netMsmqBinding>  
            <binding name="TransactedBinding" >  
             <security mode="None" />  
            </binding>  
          </netMsmqBinding>  
        </bindings>  
  
      </system.serviceModel>  
  
    </configuration>  
    ```  
  
3.  Il servizio per questo esempio crea un'associazione in `OrderProcessorService`.  Aggiungere una riga di codice dopo la creazione dell'istanza dell'associazione per impostare la modalità di sicurezza su `None`.  
  
    ```  
    NetMsmqBinding msmqCallbackBinding = new NetMsmqBinding();  
    msmqCallbackBinding.Security.Mode = NetMsmqSecurityMode.None;  
    ```  
  
4.  Assicurarsi di modificare la configurazione sul server e sul client prima di eseguire l'esempio.  
  
    > [!NOTE]
    >  L'impostazione di `security mode` su `None` è equivalente all'impostazione di <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> o della sicurezza del `Message` su `None`.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Binding\Net\MSMQ\Two-Way`  
  
## Vedere anche