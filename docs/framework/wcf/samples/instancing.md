---
title: "Istanze | Microsoft Docs"
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
  - "Esempio di istanze [Windows Communication Foundation]"
  - "comportamenti dei servizi, esempio di istanze"
ms.assetid: c290fa54-f6ae-45a1-9186-d9504ebc6ee6
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Istanze
Nell'esempio relativo alle istanze viene descritta l'impostazione del comportamento delle istanze che controlla come vengono create le istanze di una classe del servizio in risposta alle richieste del client.  L'esempio si basa su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa il contratto di servizio `ICalculator`.  Questo esempio definisce un contratto nuovo, `ICalculatorInstance`, che eredita da `ICalculator`.  Il contratto specificato da `ICalculatorInstance` fornisce tre operazioni aggiuntive per il controllo dello stato dell'istanza del servizio.  Modificando l'impostazione delle istanze, è possibile osservare come viene modificato il comportamento quando si esegue il client.  
  
 In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Sono disponibili le modalità di istanza seguenti:  
  
-   <xref:System.ServiceModel.InstanceContextMode>: viene creata una nuova istanza del servizio per ogni richiesta del client.  
  
-   <xref:System.ServiceModel.InstanceContextMode>: viene creata una nuova istanza per ogni sessione del client e questa istanza viene mantenuta per tutta la durata della sessione \(richiede un'associazione che supporta la sessione\).  
  
-   <xref:System.ServiceModel.InstanceContextMode>: una singola istanza della classe del servizio gestisce tutte le richieste del client per la durata dell'applicazione.  
  
 La classe del servizio specifica il comportamento di istanza con l'attributo `[ServiceBehavior(InstanceContextMode=<setting>)]`, come illustrato nell'esempio di codice seguente.  Modificando quali righe vengono impostate come commento, è possibile osservare il comportamento di ognuna delle modalità dell'istanza.  Ricordarsi di ricompilare il servizio dopo avere modificato la modalità dell'istanza.  Non è necessario specificare impostazioni correlate all'istanza sul client.  
  
```  
// Enable one of the following instance modes to compare instancing behaviors.  
 [ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
  
// PerCall creates a new instance for each operation.  
//[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerCall)]  
  
// Singleton creates a single instance for application lifetime.  
//[ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
public class CalculatorService : ICalculatorInstance  
{  
    static Object syncObject = new object();  
    static int instanceCount;  
    int instanceId;  
    int operationCount;  
  
    public CalculatorService()  
    {  
        lock (syncObject)  
        {  
            instanceCount++;  
            instanceId = instanceCount;  
        }  
    }  
  
    public double Add(double n1, double n2)  
    {  
        operationCount++;  
        return n1 + n2;  
    }  
  
    public double Subtract(double n1, double n2)  
    {  
        Interlocked.Increment(ref operationCount);  
        return n1 - n2;  
    }  
  
    public double Multiply(double n1, double n2)  
    {  
        Interlocked.Increment(ref operationCount);  
        return n1 * n2;  
    }  
  
    public double Divide(double n1, double n2)  
    {  
        Interlocked.Increment(ref operationCount);  
        return n1 / n2;  
    }  
  
    public string GetInstanceContextMode()  
    {   // Return the InstanceContextMode of the service  
        ServiceHost host = (ServiceHost)OperationContext.Current.Host;  
        ServiceBehaviorAttribute behavior = host.Description.Behaviors.Find<ServiceBehaviorAttribute>();  
        return behavior.InstanceContextMode.ToString();  
    }  
  
    public int GetInstanceId()  
    {   // Return the id for this instance  
        return instanceId;  
    }  
  
    public int GetOperationCount()  
    {   // Return the number of ICalculator operations performed   
        // on this instance  
        lock (syncObject)  
        {  
            return operationCount;  
        }  
    }  
}  
  
static void Main()  
{  
    // Create a client.  
    CalculatorInstanceClient client = new CalculatorInstanceClient();  
    string instanceMode = client.GetInstanceContextMode();  
    Console.WriteLine("InstanceContextMode: {0}", instanceMode);  
    DoCalculations(client);  
  
    // Create a second client.  
    CalculatorInstanceClient client2 = new CalculatorInstanceClient();  
  
    DoCalculations(client2);  
  
    Console.WriteLine();  
    Console.WriteLine("Press <ENTER> to terminate client.");  
    Console.ReadLine();  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.  Viene visualizzata la modalità dell'istanza nel quale viene eseguito il servizio.  Dopo ogni operazione, l'ID dell'istanza e il conteggio dell'operazione vengono visualizzati per riflettere il comportamento della modalità dell'istanza.  Premere INVIO nella finestra del client per arrestare il client.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Instancing`  
  
## Vedere anche