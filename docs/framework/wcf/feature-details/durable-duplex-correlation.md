---
title: "Correlazione duplex durevole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8eb0e49a-6d3b-4f7e-a054-0d4febee2ffb
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Correlazione duplex durevole
La correlazione duplex durevole, nota anche come correlazione di callback, risulta utile se un servizio flusso di lavoro dispone del requisito adatto a inviare un callback al chiamante iniziale.A differenza del duplex WCF, il callback si può verificare in qualsiasi momento nel futuro e non è legato allo stesso canale o al canale di durata. L'unico requisito è costituito dal fatto che il chiamante dispone di un endpoint attivo in ascolto del messaggio di callback.In questo modo due servizi flusso di lavoro possono comunicare in una conversazione prolungata.In questo argomento vengono forniti cenni preliminari sulla correlazione duplex durevole.  
  
## Utilizzo della correlazione duplex durevole  
 Per utilizzare la correlazione duplex durevole, i due servizi devono utilizzare un'associazione abilitata per il contesto che supporta operazioni bidirezionali, ad esempio <xref:System.ServiceModel.NetTcpContextBinding> o <xref:System.ServiceModel.WSHttpContextBinding>.Il servizio chiamante registra un <xref:System.ServiceModel.WSHttpContextBinding.ClientCallbackAddress%2A> con l'associazione desiderata sul client <xref:System.ServiceModel.Endpoint>.Il servizio ricevente riceve questi dati nella chiamata iniziale, quindi li utilizza sul proprio <xref:System.ServiceModel.Endpoint> nell'attività <xref:System.ServiceModel.Activities.Send> che effettua nuovamente la chiamata al servizio chiamante.In questo esempio, due servizi comunicano l'uno con l'altro.Il primo servizio richiama un metodo nel secondo servizio, quindi attende una risposta.Il secondo servizio conosce il nome del metodo di callback, ma l'endpoint del servizio che implementa questo metodo non è noto in fase di progettazione.  
  
> [!NOTE]
>  La correlazione duplex durevole può essere utilizzata soltanto quando <xref:System.ServiceModel.Channels.AddressingVersion> dell'endpoint è configurato con <xref:System.ServiceModel.Channels.AddressingVersion.WSAddressing10%2A>.In caso contrario, viene generata un'eccezione <xref:System.InvalidOperation> con il messaggio seguente: "Il messaggio contiene un'intestazione del contesto di callback con un riferimento dell'endpoint per AddressingVersion "Addressing200408 \(http:\/\/schemas.xmlsoap.org\/ws\/2004\/08\/addressing\)".Il contesto di callback può essere trasmesso solo quando AddressingVersion è configurato con 'WSAddressing10'".  
  
 Nell'esempio seguente viene ospitato un servizio flusso di lavoro che crea un <xref:System.ServiceModel.Endpoint> del callback mediante <xref:System.ServiceModel.WSHttpContextBinding>.  
  
```csharp  
// Host WF Service 1.  
string baseAddress1 = "http://localhost:8080/Service1";  
WorkflowServiceHost host1 = new WorkflowServiceHost(GetWF1(), new Uri(baseAddress1));  
  
// Add the callback endpoint.  
WSHttpContextBinding Binding1 = new WSHttpContextBinding();  
host1.AddServiceEndpoint("ICallbackItemsReady", Binding1, "ItemsReady");  
  
// Add the service endpoint.  
host1.AddServiceEndpoint("IService1", Binding1, baseAddress1);  
  
// Open the first workflow service.  
host1.Open();  
Console.WriteLine("Service1 waiting at: {0}", baseAddress1);  
```  
  
 Il flusso di lavoro che implementa questo servizio flusso di lavoro inizializza la correlazione di callback con l'attività <xref:System.ServiceModel.Activities.Send> e fa riferimento a questo endpoint di callback dall'attività <xref:System.ServiceModel.Activities.Receive> correlata all'elemento <xref:System.ServiceModel.Activities.Send>.Nell'esempio seguente viene rappresentato il flusso di lavoro restituito dal metodo `GetWF1`.  
  
