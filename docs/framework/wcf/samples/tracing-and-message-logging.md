---
title: "Traccia e registrazione dei messaggi | Microsoft Docs"
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
  - "Analisi e registrazione"
ms.assetid: a4f39bfc-3c5e-4d51-a312-71c5c3ce0afd
caps.latest.revision: 53
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 53
---
# Traccia e registrazione dei messaggi
In questo esempio viene illustrato come attivare la traccia e la registrazione dei messaggi.Le tracce e i log dei messaggi risultanti vengono visualizzati utilizzando [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md).Questo esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
## Traccia  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizza il meccanismo di traccia definito nello spazio dei nomi <xref:System.Diagnostics>.In questo modello di traccia, i dati di traccia vengono prodotti da origini di traccia implementate dalle applicazioni.Ogni origine è identificata da un nome.Gli utenti della traccia creano listener di traccia per le origini di traccia per le quali desiderano recuperare informazioni.Per ricevere dati di traccia è necessario creare un listener per l'origine di traccia.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è possibile eseguire questa operazione aggiungendo il codice seguente al file di configurazione del servizio o del client impostando il `switchValue` dell'origine della traccia del modello di servizio:  
  
```  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-service.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>  
```  
  
 Per ulteriori informazioni sulle origini di traccia, vedere la sezione Origine di traccia nell'argomento [Configurazione delle funzionalità di traccia](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md).  
  
## Traccia e propagazione delle attività  
 Se è stata attivata la `ActivityTracing` e `propagateActivity`  è impostata su `true` in `system.ServiceModel`, le origini di traccia del client e del servizio forniscono la correlazione delle tracce all'interno di unità logiche di elaborazione \(attività\), per più attività all'interno di endpoint \(tramite trasferimenti di attività\) e per più attività che si estendono in più endpoint \(tramite la propagazione dell'ID attività\).  
  
 Questi tre meccanismi \(attività, trasferimenti e propagazione\) possono essere utili per individuare più velocemente la causa radice di un errore utilizzando Service Trace Viewer.Per ulteriori informazioni, vedere [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
 È possibile estendere la traccia fornita da ServiceModel creando tracce di attività definite dall'utente.Le tracce di attività definite dall'utente consentono all'utente di creare tracce delle attività per:  
  
-   Raggruppare le tracce in unità logiche di lavoro.  
  
-   Correlare le attività tramite trasferimenti e propagazione.  
  
-   Diminuire il costo delle prestazioni di traccia di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(ad esempio, il costo dello spazio su disco di un file di log\).  
  
 Per ulteriori informazioni sulle tracce di attività definite dall'utente, vedere l'esempio [Estensione della funzionalità di traccia](../../../../docs/framework/wcf/samples/extending-tracing.md).  
  
## Registrazione messaggi  
 La registrazione di messaggi può essere abilitata sia sul client e che sul servizio di qualsiasi applicazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per abilitare la registrazione messaggi è necessario aggiungere il codice seguente al client o al servizio:  
  
```  
<configuration>  
  <system.serviceModel>  
    <diagnostics>  
      <!-- Enable Message Logging here. -->  
      <!-- log all messages received or sent at the transport or service model levels >  
      <messageLogging logEntireMessage="true"  
                      maxMessagesToLog="300"  
                      logMessagesAtServiceLevel="true"  
                      logMalformedMessages="true"  
                      logMessagesAtTransportLevel="true" />  
    </diagnostics>  
  </system.serviceModel>  
</configuration>  
```  
  
 Quando un messaggio viene registrato, il tipo di traccia dipende da se si traccia il client o il server.Ad esempio, un messaggio "Add" inviato a un client è tracciato nella categoria "TransportWrite" sul client, mentre lo stesso messaggio è tracciato nella la categoria "TransportRead" sul servizio.  
  
 Configurare il listener di traccia aggiungendo il codice seguente alla sezione <xref:System.Diagnostics> del file App.config del client o al file Web.config del servizio:  
  
```  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-client.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
```  
  
 I messaggi vengono registrati in formato XML nella directory di destinazione specificata nel file di configurazione.  
  
> [!NOTE]
>  I file di traccia non vengono creati senza creare inizialmente la directory del log.Assicurarsi che la directory C:\\log\\ esista o specificare una directory alternativa per il log nella configurazione del listener.Per ulteriori informazioni, vedere le istruzioni di installazione iniziali alla fine di questo documento.  
  
 Per ulteriori informazioni sulla registrazione di messaggi, vedere [Configurazione della registrazione dei messaggi](../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md).  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Prima di eseguire l'esempio di Traccia e registrazione di messaggi, creare la directory C:\\log\\ in cui il servizio salva i file .svclog.Il nome di questa directory è definito nel file di configurazione come il percorso per la registrazione delle tracce e dei messaggi e può essere modificato.Assegnare all'utente accesso in scrittura al servizio di rete per la directory dei log.  
  
3.  Per compilare l'edizione C\#, C\+\+ o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Management\TracingAndLogging`  
  
## Vedere anche  
 [Traccia](../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)