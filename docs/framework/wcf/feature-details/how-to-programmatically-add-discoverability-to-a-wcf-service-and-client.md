---
title: "Procedura: aggiungere capacit&#224; di individuazione a un client e un servizio WCF a livello di codice | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4f7ae7ab-6fc8-4769-9730-c14d43f7b9b1
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: aggiungere capacit&#224; di individuazione a un client e un servizio WCF a livello di codice
In questo argomento viene illustrato come rendere individuabile un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. È basato sul [indipendente](http://go.microsoft.com/fwlink/?LinkId=145523) esempio.  
  
### <a name="to-configure-the-existing-self-host-service-sample-for-discovery"></a>Per configurare l'esempio di servizio indipendente esistente per l'individuazione  
  
1.  Aprire la soluzione Self-Host in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]. L'esempio si trova nella directory TechnologySamples\Basic\Service\Hosting\SelfHost.  
  
2.  Aggiungere al progetto di servizio un riferimento a `System.ServiceModel.Discovery.dll`. Potrebbe essere visualizzato un messaggio di errore a indicare che il sistema ServiceModel.Discovery.dll o una delle relative dipendenze richiede una versione successiva del [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] rispetto a quello specificato nel progetto... " Se questo messaggio viene visualizzato, fare clic sul progetto in Esplora soluzioni e scegliere **proprietà**. Nel **le proprietà del progetto** finestra, assicurarsi che il **Framework di destinazione** è [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
3.  Aprire il file Service.cs e aggiungere l'istruzione `using` seguente.  
  
    ```  
    using System.ServiceModel.Discovery;  
    ```  
  
4.  Nel `Main()` (metodo), all'interno di `using` istruzione, aggiungere un <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> istanza all'host del servizio.  
  
    ```  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService)))  
        {  
            // Add a ServiceDiscoveryBehavior  
            serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());                  
  
            // ...  
        }  
    }  
    ```  
  
     Il <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> specifica che il servizio di cui è applicato è individuabile.  
  
5.  Aggiungere un <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> all'host del servizio subito dopo il codice che aggiunge il <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>.  
  
    ```  
    // Add ServiceDiscoveryBehavior  
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
  
    // Add a UdpDiscoveryEndpoint  
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
    ```  
  
     Questo codice specifica che i messaggi di individuazione devono essere inviati all'endpoint di individuazione UDP standard.  
  
### <a name="to-create-a-client-application-that-uses-discovery-to-call-the-service"></a>Per creare un'applicazione client che utilizza l'individuazione per chiamare il servizio  
  
1.  Aggiungere alla soluzione una nuova applicazione console denominata `DiscoveryClientApp`.  
  
2.  Aggiungere un riferimento a `System.ServiceModel.dll` e `System.ServiceModel.Discovery.dll`  
  
3.  Copiare i file GeneratedClient.cs e App.config dal progetto client esistente al nuovo progetto DiscoveryClientApp. A tale scopo, fare clic sui file nel **Esplora soluzioni**, selezionare **copia**, quindi selezionare il **DiscoveryClientApp** progetto del mouse e scegliere **Incolla**.  
  
4.  Aprire Program.cs.  
  
5.  Aggiungere le istruzioni `using` riportate di seguito.  
  
    ```  
    using System.ServiceModel;  
    using System.ServiceModel.Discovery;  
    using Microsoft.ServiceModel.Samples;  
  
    ```  
  
6.  Aggiungere un metodo statico denominato `FindCalculatorServiceAddress()` alla classe `Program`.  
  
    ```  
    static EndpointAddress FindCalculatorServiceAddress()  
    {  
    }  
    ```  
  
     Questo metodo utilizza l'individuazione per cercare il servizio `CalculatorService`.  
  