```csharp  
Variable<CorrelationHandle> CallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = "IService1",  
    OperationName = "StartOrder"  
};  
  
Send GetItems = new Send  
{  
    CorrelationInitializers =   
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = CallbackHandle  
        }  
    },  
    ServiceContractName = "IService2",  
    OperationName = "StartItems",  
    Endpoint = new Endpoint  
    {  
        AddressUri = new Uri("http://localhost:8081/Service2"),  
        Binding = new WSHttpContextBinding  
        {  
            ClientCallbackAddress = new Uri("http://localhost:8080/Service1/ItemsReady")                          
        }  
    }  
};  
  
Receive ItemsReady = new Receive  
{  
    ServiceContractName = "ICallbackItemsReady",  
    OperationName = "ItemsReady",  
    CorrelatesWith = CallbackHandle,  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        CallbackHandle  
    },  
    Activities =  
    {  
        StartOrder,  
        new WriteLine  
        {  
            Text = "WF1 - Started"  
        },  
        GetItems,  
        new WriteLine  
        {  
            Text = "WF1 - Request Submitted"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF1 - Items Received"  
        }  
     }  
};  
```  
  
 Il secondo servizio flusso di lavoro viene ospitato utilizzando un'associazione fornita dal sistema e basata sul contesto.  
  
```csharp  
// Host WF Service 2.  
string baseAddress2 = "http://localhost:8081/Service2";  
WorkflowServiceHost host2 = new WorkflowServiceHost(GetWF2(), new Uri(baseAddress2));  
  
// Add the service endpoint.  
WSHttpContextBinding Binding2 = new WSHttpContextBinding();  
host2.AddServiceEndpoint("IService2", Binding2, baseAddress2);  
  
// Open the second workflow service.  
host2.Open();  
Console.WriteLine("Service2 waiting at: {0}", baseAddress2);  
```  
  
 Il flusso di lavoro che implementa questo servizio flusso di lavoro inizia con un'attività <xref:System.ServiceModel.Activities.Receive>.Questa attività di ricezione inizializza la correlazione di callback per questo servizio, ritarda per un periodo di tempo al fine di simulare un lavoro dall'esecuzione prolungata, quindi esegue una nuova chiamata nel primo servizio utilizzando il contesto di callback passato nella prima chiamata nel servizio.Nell'esempio seguente viene rappresentato il flusso di lavoro restituito da una chiamata a `GetWF2`.L'attività <xref:System.ServiceModel.Activities.Send> dispone di un indirizzo del segnaposto `http://www.contoso.com`. L'indirizzo effettivo utilizzato al runtime coincide con l'indirizzo di callback fornito.  
  
```csharp  
Variable<CorrelationHandle> ItemsCallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartItems = new Receive  
{  
    CorrelationInitializers =   
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = ItemsCallbackHandle  
        }  
    },  
    CanCreateInstance = true,  
    ServiceContractName = "IService2",  
    OperationName = "StartItems"  
};  
  
Send ItemsReady = new Send  
{  
    CorrelatesWith = ItemsCallbackHandle,  
    Endpoint = new Endpoint  
    {  
        // The callback address on the binding is used  
        // instead of this placeholder address.  
        AddressUri = new Uri("http://www.contoso.com"),  
  
        Binding = new WSHttpContextBinding()  
    },  
    OperationName = "ItemsReady",  
    ServiceContractName = "ICallbackItemsReady"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        ItemsCallbackHandle  
    },  
    Activities =  
    {  
        StartItems,  
        new WriteLine  
        {  
            Text = "WF2 - Request Received"  
        },  
        new Delay  
        {  
            Duration = TimeSpan.FromMinutes(90)  
        },  
        new WriteLine  
        {  
            Text = "WF2 - Sending items"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF2 - Items sent"  
        }  
     }  
};  
```  
  
 Quando il metodo `StartOrder` viene richiamato nel primo flusso di lavoro, viene visualizzato l'output seguente che indica il flusso di esecuzione tramite i due flussi di lavoro.  
  
```Output  
Service1 waiting at: http://localhost:8080/Service1  
Service2 waiting at: http://localhost:8081/Service2  
Press enter to exit.   
WF1 - Started  
WF2 - Request Received  
WF1 - Request Submitted  
WF2 - Sending items  
WF2 - Items sent  
WF1 - Items Received  
  
```  
  
 In questo esempio, entrambi i flussi di lavoro gestiscono in modo esplicito la correlazione mediante un <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer>.Poiché in questi flussi di lavoro di esempio era presente una sola correlazione, sarebbe stata sufficiente la gestione di <xref:System.ServiceModel.Activities.CorrelationHandle> predefinita.  
  
## Vedere anche  
 [Duplex durevole &#91;Esempi WF&#93;](../../../../docs/framework/windows-workflow-foundation/samples/durable-duplex.md)