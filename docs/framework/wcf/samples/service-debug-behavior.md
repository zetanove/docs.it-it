---
title: "Comportamento di debug del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9d8fd3fb-dc39-427a-8235-336a7e7162ba
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Comportamento di debug del servizio
In questo esempio viene illustrato come configurare le impostazioni del comportamento di debug.L'esempio si bassa su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa il contratto di servizio  `ICalculator`.Questo esempio definisce in modo esplicito il comportamento di debug del servizio nel file di configurazione.Questa operazione può essere eseguita anche nel codice in modo imperativo.  
  
 In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Il file Web.config per il server definisce il comportamento di debug del servizio per attivare la pagina della Guida e la gestione delle eccezioni come illustrato nell'esempio seguente.  
  
```  
  
<behaviors>  
     <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
         <!-- WARNING: Setting includeExceptionDetailInFaults = "True" could result in leaking secured server information to the client.-->  
         <!-- Please set this to false when deploying -->  
             <serviceDebug includeExceptionDetailInFaults="True" httpHelpPageEnabled="True"/>  
         </behavior>  
     </serviceBehaviors>  
</behaviors>  
  
```  
  
 [\<debugServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md) è l'elemento di configurazione che consente di modificare le proprietà del comportamento di debug del servizio.L'utente può modificare questo comportamento per raggiungere i seguenti obiettivi:  
  
-   Questo consente al servizio di restituire qualsiasi eccezione che viene generata dal codice dell'applicazione anche se l'eccezione non è dichiarata mediante <xref:System.ServiceModel.FaultContractAttribute>.Per eseguire questa operazione si imposta `includeExceptionDetailInFaults` su `true`.Questa impostazione è utile in caso dell'esecuzione il debug di casi dove il server sta generando un'eccezione imprevista.  
  
    > [!IMPORTANT]
    >  Attivare questa impostazione in un ambiente di produzione può comportare dei rischi.Un'eccezione del server imprevista può avere alcune informazioni che non sono destinate al client, quindi impostare `includeExceptionDetailsInFaults` su `true` potrebbe comportare una perdita di informazioni.  
  
-   Il [\<debugServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md) consente inoltre agli utenti di abilitare o disabilitare la pagina della Guida.Ogni servizio può esporre facoltativamente una pagina della Guida che contiene informazioni sul servizio incluso l'endpoint ottenere WSDL per il servizio.A tale fine, impostare `httpHelpPageEnabled` su `true`.Consente di restituire la pagina della Guida a una richiesta GET all'indirizzo di base del servizio.È possibile modificare questo indirizzo impostando un altro attributo `httpHelpPageUrl`.L'operazione può essere protetta utilizzando HTTPS anziché HTTP.A tale fine, impostare `httpsHelpPageEnabled` e `httpsHelpPageUrl`.  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Le prime tre operazioni \(di addizione, sottrazione e moltiplicazione\) devono essere completate.L'ultima operazione \(di divisione\) ha esito negativo con un'eccezione di divisione per zero.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\ServiceDebug`  
  
## Vedere anche