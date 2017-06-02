---
title: "Impostazione predefinita dei contratti di messaggio | Microsoft Docs"
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
  - "Contratto di messaggio"
ms.assetid: 5a200b78-1a46-4104-b7fb-da6dbab33893
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# Impostazione predefinita dei contratti di messaggio
L'esempio Impostazione predefinita dei contratti di messaggio illustra un servizio in cui un messaggio personalizzato definito dall'utente viene passato da e verso le operazioni del servizio.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di interfaccia  calcolatrice.Invece delle singole operazioni del servizio singole per addizione, sottrazione, moltiplicazione e divisione utilizzate in [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), questo esempio passa un messaggio personalizzato che contiene gli operandi e l'operatore e restituisce il risultato del calcolo aritmetico.  
  
 Il client è un programma console \(estensione exe\) e la libreria \(estensione dll\) del servizio è ospitata su Internet Information Services \(IIS\).L'attività del client è visibile nella finestra della console.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Nel servizio, viene definita una sola operazione del servizio che accetta e restituisce messaggi personalizzati di tipo `MyMessage`.Benché in questo esempio i messaggi di richiesta e risposta siano dello stesso tipo, potrebbero ovviamente essere contratti di messaggio diversi se necessario.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract(Action="http://test/MyMessage_action",  
                  ReplyAction="http://test/MyMessage_action")]  
    MyMessage Calculate(MyMessage request);  
}  
  
```  
  
 Il messaggio personalizzato `MyMessage` viene definito in una classe annotata con gli attributi <xref:System.ServiceModel.MessageContractAttribute>, <xref:System.ServiceModel.MessageHeaderAttribute> e <xref:System.ServiceModel.MessageBodyMemberAttribute>.In questo esempio viene utilizzato solo il terzo costruttore.L'utilizzo dei contratti di messaggio consentono di esercitare pieno controllo sui messaggi SOAP.In questo esempio, l'attributo <xref:System.ServiceModel.MessageHeaderAttribute> viene utilizzato per inserire `Operation` in un'intestazione SOAP.Gli operandi `N1`, `N2` e `Result` appaiono all'interno del corpo SOAP perché hanno l'attributo <xref:System.ServiceModel.MessageBodyMemberAttribute> applicato.  
  
```  
[MessageContract]  
public class MyMessage  
{  
    private string operation;  
    private double n1;  
    private double n2;  
    private double result;  
  
    //Constructor - create an empty message.  
  
    public MyMessage() {}  
  
    //Constructor - create a message and populate its members.  
  
    public MyMessage(double n1, double n2, string operation,   
                     double result)  
    {  
        this.n1 = n1;  
        this.n2 = n2;  
        this.operation = operation;  
        this.result = result;  
    }  
  
    //Constructor - create a message from another message.  
  
    public MyMessage(MyMessage message)  
    {  
        this.n1 = message.n1;  
        this.n2 = message.n2;  
        this.operation = message.operation;  
        this.result = message.result;  
    }  
  
    [MessageHeader]  
    public string Operation  
    {  
        get { return operation; }  
        set { operation = value; }  
    }  
  
    [MessageBodyMember]  
    public double N1  
    {  
        get { return n1; }  
        set { n1 = value; }  
    }  
  
    [MessageBodyMember]  
    public double N2  
    {  
        get { return n2; }  
        set { n2 = value; }  
    }  
  
    [MessageBodyMember]  
    public double Result  
    {  
        get { return result; }  
        set { result = value; }  
    }  
}  
```  
  
 La classe di implementazione contiene il codice per l'operazione del servizio  `Calculate`.La classe `CalculateService` ottiene gli operandi e l'operatore dal messaggio di richiesta e crea un messaggio di risposta che contiene il risultato del calcolo richiesto, come mostra il codice di esempio seguente.  
  
```  
// Service class which implements the service contract.  
public class CalculatorService : ICalculator  
{  
    // Perform a calculation.  
  
    public MyMessage Calculate(MyMessage request)  
    {  
        MyMessage response = new MyMessage(request);  
        switch (request.Operation)  
        {  
            case "+":  
                response.Result = request.N1 + request.N2;  
                break;  
            case "-":  
                response.Result = request.N1 - request.N2;  
                break;  
            case "*":  
                response.Result = request.N1 * request.N2;  
                break;  
            case "/":  
                response.Result = request.N1 / request.N2;  
                break;  
            default:  
                response.Result = 0.0D;  
                break;  
        }  
        return response;  
    }  
}  
```  
  
 Il codice client generato per il client viene creato con lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)Lo strumento crea automaticamente i tipi di contratto del messaggio nel codice client generato se necessario.L'opzione di comando `/messageContract` può essere specificata per forzare la generazione di contratti del messaggio.  
  
```  
svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" /o:client\generatedClient.cs http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 Nell'esempio di codice seguente viene mostrato un client che utilizza il messaggio `MyMessage`.  
  
```  
// Create a client with given client endpoint configuration  
CalculatorClient client = new CalculatorClient();  
  
// Perform addition using a typed message.  
  
MyMessage request = new MyMessage();  
request.N1 = 100D;  
request.N2 = 15.99D;  
request.Operation = "+";  
MyMessage response = ((ICalculator)client).Calculate(request);  
Console.WriteLine("Add({0},{1}) = {2}", request.N1, request.N2, response.Result);  
```  
  
 Quando si esegue l'esempio, i calcoli vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
  
```  
  
 In questa fase, messaggi personalizzati definiti dall'utente vengono passati tra il client e l'operazione del servizio.Il contratto del messaggio definisce che gli operandi e risultati sono nel corpo del messaggio e che l'operatore è in un'intestazione del messaggio.La registrazione dei messaggi può essere configurata per osservare questa struttura del messaggio.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Contract\Message\Default`  
  
## Vedere anche