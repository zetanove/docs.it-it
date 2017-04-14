---
title: "Configurazione delle funzionalit&#224; di traccia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "analisi [WCF]"
ms.assetid: 82922010-e8b3-40eb-98c4-10fc05c6d65d
caps.latest.revision: 53
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 53
---
# Configurazione delle funzionalit&#224; di traccia
In questo argomento viene illustrato come attivare la funzionalità di traccia, configurare origini di traccia affinché vengano create tracce e impostati livelli di traccia, impostare traccia e propagazione di attività per supportare la correlazione tra tracce end\-to\-end e configurare i listener di traccia affinché accedano alle tracce.  
  
 Per consigli sulle impostazioni della funzionalità di traccia negli ambienti di produzione o debug, fare riferimento a [Impostazioni consigliate per la traccia e la registrazione dei messaggi](../../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md).  
  
> [!IMPORTANT]
>  In Windows 8 è necessario eseguire l'applicazione con privilegi elevati \(Esegui come amministratore\) affinché tramite l'applicazione in uso vengano generati log di traccia.  
  
## Abilitazione della traccia  
 Tramite [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] vengono restituiti i dati seguenti per la traccia diagnostica:  
  
-   Tracce per le attività cardine dei processi in tutti i componenti delle applicazioni, ad esempio chiamate dell'operazione, eccezioni del codice, avvisi e altri eventi di elaborazione significativi.  
  
-   Eventi di errore di Windows quando la funzionalità di traccia non viene eseguita correttamente.Vedere [Registrazione eventi](../../../../../docs/framework/wcf/diagnostics/event-logging/index.md).  
  
 La traccia di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] viene generata sulla base di <xref:System.Diagnostics>.Per utilizzare la funzionalità di traccia, è necessario definire le origini di traccia nel file di configurazione o nel codice.[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] definisce un'origine di traccia per ogni assembly [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].`System.ServiceModel` è l'origine di traccia di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] più generale e registra attività cardine di elaborazione nello stack di comunicazione di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], dall'immissione\/abbandono del trasporto all'immissione\/abbandono di codice utente.L'origine della traccia `System.ServiceModel.MessageLogging` registra tutti i messaggi che vengono propagati nel sistema.  
  
 Per impostazione predefinita, la traccia non è attivata.Per attivarla è necessario creare un listener di traccia e impostare un livello di traccia diverso da "Disattivo" per l'origine di traccia selezionata nella configurazione; in caso contrario [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] non genera tracce.Se non si specifica un listener, la traccia verrà disattivata automaticamente.Se viene definito un listener ma non è specificato alcun livello, per impostazione predefinita viene selezionato il livello "Disattivo", ovvero non viene generata alcuna traccia.  
  
 Se si utilizzano punti di estendibilità di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], ad esempio invoker di operazioni personalizzati, è necessario generare tracce proprieperché se si implementa un punto di questo tipo in [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] non è più possibile creare tracce standard nel percorso predefinito.Se non si implementa il supporto della traccia manuale creando tracce, è possibile che le tracce previste non vengano visualizzate.  
  
 È possibile configurare la funzionalità di traccia modificando il file di configurazione dell'applicazione, Web.config per applicazioni di tipo host Web o Appname.exe.config per applicazioni indipendenti.Di seguito è riportato un esempio di modifica applicabile.Per ulteriori informazioni su queste impostazioni, vedere la sezione "Configurazione dei listener di traccia per l'utilizzo di tracce".  
  
```  
<configuration>  
   <system.diagnostics>  
      <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
            <listeners>  
               <add name="traceListener"   
                   type="System.Diagnostics.XmlWriterTraceListener"   
                   initializeData= "c:\log\Traces.svclog" />  
            </listeners>  
         </source>  
      </sources>  
   </system.diagnostics>  
</configuration>  
```  
  
