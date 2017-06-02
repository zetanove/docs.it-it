---
title: "Trasporto: transazioni personalizzate nell&#39;esempio UDP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6cebf975-41bd-443e-9540-fd2463c3eb23
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Trasporto: transazioni personalizzate nell&#39;esempio UDP
Questo esempio è basato sull'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md) presente in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)][Estensibilità del trasporto](../../../../docs/framework/wcf/samples/transport-extensibility.md).Estende l'esempio Trasporto di UDP per supportare flussi di transazioni personalizzate e illustra l'utilizzo della proprietà <xref:System.ServiceModel.Channels.TransactionMessageProperty>.  
  
## Modifiche al codice nell'esempio Trasporto di UDP  
 Per illustrare il flusso della transazione l'esempio modifica il contratto di servizio affinché `ICalculatorContract` richieda un ambito della transazione per `CalculatorService.Add()`.L'esempio aggiunge anche un parametro `System.Guid` supplementare al contratto dell'operazione `Add`.Questo parametro viene utilizzato per passare l'identificatore della transazione client al servizio.  
  
```  
class CalculatorService : IDatagramContract, ICalculatorContract  
{  
    [OperationBehavior(TransactionScopeRequired=true)]  
    public int Add(int x, int y, Guid clientTransactionId)  
    {  
        if(Transaction.Current.TransactionInformation.DistributedIdentifier == clientTransactionId)  
    {  
        Console.WriteLine("The client transaction has flowed to the service");  
    }  
    else  
    {  
     Console.WriteLine("The client transaction has NOT flowed to the service");  
    }  
  
    Console.WriteLine("   adding {0} + {1}", x, y);              
    return (x + y);  
    }  
  
    [...]  
}  
```  
  
 L'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md) utilizza pacchetti UDP per passare messaggi tra un client e un servizio.[Transport: Custom Transport Sample](../../../../docs/framework/wcf/samples/transport-custom-transactions-over-udp-sample.md) utilizza lo stesso meccanismo per trasportare messaggi, ma quando una transazione viene propagata, viene inserito nel pacchetto UDP insieme al messaggio codificato.  
  
```  
byte[] txmsgBuffer =                TransactionMessageBuffer.WriteTransactionMessageBuffer(txPropToken, messageBuffer);  
  
int bytesSent = this.socket.SendTo(txmsgBuffer, 0, txmsgBuffer.Length, SocketFlags.None, this.remoteEndPoint);  
```  
  
 `TransactionMessageBuffer.WriteTransactionMessageBuffer` è un metodo di supporto che contiene nuove funzionalità che consentono di unire il token di propagazione della transazione corrente con l'entità del messaggio e di posizionarlo in un buffer.  
  
 Per il trasporto di flussi di transazioni personalizzate, l'implementazione client deve conoscere quali operazioni del servizio richiedono il flusso della transazione e passare queste informazioni a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Ci deve anche essere un meccanismo per trasmettere la transazione utente al livello di trasporto.Per ottenere queste informazioni, in questo esempio vengono utilizzati "controlli messaggi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]" .Il controllo messaggi del client qui implementato, denominato `TransactionFlowInspector`, esegue le attività seguenti:  
  
-   Determina se una transazione deve essere propagata per un'azione del messaggio specificata mediante `IsTxFlowRequiredForThisOperation()`.  
  
-   Allega la transazione di ambiente corrente al messaggio utilizzando `TransactionFlowProperty`, se una transazione deve essere propagata \(ciò viene realizzato in `BeforeSendRequest()`\).  
  
```  
public class TransactionFlowInspector : IClientMessageInspector  
{  
   void IClientMessageInspector.AfterReceiveReply(ref           System.ServiceModel.Channels.Message reply, object correlationState)  
  {  
  }  
  
   public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel)  
   {  
       // obtain the tx propagation token  
       byte[] propToken = null;             
       if (Transaction.Current != null && IsTxFlowRequiredForThisOperation(request.Headers.Action))  
       {  
           try  
           {  
               propToken = TransactionInterop.GetTransmitterPropagationToken(Transaction.Current);  
           }  
           catch (TransactionException e)  
           {  
              throw new CommunicationException("TransactionInterop.GetTransmitterPropagationToken failed.", e);  
           }  
       }  
  
      // set the propToken on the message in a TransactionFlowProperty  
       TransactionFlowProperty.Set(propToken, request);  
  
       return null;              
    }  
  }  
  
  static bool IsTxFlowRequiredForThisOperation(String action)  
 {  
       // In general, this should contain logic to identify which operations (actions)      require transaction flow.  
      [...]  
 }  
}  
  
```  
  
 L'oggetto `TransactionFlowInspector` viene passato al framework utilizzando un comportamento personalizzato, ovvero `TransactionFlowBehavior`.  
  
```  
public class TransactionFlowBehavior : IEndpointBehavior  
{  
       public void AddBindingParameters(ServiceEndpoint endpoint,            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
      {  
      }  
  
       public void ApplyClientBehavior(ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.ClientRuntime clientRuntime)  
      {  
            TransactionFlowInspector inspector = new TransactionFlowInspector();  
            clientRuntime.MessageInspectors.Add(inspector);  
      }  
  
      public void ApplyDispatchBehavior(ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.EndpointDispatcher endpointDispatcher)  
     {  
     }  
  
      public void Validate(ServiceEndpoint endpoint)  
      {  
      }  
}  
```  
  
 Con il meccanismo precedente in opera, il codice utente crea un `TransactionScope` prima di chiamare l'operazione del servizio.Il controllo messaggi assicura che la transazione venga passata al trasporto in caso debba essere propagata all'operazione del servizio.  
  