7.  All'interno di `FindCalculatorServiceAddress` (metodo), creare un nuovo <xref:System.ServiceModel.Discovery.DiscoveryClient> istanza, passando un <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> al costruttore.  
  
    ```  
    static EndpointAddress FindCalculatorServiceAddress()  
    {  
        // Create DiscoveryClient  
        DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
    }  
    ```  
  
     In questo modo [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che il <xref:System.ServiceModel.Discovery.DiscoveryClient> classe deve utilizzare l'endpoint di individuazione UDP standard per inviare e ricevere messaggi di individuazione.  
  
8.  Nella riga successiva, chiamare il <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> metodo e specificare un <xref:System.ServiceModel.Discovery.FindCriteria> istanza che contiene il contratto di servizio desiderato per la ricerca. In questo caso specificare `ICalculator`.  
  
    ```  
    // Find ICalculatorService endpoints              
    FindResponse findResponse = discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
    ```  
  
9. Dopo la chiamata a <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A>, verificare se esiste almeno un servizio corrispondente e restituire il <xref:System.ServiceModel.EndpointAddress> del primo servizio corrispondente. In caso contrario, restituire `null`.  
  
    ```  
    if (findResponse.Endpoints.Count > 0)  
    {  
        return findResponse.Endpoints[0].Address;  
    }  
    else  
    {  
        return null;  
    }  
    ```  
  
10. Aggiungere un metodo statico denominato `InvokeCalculatorService` alla classe `Program`.  
  
    ```  
    static void InvokeCalculatorService(EndpointAddress endpointAddress)  
    {  
    }  
    ```  
  
     Questo metodo utilizza l'indirizzo endpoint restituito da `FindCalculatorServiceAddress` per chiamare il servizio di calcolo.  
  
11. Creare all'interno del metodo `InvokeCalculatorService` un'istanza della classe `CalculatorServiceClient`. Questa classe viene definita la [indipendente](http://go.microsoft.com/fwlink/?LinkId=145523) esempio. È stata generata utilizzando Svcutil.exe.  
  
    ```  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
    ```  
  
12. Alla riga successiva impostare l'indirizzo endpoint del client sull'indirizzo endpoint restituito da `FindCalculatorServiceAddress()`.  
  
    ```  
    // Connect to the discovered service endpoint  
    client.Endpoint.Address = endpointAddress;  
    ```  
  
13. Immediatamente dopo il codice per il passaggio precedente, chiamare i metodi esposti dal servizio di calcolo.  
  
    ```  
    Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
  
    // Call the Add service operation.  
    double result = client.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Subtract service operation.  
    result = client.Subtract(value1, value2);  
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Multiply service operation.  
    result = client.Multiply(value1, value2);  
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Divide service operation.  
    result = client.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
    Console.WriteLine();  
  
    //Closing the client gracefully closes the connection and cleans up resources  
    client.Close();  
    ```  
  
14. Aggiungere codice al metodo `Main()` nella classe `Program` per chiamare `FindCalculatorServiceAddress`.  
  
    ```  
    public static void Main()  
    {  
        EndpointAddress endpointAddress = FindCalculatorServiceAddress();  
    }  
    ```  
  
15. Alla riga successiva chiamare `InvokeCalculatorService()` e passare l'indirizzo endpoint restituito da `FindCalculatorServiceAddress()`.  
  
    ```  
    if (endpointAddress != null)  
    {  
        InvokeCalculatorService(endpointAddress);  
    }  
  
    Console.WriteLine("Press <ENTER> to exit.");  
    Console.ReadLine();  
    ```  
  
### <a name="to-test-the-application"></a>Per eseguire il test dell'applicazione  
  
1.  Aprire un prompt dei comandi con privilegi elevati ed eseguire Service.exe.  
  
2.  Aprire un prompt dei comandi ed eseguire Discoveryclientapp.exe.  
  
3.  L'output di service.exe deve essere analogo all'output indicato di seguito.  
  
    ```Output  
    Received Add(100,15.99)  
    Return: 115.99  
    Received Subtract(100,15.99)  
    Return: 84.01  
    Received Multiply(100,15.99)  
    Return: 1599  
    Received Divide(100,15.99)  
    Return: 6.25390869293308  
    ```  
  
4.  L'output di Discoveryclientapp.exe deve essere analogo all'output indicato di seguito.  
  
    ```Output  
    Invoking CalculatorService at http://localhost:8000/ServiceModelSamples/service  
    Add(100,15.99) = 115.99  
    Subtract(100,15.99) = 84.01  
    Multiply(100,15.99) = 1599  
    Divide(100,15.99) = 6.25390869293308  
  
    Press <ENTER> to exit.  
    ```  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un elenco del codice per questo esempio. Poiché questo codice si basa sul [indipendente](http://go.microsoft.com/fwlink/?LinkId=145523) esempio, vengono elencati solo i file che sono stati modificati. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]l'esempio indipendente, vedere [le istruzioni di installazione](http://go.microsoft.com/fwlink/?LinkId=145522).  
  
```  
  
// Service.cs  
using System;  
using System.Configuration;  
using System.ServiceModel;  
using System.ServiceModel.Discovery;  
  
namespace Microsoft.ServiceModel.Samples  
{  
    // See SelfHost sample for service contract and implementation  
    // ...  
  
        // Host the service within this EXE console application.  
        public static void Main()  
        {  
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService)))  
            {  
                // Add the ServiceDiscoveryBehavior to make the service discoverable  
                serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
                serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
  
                // Open the ServiceHost to create listeners and start listening for messages.  
                serviceHost.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
            }  
        }  
    }  
}  
```  
  
```  
// Program.cs  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.ServiceModel;  
using System.ServiceModel.Discovery;  
using Microsoft.ServiceModel.Samples;  
using System.Text;  
  
namespace DiscoveryClientApp  
{  
    class Program  
    {  
        static EndpointAddress FindCalculatorServiceAddress()  
        {  
            // Create DiscoveryClient  
            DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
            // Find ICalculatorService endpoints              
            FindResponse findResponse = discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
  
            if (findResponse.Endpoints.Count > 0)  
            {  
                return findResponse.Endpoints[0].Address;  
            }  
            else  
            {  
                return null;  
            }  
        }  
  
        static void InvokeCalculatorService(EndpointAddress endpointAddress)  
        {  
            // Create a client  
            CalculatorClient client = new CalculatorClient();  
  
            // Connect to the discovered service endpoint  
            client.Endpoint.Address = endpointAddress;  
  
            Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
            double value1 = 100.00D;  
            double value2 = 15.99D;  
  
            // Call the Add service operation.  
            double result = client.Add(value1, value2);  
            Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Subtract service operation.  
            result = client.Subtract(value1, value2);  
            Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Multiply service operation.  
            result = client.Multiply(value1, value2);  
            Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Divide service operation.  
            result = client.Divide(value1, value2);  
            Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
            Console.WriteLine();  
  
            //Closing the client gracefully closes the connection and cleans up resources  
            client.Close();  
        }  
        static void Main(string[] args)  
        {  
            EndpointAddress endpointAddress = FindCalculatorServiceAddress();  
  
            if (endpointAddress != null)  
            {  
                InvokeCalculatorService(endpointAddress);  
            }  
  
            Console.WriteLine("Press <ENTER> to exit.");  
            Console.ReadLine();  
  
        }  
    }  
}  
```  
  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di WCF Discovery](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [Modello a oggetti WCF Discovery](../../../../docs/framework/wcf/feature-details/wcf-discovery-object-model.md)