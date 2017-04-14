---
title: "Batch transazionale. | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ecd328ed-332e-479c-a894-489609bcddd2
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Batch transazionale.
Questo esempio dimostra come raggruppare letture transazionali usando Accodamento messaggi \(MSMQ\).  Il batch transazionale è una funzionalità di ottimizzazione delle prestazioni per le letture transazionali nella comunicazione in coda.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Nella comunicazione in coda, il client comunica al servizio usando una coda.  Più precisamente, il client invia messaggi a una coda.  Il servizio riceve messaggi dalla coda.  Di conseguenza, per comunicare mediante una coda il servizio e il client non devono essere in esecuzione contemporaneamente.  
  
 Nell'esempio viene dimostrato il batch transazionale.  Il batch transazionale è un comportamento che consente di usare una singola transazione per la lettura di molti messaggi nella coda e la relativa elaborazione.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Se il servizio viene eseguito prima, verificherà la presenza della coda.  Se la coda non è presente, il servizio ne creerà una.  È possibile eseguire il servizio prima per creare la coda oppure è possibile crearne una tramite il gestore code MSMQ.  Per creare una coda in Windows 2008, eseguire i passaggi riportati di seguito.  
  
    1.  Aprire Server Manager in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
    2.  Espandere la scheda **Funzionalità**.  
  
    3.  Fare clic con il pulsante destro del mouse su **Code private**, quindi scegliere **Nuova** **coda privata**.  
  
    4.  Selezionare la casella **Di transazione**.  
  
    5.  Immettere `ServiceModelSamplesTransacted` come nome della nuova coda.  
  
    > [!NOTE]
    >  In questo esempio il client invia centinaia di messaggi come parte del batch.  È pertanto normale che l'applicazione di servizio impieghi del tempo per elaborarli.  
  
3.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### Per eseguire l'esempio in un computer appartenente a un gruppo di lavoro o privo di integrazione con Active Directory  
  
1.  Per impostazione predefinita con l'associazione <xref:System.ServiceModel.NetMsmqBinding>, la sicurezza del trasporto è abilitata.  Sono disponibili due proprietà di rilievo per la sicurezza del trasporto MSMQ, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> e <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>`.` Per impostazione predefinita, la modalità di autenticazione è impostata su `Windows` e il livello di protezione è impostato su `Sign`.  Affinché MSMQ fornisca la funzionalità di autenticazione e firma, è necessario che faccia parte di un dominio e che sia installata l'opzione di integrazione di Active Directory per MSMQ.  Se si esegue questo esempio in un computer che non soddisfà questi criteri si riceve un errore.  
  
2.  Se il computer non appartiene a un dominio o non è installato con l'integrazione di Active Directory, disattivare la sicurezza del trasporto impostando la modalità di autenticazione e il livello di protezione su `None` come illustrato nella configurazione di esempio seguente:  
  
    ```  
    <system.serviceModel>  
      <behaviors>  
        <serviceBehaviors>  
          <behavior name="ThrottlingBehavior">  
            <serviceMetadata httpGetEnabled="true"/>  
            <serviceThrottling maxConcurrentCalls="5"/>  
          </behavior>  
        </serviceBehaviors>  
  
        <endpointBehaviors>  
          <behavior name="BatchingBehavior">  
            <transactedBatching maxBatchSize="100"/>  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>  
      <services>  
        <service   
            behaviorConfiguration="ThrottlingBehavior"   
            name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
          <host>  
            <baseAddresses>  
              <add baseAddress="http://localhost:8000/orderProcessor/transactedBatchingSample"/>  
            </baseAddresses>  
          </host>  
          <!-- Define NetMsmqEndpoint -->  
          <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTransactedBatching"  
                    binding="netMsmqBinding"  
                    bindingConfiguration="Binding1"   
                    behaviorConfiguration="BatchingBehavior"   
                    contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
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
  
    </system.serviceModel>  
  
    ```  
  
3.  Assicurarsi di modificare la configurazione sul server e sul client prima di eseguire l'esempio.  
  
    > [!NOTE]
    >  L'impostazione di `security` `mode` su `None` è equivalente all'impostazione della sicurezza di <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> e `Message` su `None`.  
  
4.  Per eseguire il database in un computer remoto, modificare la stringa di connessione per puntare al computer sul quale risiede il database.  
  
## Requisiti  
 Per eseguire questo esempio, è necessario che MSMQ sia installato ed è necessario SQL o SQL ExpressSQL.  
  
