---
title: "Misurazione dei miglioramenti dell&#39;avvio con .NET Native | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d25b24-9c1a-4b3e-9705-97ba0d6c0289
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Misurazione dei miglioramenti dell&#39;avvio con .NET Native
[!INCLUDE[net_native](../../../includes/net-native-md.md)] consente di migliorare in modo significativo il tempo di avvio delle applicazioni.  Questo miglioramento è particolarmente evidente nei dispositivi portatili a basso consumo e con app complesse.  In questo argomento viene introdotta la strumentazione di base necessaria per misurare il miglioramento dell'avvio.  
  
 Per facilitare l'analisi delle prestazioni, .NET Framework e Windows usano un framework di eventi chiamato Event Tracing for Windows \(ETW\) che consente all'app di notificare gli strumenti quando si verificano degli eventi.  È quindi possibile usare uno strumento chiamato PerfView per visualizzare e analizzare facilmente gli eventi ETW.  In questo argomento viene descritto come:  
  
-   Usare la classe <xref:System.Diagnostics.Tracing.EventSource> per creare eventi.  
  
-   Usare PerfView per raccogliere gli eventi.  
  
-   Usare PerfView per visualizzare gli eventi.  
  
## Uso di EventSource per creare eventi  
 <xref:System.Diagnostics.Tracing.EventSource> fornisce una classe base da cui creare un provider di eventi personalizzato.  In genere si crea una sottoclasse di <xref:System.Diagnostics.Tracing.EventSource> e si esegue il wrapping dei metodi `Write*` con i propri metodi di eventi.  In genere viene usato un criterio singleton per ogni <xref:System.Diagnostics.Tracing.EventSource>.  
  
 Ad esempio, la classe nel seguente esempio può essere usata per misurare due caratteristiche di prestazioni:  
  
-   L'ora di fine delle chiamate al costruttore della classe `App`.  
  
