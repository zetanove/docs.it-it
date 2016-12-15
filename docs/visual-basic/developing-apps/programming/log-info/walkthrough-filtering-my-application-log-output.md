---
title: "Procedura dettagliata: filtro dell&#39;output di My.Application.Log | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Oggetto My. log, il filtro di output"
  - "My.Application.Log (oggetto), il filtro di output"
  - "filtraggio dell'output di registro eventi dell'applicazione,"
ms.assetid: 2c0a457a-38a4-49e1-934d-a51320b7b4ca
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura dettagliata: filtro dell&#39;output di My.Application.Log
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Questa procedura dettagliata viene illustrato come modificare il log predefinito applicazione di filtri per il `My.Application.Log` oggetto, per controllare quali informazioni vengono passate dal `Log` per i listener e quali informazioni vengono scritte dai listener. È possibile modificare il comportamento di registrazione anche dopo la compilazione dell'applicazione, poiché le informazioni di configurazione vengono archiviate nel file di configurazione dell'applicazione.  
  
## <a name="getting-started"></a>Introduzione  
 Ogni messaggio che `My.Application.Log` scritture ha un livello di gravità, utilizzano i meccanismi di filtraggio per controllare l'output del log. Applicazione di esempio Usa `My.Application.Log` metodi per scrivere numerosi messaggi di log con diversi livelli di gravità.  
  
#### <a name="to-build-the-sample-application"></a>Per compilare l'applicazione di esempio  
  
1.  Aprire un nuovo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] progetto applicazione Windows.  
  
2.  Aggiungere un pulsante denominato Button1 a Form1.  
  
