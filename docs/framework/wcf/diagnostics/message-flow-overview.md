---
title: "Cenni preliminari sul flusso di messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb0899e1-84cc-4d90-b45b-dc5a50063943
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Cenni preliminari sul flusso di messaggi
In un sistema distribuito che contiene servizi interconnessi è necessario determinare relazioni causali tra i servizi.  È importante comprendere i vari componenti che appartengono a un flusso di richiesta per supportare scenari critici, ad esempio monitoraggio dello stato, risoluzione dei problemi e analisi della causa radice.  Per abilitare la correlazione di tracce tra i vari servizi, in .NET Framework 4 è stato aggiunto supporto tramite le funzionalità seguenti:  
  
-   Traccia analitica: funzionalità di traccia a prestazioni elevate e verbosità ridotta impostata in base a Event Tracing for Windows \(ETW\).  
  
-   Modello di attività end\-to\-end per i servizi WCF\/WF: questa funzionalità supporta la correlazione di tracce generate dagli spazi dei nomi <xref:System.ServiceModel> e <xref:System.WorkflowModel>.  
  
-   Rilevamento ETW per WF: questa funzionalità usa record di rilevamento generati dai servizi WF per fornire visibilità nello stato corrente e in quello di avanzamento del flusso di lavoro.  
  
 Gli errori registrati in un record di rilevamento o di traccia possono essere usati per individuare difetti del codice o messaggi in formato non corretto.  La proprietà ActivityId del nodo relativo alla correlazione nell'intestazione del messaggio dell'evento può essere usata per determinare l'attività in cui si è verificato l'errore.  Per abilitare la traccia del flusso di messaggi in base all'ID attività, vedere [Configurazione della traccia del flusso di messaggi](../../../../docs/framework/wcf/diagnostics/etw/configuring-message-flow-tracing.md).  In questo argomento viene illustrato come abilitare la traccia del flusso di messaggi nel progetto creato nell'Esercitazione introduttiva.  
  
### Per abilitare la traccia del flusso di messaggi nell'Esercitazione introduttiva  
  
1.  Fare clic sul pulsante **Start**, scegliere **Esegui**, quindi immettere `eventvwr.exe` per aprire il Visualizzatore eventi.  
  
2.  Se la traccia analitica non è stata abilitata, espandere **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.  Selezionare **Visualizza**, **Visualizza registri analitici e di debug**.  Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Attiva registro**.  Lasciare aperto il Visualizzatore eventi in modo che sia possibile visualizzare le tracce.  
  
3.  Aprire l'esempio creato in [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md) in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  So noti che è necessario eseguire [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] come amministratore in modo che sia possibile creare il servizio.  Se gli esempi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono installati, sarà possibile aprire l'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md) contenente il progetto completato creato nell'esercitazione.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto **Service**, quindi scegliere **Aggiungi**, **Nuovo elemento**.  Selezionare il modello **File di configurazione dell'applicazione**, quindi fare clic su **OK**.  
  
5.  Aggiungere il codice seguente al file App.Config creato nel passaggio precedente.  
  
    ```  
    <system.serviceModel>  
      <diagnostics>  
        <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>  
      </diagnostics>  
    </system.serviceModel>  
  
    ```  
  
6.  Premere CTRL\+F5 per eseguire l'applicazione server senza debug.  Fare clic con il pulsante destro del mouse sul progetto **Client**, quindi scegliere **Debug**, **Avvia nuova istanza** per eseguire il progetto client.  
  
7.  Per tracciare gli eventi dal client al server, aggiungere il codice seguente al file di configurazione dell'applicazione nel progetto Client.  
  
    ```  
    <diagnostics>  
      <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>  
    </diagnostics>  
  
    ```  
  
8.  In Program.cs nel client aggiungere l'istruzione Using seguente.  
  
    ```  
    using System.Diagnostics;  
  
    ```  
  
9. Nel metodo Main presente nel file program.cs del progetto client impostare il GUID della traccia in modo che venga propagato nel registro eventi.  
  
    ```  
    Guid guid = Guid.NewGuid();  
    Trace.CorrelationManager.ActivityId = guid;  
  
    ```  
  
10. Aggiornare ed esaminare il registro **Analitico** .  Cercare gli eventi con ID evento 220.  Selezionare l'evento, quindi fare clic sulla scheda **Dettagli** nel riquadro di anteprima.  Questo evento conterrà l'ID di correlazione per l'attività chiamante.  
  
    ```  
    <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" />  
    ```  
  
    > [!NOTE]
    >  Tutti gli eventi con stesso GUID in ActivityID sono correlati a una richiesta.  In questo modo è possibile correlare messaggi tra un client e un servizio specifici.  Se il client ha chiamato un altro servizio, lo stesso client potrebbe essere identificato da ActivityID.  
  
11. In alcuni casi l'elemento ActivityID può essere modificato dal GUID originale in un nuovo ActivityID.  In questo caso viene generato un evento di trasferimento.  L'ID evento è 499 e l'evento conterrà i dati seguenti nell'intestazione.  
  
    ```  
    <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">  
        <System>  
            <Provider Name="Microsoft-Windows-Application Server-Applications" Guid="{c651f5f6-1c0d-492e-8ae1-b4efd7c9d503}" />   
            <EventID>499</EventID>   
            ...  
            <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" RelatedActivityID="{85FC0930-9C49-42DA-804B-A7368104BD1B}" />   
            ...  
       </System>  
    </Event>  
    ```  
  
    > [!NOTE]
    >  L'evento di trasferimento registra la modifica dell'elemento ActivityID attivo dal GUID specificato come ActivityID al GUID specificato come RelatedActivityID.  Dopo che l'evento di trasferimento viene generato, tutti gli eventi conterranno il nuovo GUID come elemento ActivityID.