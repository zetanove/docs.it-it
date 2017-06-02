---
title: "Comportamento predefinito del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Esempio di comportamento predefinito di un servizio[Windows Communication Foundation]"
  - "comportamenti dei servizi, impostazioni predefinite"
ms.assetid: 442d4f71-c64e-4c62-816a-a66c38e7d3ec
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Comportamento predefinito del servizio
In questo esempio viene illustrato come configurare le impostazioni del comportamento del servizio.L'esempio si basa su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa il contratto di servizio `ICalculator`.In questo esempio vengono definiti in modo esplicito i comportamenti del servizio e i comportamenti dell'operazione utilizzando gli attributi <xref:System.ServiceModel.ServiceBehaviorAttribute> e <xref:System.ServiceModel.OperationBehaviorAttribute>.È possibile configurare i comportamenti nei file di configurazione oppure in modo imperativo nel codice, come illustrato in questo esempio.  
  
 In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 La classe del servizio specifica i comportamenti con <xref:System.ServiceModel.ServiceBehaviorAttribute> e <xref:System.ServiceModel.OperationBehaviorAttribute>, come illustrato nell'esempio di codice seguente.Tutti i valori specificati sono le impostazioni predefinite.  
  
```  
[ServiceBehavior(  
    AutomaticSessionShutdown=true,  
    ConcurrencyMode=ConcurrencyMode.Single,  
    InstanceContextMode=InstanceContextMode.PerSession,  
    IncludeExceptionDetailInFaults=false,  
    UseSynchronizationContext=true,  
    ValidateMustUnderstand=true)]  
public class CalculatorService : ICalculator  
{  
    [OperationBehavior(  
        TransactionAutoComplete=true,  
        TransactionScopeRequired=false,  
        Impersonation=ImpersonationOption.NotAllowed)]  
    public double Add(double n1, double n2)  
    {  
        System.Threading.Thread.Sleep(1600);  
        return n1 + n2;  
    }  
    ...  
}  
  
```  
  
 I comportamenti del servizio vengono specificati con l'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute>.Nella tabella seguente sono descritti alcuni di tali comportamenti.  
  
|Comportamento del servizio|Descrizione|  
|--------------------------------|-----------------|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.AutomaticSessionShutdown%2A>|Arresta automaticamente una sessione alla richiesta del client.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>|Specifica la modalità di concorrenza per ogni istanza del servizio.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>|Specifica la modalità di contesto dell'istanza.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.UseSynchronizationContext%2A>|Determina se utilizzare il contesto di sincronizzazione fornito, se impostato.Utilizzare questa proprietà quando si desidera controllare se utilizzare un `WindowsFormsSynchronizationContext` nelle applicazioni Windows Form.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A>|Determina se le eccezioni di esecuzione generali non gestite devono essere convertite in una `Fault<string>` e inviate come messaggio di errore.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A>|Specifica il livello di isolamento per le transazioni.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.ValidateMustUnderstand%2A>|Determina se intestazioni impreviste del messaggio provocano una condizione di errore.|  
  
 I comportamenti dell'operazione vengono specificati utilizzando l'attributo <xref:System.ServiceModel.OperationBehaviorAttribute>.Nella tabella seguente sono descritti alcuni di tali comportamenti.  
  
|Comportamento dell'operazione|Descrizione|  
|-----------------------------------|-----------------|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A>|Determina se il completamento dell'operazione del servizio esegue il commit della transazione corrente.|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>|Determina se l'operazione del servizio si integra in una transazione propagata dal client.|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>|Determina se l'operazione del servizio rappresenta l'identità del chiamante.|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A>|Determina se le istanze del servizio vengono riciclate all'inizio o alla fine della chiamata dell'operazione di servizio.|  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Il ritardo tra le chiamate è il risultato delle chiamate a `System.Threading.Thread.Sleep()` eseguite nelle operazioni del servizio.Gli altri esempi di comportamento illustrano questi comportamenti in maggiore dettaglio.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
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
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Default`  
  
## Vedere anche