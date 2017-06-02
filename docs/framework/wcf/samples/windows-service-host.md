---
title: "Host del servizio Windows | Microsoft Docs"
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
  - "Servizio NT"
  - "Esempio di host del servizio NT [Windows Communication Foundation]"
ms.assetid: 1b2f45c5-2bed-4979-b0ee-8f9efcfec028
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Host del servizio Windows
In questo esempio viene illustrato un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] ospitato in un servizio Windows gestito.I servizi Windows vengono controllati mediante l'applet Servizi nel **Pannello di controllo** e possono essere configurati per l'avvio automatico dopo un riavvio del sistema.L'esempio è costituito da un programma client e da un programma di Servizio Windows.Il servizio viene implementato come programma con estensione exe e contiene il proprio codice di hosting.In altri ambienti host, quali ad esempio il servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\) o Internet Information Services \(IIS\), non è necessario scrivere codice di hosting.  
  
> [!NOTE]
>  La procedura di configurazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WindowsService`  
  
 Dopo aver compilato questo servizio, è necessario installarlo con l'utilità Installutil.exe come qualsiasi altro servizio Windows.Se si apportano modifiche al servizio, è prima necessario arrestarlo con `installutil /u`.I file Setup.bat e Cleanup.bat inclusi in questo esempio sono i comandi per installare e avviare il servizio Windows e per arrestarlo e disinstallarlo.Il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può rispondere ai client solo se il servizio Windows è in esecuzione.Se si arresta il servizio Windows utilizzando l'applet Servizi dal **Pannello di controllo** e si esegue il client, si verifica un'eccezione <xref:System.ServiceModel.EndpointNotFoundException> quando un client tenta di accedere al servizio.Se si riavvia il servizio Windows e si esegue di nuovo il client, la comunicazione ha esito positivo.  
  
 Il codice del servizio include una classe Installer, ovvero una classe di implementazione del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che implementa il contratto ICalculator, e una classe del servizio Windows che funge da host di runtime.La classe Installer, che eredita da <xref:System.Configuration.Install.Installer>, consente di installare il programma come servizio NT mediante lo strumento Installutil.exe.La classe di implementazione del servizio, `WcfCalculatorService`, è un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che implementa un contratto di servizio di base.Questo servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ospitato in una classe del servizio Windows denominata `WindowsCalculatorService`.Per essere qualificata come un servizio Windows, la classe eredita da <xref:System.ServiceProcess.ServiceBase> e implementa i metodi [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> e <xref:System.ServiceProcess.ServiceBase.OnStop>.In [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>, viene creato un oggetto <xref:System.ServiceModel.ServiceHost> per il tipo `WcfCalculatorService` e viene aperto.In <xref:System.ServiceProcess.ServiceBase.OnStop>, ServiceHost viene chiuso chiamando il metodo <xref:System.ServiceModel.Channels.CommunicationObject.Close%28System.TimeSpan%29> dell'oggetto <xref:System.ServiceModel.ServiceHost>.L'indirizzo di base dell'host viene configurato utilizzando l'elemento [\<aggiunta\>](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddresses.md), che è un elemento figlio dell'elemento [\<indirizziDiBase\>](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddresses.md), a sua volta figlio dell'elemento [\<host\>](../../../../docs/framework/configure-apps/file-schema/wcf/host.md), il quale è figlio dell'elemento [\<service\>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md).  
  
 L'endpoint definito utilizza l'indirizzo di base e un [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).Nell'esempio seguente viene mostrata la configurazione dell'indirizzo di base e l'endpoint che espone CalculatorService.  
  
```  
<services>  
  <service name="Microsoft.ServiceModel.Samples.WcfCalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    <host>  
      <baseAddresses>  
        <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
      </baseAddresses>  
    </host>  
    <!-- This endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service.  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Dopo che la soluzione è stata compilata, eseguire Setup.bat da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi elevati per installare il servizio Windows con lo strumento Installutil.exe.Il servizio viene visualizzato in Servizi.  
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)