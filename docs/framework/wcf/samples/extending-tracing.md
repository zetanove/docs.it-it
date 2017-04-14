---
title: "Estensione della funzionalit&#224; di traccia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b971a99-16ec-4949-ad2e-b0c8731a873f
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Estensione della funzionalit&#224; di traccia
In questo esempio viene illustrato come estendere la funzionalità di traccia di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] scrivendo le tracce dell'attività definite dall'utente nel codice del client e del servizio.In questo modo l'utente può creare attività di traccia e raggruppare le tracce in unità logiche di lavoro.È anche possibile correlare le attività tramite trasferimenti \(all'interno dello stesso endpoint\) e propagazione \(attraverso diversi endpoint\).In questo esempio la traccia è abilitata sia per il client che per il servizio.Per ulteriori informazioni su come abilitare la traccia nei file di configurazione del client e del servizio, vedere [Traccia e registrazione dei messaggi](../../../../docs/framework/wcf/samples/tracing-and-message-logging.md).  
  
 Questo esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
> [!NOTE]
>  La procedura di configurazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Management\ExtendingTracing`  
  
## Traccia e propagazione delle attività  
 La traccia delle attività definita dall'utente consente all'utente di creare attività di traccia personalizzate per raggruppare le tracce in unità logiche di lavoro, correlare le attività tramite trasferimenti e propagazione, e ridurre i costi della traccia [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(ad esempio, lo spazio su disco di un file di log\).  
  
### Aggiunta di origini personalizzate  
 Le tracce definite dall'utente possono essere aggiunte sia al codice del client che al codice del servizio.L'aggiunta di origini di traccia ai file di configurazione del client o del servizio consente di registrare e visualizzare queste tracce personalizzate in [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md).Nell'esempio di codice seguente viene illustrato come aggiungere un'origine di traccia definita dall'utente denominata `ServerCalculatorTraceSource` al file di configurazione.  
  
```  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
        <source name="ServerCalculatorTraceSource" switchValue="Information,ActivityTracing">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
       <add initializeData="C:\logs\ServerTraces.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" traceOutputOptions="Callstack">  
            <filter type="" />  
        </add>  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>....  
....  
```  
  
### Correlazione di attività  
 Per correlare direttamente le attività attraverso gli endpoint, l'attributo `propagateActivity` deve essere impostato su `true` nell'origine di traccia `System.ServiceModel`.Per propagare inoltre le tracce senza passare attraverso le attività [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è necessario disattivare la traccia dell'attività ServiceModel.Tutto ciò è illustrato nell'esempio di codice seguente.  
  
> [!NOTE]
>  La disattivazione dell'attività di traccia ServiceModel non equivale a disattivare il livello di traccia, indicato dalla proprietà `switchValue`.  
  
```  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
  
    ...  
  
       </source>  
    </sources>  
</system.diagnostics>  
```  
  
### Riduzione del costo in termini di prestazioni  
 La disattivazione di `ActivityTracing` nell'origine di traccia `System.ServiceModel` genera un file di traccia che contiene solo le tracce di attività definite dall'utente, senza includere le tracce di attività ServiceModel.Di conseguenza, le dimensioni del file di log risulteranno molto più piccole.Tuttavia, si perde la possibilità per correlare le tracce di elaborazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
##### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche  
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)