## Dimostrazione  
 Questo esempio dimostra il comportamento batch transazionale.  Il batch transazionale è una funzionalità di ottimizzazione delle prestazione fornita con il trasporto in coda MSMQ.  
  
 Quando vengono usate transazioni per inviare e ricevere messaggi, di fatto vi sono 2 transazioni distinte.  Quando il client invia messaggi all'interno dell'ambito di una transazione, questa è locale per il client e il gestore delle code client.  Quando il servizio riceve messaggi all'interno dell'ambito di una transazione, questa è locale per il servizio e il gestore delle code di destinazione.  È molto importante ricordare che il client e il servizio non partecipano alla stessa transazione; essi usano invece transazioni diverse per le operazioni con la coda, quali l'invio e la ricezione.  
  
 Nell'esempio viene usata una sola transazione per l'esecuzione di più operazioni del servizio.  Questa viene usata solo come funzionalità di ottimizzazione delle prestazioni e non influisce sulla semantica dell'applicazione.  L'esempio è basato sull'[Associazioni MSMQ transazionali](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md).  
  
## Commenti  
 In questo esempio, il client invia un batch di messaggi al servizio dall'interno dell'ambito di una transazione.  Per mostrare l'ottimizzazione delle prestazioni viene inviato un numero elevato di messaggi; in questo caso, fino a 2500 messaggi.  
  
 I messaggi inviati alla coda vengono quindi ricevuti dal servizio fra l'ambito della transazione definito dal servizio.  Senza il raggruppamento, ciò si traduce in 2500 transazioni per ogni chiamata dell'operazione del servizio.  Questo influisce sulle prestazioni del sistema.  Poiché sono coinvolti due gestori due gestori di risorse, la coda MSMQ e il database `Orders`, ciascuna di queste transazioni è una transazione DTC.  Ciò viene ottimizzato usando un numero molto inferiore di transazioni per garantire che a un batch di messaggi e chiamate delle operazioni del servizio abbia luogo in un'unica transazione.  
  
 La funzionalità batch viene usata nel modo seguente:  
  
-   Specificando il comportamento del batch transazionale nella configurazione.  
  
-   Specificando una dimensione di batch in termini di numero di messaggi da leggere in un'unica transazione.  
  
-   Specificando il numero massimo di batch simultanei da eseguire.  
  
 In questo esempio, vengono dimostrati i guadagni di prestazioni tramite la riduzione del numero di transazioni assicurando che vengano chiamate 100 operazioni del servizio in una sola transazione prima di eseguire il commit della transazione.  
  
 Il comportamento del servizio definisce un comportamento dell'operazione con `TransactionScopeRequired` impostato su `true`.  Questo assicura che lo stesso ambito della transazione che viene usato per recuperare il messaggio dalla coda sia usato da tutti i gestori di risorse ai quali accede il metodo.  In questo esempio, viene usato un database di base per archiviare le informazioni sull'ordine di acquisto contenute nel messaggio.  L'ambito della transazione garantisce anche che se il metodo genera un'eccezione, il messaggio viene restituito alla coda.  Senza impostare questo comportamento dell'operazione, un canale in coda crea una transazione per leggere il messaggio dalla coda e ne esegue automaticamente il commit prima che venga inviato in modo che se l'operazione non riesce, il messaggio va perduto.  Lo scenario più comune per le operazioni del servizio è di inserirsi nella transazione che viene usata per leggere il messaggio dalla coda come dimostrato nel codice seguente.  
  
 Notare che `ReleaseServiceInstanceOnTransactionComplete` è impostato su `false`.  Si tratta di un requisito importante per il raggruppamento.  La proprietà `ReleaseServiceInstanceOnTransactionComplete` in `ServiceBehaviorAttribute` indica che cosa fare con l'istanza del servizio dopo che la transazione è stata completata.  Per impostazione predefinita, l'istanza del servizio viene rilasciata al completa della transazione.  L'aspetto centrale del raggruppamento è l'uso di una singola transazione per la lettura e l'invio di molti messaggi nella coda.  Di conseguenza, il rilascio dell'istanza del servizio comporta il completamento della transazione vanificando in modo prematuro l'effettivo uso del raggruppamento.  Se questa proprietà è impostata su `true` e all'endpoint viene aggiunto il comportamento del batch transazionale, il comportamento di convalida batch genera un'eccezione.  
  
```  
// Service class that implements the service contract.  
// Added code to write output to the console window.  
[ServiceBehavior(ReleaseServiceInstanceOnTransactionComplete=false,   
TransactionIsolationLevel=  
System.Transactions.IsolationLevel.Serializable, ConcurrencyMode=ConcurrencyMode.Multiple)]  
public class OrderProcessorService : IOrderProcessor  
{  
    [OperationBehavior(TransactionScopeRequired = true,  
                       TransactionAutoComplete = true)]  
    public void SubmitPurchaseOrder(PurchaseOrder po)  
    {  
        Orders.Add(po);  
        Console.WriteLine("Processing {0} ", po);  
    }  
    …  
}  
  
```  
  
 La classe `Orders` incapsula l'elaborazione dell'ordine.  Nell'esempio, aggiorna il database con le informazioni dell'ordine di acquisto.  
  
