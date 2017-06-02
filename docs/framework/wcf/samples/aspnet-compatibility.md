---
title: "Compatibilit&#224; con ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8b51f1e-c096-4c42-ad99-0519887bbbc5
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Compatibilit&#224; con ASP.NET
In questo esempio viene illustrato come abilitare la modalità di compatibilità di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  I servizi in esecuzione nella modalità di compatibilità di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] si integrano pienamente nella pipeline dell'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e possono avvalersi delle funzionalità di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], ad esempio l'autorizzazione file\/URL, lo stato della sessione e la classe <xref:System.Web.HttpContext>.  La classe <xref:System.Web.HttpContext> consente di accedere ai cookie, alle sessioni e ad altre funzionalità di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  Questa modalità richiede che le associazioni usino il trasporto HTTP e che il servizio stesso debba essere ospitato in IIS.  
  
 In questo esempio, il client è un'applicazione console \(un file eseguibile\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
> [!NOTE]
>  Per eseguire questo esempio è necessario un pool di applicazioni di [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)].  Per creare un nuovo pool di applicazioni o modificare il pool di applicazioni predefinito, attenersi alla procedura seguente.  
>   
>  1.  Aprire il **Pannello di controllo**.  Aprire l'applet di **Strumenti di amministrazione** sotto l'intestazione **Sistema e sicurezza**.  Aprire l'applet di **Gestione Internet Information Services \(IIS\)**.  
> 2.  Espandere il TreeView nel riquadro **Connessioni**.  Selezionare il nodo **Pool di applicazioni**.  
> 3.  Per impostare il pool di applicazioni predefinito per l'uso di [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] \(che potrebbe causare problemi di incompatibilità con i siti esistenti\), fare clic con il pulsante destro del mouse sull'elemento dell'elenco **DefaultAppPool**, quindi scegliere **Impostazioni di base**.  Impostare l'elenco a discesa **Versione .NET Framework** su **.Net Framework v4.0.30128** \(o versione successiva\).  
> 4.  Per creare un nuovo pool di applicazioni che usi [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] \(per mantenere la compatibilità per altre applicazioni\), fare clic con il pulsante destro del mouse sul nodo **Pool di applicazioni**, quindi scegliere **Aggiungi pool di applicazioni**.  Assegnare un nome al nuovo pool di applicazioni e impostare l'elenco a discesa **Versione .NET Framework** su **.Net Framework v4.0.30128** \(o versione successiva\).  Dopo avere eseguito i passaggi di installazione riportati di seguito, fare clic con il pulsante destro del mouse sull'applicazione **ServiceModelSamples** e scegliere **Gestisci applicazione**, Impostazioni **avanzate**.  Impostare **Pool di applicazioni** sul nuovo pool di applicazioni.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\ASPNetCompatibility`  
  
 Questo esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), in cui viene implementato un servizio di calcolatrice.  Il contratto `ICalculator` è stato modificato al contratto `ICalculatorSession` per consentire l'esecuzione di un set di operazioni mantenendo il risultato della sessione.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculatorSession  
{  
    [OperationContract]  
    void Clear();  
    [OperationContract]  
    void AddTo(double n);  
    [OperationContract]  
    void SubtractFrom(double n);  
    [OperationContract]  
    void MultiplyBy(double n);  
    [OperationContract]  
    void DivideBy(double n);  
    [OperationContract]  
    double Result();  
}  
  
```  
  
 Usando questa funzionalità il servizio mantiene lo stato di ogni client, mentre vengono chiamate più operazioni del servizio per eseguire un calcolo.  Il client può recuperare il risultato corrente chiamando `Result` e può azzerare il risultato chiamando `Clear`.  
  
 Il servizio usa la sessione di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] per archiviare il risultato per ogni sessione client.  Questo consente al servizio di mantenere il risultato della sessione per ogni client, su più chiamate al servizio.  
  
> [!NOTE]
>  Lo stato della sessione di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e delle sessioni di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono molto diversi.  Vedere l'esempio [Sessione](../../../../docs/framework/wcf/samples/session.md) per altri dettagli sulle sessioni di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Il servizio ha una dipendenza stretta con lo stato della sessione di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e richiede che la modalità di compatibilità di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] funzioni correttamente.  Questi requisiti vengono espressi in modo dichiarativo applicando l'attributo `AspNetCompatibilityRequirements`.  
  
```  
[AspNetCompatibilityRequirements(RequirementsMode =  
                       AspNetCompatibilityRequirementsMode.Required)]  
public class CalculatorService : ICalculatorSession  
{  
    double Result  
    {  // store result in AspNet Session  
       get {  
          if (HttpContext.Current.Session["Result"] != null)  
             return (double)HttpContext.Current.Session["Result"];  
          return 0.0D;  
       }  
       set  
       {  
          HttpContext.Current.Session["Result"] = value;  
       }  
    }  
    public void Clear()  
    {  
        Result = 0.0D;  
    }  
    public void AddTo(double n)  
    {  
        Result += n;  
    }  
    public void SubtractFrom(double n)  
    {  
        Result -= n;  
    }  
    public void MultiplyBy(double n)  
    {  
        Result *= n;  
    }  
    public void DivideBy(double n)  
    {  
        Result /= n;  
    }  
    public double Result()  
    {  
        return Result;  
    }  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.  Premere INVIO nella finestra del client per arrestare il client.  
  
```  
  
0, + 100, - 50, * 17.65, / 2 = 441.25  
Press <ENTER> to terminate client.  
  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Dopo aver compilato la soluzione, eseguire Setup.bat per configurare l'applicazione ServiceModelSamples in [!INCLUDE[iisver](../../../../includes/iisver-md.md)].  La directory ServiceModelSamples verrà ora visualizzata come applicazione [!INCLUDE[iisver](../../../../includes/iisver-md.md)].  
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche  
 [Esempi di hosting e salvataggio permanente di AppFabric](http://go.microsoft.com/fwlink/?LinkId=193961)