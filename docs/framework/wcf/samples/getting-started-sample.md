---
title: "Esempio della guida introduttiva | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Esempi di base [WCF], guida introduttiva"
ms.assetid: 967a3d94-0261-49ff-b85a-20bb07f1af20
caps.latest.revision: 60
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 60
---
# Esempio della guida introduttiva
Nell'esempio della guida introduttiva viene illustrato come implementare un servizio tipico e un client tipico utilizzando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Questo esempio è la base per tutti gli altri esempi di tecnologia di base.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\GettingStarted\GettingStarted`  
  
 Il servizio descrive le operazioni eseguite in un contratto di servizio che espone pubblicamente come metadati.Il servizio contiene inoltre il codice per implementare le operazioni.  
  
 Il client contiene una definizione del contratto di servizio e una classe proxy per accedere al servizio.Il codice proxy viene generato dai metadati del servizio utilizzando lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
 Su [!INCLUDE[wv](../../../../includes/wv-md.md)], il servizio è ospitato in Windows Activation Service \(WAS\).Su [!INCLUDE[wxp](../../../../includes/wxp-md.md)] e [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] è ospitato da Internet Information Services \(IIS\) e ASP.NET.Ospitare un servizio in IIS o WAS consente l'attivazione automatica del servizio quando si esegue l'accesso per la prima volta.  
  
> [!NOTE]
>  Se si desidera iniziare con un esempio che ospita il servizio in un'applicazione console anziché in IIS, vedere l'esempio [Servizio indipendente](../../../../docs/framework/wcf/samples/self-host.md).  
  
 Il servizio e il client specificano i dettagli di accesso nelle impostazioni del file di configurazione, dettagli che forniscono flessibilità al momento della distribuzione.Questi dettagli comprendono una definizione dell'endpoint che specifica un indirizzo, un associazione e un contratto.L'associazione specifica i dettagli di trasporto e di sicurezza per la modalità di accesso al servizio.  
  
 Il servizio configura un comportamento in fase di esecuzione per pubblicare i metadati.  
  
 Il servizio implementa un contratto che definisce il modello di comunicazione request\/reply.Il contratto è definito dall'interfaccia `ICalculator` che espone operazioni matematiche \(somma, sottrazione, moltiplicazione e divisione\).Il client esegue richieste a un'operazione matematica specificata e il servizio risponde fornendo il risultato.Il servizio implementa un contratto `ICalculator` definito nel codice seguente.  
  
```vb  
' Define a service contract.  
    <ServiceContract(Namespace:="http://Microsoft.Samples.GettingStarted")>  
     Public Interface ICalculator  
        <OperationContract()>  
        Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()>  
        Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()>  
        Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()>  
        Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double  
    End Interface  
  
```  
  
```csharp  
// Define a service contract.  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    [OperationContract]  
    double Subtract(double n1, double n2);  
    [OperationContract]  
    double Multiply(double n1, double n2);  
    [OperationContract]  
    double Divide(double n1, double n2);  
}  
  
```  
  
 L'implementazione del servizio calcola e restituisce il risultato appropriato, come illustrato nell'esempio di codice seguente.  
  
```vb  
' Service class which implements the service contract.  
Public Class CalculatorService  
Implements ICalculator  
Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Add  
Return n1 + n2  
End Function  
  
Public Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Subtract  
Return n1 - n2  
End Function  
  
Public Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Multiply  
Return n1 * n2  
End Function  
  
Public Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Divide  
Return n1 / n2  
End Function  
End Class  
  
```  
  
```csharp  
// Service class that implements the service contract.  
public class CalculatorService : ICalculator  
{  
    public double Add(double n1, double n2)  
    {  
        return n1 + n2;  
    }  
    public double Subtract(double n1, double n2)  
    {  
        return n1 - n2;  
    }  
    public double Multiply(double n1, double n2)  
    {  
        return n1 * n2;  
    }  
    public double Divide(double n1, double n2)  
    {  
        return n1 / n2;  
    }  
}  
  
```  
  
 Il servizio espone un endpoint per comunicare con il servizio che viene definito mediante un file di configurazione \(Web.config\), come illustrato nella configurazione di esempio seguente.  
  
