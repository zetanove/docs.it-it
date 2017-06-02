---
title: "Servizio indipendente | Microsoft Docs"
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
  - "Esempio di servizio indipendente [Windows Communication Foundation]"
  - "Servizio indipendente"
ms.assetid: 05e68661-1ddf-4abf-a899-9bb1b8272a5b
caps.latest.revision: 38
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 38
---
# Servizio indipendente
In questo esempio viene illustrato come implementare un servizio indipendente in un'applicazione console.Questo esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).Il file di configurazione del servizio è stato rinominato da Web.config a App.config ed è stato modificato per configurare un indirizzo di base utilizzato dall'host.Il codice sorgente del servizio è stato modificato per implementare una funzione `Main` statica che crea e apre un host del servizio che fornisce l'indirizzo di base configurato.L'implementazione del servizio è stata modificata per scrivere l'output nella console per ogni operazione.Il client non è stato modificato, a parte la configurazione dell'indirizzo dell'endpoint corretto del servizio.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Nell'esempio viene implementata una funzione main statica per creare una classe <xref:System.ServiceModel.ServiceHost> per il tipo `CalculatorService` specificato, come illustrato nel codice seguente.  
  
```  
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Create a ServiceHost for the CalculatorService type.  
    using (ServiceHost serviceHost =   
           new ServiceHost(typeof(CalculatorService)))  
    {  
        // Open the ServiceHost to create listeners   
        // and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
    }  
}  
  
```  
  
 Quando un servizio viene ospitato in IIS \(Internet Information Services\) o WAS \(Windows Process Activation Service\), l'indirizzo di base del servizio viene fornito dall'ambiente host.Nel caso di un servizio indipendente, è necessario specificare manualmente l'indirizzo di base.Questa operazione viene eseguita utilizzando l'elemento `add`, figlio di [\<indirizziDiBase\>](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddresses.md), figlio di [\<host\>](../../../../docs/framework/configure-apps/file-schema/wcf/host.md), figlio di [\<service\>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md), come illustrato nella configurazione di esempio seguente.  
  
```  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
  ...  
</service>  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\SelfHost`  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)