3.  Nel <xref:System.Windows.Forms.Control.Click> gestore eventi per Button1, aggiungere il codice seguente:  
  
     [!code-vb[VbVbcnMyApplicationLogFiltering#1](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-filtering-my-application-log-output_1.vb)]  
  
4.  Eseguire l'applicazione nel debugger.  
  
5.  Premere **Button1**.  
  
     L'applicazione scrive le informazioni seguenti al file di log e di output di debug dell'applicazione.  
  
     `DefaultSource Information: 0 : In Button1_Click`  
  
     `DefaultSource Error: 2 : Error in the application.`  
  
6.  Chiudere l'applicazione.  
  
     Per informazioni su come visualizzare una finestra di output di debug dell'applicazione, vedere [finestra di Output](/visual-studio/ide/reference/output-window). Per informazioni sulla posizione del file di log dell'applicazione, vedere [procedura dettagliata: determinazione della destinazione di scrittura delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).  
  
    > [!NOTE]
    >  Per impostazione predefinita, l'applicazione scarica l'output del file di log alla chiusura dell'applicazione.  
  
     Nell'esempio precedente, la seconda chiamata al <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A> metodo e la chiamata al <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A> genera output del log, mentre il primo e l'ultima chiamata per il `WriteEntry` metodo non. Infatti i livelli di gravità di `WriteEntry` e `WriteException` sono "Informazioni" e "Error", che sono consentiti per il `My.Application.Log` dell'oggetto predefinito il filtraggio di log. Tuttavia, gli eventi con i livelli di gravità "Start" e "Stop" non è possibile creare output di log.  
  
## <a name="filtering-for-all-myapplicationlog-listeners"></a>Il filtro per tutti i listener My.Application.Log  
 Il `My.Application.Log` viene utilizzata da object un <xref:System.Diagnostics.SourceSwitch> denominato `DefaultSwitch` per controllare quali messaggi vengono inviati dalla `WriteEntry` e `WriteException` metodi ai listener di log. È possibile configurare `DefaultSwitch` nel file di configurazione dell'applicazione impostando il relativo valore su uno del <xref:System.Diagnostics.SourceLevels> valori di enumerazione. Per impostazione predefinita, il valore è "Informazioni".  
  
 Questa tabella mostra il livello di gravità richiesto per il Log scrivere un messaggio ai listener, fornendo una particolare `DefaultSwitch` impostazione.  
  
|||  
|-|-|  
|Valore DefaultSwitch|Gravità del messaggio di richiesta per l'output|  
|`Critical`|`Critical`|  
|`Error`|`Critical` o `Error`|  
|`Warning`|`Critical`, `Error` o `Warning`|  
|`Information`|`Critical`, `Error`, `Warning` o `Information`|  
|`Verbose`|`Critical`, `Error`, `Warning`, `Information` o `Verbose`|  
|`ActivityTracing`|`Start`, `Stop`, `Suspend`, `Resume` o `Transfer`|  
|`All`|Sono consentiti tutti i messaggi.|  
|`Off`|Tutti i messaggi vengono bloccati.|  
  
> [!NOTE]
>  Il `WriteEntry` e `WriteException` i metodi hanno un overload che non specifica un livello di gravità. Il livello di gravità implicito per il `WriteEntry` overload è "Informazioni" e il livello di gravità implicito per il `WriteException` overload è "Error".  
  
 Questa tabella viene illustrato l'output di log mostrato nell'esempio precedente: con il valore predefinito `DefaultSwitch` l'impostazione di "Informazioni", solo la seconda chiamata al `WriteEntry` (metodo) e la chiamata al `WriteException` output del metodo producono log.  
  
#### <a name="to-log-only-activity-tracing-events"></a>Per registrare gli eventi di traccia solo attività  
  
1.  Fare doppio clic su app. config nel **Esplora** e selezionare **aprire**.  
  
     -oppure-  
  
     Se non è presente alcun file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.  
  
    3.  Fare clic su **Aggiungi**.  
  
2.  Individuare il `<switches>` sezione, ovvero nel `<system.diagnostics>` sezione, ovvero nel primo livello `<configuration>` sezione.  
  
3.  Trovare l'elemento che consente di aggiungere `DefaultSwitch` alla raccolta di parametri. Dovrebbe essere simile a questo elemento:  
  
     `<add name="DefaultSwitch" value="Information" />`  
  
4.  Modificare il valore di `value` attributo in "ActivityTracing".  
  
5.  Il contenuto del file app.config dovrebbe essere simile al codice XML seguente.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="ActivityTracing" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
6.  Eseguire l'applicazione nel debugger.  
  
7.  Premere **Button1**.  
  
     L'applicazione scrive le informazioni seguenti al file di log e di output di debug dell'applicazione:  
  
     `DefaultSource Start: 4 : Entering Button1_Click`  
  
     `DefaultSource Stop: 5 : Leaving Button1_Click`  
  
8.  Chiudere l'applicazione.  
  
9. Modificare il valore di `value` attributo "Informazioni".  
  
    > [!NOTE]
    >  Il `DefaultSwitch` switch impostazione controlla solo `My.Application.Log`. Non modifica il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.Diagnostics.Trace?displayProperty=fullName> e <xref:System.Diagnostics.Debug?displayProperty=fullName> comportamento delle classi.  
  
## <a name="individual-filtering-for-myapplicationlog-listeners"></a>Filtraggio individuale per i listener My.Application.Log  
 Nell'esempio precedente viene illustrato come modificare il filtro per tutti `My.Application.Log` output. In questo esempio viene illustrato come filtrare un listener di log individuali. Per impostazione predefinita, un'applicazione dispone di due listener che consentono di scrivere output di debug dell'applicazione e il file di log.  
  
 Il file di configurazione controlla il comportamento dei listener di log, consentendo di disporre di un filtro che è simile a un'opzione per ciascuno di essi `My.Application.Log`. Un listener di log verrà visualizzato un messaggio solo se la gravità del messaggio è consentita sia il log `DefaultSwitch` e filtro del listener di log.  
  
 In questo esempio viene illustrato come configurare il filtro per un nuovo listener di debug e aggiungerlo al `Log` oggetto. Il listener di debug predefinito deve essere rimossa la `Log` dell'oggetto, in modo chiaro che i messaggi di debug provengano dal nuovo listener di debug.  
  
#### <a name="to-log-only-activity-tracing-events"></a>Per registrare solo gli eventi di traccia di attività  
  
1.  Fare doppio clic su app. config nel **Esplora** e scegliere **aprire**.  
  
     -oppure-  
  
     Se non è presente alcun file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.  
  
    3.  Fare clic su **Aggiungi**.  
  
2.  Fare doppio clic su app. config in **Esplora**. Scegliere **aprire**.  
  
3.  Individuare il `<listeners>` nella sezione di `<source>` sezione con il `name` attributo "DefaultSource", che si trova il `<sources>` sezione. Il `<sources>` sezione si trova il `<system.diagnostics>` della sezione di primo livello `<configuration>` sezione.  
  
4.  Aggiungere questo elemento per il `<listeners>` sezione:  
  
    ```xml  
    <!-- Remove the default debug listener. -->  
    <remove name="Default"/>  
    <!-- Add a filterable debug listener. -->  
    <add name="NewDefault"/>  
    ```  
  
5.  Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .  
  
6.  Aggiungere l'elemento seguente alla sezione `<sharedListeners>` :  
  
    ```xml  
    <add name="NewDefault"   
         type="System.Diagnostics.DefaultTraceListener,   
               System, Version=2.0.0.0, Culture=neutral,   
               PublicKeyToken=b77a5c561934e089,   
               processorArchitecture=MSIL">  
        <filter type="System.Diagnostics.EventTypeFilter"   
                initializeData="Error" />  
    </add>  
    ```  
  
     Il <xref:System.Diagnostics.EventTypeFilter> filtro accetta uno dei valori di <xref:System.Diagnostics.SourceLevels> valori di enumerazione come relativo `initializeData` attributo.  
  
7.  Il contenuto del file app.config dovrebbe essere simile al codice XML seguente.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
              <!-- Remove the default debug listener. -->  
              <remove name="Default"/>  
              <!-- Add a filterable debug listener. -->  
              <add name="NewDefault"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="Information" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
          <add name="NewDefault"   
               type="System.Diagnostics.DefaultTraceListener,   
                     System, Version=2.0.0.0, Culture=neutral,   
                     PublicKeyToken=b77a5c561934e089,   
                     processorArchitecture=MSIL">  
            <filter type="System.Diagnostics.EventTypeFilter"   
                    initializeData="Error" />  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
8.  Eseguire l'applicazione nel debugger.  
  
9. Premere **Button1**.  
  
     L'applicazione scrive le informazioni seguenti al file di log dell'applicazione:  
  
     `Default Information: 0 : In Button1_Click`  
  
     `Default Error: 2 : Error in the application.`  
  
     L'applicazione scrive meno informazioni sull'output di debug dell'applicazione a causa di filtro più restrittivo.  
  
     `Default Error   2   Error`  
  
10. Chiudere l'applicazione.  
  
 Per ulteriori informazioni su come modificare le impostazioni del log dopo la distribuzione, vedere [utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Individuazione della posizione di inserimento delle informazioni con My.Application.log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)   
 [Procedura dettagliata: Modifica della posizione di inserimento delle informazioni con My.Application.log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [Procedura dettagliata: Creazione di listener di Log personalizzati](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)   
 [Procedura: scrivere messaggi di Log](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [Opzioni di traccia](../Topic/Trace%20Switches.md)   
 [Registrazione di informazioni dell'applicazione](../../../../visual-basic/developing-apps/programming/log-info/logging-information-from-the-application.md)