```xaml  
<services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- ICalculator is exposed at the base address provided by  
         host: http://localhost/servicemodelsamples/service.svc.  -->  
       <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
       ...  
    </service>  
</services>  
  
```  
  
 Il servizio espone l'endpoint dell'indirizzo di base fornito dall'host IIS o WAS.L'associazione è configurata con una classe <xref:System.ServiceModel.WSHttpBinding> standard che fornisce comunicazione HTTP e protocolli del servizio Web standard per l'indirizzamento e la sicurezza.Il contratto rappresenta il `ICalculator` implementato dal servizio.  
  
 In questa configurazione un client sullo stesso computer può accedere al servizio da http:\/\/localhost\/servicemodelsamples\/service.svc.Affinché i client presenti nei computer remoti accedano al servizio, è necessario specificare un nome di dominio completo anziché localhost.  
  
 Per impostazione predefinita il framework non espone metadati.Per questa ragione, il servizio attiva la classe <xref:System.ServiceModel.Description.ServiceMetadataBehavior> ed espone un endpoint di scambio metadati \(MEX\) su http:\/\/localhost\/servicemodelsamples\/service.svc\/mex.Nella configurazione seguente viene illustrata questa evenienza.  
  
```xaml  
<system.serviceModel>  
  <services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      ...  
      <!-- the mex endpoint is explosed at  
       http://localhost/servicemodelsamples/service.svc/mex -->  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange" />  
    </service>  
  </services>  
  
  <!--For debugging purposes set the includeExceptionDetailInFaults  
   attribute to true-->  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <serviceMetadata httpGetEnabled="True"/>  
        <serviceDebug includeExceptionDetailInFaults="False" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
 Il client comunica utilizzando un tipo di contratto specificato mediante una classe client generata dallo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).Questo client generato è contenuto nel file generatedClient.cs o generatedClient.vb.Questa utilità recupera metadati per un servizio specificato e genera un client che viene utilizzato dall'applicazione client per comunicare utilizzando un tipo di contratto specificato.Il servizio ospitato deve essere disponibile per generare il codice client, perché il servizio viene utilizzato per recuperare i metadati aggiornati.  
  
 Eseguire il comando seguente dal prompt dei comandi SDK nella directory del client per generare il proxy tipizzato:  
  
```  
svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs  
```  
  
 Per generare il client in Visual Basic, immettere il codice seguente nel prompt dei comandi SDK:  
  
 `Svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb`  
  
 Utilizzando il client generato, il client può accedere a un endpoint del servizio specificato configurando l'indirizzo e l'associazione appropriati.Analogamente al servizio, il client utilizza un file di configurazione \(App.config\) per specificare l'endpoint con il quale desidera comunicare.La configurazione dell'endpoint client è costituita da un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto, come illustrato nell'esempio seguente.  
  
```xaml  
<client>  
     <endpoint  
         address="http://localhost/servicemodelsamples/service.svc"   
         binding="wsHttpBinding"   
         contract=" Microsoft.ServiceModel.Samples.ICalculator" />  
</client>  
  
```  
  
 L'implementazione del client crea un'istanza del client e utilizza l'interfaccia tipizzata per avviare la comunicazione con il servizio, come illustrato nell'esempio di codice seguente.  
  
```vb  
' Create a client  
Dim client As New CalculatorClient()  
  
' Call the Add service operation.  
            Dim value1 = 100.0R  
            Dim value2 = 15.99R  
            Dim result = client.Add(value1, value2)  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)  
  
' Call the Subtract service operation.  
value1 = 145.00R  
value2 = 76.54R  
result = client.Subtract(value1, value2)  
Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result)  
  
' Call the Multiply service operation.  
value1 = 9.00R  
value2 = 81.25R  
result = client.Multiply(value1, value2)  
Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result)  
  
' Call the Divide service operation.  
value1 = 22.00R  
value2 = 7.00R  
result = client.Divide(value1, value2)  
Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result)  
  
'Closing the client gracefully closes the connection and cleans up resources  
  
```  
  
```csharp  
// Create a client.  
CalculatorClient client = new CalculatorClient();  
  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
// Call the Subtract service operation.  
value1 = 145.00D;  
value2 = 76.54D;  
result = client.Subtract(value1, value2);  
Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
// Call the Multiply service operation.  
value1 = 9.00D;  
value2 = 81.25D;  
result = client.Multiply(value1, value2);  
Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
// Call the Divide service operation.  
value1 = 22.00D;  
value2 = 7.00D;  
result = client.Divide(value1, value2);  
Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
//Closing the client releases all communication resources.  
client.Close();  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
  
```  
  
 Nell'esempio della guida introduttiva viene illustrata la modalità standard per creare un servizio e un client.Altri [Di base](../../../../docs/framework/wcf/samples/basic-sample.md) si basano su questo esempio per illustrare funzionalità del prodotto specifiche.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito la  [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche  
 [Procedura: ospitare un servizio WCF in un'applicazione gestita](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)   
 [Procedura: ospitare un servizio WCF in IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)