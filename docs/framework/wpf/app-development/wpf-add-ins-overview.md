---
title: "Cenni preliminari sui componenti aggiuntivi di WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework (modello di componente aggiuntivo) [WPF]"
  - "componenti aggiuntivi [WPF], architettura"
  - "componenti aggiuntivi [WPF], vantaggi"
  - "componenti aggiuntivi [WPF], limiti"
  - "componenti aggiuntivi [WPF], prestazioni"
  - "componenti aggiuntivi [WPF], interfaccia utente"
  - "componenti aggiuntivi e interfaccia utente [WPF]"
  - "componenti aggiuntivi e applicazioni browser XAML [WPF]"
  - "componenti aggiuntivi (panoramica) [WPF]"
ms.assetid: 00b4c776-29a8-4dba-b603-280a0cdc2ade
caps.latest.revision: 36
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 35
---
# Cenni preliminari sui componenti aggiuntivi di WPF
<a name="Introduction"></a> [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] include un modello di componente aggiuntivo utilizzabile dagli sviluppatori per creare applicazioni che supportano l'estensibilità mediante componenti aggiuntivi.  Questo modello consente di creare componenti aggiuntivi che integrano ed estendono le funzionalità dell'applicazione.  In alcuni scenari, le applicazioni devono anche visualizzare le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] fornite dai componenti aggiuntivi.  In questo argomento viene illustrato come [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] integra il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per consentire i suddetti scenari, oltre all'architettura di base, i vantaggi e le limitazioni.  
  
   
  
<a name="Requirements"></a>   
## Prerequisiti  
 È richiesta una buona conoscenza del modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  Per ulteriori informazioni, vedere [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml).  
  
<a name="AddInsOverview"></a>   
## Cenni preliminari sui componenti aggiuntivi  
 Al fine di evitare le complessità dovute alla ricompilazione e ridistribuzione di un'applicazione per incorporare nuove funzionalità, le applicazioni implementano meccanismi di estensibilità che consentono agli sviluppatori del produttore e di terze parti di creare altre applicazioni di integrazione.  Il metodo più comune per supportare questo tipo di estensibilità consiste nell'utilizzo di componenti aggiuntivi, noti anche come "plug\-in".  Di seguito vengono riportati alcuni esempi di applicazioni reali che espongono l'estensibilità mediante componenti aggiuntivi:  
  
-   Componenti aggiuntivi Internet Explorer  
  
-   Plug\-in Windows Media Player  
  
-   Componenti aggiuntivi Visual Studio  
  
 Il modello di componente aggiuntivo Windows Media Player, ad esempio, consente agli sviluppatori di terze parti di implementare "plug\-in" che estendono Windows Media Player in diversi modi, incluso creando decodificatori e codificatori per formati multimediali non supportati a livello nativo da Windows Media Player \(ad esempio DVD, MP3\), effetti audio e interfacce.  Ogni modello di componente aggiuntivo viene compilato per esporre le funzionalità univoche di un'applicazione, benché vi siano diverse entità e comportamenti comuni a tutti i modelli.  
  
 Le tre entità principali delle soluzioni tipiche di estensibilità mediante componenti aggiuntivi sono *contratti*, *componenti aggiuntivi* e *applicazioni host*.  I contratti definiscono la modalità di integrazione dei componenti aggiuntivi con le applicazioni host in due modi:  
  
-   I componenti aggiuntivi vengono integrati con le funzionalità implementate dalle applicazioni host.  
  
-   Le applicazioni host espongono le funzionalità con cui i componenti aggiuntivi vengono integrati.  
  
 Per poter utilizzare i componenti aggiuntivi, occorre che questi vengano individuati e caricati dalle applicazioni host in fase di esecuzione.  Di conseguenza, le applicazioni che supportano i componenti aggiuntivi sono responsabili di quanto segue:  
  
-   **Individuazione**, ovvero cercare i componenti aggiuntivi conformi ai contratti supportati dalle applicazioni host.  
  
-   **Attivazione**, ovvero caricare, eseguire e stabilire la comunicazione con i componenti aggiuntivi.  
  
-   **Isolamento**, ovvero utilizzare i processi o domini dell'applicazione per stabilire i limiti di isolamento che proteggono le applicazioni da potenziali problemi di sicurezza e di esecuzione dovuti ai componenti aggiuntivi.  
  
-   **Comunicazione**, ovvero consentire ai componenti aggiuntivi di comunicare con le applicazioni host oltre i limiti di isolamento, mediante la chiamata a metodi e il passaggio di dati.  
  
-   **Gestione della durata**, ovvero caricare e scaricare processi e domini dell'applicazione in modo netto e prevedibile; vedere in proposito [Domini applicazione](../../../../docs/framework/app-domains/application-domains.md).  
  
-   **Controllo delle versioni**, ovvero accertare che le applicazioni host e i componenti aggiuntivi possano ancora comunicare successivamente alla creazione di nuove versioni.  
  
 Come si evince, lo sviluppo di un modello di componente aggiuntivo affidabile è un'operazione per nulla semplice.  Per questo motivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] fornisce un'infrastruttura per la compilazione di modelli di componente aggiuntivo.  
  
> [!NOTE]
>  Per informazioni più dettagliate sui componenti aggiuntivi, vedere [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml).  
  
<a name="NETFrameworkAddInModelOverview"></a>   
## Cenni preliminari sul modello di componente aggiuntivo .NET Framework  
 Il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], situato nello spazio dei nomi <xref:System.AddIn>, contiene un set di tipi progettati per semplificare lo sviluppo dell'estensibilità mediante componenti aggiuntivi.  L'unità fondamentale del modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] è il *contratto*, il quale definisce la modalità di comunicazione tra applicazione host e componente aggiuntivo.  Un contratto viene esposto a un'applicazione host utilizzando un'apposita *visualizzazione* specifica dell'applicazione.  Analogamente, una *visualizzazione* del contratto specifica del componente aggiuntivo viene esposta a tale componente.  Un *adattatore* viene utilizzato per consentire la comunicazione tra le rispettive visualizzazioni del contratto.  Contratti, visualizzazioni e adattatori sono definiti segmenti; un insieme di segmenti correlati costituisce una *pipeline*.  Le pipeline sono le basi di supporto del modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per l'individuazione, l'attivazione, l'isolamento di sicurezza, l'isolamento di esecuzione tramite processi e domini dell'applicazione, la comunicazione, la gestione della durata e il controllo delle versioni.  
  
 L'intero supporto consente agli sviluppatori di compilare componenti aggiuntivi che vengono integrati con le funzionalità di un'applicazione host.  In alcuni scenari, tuttavia, le applicazioni host devono visualizzare le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] fornite dai componenti aggiuntivi.  Dal momento che ogni tecnologia di presentazione in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] dispone di un proprio modello di implementazione delle [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)], il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] non supporta alcuna tecnologia in particolare.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] estende invece il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] con il supporto dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] per i componenti aggiuntivi.  
  
<a name="WPFAddInModel"></a>   
## Componenti aggiuntivi WPF  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], insieme con il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], consente di gestire un'ampia varietà di scenari che richiedono la visualizzazione di [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] da componenti aggiuntivi da parte delle applicazioni host.  In particolare, questi scenari vengono gestiti da [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] con i due modelli di programmazione che seguono:  
  
1.  **Componente aggiuntivo che restituisce un'interfaccia utente**.  Un componente aggiuntivo restituisce un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] all'applicazione host tramite una chiamata al metodo, come definito dal contratto.  Questo scenario viene utilizzato nei seguenti casi:  
  
    -   L'aspetto di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] restituita da un componente aggiuntivo dipende da dati o condizioni esistenti solo in fase di esecuzione, ad esempio i report generati in modo dinamico.  
  
    -   L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] per i servizi fornita da un componente aggiuntivo è diversa dall'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] delle applicazioni host che possono utilizzare tale componente.  
  
    -   Il componente aggiuntivo esegue principalmente un servizio per l'applicazione host e segnala lo stato all'applicazione con un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  
  
2.  **Componente aggiuntivo che rappresenta un'interfaccia utente**.  Un componente aggiuntivo rappresenta un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], come definito dal contratto.  Questo scenario viene utilizzato nei seguenti casi:  
  
    -   Un componente aggiuntivo non fornisce alcun servizio eccetto la visualizzazione, come ad esempio un annuncio.  
  
    -   L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] per i servizi fornita da un componente aggiuntivo è comune a tutte le applicazioni host che possono utilizzare tale componente, ad esempio una calcolatrice o una finestra Selezione colori.  
  
 Questi scenari richiedono che gli oggetti dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] possano essere passati tra i domini dell'applicazione del componente aggiuntivo e dell'applicazione host.  Poiché il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] si basa sulla comunicazione remota tra domini dell'applicazione, gli oggetti passati devono essere utilizzabili in modalità remota.  
  
 Un oggetto utilizzabile in modalità remota è un'istanza di una classe che soddisfa una o più delle condizioni che seguono:  
  
-   Deriva dalla classe <xref:System.MarshalByRefObject>.  
  
-   Implementa l'interfaccia <xref:System.Runtime.Serialization.ISerializable>.  
  
-   All'istanza viene applicato l'attributo <xref:System.SerializableAttribute>.  
  
> [!NOTE]
>  Per ulteriori informazioni sulla creazione di oggetti [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] utilizzabili in modalità remota, vedere [Making Objects Remotable](http://msdn.microsoft.com/it-it/01197253-3f13-43b7-894d-9683e431192a).  
  
 I tipi di [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] non sono utilizzabili in modalità remota.  Per risolvere il problema, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] estende il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per consentire la visualizzazione da applicazioni host dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] creata dai componenti aggiuntivi.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce questo supporto mediante due tipi: l'interfaccia <xref:System.AddIn.Contract.INativeHandleContract> e due metodi statici implementati dalla classe <xref:System.AddIn.Pipeline.FrameworkElementAdapters>, ovvero <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> e <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>.  A un livello elevato, questi tipi e metodi vengono utilizzati nel modo seguente:  
  
1.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] richiede che le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] fornite dai componenti aggiuntivi siano classi derivanti direttamente o indirettamente da <xref:System.Windows.FrameworkElement>, ad esempio forme, controlli, controlli utente, pannelli di layout e pagine.  
  
2.  Quando il contratto dichiara che un'interfaccia utente verrà passata tra il componente aggiuntivo e l'applicazione host, tale contratto deve essere dichiarato come <xref:System.AddIn.Contract.INativeHandleContract> e non come <xref:System.Windows.FrameworkElement>; <xref:System.AddIn.Contract.INativeHandleContract> è una rappresentazione utilizzabile in modalità remota dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del componente aggiuntivo che può essere passata oltre i limiti di isolamento.  
  
3.  Prima di essere passato dal dominio dell'applicazione del componente aggiuntivo, <xref:System.Windows.FrameworkElement> viene assemblato sotto forma di <xref:System.AddIn.Contract.INativeHandleContract> mediante una chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>.  
  
4.  Una volta passato al dominio dell'applicazione host, <xref:System.AddIn.Contract.INativeHandleContract> deve essere nuovamente assemblato come <xref:System.Windows.FrameworkElement> mediante una chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>.  
  
 Le modalità di utilizzo di <xref:System.AddIn.Contract.INativeHandleContract>, <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> e <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> dipendono dallo scenario specifico.  Nelle sezioni riportate di seguito vengono forniti i dettagli per ogni modello di programmazione.  
  
<a name="ReturnUIFromAddInContract"></a>   
## Componente aggiuntivo che restituisce un'interfaccia utente  
 Per fare in modo che un componente aggiuntivo restituisca un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] a un'applicazione host, è necessario quanto segue:  
  
1.  L'applicazione host, il componente aggiuntivo e la pipeline devono essere creati, come descritto nella documentazione [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml) di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
2.  Il contratto deve implementare <xref:System.AddIn.Contract.IContract> e, per restituire un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], deve dichiarare un metodo con un valore restituito di tipo <xref:System.AddIn.Contract.INativeHandleContract>.  
  
3.  L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] passata tra il componente aggiuntivo e l'applicazione host deve derivare direttamente o indirettamente da <xref:System.Windows.FrameworkElement>.  
  
4.  L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] restituita dal componente aggiuntivo deve essere convertita da <xref:System.Windows.FrameworkElement> a <xref:System.AddIn.Contract.INativeHandleContract> prima di oltrepassare il limite di isolamento.  
  
5.  L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] restituita deve essere convertita da <xref:System.AddIn.Contract.INativeHandleContract> a <xref:System.Windows.FrameworkElement> dopo aver oltrepassato il limite di isolamento.  
  
6.  L'applicazione host visualizza l'oggetto <xref:System.Windows.FrameworkElement> restituito.  
  
 Per un esempio che dimostra come implementare un componente aggiuntivo che restituisce un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], vedere [Procedura: creare un componente aggiuntivo che restituisce un'interfaccia utente](../../../../docs/framework/wpf/app-development/how-to-create-an-add-in-that-returns-a-ui.md).  
  
<a name="AddInIsAUI"></a>   
## Componente aggiuntivo che rappresenta un'interfaccia utente  
 Quando un componente aggiuntivo rappresenta un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], è necessario quanto segue:  
  
1.  L'applicazione host, il componente aggiuntivo e la pipeline devono essere creati, come descritto nella documentazione [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml) di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
2.  L'interfaccia del contratto per il componente aggiuntivo deve implementare <xref:System.AddIn.Contract.INativeHandleContract>.  
  
3.  Il componente aggiuntivo passato all'applicazione host deve derivare direttamente o indirettamente da <xref:System.Windows.FrameworkElement>.  
  
4.  Il componente aggiuntivo deve essere convertito da <xref:System.Windows.FrameworkElement> a <xref:System.AddIn.Contract.INativeHandleContract> prima di oltrepassare il limite di isolamento.  
  
5.  Il componente aggiuntivo deve essere convertito da <xref:System.AddIn.Contract.INativeHandleContract> a <xref:System.Windows.FrameworkElement> dopo aver oltrepassato il limite di isolamento.  
  
6.  L'applicazione host visualizza l'oggetto <xref:System.Windows.FrameworkElement> restituito.  
  
 Per un esempio che dimostra come implementare un componente aggiuntivo che costituisce un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], vedere [Creare un componente aggiuntivo che costituisce un'interfaccia utente](../../../../docs/framework/wpf/app-development/how-to-create-an-add-in-that-is-a-ui.md).  
  
<a name="ReturningMultipleUIsFromAnAddIn"></a>   
## Restituzione di più interfacce utente da un componente aggiuntivo  
 Nei componenti aggiuntivi sono spesso disponibili più [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] per la visualizzazione di applicazioni host.  Si consideri ad esempio un componente aggiuntivo che rappresenta un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] e fornisce anche informazioni sullo stato all'applicazione host, sempre sotto forma di [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  Un componente aggiuntivo di questo tipo può essere implementato utilizzando una combinazione di tecniche afferenti ai modelli [Componente aggiuntivo che restituisce un'interfaccia utente](#ReturnUIFromAddInContract) e [Componente aggiuntivo che rappresenta un'interfaccia utente](#AddInIsAUI).  
  
<a name="AddInsAndXBAPs"></a>   
## Componenti aggiuntivi e applicazioni browser XAML  
 Negli esempi illustrati finora l'applicazione host era un'applicazione autonoma installata.  Anche le [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)], però, possono ospitare componenti aggiuntivi, sebbene con i requisiti di compilazione e implementazione aggiuntivi che seguono:  
  
-   Il manifesto dell'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] deve essere appositamente configurato per scaricare la pipeline \(cartelle e assembly\) e l'assembly del componente aggiuntivo nella cache dell'applicazione [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] sul computer client, nella stessa cartella dell'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)].  
  
-   Il codice [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] che consente di individuare e caricare i componenti aggiuntivi deve utilizzare la cache dell'applicazione [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] per l'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] come percorso della pipeline e dei componenti aggiuntivi.  
  
-   L'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] deve caricare il componente aggiuntivo in un contesto di sicurezza speciale se tale componente fa riferimento a file separati situati nel sito di origine; se ospitati da applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)], i componenti aggiuntivi possono fare riferimento unicamente a file separati che si trovano nel sito di origine dell'applicazione host.  
  
 Queste attività vengono descritte in dettaglio nelle sottosezioni riportate di seguito.  
  
### Configurazione della pipeline e del componente aggiuntivo per la distribuzione ClickOnce  
 Le applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] vengono scaricate in una cartella sicura nella cache di distribuzione [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] e da questa eseguite.  Affinché un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] ospiti un componente aggiuntivo, anche l'assembly della pipeline e del componente deve essere scaricato nella cartella sicura.  A tal proposito, è necessario configurare il manifesto dell'applicazione per includere l'assembly della pipeline e del componente aggiuntivo per il download.  L'operazione risulta più semplice in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], anche se l'assembly della pipeline e del componente aggiuntivo deve trovarsi nella cartella radice del progetto di applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] affinché [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] rilevi gli assembly della pipeline.  
  
 Di conseguenza, il primo passaggio consiste nel compilare l'assembly della pipeline e del componente aggiuntivo nella radice del progetto di applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] impostando l'output di compilazione di ogni progetto di assembly della pipeline e del componente aggiuntivo.  Nella tabella seguente vengono illustrati i percorsi dell'output di compilazione per i progetti di assembly della pipeline e del componente aggiuntivo che si trovano nella stessa soluzione e cartella radice del progetto di applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] host.  
  
 Tabella 1: Percorsi dell'output di compilazione per gli assembly della pipeline ospitati da un'applicazione XBAP  
  
|Progetto di assembly della pipeline|Percorso dell'output di compilazione|  
|-----------------------------------------|------------------------------------------|  
|Contratto|`..  \HostXBAP\Contracts\`|  
|Visualizzazione del componente aggiuntivo|`..  \HostXBAP\AddInViews\`|  
|Adattatore sul lato componente aggiuntivo|`..  \HostXBAP\AddInSideAdapters\`|  
|Adattatore sul lato host|`..  \HostXBAP\HostSideAdapters\`|  
|Componente aggiuntivo|`..  \HostXBAP\AddIns\WPFAddIn1`|  
  
 Il passaggio successivo consiste nello specificare gli assembly della pipeline e l'assembly del componente aggiuntivo come file di dati delle applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], attenendosi alla procedura riportata di seguito:  
  
1.  Includere l'assembly della pipeline e del componente aggiuntivo nel progetto facendo clic con il pulsante destro del mouse su ogni cartella della pipeline in Esplora soluzioni e scegliendo **Includi nel progetto**.  
  
2.  Nella finestra **Proprietà**, impostare l'**Operazione di compilazione** di ogni assembly della pipeline e del componente aggiuntivo su **Contenuto**.  
  
 Il passaggio finale consiste nel configurare il manifesto dell'applicazione per includere i file di assembly della pipeline e il file di assembly del componente aggiuntivo per il download.  I file devono trovarsi all'interno di cartelle nella radice della cartella contenuta nella cache [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] occupata dall'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)].  La configurazione può essere effettuata in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] attenendosi alla procedura che segue:  
  
1.  Fare clic con il pulsante destro del mouse sul progetto di applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)], scegliere **Proprietà**, **Pubblica**, quindi fare clic sul pulsante **File applicazione**.  
  
2.  Nella finestra di dialogo **File applicazione**, impostare lo **Stato pubblicazione** di ogni DLL della pipeline e del componente aggiuntivo su **Includi \(Auto\)**, quindi impostare il **Gruppo di download** per ogni DLL della pipeline e del componente aggiuntivo su **\(Obbligatorio\)**.  
  
### Utilizzo della pipeline e del componente aggiuntivo dalla base dell'applicazione  
 Quando la pipeline e il componente aggiuntivo sono configurati per la distribuzione [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)], vengono scaricati nella stessa cartella della cache [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] in cui si trova l'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)].  Per utilizzare la pipeline e il componente aggiuntivo dall'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)], è necessario che il codice [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] li ottenga dalla base dell'applicazione.  I diversi tipi e membri del modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per l'utilizzo di pipeline e componenti aggiuntivi forniscono uno speciale supporto per questo scenario.  Innanzitutto, il percorso viene identificato dal valore di enumerazione <xref:System.AddIn.Hosting.PipelineStoreLocation>.  Questo valore viene utilizzato con gli overload dei membri del componente aggiuntivo relativi all'utilizzo delle pipeline, che includono quanto segue:  
  
-   <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=fullName>  
  
-   [AddInStore.FindAddIns\(Type, PipelineStoreLocation, String\<xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%2CSystem.String%5B%5D%29?displayProperty=fullName>  
  
-   <xref:System.AddIn.Hosting.AddInStore.Rebuild%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=fullName>  
  
-   <xref:System.AddIn.Hosting.AddInStore.Update%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=fullName>  
  
### Accesso al sito di origine host  
 Per assicurare che un componente aggiuntivo possa fare riferimento ai file del sito di origine, tale componente deve essere caricato con lo stesso isolamento di sicurezza dell'applicazione host.  Questo livello di sicurezza viene identificato dal valore di enumerazione <xref:System.AddIn.Hosting.AddInSecurityLevel?displayProperty=fullName> e passato al metodo <xref:System.AddIn.Hosting.AddInToken.Activate%2A> in fase di attivazione di un componente aggiuntivo.  
  
<a name="WPFAddInModelArchitecture"></a>   
## Architettura dei componenti aggiuntivi WPF  
 Al livello più elevato, come illustrato in precedenza, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente ai componenti aggiuntivi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] di implementare le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)], derivanti direttamente o indirettamente da <xref:System.Windows.FrameworkElement>, utilizzando <xref:System.AddIn.Contract.INativeHandleContract>, <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> e <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>.  Di conseguenza, l'applicazione host restituisce un oggetto <xref:System.Windows.FrameworkElement> visualizzato dall'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] nell'applicazione stessa.  
  
 Nel caso di scenari semplici di componente aggiuntivo dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], gli sviluppatori non necessitano di ulteriori dettagli.  Nel caso di scenari più complessi, e in particolare quando si tenta di utilizzare servizi [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] aggiuntivi quali layout, risorse e associazione dati, sarà necessaria una conoscenza più dettagliata del modo in cui [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] estende il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] con il supporto dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], al fine di comprenderne i vantaggi e le limitazioni.  
  
 Fondamentalmente, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] non passa un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] da un componente aggiuntivo a un'applicazione host; al contrario, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] passa l'handle della finestra Win32 per l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] utilizzando l'interoperabilità [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Di conseguenza, quando un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] viene passata da un componente aggiuntivo a un'applicazione host, si verifica quanto segue:  
  
-   Sul lato del componente aggiuntivo, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] acquisisce un handle della finestra per l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] che verrà visualizzata dall'applicazione host.  L'handle della finestra viene incapsulato da una classe [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] interna che deriva da <xref:System.Windows.Interop.HwndSource> e implementa <xref:System.AddIn.Contract.INativeHandleContract>.  Un'istanza di questa classe viene restituita da <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> e sottoposta a marshalling dal dominio dell'applicazione del componente aggiuntivo al dominio dell'applicazione host.  
  
-   Sul lato dell'applicazione host, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] assembla nuovamente <xref:System.Windows.Interop.HwndSource> come classe [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] interna che deriva da <xref:System.Windows.Interop.HwndHost> e utilizza <xref:System.AddIn.Contract.INativeHandleContract>.  Un'istanza di questa classe viene restituita da <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> all'applicazione host.  
  
 <xref:System.Windows.Interop.HwndHost> è disponibile per visualizzare [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)], identificate da handle della finestra, da [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Per ulteriori informazioni, vedere [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md).  
  
 In sintesi, <xref:System.AddIn.Contract.INativeHandleContract>, <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> e <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> consentono di passare l'handle della finestra di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] da un componente aggiuntivo a un'applicazione host, dove viene incapsulato da <xref:System.Windows.Interop.HwndHost> e visualizzato nell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'applicazione.  
  
> [!NOTE]
>  Dal momento che ottiene <xref:System.Windows.Interop.HwndHost>, l'applicazione host non può convertire l'oggetto restituito da <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> nel tipo in cui viene implementato dal componente aggiuntivo, ad esempio <xref:System.Windows.Controls.UserControl>.  
  
 Per sua natura, <xref:System.Windows.Interop.HwndHost> possiede alcune limitazioni che influiscono sul relativo utilizzo da parte delle applicazioni host.  Tuttavia, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] estende <xref:System.Windows.Interop.HwndHost> con diverse funzionalità per gli scenari del componente aggiuntivo.  Di seguito vengono riportati i vantaggi e le limitazioni.  
  
<a name="WPFAddInModelBenefits"></a>   
## Vantaggi dei componenti aggiuntivi WPF  
 Poiché le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] dei componenti aggiuntivi [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] vengono visualizzate dalle applicazioni host tramite una classe interna derivante da <xref:System.Windows.Interop.HwndHost>, tali [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] sono vincolate dalle funzionalità di <xref:System.Windows.Interop.HwndHost> relative ai servizi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] quali layout, rendering, associazione dati, stili, modelli e risorse.  Tuttavia, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] integra la sottoclasse <xref:System.Windows.Interop.HwndHost> interna con funzionalità aggiuntive che includono quanto segue:  
  
-   Passaggio dall'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un'applicazione host all'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo e viceversa.  Il modello di programmazione "componente aggiuntivo che rappresenta un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]" richiede che l'adattatore sul lato componente aggiuntivo esegua l'override di <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> per consentire tale passaggio, indipendentemente dal fatto che il componente sia completamente attendibile o parzialmente attendibile.  
  
-   Rispetto dei requisiti di accessibilità per le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] dei componenti aggiuntivi visualizzate dalle [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] delle applicazioni host.  
  
-   Esecuzione sicura delle applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] in diversi scenari del dominio dell'applicazione.  
  
-   Protezione contro l'accesso illegale agli handle della finestra dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del componente aggiuntivo in caso di esecuzione dei componenti aggiuntivi con isolamento di sicurezza, vale a dire una sandbox di sicurezza con attendibilità parziale.  La chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> garantisce questa sicurezza:  
  
    -   Nel caso del modello di programmazione "componente aggiuntivo che restituisce un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]", l'unico modo per passare l'handle della finestra per l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo oltre il limite di isolamento consiste nella chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>.  
  
    -   Nel caso del modello di programmazione "componente aggiuntivo che rappresenta un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]", si richiede l'override di <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> nell'adattatore sul lato componente aggiuntivo e la chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>, come illustrato negli esempi precedenti, nonché la chiamata all'implementazione `QueryContract` dello stesso adattatore dall'adattatore sul lato host.  
  
-   Protezione dell'esecuzione per più domini dell'applicazione.  A causa delle limitazioni relative ai domini dell'applicazione, le eccezioni non gestite generate nei domini dell'applicazione del componente aggiuntivo provocano un arresto anomalo dell'intera applicazione, nonostante sia presente un limite di isolamento.  Tuttavia, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] e il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] offrono un modo semplice per ovviare al problema e migliorare la stabilità dell'applicazione.  Un componente aggiuntivo [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] che visualizza un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] crea un oggetto <xref:System.Windows.Threading.Dispatcher> per il thread nel quale viene eseguito il dominio dell'applicazione, nel caso in cui l'applicazione host sia un'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Per rilevare tutte le eccezioni non gestite che si verificano nel dominio dell'applicazione, è possibile gestire l'evento <xref:System.Windows.Threading.Dispatcher.UnhandledException> dell'oggetto <xref:System.Windows.Threading.Dispatcher> del componente aggiuntivo [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  È possibile ottenere <xref:System.Windows.Threading.Dispatcher> dalla proprietà <xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A>.  
  
<a name="WPFAddInModelLimitations"></a>   
## Limitazioni dei componenti aggiuntivi WPF  
 Oltre ai vantaggi aggiunti da [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ai comportamenti predefiniti forniti da <xref:System.Windows.Interop.HwndSource>, <xref:System.Windows.Interop.HwndHost> e dagli handle della finestra, esistono anche alcune limitazioni per le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] dei componenti aggiuntivi visualizzate dalle applicazioni host:  
  
-   Le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] del componente aggiuntivo visualizzate da un'applicazione host non rispettano il comportamento dell'area di visualizzazione dell'applicazione stessa.  
  
-   Il concetto di *spazio aereo* degli scenari di interoperabilità viene applicato anche ai componenti aggiuntivi; vedere in proposito [Cenni preliminari sulle aree di tecnologia](../../../../docs/framework/wpf/advanced/technology-regions-overview.md).  
  
-   I servizi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un'applicazione host, ad esempio l'ereditarietà delle risorse, l'associazione dati e i comandi non sono automaticamente disponibili per le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] del componente aggiuntivo.  Per fornire questi servizi al componente aggiuntivo è necessario aggiornare la pipeline.  
  
-   L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo non può essere ruotata, ridimensionata, inclinata né trasformata in altro modo; vedere in proposito [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md).  
  
-   Il contenuto delle [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] del componente aggiuntivo sottoposto a rendering mediante operazioni di disegno dallo spazio dei nomi <xref:System.Drawing> può includere la fusione alfa.  Tuttavia, sia l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo che l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'applicazione host che lo contiene devono essere opache al 100%; in altre parole, la proprietà `Opacity` di entrambe deve essere impostata su 1.  
  
-   Se la proprietà <xref:System.Windows.Window.AllowsTransparency%2A> di una finestra nell'applicazione host contenente l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo è impostata su `true`, il componente risulta invisibile.  Questo accade anche se l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del componente aggiuntivo è opaca al 100%, ovvero se la proprietà `Opacity` ha un valore pari a 1.  
  
-   L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo deve essere visualizzata in cima ad altri elementi [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] nella stessa finestra di primo livello.  
  
-   Nessuna parte dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo può essere sottoposta a rendering mediante un oggetto <xref:System.Windows.Media.VisualBrush>.  Il componente aggiuntivo può invece eseguire uno snapshot dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] generata per creare una bitmap da passare all'applicazione host utilizzando i metodi definiti dal contratto.  
  
-   I file multimediali non possono essere riprodotti da un oggetto <xref:System.Windows.Controls.MediaElement> nell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo.  
  
-   Gli eventi del mouse generati per l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del componente aggiuntivo non vengono ricevuti né generati dall'applicazione host e la proprietà `IsMouseOver` dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'applicazione è impostata su `false`.  
  
-   Quando lo stato attivo passa da un controllo a un altro nell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo, gli eventi `GotFocus` e `LostFocus` non vengono ricevuti né generati dall'applicazione host.  
  
-   La parte di un'applicazione host contenente l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo appare bianca quando viene stampata.  
  
-   Se l'applicazione host prosegue con l'esecuzione, tutti i dispatcher \(vedere <xref:System.Windows.Threading.Dispatcher>\) creati dall'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del componente aggiuntivo devono essere arrestati manualmente prima che il componente aggiuntivo proprietario venga scaricato.  Il contratto può implementare metodi che consentono all'applicazione host di segnalare il componente aggiuntivo prima che questo venga scaricato, permettendo così all'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del componente di arrestare i dispatcher.  
  
-   Se l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di un componente aggiuntivo è un oggetto <xref:System.Windows.Controls.InkCanvas> o contiene un oggetto <xref:System.Windows.Controls.InkCanvas>, non è possibile scaricare tale componente.  
  
<a name="PerformanceOptimization"></a>   
## Ottimizzazione delle prestazioni  
 Per impostazione predefinita, quando si utilizzano più domini dell'applicazione, tutti gli assembly [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] richiesti da ogni applicazione vengono caricati nel dominio della stessa.  Di conseguenza, il tempo necessario per creare nuovi domini dell'applicazione e avviare le applicazioni al loro interno potrebbe influire sulle prestazioni.  [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] fornisce tuttavia un metodo per ridurre i tempi di avvio, indicando alle applicazioni di condividere gli assembly tra i vari domini dell'applicazione, se già caricati.  A tal proposito, occorre utilizzare l'attributo <xref:System.LoaderOptimizationAttribute>, che deve essere applicato al metodo del punto di ingresso \(`Main`\).  In questo caso, è necessario utilizzare soltanto il codice per implementare la definizione dell'applicazione; vedere in proposito [Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
## Vedere anche  
 <xref:System.LoaderOptimizationAttribute>   
 [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml)   
 [Domini applicazione](../../../../docs/framework/app-domains/application-domains.md)   
 [.NET Framework Remoting Overview](http://msdn.microsoft.com/it-it/eccb1d31-0a22-417a-97fd-f4f1f3aa4462)   
 [Making Objects Remotable](http://msdn.microsoft.com/it-it/01197253-3f13-43b7-894d-9683e431192a)   
 [Procedure relative](../../../../docs/framework/wpf/app-development/how-to-topics.md)