-   L'ora di fine delle chiamate al costruttore della classe `MainPage`.  
  
 [!code-csharp[ProjectN_ETW#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_etw/cs/etw1.cs#1)]  
  
 È opportuno fare alcune considerazioni.  Prima di tutto, un singleton viene creato in `AppEventSource.Log`.  Questa istanza viene usata per tutte le registrazioni.  Secondo, ogni metodo di eventi ha un <xref:System.Diagnostics.Tracing.EventAttribute>.  In questo modo, gli strumenti possono associare l'indice del metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> al metodo chiamato in `AppEventSource`.  
  
 Questi eventi sono puramente illustrativi.  La maggior parte dei codici app viene eseguita dopo questi eventi.  È necessario comprendere quali eventi nel codice corrispondono alle interazioni dell'utente, misurarli e migliorare i benchmark.  Inoltre, gli stessi eventi possono registrare una sola istanza alla volta.  Spesso, è utile disporre di una coppia di eventi di inizio e di fine per ogni operazione.  Quando si esamina l'avvio dell'app, l'evento di inizio corrisponde in genere all'evento "Processo\/Avvio" generato dal sistema operativo.  
  
 Ad esempio, si supponga di creare un lettore RSS.  Alcuni scenari interessanti per la registrazione di un evento sono:  
  
-   Quando viene eseguito il primo rendering della pagina principale.  
  
-   Quando le storie RSS obsolete vengono deserializzate dall'archivio locale.  
  
-   Quando l'app inizia la sincronizzazione con le nuove storie.  
  
-   Quando l'app termina la sincronizzazione delle nuove storie.  
  
 La strumentazione di un'app è semplice: è sufficiente chiamare il metodo appropriato nella classe derivata.  Usando `AppEventSource` dell'esempio precedente, è possibile instrumentare l'app come segue:  
  
 [!code-csharp[ProjectN_ETW#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_etw/cs/etw2.cs#2)]  
  
 Dopo la strumentazione dell'app è possibile raccogliere gli eventi.  
  
## Raccolta di eventi con PerfView  
 PerfView usa gli eventi ETW per eseguire tutti i tipi di analisi delle prestazioni sull'app.  Include anche una configurazione GUI che consente di attivare e disattivare la registrazione per i diversi tipi di eventi.  PerfView è uno strumento gratuito e può essere scaricato dall'[Area download Microsoft](http://www.microsoft.com/download/details.aspx?id=28567).  Per altre informazioni, guardare i [video delle esercitazioni di PerfView](http://channel9.msdn.com/Series/PerfView-Tutorial).  
  
> [!NOTE]
>  PerfView non consente di raccogliere eventi nei sistemi ARM.  Per raccogliere gli eventi nei sistemi ARM, usare Windows Performance Recorder \(WPR\).  Per altre informazioni, vedere il [post del blog di Vance Morrison](http://blogs.msdn.com/b/vancem/archive/2012/12/19/collecting-etw-perfview-data-on-an-windows-rt-winrt-arm-surface-device.aspx).  
  
 PerfView può essere richiamato anche dalla riga di comando.  Per registrare solo gli eventi dal provider, aprire la finestra del prompt dei comandi e digitare il comando:  
  
```  
perfview -KernelEvents:Process -OnlyProviders:*MyCompany-MyApp collect outputFile   
```  
  
 dove:  
  
 `-KernelEvents:Process`  
 Indica che si vuole sapere l'ora di inizio e di fine del processo.  È necessario l'evento Processo\/Avvio per l'app, in modo da sottrarlo al tempo associato agli altri eventi.  
  
 `-OnlyProviders:*MyCompany-MyApp`  
 Disattiva gli altri provider che PerfView attiva per impostazione predefinita e attiva il provider MyCompany\-MyApp.  L'asterisco indica che si tratta di un <xref:System.Diagnostics.Tracing.EventSource>.  
  
 `collect outputFile`  
 Indica che si vuole avviare la raccolta e salvare i dati in outputFile.etl.zip.  
  
 Eseguire l'app dopo l'avvio di PerfView.  Quando si esegue l'app, ricordare quanto segue:  
  
-   Usare una build di rilascio, non una build di debug.  Le build di debug spesso contengono codice aggiuntivo per il controllo e la gestione degli errori che può causare un rallentamento della normale esecuzione dell'app.  
  
-   L'esecuzione con un debugger collegato influisce sulle prestazioni dell'app.  
  
-   Windows usa più strategie di memorizzazione nella cache per accelerare i tempi di avvio dell'app.  Se l'app è attualmente nella memoria della cache e non deve essere caricata dal disco, viene avviata più rapidamente.  Per garantire la coerenza, avviare e chiudere l'app più volte prima della misurazione.  
  
 Dopo aver eseguito l'app per consentire a PerfView di raccogliere gli eventi creati, scegliere il pulsante **Arresta raccolta**.  In genere la raccolta deve essere arrestata prima di chiudere l'app in modo da evitare eventi estranei.  Tuttavia, se si misurano le prestazioni di arresto o di sospensione è opportuno continuare la raccolta.  
  
## Visualizzazione degli eventi  
 Per visualizzare gli eventi già raccolti, usare PerfView per aprire il file ETL o etl.zip creato e scegliere **Eventi**.  ETW avrà raccolto informazioni su numerosi eventi, inclusi quelli provenienti da altri processi.  Per concentrare l'analisi, completare le seguenti caselle di testo nella visualizzazione degli eventi:  
  
-   Nella casella del **filtro del processo**, specificare il nome dell'app \(senza ".exe"\).  
  
-   Nella casella del **filtro dei tipi di evento**, specificare `Processo/Avvio | MyCompany-MyApp`.  Viene impostato un filtro per gli eventi provenienti da MyCompany\-MyApp e l'evento Kernel Windows\/Processo\/Avvio.  
  
 Selezionare tutti gli eventi elencati nel riquadro di sinistra \(Ctrl \+ A\) e scegliere **Invio**.  A questo punto, dovrebbero essere visualizzati i timestamp di tutti gli eventi.  Questi timestamp sono relativi all'inizio della traccia, quindi è necessario sottrarre il tempo di ciascun evento dall'ora di inizio del processo per identificare il tempo trascorso dall'avvio.  Se si usa CTRL \+ clic per selezionare due timestamp, la differenza tra di essi verrà visualizzata nella barra di stato nella parte inferiore della pagina.  Questo consente di visualizzare facilmente il tempo trascorso tra due eventi nella visualizzazione \(compreso l'avvio del processo\).  È possibile aprire il menu di scelta rapida per la visualizzazione e selezionare diverse opzioni utili, ad esempio l'esportazione in file CSV o l'apertura di Microsoft Excel per salvare o elaborare i dati.  
  
 Ripetendo la procedura per l'app originale e la versione compilata usando la catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)], è possibile confrontare la differenza di prestazioni.  Le app [!INCLUDE[net_native](../../../includes/net-native-md.md)] in genere vengono avviate più rapidamente delle app non\-[!INCLUDE[net_native](../../../includes/net-native-md.md)].  Se si desidera, PerfView fornisce anche informazioni dettagliate che consentono di identificare le parti di codice che richiedono più tempo.  Per altre informazioni, guardare le [esercitazioni di PerfView](http://channel9.msdn.com/Series/PerfView-Tutorial) o leggere il [post del blog di Vance Morrison](http://blogs.msdn.com/b/vancem/archive/2011/12/28/publication-of-the-perfview-performance-analysis-tool.aspx).  
  
## Vedere anche  
 <xref:System.Diagnostics.Tracing.EventSource>