> [!NOTE]
>  Per modificare il file di configurazione di un progetto di servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] in [!INCLUDE[vs_current_short](../../../../../includes/vs-current-short-md.md)], fare clic con il pulsante destro del mouse sul file di configurazione, Web.config per le applicazioni ospitate da Web o Appname.exe.config per le applicazioni indipendenti, in **Esplora soluzioni**.Scegliere quindi la voce di menu di scelta rapida **Modifica configurazione WCF**.Verrà avviato [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) che consente di modificare le impostazioni di configurazione per i servizi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] tramite un'interfaccia utente grafica.  
  
## Configurazione delle origini di traccia per la generazione di tracce  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] definisce un'origine di traccia per ogni assembly.I listener definiti per tale origine accedono alle tracce generate all'interno di un assembly.Vengono definite le origini di traccia seguenti:  
  
-   System.ServiceModel: registra tutte le fasi dell'elaborazione [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], ovvero le operazioni di lettura della configurazione, l'elaborazione di un messaggio nel trasporto, l'elaborazione della protezione, l'invio di un messaggio nel codice utente e così via.  
  
-   System.ServiceModel.MessageLogging: registra tutti i messaggi propagati nel sistema.  
  
-   System.IdentityModel.  
  
-   System.ServiceModel.Activation.  
  
-   System.IO.Log: registrazione per l'interfaccia .NET Framework nel Common Log File System \(CLFS\).  
  
-   System.Runtime.Serialization: registra quando gli oggetti vengono letti o scritti.  
  
-   CardSpace.  
  
 È possibile configurare ogni origine di traccia per l'utilizzo dello stesso listener \(condiviso\), come indicato nell'esempio di configurazione seguente.  
  
```  
<configuration>  
    <system.diagnostics>  
        <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="CardSpace">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IO.Log">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.Runtime.Serialization">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IdentityModel">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
        </sources>  
  
        <sharedListeners>  
            <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\log\Traces.svclog" />  
        </sharedListeners>  
    </system.diagnostics>  
</configuration>  
```  
  
 È inoltre possibile aggiungere origini di traccia definite dall'utente, come dimostrato nell'esempio seguente, in modo che vengano create tracce di codice utente.  
  
```  
<system.diagnostics>  
   <sources>  
       <source name="UserTraceSource" switchValue="Warning, ActivityTracing" >  
          <listeners>  
              <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="C:\logs\UserTraces.svclog" />  
          </listeners>  
       </source>  
   </sources>  
   <trace autoflush="true" />   
</system.diagnostics>  
```  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] creazione di origini di traccia definite dall'utente, vedere [Estensione della funzionalità di traccia](../../../../../docs/framework/wcf/samples/extending-tracing.md).  
  