```  
CalculatorContractClient calculatorClient = new CalculatorContractClient("SampleProfileUdpBinding_ICalculatorContract");  
calculatorClient.Endpoint.Behaviors.Add(new TransactionFlowBehavior());               
  
try  
{  
       for (int i = 0; i < 5; ++i)  
      {  
              // call the 'Add' service operation under a transaction scope  
             using (TransactionScope ts = new TransactionScope())  
             {  
        [...]  
        Console.WriteLine(calculatorClient.Add(i, i * 2));  
         }  
      }               
       calculatorClient.Close();  
}  
catch (TimeoutException)  
{  
    calculatorClient.Abort();  
}  
catch (CommunicationException)  
{  
    calculatorClient.Abort();  
}  
catch (Exception)  
{  
    calculatorClient.Abort();  
    throw;  
}  
```  
  
 Al momento della ricezione di un pacchetto UDP da parte del client, il servizio lo deserializza per estrarre il messaggio e se possibile una transazione.  
  
```  
count = listenSocket.EndReceiveFrom(result, ref dummy);  
  
// read the transaction and message                       TransactionMessageBuffer.ReadTransactionMessageBuffer(buffer, count, out transaction, out msg);  
```  
  
 `TransactionMessageBuffer.ReadTransactionMessageBuffer()` è il metodo di supporto che inverte il processo di serializzazione eseguito da `TransactionMessageBuffer.WriteTransactionMessageBuffer()`.  
  
 Se una transazione è stata propagata, viene aggiunta al messaggio in `TransactionMessageProperty`.  
  
```  
message = MessageEncoderFactory.Encoder.ReadMessage(msg, bufferManager);  
  
if (transaction != null)  
{  
       TransactionMessageProperty.Set(transaction, message);  
}  
```  
  
 Ciò assicura che il dispatcher raccolga la transazione al momento della distribuzione e l'utilizzi per chiamare l'operazione del servizio indirizzata dal messaggio.  
  
#### Per impostare, compilare ed eseguire l'esempio DIBLOOK  
  
1.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
2.  L'esempio corrente funziona in modo simile all'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md).Per eseguirlo, avviare il servizio con UdpTestService.exe.Se si sta eseguendo [!INCLUDE[windowsver](../../../../includes/windowsver-md.md)], sarà necessario avviare il servizio con privilegi elevati.A tale scopo, fare clic con il pulsante destro del mouse su UdpTestService.exe in [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)], quindi scegliere **Esegui come amministratore**.  
  
3.  Si otterrà l'output seguente:  
  
    ```  
    Testing Udp From Code.  
    Service is started from code...  
    Press <ENTER> to terminate the service and start service from config...  
    ```  
  
4.  A questo punto è possibile avviare il client eseguendo UdpTestClient.exe.L'output prodotto dal client è il seguente:  
  
    ```  
    0  
    3  
    6  
    9  
    12  
    Press <ENTER> to complete test.  
    ```  
  
5.  L'output del servizio è analogo al seguente:  
  
    ```  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    The client transaction has flowed to the service  
       adding 0 + 0  
    The client transaction has flowed to the service  
       adding 1 + 2  
    The client transaction has flowed to the service  
       adding 2 + 4  
    The client transaction has flowed to the service  
       adding 3 + 6  
    The client transaction has flowed to the service  
       adding 4 + 8  
    ```  
  
6.  L'applicazione di servizio visualizza messaggio `The client transaction has flowed to the service` se può far corrispondere all'identificatore della transazione inviato dal client, nel parametro `clientTransactionId` dell'operazione `CalculatorService.Add()`, l'identificatore della transazione del servizio.Una corrispondenza viene ottenuta solo se la transazione client è stata propagata al servizio.  
  
7.  Per eseguire l'applicazione client su endpoint pubblicati utilizzando la configurazione, premere INVIO nella finestra dell'applicazione di servizio e quindi eseguire nuovamente il client di prova.Nel servizio, si dovrebbe vedere l'output seguente.  
  
    ```  
    Testing Udp From Config.  
    Service is started from config...  
    Press <ENTER> to terminate the service and exit...  
    ```  
  
8.  L'esecuzione del client sul servizio produce un output simile a quello precedente.  
  
9. Per rigenerare il codice client e la configurazione utilizzando Svcutil.exe, avviare l'applicazione del servizio, quindi eseguire i seguenti comandi Svcutil.exe dalla directory radice dell'esempio.  
  
    ```  
    svcutil http://localhost:8000/udpsample/ /reference:UdpTranport\bin\UdpTransport.dll /svcutilConfig:svcutil.exe.config  
    ```  
  
10. Si noti che Svcutil.exe non genera la configurazione dell'estensione dell'associazione per `sampleProfileUdpBinding` ma è necessario aggiungerla manualmente.  
  
    ```  
    <configuration>  
        <system.serviceModel>      
            …  
            <extensions>  
                <!-- This was added manually because svcutil.exe does not add this extension to the file -->  
                <bindingExtensions>  
                    <add name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
                </bindingExtensions>  
            </extensions>  
        </system.serviceModel>  
    </configuration>  
    ```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Transactions\TransactionMessagePropertyUDPTransport`  
  
## Vedere anche  
 [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md)