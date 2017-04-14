---
title: "Duplex | Microsoft Docs"
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
  - "Contratto di servizio duplex"
ms.assetid: bc5de6b6-1a63-42a3-919a-67d21bae24e0
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Duplex
Nell'esempio duplex viene illustrato come definire e implementare un contratto duplex.  Una comunicazione duplex ha luogo quando un client stabilisce una sessione con un servizio e fornisce a quest'ultimo un canale usabile per inviare messaggi al client.  Questo esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  Un contratto duplex è definito come una coppia di interfacce: un'interfaccia principale dal client al servizio e un'interfaccia di callback dal servizio al client.  In questo esempio, l'interfaccia `ICalculatorDuplex` consente al client di eseguire operazioni matematiche, calcolando il risultato in una sessione.  Il servizio restituisce i risultati sull'interfaccia `ICalculatorDuplexCallback`.  Poiché occorre definire un contesto per correlare il set di messaggi scambiati fra il client e il servizio, i contratti duplex richiedono una sessione.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  Il contratto duplex è definito come segue:  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required,  
                 CallbackContract=typeof(ICalculatorDuplexCallback))]  
public interface ICalculatorDuplex  
{  
    [OperationContract(IsOneWay = true)]  
    void Clear();  
    [OperationContract(IsOneWay = true)]  
    void AddTo(double n);  
    [OperationContract(IsOneWay = true)]  
    void SubtractFrom(double n);  
    [OperationContract(IsOneWay = true)]  
    void MultiplyBy(double n);  
    [OperationContract(IsOneWay = true)]  
    void DivideBy(double n);  
}  
  
public interface ICalculatorDuplexCallback  
{  
    [OperationContract(IsOneWay = true)]  
    void Result(double result);  
    [OperationContract(IsOneWay = true)]  
    void Equation(string eqn);  
}  
  
```  
  
 La classe `CalculatorService` implementa l'interfaccia `ICalculatorDuplex` primaria.  Il servizio usa la modalità di istanza <xref:System.ServiceModel.InstanceContextMode> per gestire il risultato per ogni sessione.  Una proprietà privata denominata `Callback` viene usata per far accedere il canale callback al client.  Il servizio usa il callback per inviare i messaggi al client tramite l'interfaccia callback.  
  
```  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
public class CalculatorService : ICalculatorDuplex  
{  
    double result = 0.0D;  
    string equation;  
  
    public CalculatorService()  
    {  
        equation = result.ToString();  
    }  
  
    public void Clear()  
    {  
        Callback.Equation(equation + " = " + result.ToString());  
        equation = result.ToString();  
    }  
  
    public void AddTo(double n)  
    {  
        result += n;  
        equation += " + " + n.ToString();  
        Callback.Result(result);  
    }  
    ...  
    ICalculatorDuplexCallback Callback  
    {  
        get  
        {  
            return OperationContext.Current.GetCallbackChannel<ICalculatorDuplexCallback>();  
        }  
    }  
}  
```  
  
 Il client deve fornire una classe che implementi l'interfaccia callback del contratto duplex per ricevere messaggi dal servizio.  Nell'esempio, viene definita una classe `CallbackHandler` per implementare l'interfaccia `ICalculatorDuplexCallback`.  
  
```  
public class CallbackHandler : ICalculatorDuplexCallback  
{  
   public void Result(double result)  
   {  
      Console.WriteLine("Result({0})", result);  
   }  
  
   public void Equation(string equation)  
   {  
      Console.WriteLine("Equation({0}", equation);  
   }  
}  
  
```  
  
 Il proxy che viene generato per un contratto duplex richiede che venga fornito un <xref:System.ServiceModel.InstanceContext> dopo la costruzione.  La classe <xref:System.ServiceModel.InstanceContext> viene usata come sito per un oggetto che implementa l'interfaccia di callback e gestisce i messaggi restituiti dal servizio.  Una classe <xref:System.ServiceModel.InstanceContext> viene costruita con un'istanza della classe `CallbackHandler`.  Questo oggetto gestisce i messaggi inviati dal servizio al client sull'interfaccia di callback.  
  
```  
// Construct InstanceContext to handle messages on callback interface.  
InstanceContext instanceContext = new InstanceContext(new CallbackHandler());  
  
// Create a client.  
CalculatorDuplexClient client = new CalculatorDuplexClient(instanceContext);  
  
Console.WriteLine("Press <ENTER> to terminate client once the output is displayed.");  
Console.WriteLine();  
  
// Call the AddTo service operation.  
double value = 100.00D;  
client.AddTo(value);  
  
// Call the SubtractFrom service operation.  
value = 50.00D;  
client.SubtractFrom(value);  
  
// Call the MultiplyBy service operation.  
value = 17.65D;  
client.MultiplyBy(value);  
  
// Call the DivideBy service operation.  
value = 2.00D;  
client.DivideBy(value);  
  
// Complete equation.  
client.Clear();  
  
Console.ReadLine();  
  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
  
```  
  
 La configurazione è stata modificata in modo da fornire un'associazione che supporta sia la comunicazione della sessione che la comunicazione duplex.  L'elemento `wsDualHttpBinding` supporta la comunicazione della sessione e consente la comunicazione duplex fornendo connessioni HTTP doppie, una per ogni direzione.  Nel servizio, l'unica differenza di configurazione è l'associazione usata.  Nel client, è necessario configurare un indirizzo usabile dal server per la connessione al client, come illustrato nella configurazione di esempio seguente.  
  
```  
<client>  
  <endpoint name=""  
            address="http://localhost/servicemodelsamples/service.svc"   
            binding="wsDualHttpBinding"   
            bindingConfiguration="DuplexBinding"   
            contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex" />  
</client>  
  
<bindings>  
  <!-- Configure a binding that support duplex communication. -->  
  <wsDualHttpBinding>  
    <binding name="DuplexBinding"   
             clientBaseAddress="http://localhost:8000/myClient/">  
    </binding>  
  </wsDualHttpBinding>  
</bindings>  
  
```  
  
 Quando si esegue l'esempio, vengono visualizzati i messaggi restituiti al client sull'interfaccia di callback inviata dal servizio.  Una volta completate tutte le operazioni, vengono visualizzati tutti i risultati intermedi, seguiti dall'intera equazione.  Premere INVIO per arrestare il client.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\#, C\+\+ o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
    > [!IMPORTANT]
    >  Quando si esegue il client tra più computer, assicurarsi di sostituire "localhost" sia nell'attributo `address` dell'elemento [endpoint](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) che nell'attributo `clientBaseAddress` dell'elemento [\<associazione\>](../../../../docs/framework/misc/binding.md) dell'elemento [\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md) con il nome del computer appropriato, come illustrato di seguito:  
  
    ```  
    <client>  
    <endpoint name = ""  
    address="http://service_machine_name/servicemodelsamples/service.svc"  
    ... />  
    </client>  
    ...  
    <wsDualHttpBinding>  
    <binding name="DuplexBinding" clientBaseAddress="http://client_machine_name:8000/myClient/">  
    </binding>  
    </wsDualHttpBinding>  
    ```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Duplex`  
  
## Vedere anche