## Configurazione dei listener di traccia per l'utilizzo di tracce  
 In fase di esecuzione, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] fornisce dati di traccia ai listener che elaborano i dati.[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] fornisce vari listener predefiniti per <xref:System.Diagnostics>, diversi a livello del formato utilizzato per l'output.È inoltre possibile aggiungere tipi di listener personalizzati.  
  
 È possibile utilizzare l'istruzione `add` per specificare il nome e il tipo del listener di traccia che si desidera utilizzare.Nella configurazione di esempio, il listener viene denominato `traceListener` e viene aggiunto il listener di traccia standard di .NET Framework, ovvero `System.Diagnostics.XmlWriterTraceListener`, come tipo da utilizzare.Per ogni origine di traccia è possibile aggiungere il numero desiderato di listener.Se il listener di traccia genera la traccia in un file, nel file di configurazione è necessario specificare il percorso e il nome del file di output.A tal fine impostare `initializeData` sul nome del file per quel listener.Se non si specifica un nome file, viene generato un nome file a caso in base al tipo di listener utilizzato.Se viene utilizzato <xref:System.Diagnostics.XmlWriterTraceListener>, viene generato un nome file senza estensione.Se si implementa un listener personalizzato, è inoltre possibile utilizzare questo attributo per ricevere dati di inizializzazione diversi dal nome file.È ad esempio possibile specificare un identificatore di database per questo attributo.  
  
 È possibile configurare un listener di traccia personalizzato per l'invio di tracce in transito, ad esempio a un database remoto.I distributori di applicazioni devono applicare un apposito controllo di accesso nei log di traccia del computer remoto.  
  
 È inoltre possibile configurare un listener di traccia a livello di programmazione.[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][Procedura: creare e inizializzare listener di analisi](http://go.microsoft.com/fwlink/?LinkId=94648) e [Creazione di un listener di analisi personalizzato](http://go.microsoft.com/fwlink/?LinkId=96239) \(il contenuto potrebbe essere in inglese\).  
  
> [!CAUTION]
>  Poiché `System.Diagnostics.XmlWriterTraceListener` non è thread\-safe, è possibile che l'origine di traccia blocchi le risorse in modo esclusivo durante la restituzione di tracce.Quando molti thread restituiscono tracce a un'origine configurata per l'utilizzo di questo listener, può verificarsi un conflitto di risorse con conseguente calo delle prestazioni.Per risolvere il problema, è necessario implementare un listener personalizzato di tipo thread\-safe.  
  
## Livello di traccia  
 Il livello di traccia viene controllato in base all'impostazione `switchValue` dell'origine di traccia.Nella tabella seguente viene fornita una descrizione dei livelli di traccia disponibili.  
  
|Livello di traccia|Natura degli eventi registrati|Contenuto degli eventi registrati|Eventi registrati|Destinazione utente|  
|------------------------|------------------------------------|---------------------------------------|-----------------------|-------------------------|  
|Off|N\/D|N\/D|Non vengono create tracce.|N\/D|  
|Critico|Eventi "negativi": eventi che indicano un'elaborazione imprevista o una condizione di errore.||Vengono registrate eccezioni non gestite comprese le seguenti:<br /><br /> -   OutOfMemoryException<br />-   ThreadAbortException \(il CLR richiama qualsiasi ThreadAbortExceptionHandler\)<br />-   StackOverflowException \(non intercettabile\)<br />-   ConfigurationErrorsException<br />-   SEHException<br />-   Errori di avvio di applicazione<br />-   Eventi FailFast<br />-   Il sistema si blocca<br />-   Messaggi non elaborabili: tracce di messaggi che determinano il blocco dell'applicazione.|Amministratori<br /><br /> Sviluppatori di applicazioni|  
|Error|Eventi "negativi": eventi che indicano un'elaborazione imprevista o una condizione di errore.|Si è verificata un'elaborazione imprevista.L'applicazione non è stata in grado di eseguire un'attività come previsto.L'applicazione, tuttavia, è ancora in esecuzione.|Vengono registrate tutte le eccezioni.|Amministratori<br /><br /> Sviluppatori di applicazioni|  
|Avviso|Eventi "negativi": eventi che indicano un'elaborazione imprevista o una condizione di errore.|Un possibile problema si è verificato o potrebbe verificarsi, ma l'applicazione funziona ancora correttamente.Tuttavia, potrebbe smettere di farlo.|-   L'applicazione riceve più richieste di quanto sia consentito dalle impostazioni di limitazione.<br />-   La coda di ricezione ha quasi raggiunto la capacità massima configurata.<br />-   Tempo scaduto.<br />-   Le credenziali sono rifiutate.|Amministratori<br /><br /> Sviluppatori di applicazioni|  
|Informazioni|Eventi "positivi": eventi che contrassegnano attività cardine eseguite correttamente.|Attività cardine importanti e corrette di esecuzione dell'applicazione, indipendentemente dal funzionamento corretto o non corretto dell'applicazione.|In generale il sistema genera messaggi informativi utili per il monitoraggio e la diagnosi dello stato di sistema, la valutazione delle prestazioni o il profiling.È possibile utilizzare queste informazioni per la pianificazione della capacità e la gestione delle prestazioni:<br /><br /> -   Vengono creati canali.<br />-   Vengono creati listener di endpoint.<br />-   Il messaggio entra o abbandona il trasporto.<br />-   Il token di sicurezza viene recuperato.<br />-   L'impostazione di configurazione viene letta.|Amministratori<br /><br /> Sviluppatori di applicazioni<br /><br /> Sviluppatori di prodotti|  
|Verbose|Eventi "positivi": eventi che contrassegnano attività cardine eseguite correttamente.|Vengono generati eventi di basso livello per codice utente e manutenzione.|In genere è possibile utilizzare questo livello per il debug o l'ottimizzazione dell'applicazione.<br /><br /> -   L'intestazione del messaggio è stata intesa.|Amministratori<br /><br /> Sviluppatori di applicazioni<br /><br /> Sviluppatori di prodotti|  
|ActivityTracing||Eventi di flusso tra attività di elaborazione e componenti.|Questo livello consente ad amministratori e sviluppatori di mettere in correlazione applicazioni nello stesso dominio applicazione:<br /><br /> -   Tracce per limiti di attività, ad esempio start\/stop.<br />-   Tracce per trasferimenti.|Tutto|  
|Tutto||L'applicazione può funzionare correttamente.Vengono generati tutti gli eventi.|Tutti gli eventi precedenti.|Tutto|  
  
 I livelli da Dettagliato a Critico sono inclusi l'uno dentro l'altro, ovvero ogni livello di traccia comprende tutti i livelli che lo precedono ad eccezione del livello Disattivo.Un listener in ascolto al livello Avviso, ad esempio, riceve le tracce Critico, Errore e Avviso.Il livello Tutto comprende gli eventi da Dettagliato a Critico ed eventi di Traccia attività.  
  
> [!CAUTION]
>  I livelli Informazioni, Dettagliato e ActivityTracing generano molte tracce che possono influire negativamente sulla velocità effettiva dei messaggi se tutte le risorse disponibili nel computer sono esaurite.  
  
## Configurazione della traccia e della propagazione di attività a fini di correlazione  
 Il valore `activityTracing` specificato per l'attributo `switchValue` consente di attivare la traccia di attività, che genera tracce per limiti e trasferimenti di attività all'interno di endpoint.  
  
> [!NOTE]
>  Quando si utilizzano determinate funzioni di estensibilità in [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], potrebbe venire generata la classe <xref:System.NullReferenceException> se la traccia attività è attiva.Per risolvere questo problema, controllare il file di configurazione dell'applicazione e verificare che l'attributo `switchValue` per l'origine di traccia non sia impostato su `activityTracing`.  
  
 L'attributo `propagateActivity` indica se l'attività deve essere propagata ad altri endpoint che partecipano nello scambio di messaggi.Impostando questo valore su `true`, è possibile osservare file di traccia generati da due endpoint qualsiasi e notare come un set di tracce in un endpoint venga propagato a un set di tracce in un altro endpoint.  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] traccia e propagazione di attività, vedere [Propagazione](../../../../../docs/framework/wcf/diagnostics/tracing/propagation.md).  
  
 Entrambi i valori booleani `propagateActivity`and `ActivityTracing` si applicano a System.ServiceModel TraceSource.Il valore `ActivityTracing` si applica inoltre a qualsiasi origine di traccia, comprese le origini di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] o quelle definite dall'utente.  
  
 Non è possibile utilizzare l'attributo `propagateActivity` con le origini di traccia definite dall'utente.Per la propagazione di ID attività di codice utente, accertarsi di non impostare l'attributo `ActivityTracing` di ServiceModel, mantenendo l'attributo `propagateActivity` di ServiceModel impostato su `true`.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [Procedura: creare e inizializzare listener di traccia](http://go.microsoft.com/fwlink/?LinkId=94648)   
 [Creazione di un TraceListener personalizzato](http://go.microsoft.com/fwlink/?LinkId=96239)