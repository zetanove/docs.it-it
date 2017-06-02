---
title: "Pi&#249; contratti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2bef319b-fe9c-4d49-ac6c-dfb23eb35099
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Pi&#249; contratti
Nell'esempio dei contratti multipli viene illustrato come implementare più di un contratto in un servizio e come configurare gli endpoint per comunicare con ognuno dei contratti implementati.Questo esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).Il servizio è stato modificato per definire due contratti, il contratto `ICalculator` e il contratto `ICalculatorSession`.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 La classe del servizio implementa sia il contratto il servizio Web da `ICalculator` che il contratto `ICalculatorSession`.Poiché uno dei contratti richiede una sessione, il servizio utilizza la modalità dell'istanza <xref:System.ServiceModel.InstanceContextMode> per gestire lo stato per tutta la durata della sessione.  
  
 La configurazione del servizio è stata modificata per definire due endpoint allo scopo di esporre ogni contratto.L'endpoint `ICalculator` viene esposto all'indirizzo di base utilizzando `basicHttpBinding`.L'endpoint `ICalculatorSession` viene esposto all'indirizzo\/sessione di base utilizzando `wsHttpBinding` con l'attributo `bindingConfiguration` impostato su `BindingWithSession`, come illustrato nella configurazione dell'esempio seguente.  
  
```  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <!-- ICalculator endpoint is exposed using BasicBinding at the base  
       address provided by host:   
       http://localhost/servicemodelsamples/service.svc  -->  
  <endpoint address=""  
            binding="basicHttpBinding"  
            contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  <!-- ICalculatorSession endpoint is exposed using BindingWithSession  
       at {baseaddress}/session:  
       http://localhost/servicemodelsamples/service.svc/session -->  
  <endpoint address="session"  
            binding="wsHttpBinding"  
            bindingConfiguration="BindingWithSession"   
           contract="Microsoft.ServiceModel.Samples.ICalculatorSession" />  
  ...  
</service>  
  
```  
  
 Il codice client generato include ora una classe client sia per il contratto `ICalculator` originale che per il contratto `ICalculatorSession` nuovo.La configurazione client e il codice sono stati modificati per comunicare con ogni contratto all'endpoint del servizio appropriato.  
  
 Il client è un'applicazione console Windows \(con estensione exe\).Il servizio è ospitato da Internet Information Services \(IIS\).  
  
 Nella finestra della console client vengono visualizzate le operazioni inviate a ognuno degli endpoint, prima all'endpoint di base, seguito dall'endpoint protetto.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\MultipleContracts`  
  
## Vedere anche