```  
// Order Processing Logic  
public class Orders  
{  
    public static void Add(PurchaseOrder po)  
    {  
        // Insert purchase order.  
        SqlCommand insertPurchaseOrderCommand =   
        new SqlCommand(  
        "insert into PurchaseOrders(poNumber, customerId)   
                               values(@poNumber, @customerId)");  
        insertPurchaseOrderCommand.Parameters.Add("@poNumber",   
                                           SqlDbType.VarChar, 50);  
        insertPurchaseOrderCommand.Parameters.Add("@customerId",   
                                         SqlDbType.VarChar, 50);  
  
        // Insert product line item.  
        SqlCommand insertProductLineItemCommand =   
             new SqlCommand("insert into ProductLineItems(productId,   
                    unitCost, quantity, poNumber) values(@productId,   
                    @unitCost, @quantity, @poNumber)");  
        insertProductLineItemCommand.Parameters.Add("@productId",   
                                           SqlDbType.VarChar, 50);  
        insertProductLineItemCommand.Parameters.Add("@unitCost",   
                                                  SqlDbType.Float);  
        insertProductLineItemCommand.Parameters.Add("@quantity",   
                                                     SqlDbType.Int);  
        insertProductLineItemCommand.Parameters.Add("@poNumber",   
                                           SqlDbType.VarChar, 50);  
        int rowsAffected = 0;  
        using (TransactionScope scope =   
              new TransactionScope(TransactionScopeOption.Required))  
        {  
             using (SqlConnection conn = new   
                 SqlConnection(  
                 ConfigurationManager.AppSettings["connectionString"]))  
             {  
                 conn.Open();  
  
                // Insert into purchase order table.  
               insertPurchaseOrderCommand.Connection = conn;  
               insertPurchaseOrderCommand.Parameters["@poNumber"].Value   
                                                       = po.PONumber;  
             insertPurchaseOrderCommand.Parameters["@customerId"].Value   
                                                    =po.CustomerId;  
             insertPurchaseOrderCommand.ExecuteNonQuery();  
  
            // Insert into product line item table.  
            insertProductLineItemCommand.Connection = conn;  
            foreach (PurchaseOrderLineItem orderLineItem in   
                                        po.orderLineItems) {  
            insertProductLineItemCommand.Parameters["@poNumber"].Value   
                                                          =po.PONumber;  
            insertProductLineItemCommand.Parameters["@productId"].Value   
                                             = orderLineItem.ProductId;  
            insertProductLineItemCommand.Parameters["@unitCost"].Value   
                                             = orderLineItem.UnitCost;  
            insertProductLineItemCommand.Parameters["@quantity"].Value   
                                             = orderLineItem.Quantity;  
            rowsAffected +=   
            insertProductLineItemCommand.ExecuteNonQuery();  
            }  
            scope.Complete();  
        }  
     }  
     Console.WriteLine(  
     "Updated database with {0} product line items  for purchase order   
                                     {1} ", rowsAffected, po.PONumber);  
    }  
}  
```  
  
 Il comportamento batch e la relativa configurazione sono specificati nella configurazione dell'applicazione del servizio.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <appSettings>  
    <!-- Use appSetting to configure MSMQ queue name. -->  
    <add key="queueName"   
     value=".\private$\ServiceModelSamplesTransactedBatching" />  
    <add key="baseAddress"   
     value=  
     "http://localhost:8000/orderProcessor/transactedBatchingSample"/>  
    <add key="connectionString" value="Data Source=.\SQLEXPRESS;AttachDbFilename=|DataDirectory|orders.mdf;Integrated Security=True;User Instance=True;" />  
  </appSettings>  
  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="ThrottlingBehavior">  
          <serviceThrottling maxConcurrentCalls="5"/>  
        </behavior>  
      </serviceBehaviors>  
  
      <endpointBehaviors>  
        <behavior name="BatchingBehavior">  
          <transactedBatching maxBatchSize="100"/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <services>  
      <service   
          behaviorConfiguration="ThrottlingBehavior"   
          name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
        <!-- Define NetMsmqEndpoint -->  
        <endpoint address=  
"net.msmq://localhost/private/ServiceModelSamplesTransactedBatching"  
                  binding="netMsmqBinding"  
                  behaviorConfiguration="BatchingBehavior"   
                  contract=  
                    "Microsoft.ServiceModel.Samples.IOrderProcessor" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
