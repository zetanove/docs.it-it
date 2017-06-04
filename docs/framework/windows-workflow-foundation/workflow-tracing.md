---
title: "Traccia del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18737989-0502-4367-b5f6-617ebfb77c96
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Traccia del flusso di lavoro
La traccia del flusso di lavoro consente di acquisire informazioni diagnostiche utilizzando i listener di traccia di .NET Framework.La traccia può essere abilitata in seguito al rilevamento di un problema con l'applicazione, quindi nuovamente disabilitata quando il problema viene risolto.Sono disponibili due modi per abilitare la traccia di debug per i flussi di lavoro:è possibile configurarla utilizzando il visualizzatore di Traccia eventi oppure utilizzare l'oggetto <xref:System.Diagnostics> per inviare eventi di traccia a un file.  
  
## Abilitazione della traccia di debug in ETW  
 Per abilitare la traccia tramite ETW, abilitare il canale Debug in Visualizzatore eventi:  
  
1.  Passare al nodo dei registri analitici e di debug in Visualizzatore eventi.  
  
2.  Nella visualizzazione ad albero in Visualizzatore eventi, passare a **Visualizzatore eventi\-\>Registri applicazioni e servizi\-\>Microsoft\-\>Windows\-\>Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Server applicazioni\-Applicazioni** e selezionare **Visualizza\-\>Visualizza registri analitici e di debug**.Fare clic con il pulsante destro del mouse su **Debug** e selezionare **Attiva log**.  
  
3.  Quando un flusso di lavoro esegue il debug e le tracce vengono create nel canale di debug ETW, queste ultime possono essere visualizzate in Visualizzatore eventi.Passare a **Visualizzatore eventi\-\>Registri applicazioni e servizi\-\>Microsoft\-\>Windows\-\>Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Debug** e scegliere **Aggiorna**.  
  
4.  La dimensione del buffer di traccia analitica predefinita è solo 4 kilobyte \(KB\). Si consiglia di aumentare la dimensione a 32 KB.A tale scopo, eseguire i passaggi seguenti.  
  
    1.  Eseguire il comando seguente nella directory del framework corrente \(ad esempio, C:\\Windows\\Microsoft.NET\\Framework\\v4.0.21203\): `wevtutil um Microsoft.Windows.ApplicationServer.Applications.man`  
  
    2.  Impostare su 32 il valore \<bufferSize\> nel file Windows.ApplicationServer.Applications.man.  
  
        ```  
        <channel name="Microsoft-Windows-Application Server-Applications/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" >  
                    <publishing>  
                      <bufferSize>32</bufferSize>  
                    </publishing>  
                  </channel>  
  
        ```  
  
    3.  Eseguire il comando seguente nella directory del framework corrente \(ad esempio, C:\\Windows\\Microsoft.NET\\Framework\\v4.0.21203\): `wevtutil im Microsoft.Windows.ApplicationServer.Applications.man`  
  
> [!NOTE]
>  Se si utilizza .NET Framework 4 Client Profile, è necessario registrare innanzitutto il manifesto ETW eseguendo il comando seguente dalla directory di .NET Framework 4: `ServiceModelReg.exe –i –c:etw`  
  
## Abilitazione della traccia di debug utilizzando System.Diagnostics  
 Questi listener possono essere configurati nel file App.config dell'applicazione flusso di lavoro o nel file Web.config per un servizio del flusso di lavoro.In questo esempio viene configurato un oggetto [TextWriterTraceListener](http://go.microsoft.com/fwlink/?LinkId=165424) per salvare le informazioni sulla traccia nel file MyTraceLog.txt nella directory corrente.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.Activities" switchValue="Information">  
        <listeners>  
          <add name="textListener" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"  
           type="System.Diagnostics.TextWriterTraceListener"  
           initializeData="MyTraceLog.txt"  
           traceOutputOptions="ProcessId, DateTime" />  
    </sharedListeners>  
    <trace autoflush="true" indentsize="4">  
      <listeners>  
        <add name="textListener" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 [Concetti di monitoraggio](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [Monitoraggio delle applicazioni](http://go.microsoft.com/fwlink/?LinkId=201275)