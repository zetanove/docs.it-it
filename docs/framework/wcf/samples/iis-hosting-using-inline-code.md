---
title: "Hosting IIS mediante il codice inline | Microsoft Docs"
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
  - "Host IIS mediante esempio di codice inline [Windows Communication Foundation]"
  - "Servizio ospitato dal Web"
ms.assetid: 56fe3687-a34b-4661-8e30-b33770f413fa
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Hosting IIS mediante il codice inline
In questo esempio viene illustrato come implementare un servizio ospitato da Internet Information Services \(IIS\), in cui il codice del servizio è contenuto inline in un file con estensione svc e viene compilato su richiesta.Il codice del servizio può anche essere implementato direttamente nei file del codice sorgente presenti nella directory \\App\_Code dell'applicazione, oppure essere compilato in assembly distribuiti in \\bin.In questo esempio non vengono illustrate tali tecniche.  
  
> [!NOTE]
>  La procedura di configurazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\InlineCode`  
  
 Nell'esempio viene illustrato un servizio tipico che implementa un contratto in cui viene definito un modello di comunicazione di tipo request\/reply.Il servizio è ospitato in IIS e il codice del servizio è interamente contenuto nel file Service.svc.Il servizio viene attivato dall'host e compilato su richiesta dal primo messaggio inviato al servizio.Non è necessaria la precompilazione.Il servizio implementa un contratto `ICalculator`, come definito nel codice seguente:  
  
```  
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
  
 L'implementazione del servizio calcola e restituisce il risultato appropriato.  
  
```  
<%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService" %>   
…  
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
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
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
  
3.  Una volta compilata la soluzione, eseguire setup.bat per configurare l'applicazione ServiceModelSamples in [!INCLUDE[iisver](../../../../includes/iisver-md.md)].La directory ServiceModelSamples verrà ora visualizzata come applicazione [!INCLUDE[iisver](../../../../includes/iisver-md.md)].  
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).Per un esempio relativo alla creazione di un'applicazione client in grado di chiamare questo servizio, vedere [Procedura: creare un client](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)