> [!NOTE]
>  La dimensione di batch è un suggerimento al sistema.  Ad esempio, se viene specificata una dimensione di batch di 20, verrebbero letti e inviati 20 messaggi usando una singola transazione e quindi verrebbe eseguito il commit della transazione.  Vi sono però casi in cui la transazione può eseguire il commit del batch prima che venga raggiunta la dimensione di batch.  
>   
>  A ogni transazione è associato un timeout che inizia il ciclo quando viene creata la transazione.  Quando il timeout scade la transazione viene interrotta.  È possibile che il timeout scada anche prima che venga raggiunta la dimensione di batch.  Per evitare la rielaborazione del batch a causa dell'interruzione `TransactedBatchingBehavior` verifica il tempo residuo nella transazione.  Se è stato usato l'80% del timeout della transazione, viene eseguito il commit della transazione.  
>   
>  Se nella coda non sono più presenti messaggi, invece di attendere il raggiungimento della dimensione di batch <xref:System.ServiceModel.Description.TransactedBatchingBehavior> esegue il commit della transazione.  
>   
>  La scelta della dimensione di batch dipende dall'applicazione.  Se la dimensione di batch è troppo piccola, è possibile che non si ottengano le prestazioni desiderate.  Se invece la dimensione di batch è troppo grande, le prestazioni potrebbero risentirne in modo negativo.  Ad esempio, la transazione potrebbe persistere più a lungo e attivare dei blocchi sul database oppure potrebbe passare in una situazione di deadlock, determinando la restituzione del batch e la relativa rielaborazione.  
  
 Il client crea un ambito di transazione.  La comunicazione con la coda avviene all'interno dell'ambito della transazione, facendo in modo che venga trattata come unità atomica nella quale alla coda vengono inviati tutti i messaggi o nessuno.  Il commit della transazione viene eseguito chiamando <xref:System.Transactions.TransactionScope.Complete%2A> nell'ambito della transazione.  
  
```  
//Client implementation code.  
class Client  
{  
    static void Main()  
    {  
        Random randomGen = new Random();  
        for (int i = 0; i < 2500; i++)  
        {  
            // Create a client with given client endpoint configuration.  
            OrderProcessorClient client = new OrderProcessorClient("OrderProcessorEndpoint");  
  
            // Create the purchase order.  
            PurchaseOrder po = new PurchaseOrder();  
            po.CustomerId = "somecustomer" + i + ".com";  
            po.PONumber = Guid.NewGuid().ToString();  
  
            PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();  
            lineItem1.ProductId = "Blue Widget";  
            lineItem1.Quantity = randomGen.Next(1, 100);  
            lineItem1.UnitCost = (float)randomGen.NextDouble() * 10;  
  
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
                // Make a queued call to submit the purchase order.  
                client.SubmitPurchaseOrder(po);  
                // Complete the transaction.  
                scope.Complete();  
            }  
  
            client.Close();  
        }  
        Console.WriteLine();  
        Console.WriteLine("Press <ENTER> to terminate client.");  
        Console.ReadLine();  
    }  
}  
```  
  
 Quando si esegue l'esempio, le attività del client e del servizio vengono visualizzate nelle finestre della console del servizio e del client.  È possibile osservare il servizio che riceve i messaggi dal client.  Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  Notare che essendo usato l'accodamento, non è necessario che client e servizio siano in esecuzione contemporaneamente.  È possibile eseguire il client, arrestarlo e quindi avviare il servizio e riceve comunque i messaggi.  È possibile osservare un output mobile mentre i messaggi vengono letti in un batch ed elaborati.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Updated database with 2 product line items for purchase order 493ac832-d216-4e94-b2a5-d7f492fb5e39  
Processing Purchase Order: 8b567f5b-0661-4662-aae2-6cef1bd6d278  
        Customer: somecustomer849.com  
        OrderDetails  
               Order LineItem: 80 of Blue Widget @unit price: $9.751623  
               Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $41622.23  
        Order status: Pending  
  
Updated database with 2 product line items for purchase order 41130b95-4ea8-40a9-91c3-2e129117fcb8  
Processing Purchase Order: 5ce2699d-9a31-4cc2-a8c5-64cda614b3c7  
        Customer: somecustomer850.com  
        OrderDetails  
               Order LineItem: 89 of Blue Widget @unit price: $6.369128  
               Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $41408.95  
        Order status: Pending  
  
Updated database with 2 product line items for purchase order 8b567f5b-0661-4662-aae2-6cef1bd6d278  
Processing Purchase Order: ea94486b-7c86-4309-a42d-2f06c00656cd  
        Customer: somecustomer851.com  
        OrderDetails  
             Order LineItem: 47 of Blue Widget @unit price: $0.9391424  
             Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $40886.24  
        Order status: Pending  
```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Batching`  
  
## Vedere anche