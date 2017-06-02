---
title: "Sessioni affidabili WS | Microsoft Docs"
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
  - "Sessione affidabile"
ms.assetid: 86e914f2-060b-432b-bd17-333695317745
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Sessioni affidabili WS
Nell'esempio viene illustrato l'utilizzo delle sessioni affidabili.Le sessioni affidabili forniscono supporto per la messaggistica affidabile e le sessioni.La messaggistica affidabile ritenta la comunicazione in caso di errore e consente di specificare assicurazioni del recapito quali l'arrivo nell'ordine di invio dei messaggi.Le sessioni gestiscono stato per i client tra le chiamate.L'esempio implementa le sessioni per mantenere lo stato del client e specifica assicurazioni di recapito nell'ordine.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\WS\wsReliableSession`  
  
 L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.Le funzionalità di sessioni affidabili vengono abilitate e configurate nei file di configurazione dell'applicazione per il client e il servizio.  
  
 In questo esempio, il servizio è ospitato da Internet Information Services \(IIS\) e il client è un'applicazione console \(.exe\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Nell'esempio viene utilizzato il file `wsHttpBinding`.L'associazione è specificata nei file di configurazione per il client e il servizio.Il tipo di associazione è specificato nell'attributo `binding` dell'elemento endpoint, come illustrato nell'esempio di configurazione seguente.  
  
```  
<endpoint address=""  
          binding="wsHttpBinding"  
          bindingConfiguration="Binding1"   
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  
```  
  
 L'endpoint contiene l'attributo `bindingConfiguration` che fa riferimento a una configurazione di associazione denominata "Binding1". La configurazione di associazione abilita sessioni affidabili impostando l'attributo `enabled` dell'[\<sessioneAttendibile\>](../../../../docs/framework/configure-apps/file-schema/wcf/reliablesession.md) su `true`.Le garanzie di recapito per le sessioni ordinate possono essere controllate impostando l'attributo ordinato su `true` o `false`.Il valore predefinito è `true`.  
  
```  
<bindings>  
    <wsHttpBinding>  
        <binding name="Binding1">  
            <reliableSession enabled="true" />  
        </binding>  
    </wsHttpBinding>  
</bindings>  
  
```  
  
 La classe dell'implementazione del servizio implementa l'istanza <xref:System.ServiceModel.InstanceContextMode> per gestire un'istanza della classe separata per ciascun client, come mostra il codice di esempio seguente.  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)] public class CalculatorService : ICalculator  
{  
    ...  
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
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 utilizzando il comando seguente.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Verificare di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche