---
title: "Panoramica sui Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Smart (client)"
  - "Windows Form, informazioni su Windows Form"
ms.assetid: 3a2b6284-c8d6-4e1c-8c69-0bed38f38cd4
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# Panoramica sui Windows Form
Nella panoramica seguente sono illustrati i vantaggi delle applicazioni client intelligenti, le principali funzionalità della programmazione di Windows Form e come è possibile usare Windows Form per compilare client intelligenti che rispondono alle esigenze delle aziende e degli utenti finali attuali.  
  
## Applicazioni Smart Client con Windows Form  
 Con Windows Form è possibile sviluppare applicazioni Smart Client.  Gli *smart client* sono applicazioni grafiche che possono essere distribuite e aggiornate facilmente, che possono funzionare anche quando non sono collegate a Internet e che consentono di accedere alle risorse sul computer locale in maniera molto più protetta rispetto alle tradizionali applicazioni Windows.  
  
### Compilazione di interfacce utente complete e interattive  
 Windows Form è una tecnologia Smart Client per [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], un gruppo di librerie gestite che semplificano l'esecuzione di attività comuni, ad esempio la lettura e la scrittura nel file system.  Usando un ambiente di sviluppo come [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], è possibile creare applicazioni Smart Client Windows Form che visualizzano informazioni, richiedono l'input dagli utenti e comunicano con computer remoti tramite una rete.  
  
 In Windows Form un *form* è una superficie visiva sulla quale è possibile visualizzare informazioni per l'utente.  Per compilare applicazioni Windows Form, in genere si aggiungono i controlli nei form e quindi si definiscono le risposte alle azioni degli utenti, ad esempio i clic con il mouse o le pressioni dei tasti.  Un *controllo* è un elemento separato dell'interfaccia utente \(UI\) usato per visualizzare dati o accettare input di dati.  
  
 Quando un utente esegue un'azione nel form o in uno dei controlli, viene generato un evento.  L'applicazione reagisce a tali eventi usando il codice ed elabora gli eventi quando si verificano.  Per altre informazioni, vedere [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md).  
  
 Windows Form contiene diversi controlli che possono essere inseriti nei form, ad esempio i controlli che visualizzano caselle di testo, pulsanti, caselle di riepilogo a discesa, pulsanti di opzione e persino pagine Web.  Per un elenco di tutti i controlli utilizzabili in un form, vedere [Controlli da utilizzare in Windows Form](../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md).  Se un controllo esistente non dovesse soddisfare le proprie esigenze, Windows Form consente anche di creare controlli personalizzati usando la classe <xref:System.Windows.Forms.UserControl>.  
  
 Windows Form dispone di controlli UI completi che simulano le funzioni delle applicazioni di fascia alta quali Microsoft Office.  Usando i controlli <xref:System.Windows.Forms.ToolStrip> e <xref:System.Windows.Forms.MenuStrip> è possibile creare barre degli strumenti e menu contenenti testo e immagini, visualizzare sottomenu nonché includere altri controlli, ad esempio caselle di testo e caselle combinate.  
  
 Usando la funzionalità di trascinamento della selezione disponibile in Progettazione Windows Form di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], è possibile creare facilmente applicazioni Windows Form.  È sufficiente selezionare i controlli con il cursore e aggiungerli nel punto desiderato del form.  Per facilitare l'allineamento dei controlli, nella finestra di progettazione vengono forniti strumenti quali linee della griglia e guide di allineamento.  Sia che si usi [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o che si esegua la compilazione dalla riga di comando, è possibile usare i controlli <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel> e <xref:System.Windows.Forms.SplitContainer> per creare layout di form avanzati in meno tempo.  
  
 Infine, se è necessario creare elementi dell'interfaccia utente personalizzati, lo spazio dei nomi <xref:System.Drawing> contiene diverse classi che consentono di creare linee, cerchi e altre forme direttamente in un form.  
  
> [!NOTE]
>  I controlli Windows Form non sono progettati per il marshalling fra domini applicazioni.  Per questo motivo, Microsoft non supporta il passaggio di un controllo Windows Form attraverso un limite di <xref:System.AppDomain>, anche se il tipo di base <xref:System.Windows.Controls.Control> di <xref:System.MarshalByRefObject> sembri indicare che ciò sia possibile.  Le applicazioni Windows Form che presentano più domini applicazioni sono supportate purché nessun controllo Windows Form attraversi il limite di un dominio applicazione.  
  
#### Assistenza nella creazione di form e controlli  
 Per informazioni dettagliate sull'uso di queste funzionalità, vedere i seguenti argomenti della Guida.  
  
|Descrizione|Argomento della Guida|  
|-----------------|---------------------------|  
|Uso dei controlli nei form|[Procedura: aggiungere controlli a un Windows Form](../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)|  
|Uso del controllo <xref:System.Windows.Forms.ToolStrip>|[Procedura: creare un controllo ToolStrip di base con elementi standard utilizzando la finestra di progettazione](../../../docs/framework/winforms/controls/create-a-basic-wf-toolstrip-with-standard-items-using-the-designer.md)|  
|Creazione di grafica con <xref:System.Drawing>|[Guida introduttiva alla programmazione grafica](../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)|  
|Creare controlli personalizzati|[Procedura: ereditare dalla classe UserControl](../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)|  
  
### Visualizzazione e modifica dei dati  
 Molte applicazioni devono visualizzare i dati da un database, da un file XML, servizi Web XML o altre origini di dati.  In Windows Form viene fornito un controllo denominato <xref:System.Windows.Forms.DataGridView> che consente di visualizzare dati tabulari in un formato tradizionale basato su righe e colonne, in modo che ciascun blocco di dati occupi una singola cella.  Usando <xref:System.Windows.Forms.DataGridView> è possibile personalizzare l'aspetto delle singole celle, bloccare righe e colonne arbitrarie nonché visualizzare controlli complessi all'interno delle celle.  
  
 Il collegamento alle origini dati tramite una rete è un'attività semplice con gli smart client Windows Form.  Il componente <xref:System.Windows.Forms.BindingSource>, una novità di Windows Form in [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] e [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)], rappresenta una connessione a un'origine dati ed espone metodi per l'associazione di dati a controlli, lo spostamento ai record precedenti e successivi, la modifica di record e il salvataggio delle modifiche fino all'origine iniziale.  Il controllo <xref:System.Windows.Forms.BindingNavigator> fornisce un'interfaccia semplice tramite il componente <xref:System.Windows.Forms.BindingSource> per gli utenti per spostarsi tra i record.  
  
 È possibile creare facilmente controlli con associazione a dati usando la finestra Origini dati,  in cui vengono visualizzate origini dati quali database, servizi Web e oggetti contenuti nel progetto.  È possibile creare controlli associati a dati mediante il trascinamento di elementi da questa finestra nei form del progetto.  È anche possibile connettere i controlli esistenti ai dati mediante il trascinamento di oggetti dalla finestra Origini dati nei controlli esistenti.  
  
 Un altro tipo di data binding che è possibile gestire in Windows Form sono le *impostazioni*.  La maggioranza delle applicazioni client intelligenti devono conservare alcune informazioni relative al proprio stato in fase di esecuzione, ad esempio le ultime dimensioni note dei form, e conservare i dati relativi alle preferenze dell'utente, ad esempio le posizioni predefinite per i file salvati.  La funzionalità Impostazioni applicazione risolve queste problematiche offrendo un modo semplice per archiviare entrambi i tipi di impostazioni sul computer client.  Una volta definite mediante [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o un editor di codice, queste impostazioni vengono salvate in modo permanente come XML e rilette automaticamente in memoria in fase di esecuzione.  
  
#### Assistenza nella visualizzazione e nella modifica dei dati  
 Per informazioni dettagliate sull'uso di queste funzionalità, vedere i seguenti argomenti della Guida.  
  
|Descrizione|Argomento della Guida|  
|-----------------|---------------------------|  
|Uso del componente <xref:System.Windows.Forms.BindingSource>|[Procedura: associare controlli Windows Form al componente BindingSource utilizzando la finestra di progettazione](../../../docs/framework/winforms/controls/bind-wf-controls-with-the-bindingsource.md)|  
|Uso delle origini dati di [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]|[Procedura: ordinare e filtrare i dati ADO.NET con il componente BindingSource Windows Form](../../../docs/framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|  
|Uso della finestra Origini dati|[Procedura dettagliata: visualizzazione di dati in un Windows Form](../Topic/Walkthrough:%20Displaying%20Data%20on%20a%20Windows%20Form.md)|  
|Uso delle impostazioni dell'applicazione|[How to: Create Application Settings](../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)|  
  
### Distribuzione delle applicazioni ai client  
 Una volta scritta, l'applicazione deve essere inviata agli utenti in modo che possano installarla ed eseguirla sui propri client.  Quando si usa la tecnologia [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)], è possibile distribuire le applicazioni dall'interno di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con alcuni semplici clic e fornire agli utenti un indirizzo URL che punta all'applicazione sul Web o in una condivisione di file.  [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] gestisce tutti gli elementi e le dipendenze dell'applicazione e garantisce la corretta installazione dell'applicazione nel client.  
  
 Le applicazioni [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] possono essere configurate per essere eseguite solo quando l'utente è connesso alla rete oppure per essere eseguite sia online che offline.  Quando si specifica che un'applicazione deve supportare l'esecuzione offline, [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] aggiunge un collegamento all'applicazione nel menu **Start**.  In questo modo, l'utente può aprire l'applicazione senza usare l'URL.  
  
 Quando si aggiorna l'applicazione, vengono pubblicati un nuovo manifesto della distribuzione e una nuova copia dell'applicazione sul server Web.  L'aggiornamento disponibile verrà rilevato da [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] e l'installazione dell'utente verrà aggiornata. Non è necessaria alcuna operazione di programmazione personalizzata per aggiornare gli assembly precedenti.  
  
#### Assistenza nella distribuzione delle applicazioni ClickOnce  
 Per un'introduzione completa a [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)], vedere [ClickOnce Security and Deployment](../Topic/ClickOnce%20Security%20and%20Deployment.md).  Per informazioni dettagliate sull'uso di queste funzionalità, vedere i seguenti argomenti della Guida.  
  
|Descrizione|Argomento della Guida|  
|-----------------|---------------------------|  
|Distribuzione di un'applicazione mediante [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]|[How to: Publish a ClickOnce Application using the Publish Wizard](../Topic/How%20to:%20Publish%20a%20ClickOnce%20Application%20using%20the%20Publish%20Wizard.md)<br /><br /> [Walkthrough: Manually Deploying a ClickOnce Application](../Topic/Walkthrough:%20Manually%20Deploying%20a%20ClickOnce%20Application.md)|  
|Aggiornamento di una distribuzione [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]|[How to: Manage Updates for a ClickOnce Application](../Topic/How%20to:%20Manage%20Updates%20for%20a%20ClickOnce%20Application.md)|  
|Gestione della sicurezza con [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]|[How to: Enable ClickOnce Security Settings](../Topic/How%20to:%20Enable%20ClickOnce%20Security%20Settings.md)|  
  
### Altri controlli e funzionalità  
 Windows Form dispone di altre funzioni che rendono le comuni attività di implementazione estremamente semplici e rapide, quali il supporto per la creazione di caselle di dialogo, la stampa, l'aggiunta della Guida e la documentazione, la localizzazione dell'applicazione in diverse lingue.  Inoltre, Windows Form si basa sull'infrastruttura di sicurezza di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  Questo assicura la massima affidabilità delle applicazioni distribuite ai clienti.  
  
#### Assistenza nell'implementazione di altri controlli e funzionalità  
 Per informazioni dettagliate sull'uso di queste funzionalità, vedere i seguenti argomenti della Guida.  
  
|Descrizione|Argomento della Guida|  
|-----------------|---------------------------|  
|Stampa del contenuto di un form|[How to: Print Graphics in Windows Forms](../../../docs/framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [How to: Print a Multi\-Page Text File in Windows Forms](../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|  
|Altre informazioni sulla sicurezza di Windows Form|[Security in Windows Forms Overview](../../../docs/framework/winforms/security-in-windows-forms-overview.md)|  
  
## Vedere anche  
 [Getting Started with Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)   
 [Creating a New Windows Form](../../../docs/framework/winforms/creating-a-new-windows-form.md)   
 [Cenni preliminari sul controllo ToolStrip](../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo DataGridView](../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)   
 [Cenni preliminari sul componente BindingSource](../../../docs/framework/winforms/controls/bindingsource-component-overview.md)   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [ClickOnce Security and Deployment](../Topic/ClickOnce%20Security%20and%20Deployment.md)