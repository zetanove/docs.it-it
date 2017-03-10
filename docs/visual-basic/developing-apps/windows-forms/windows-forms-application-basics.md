---
title: "Windows Forms Application Basics (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Windows applications"
  - "Windows Forms, Visual Basic"
ms.assetid: 0b919d30-7fd6-42db-85c8-543d15312441
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Windows Forms Application Basics (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un aspetto importante di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] è costituito dalla possibilità di creare applicazioni Windows Form eseguite localmente sui computer degli utenti.  È possibile utilizzare Visual Studio per creare l'applicazione e l'interfaccia utente utilizzando Windows Form.  Un'applicazione Windows Forms viene compilata sulle classi dallo spazio nome <xref:System.Windows.Forms>.  
  
## Progettazione delle applicazioni Windows Form  
 È possibile creare applicazioni Windows Form e applicazioni di servizio Windows con [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  Per ulteriori informazioni, vedere i seguenti argomenti:  
  
-   [Getting Started with Windows Forms](../Topic/Getting%20Started%20with%20Windows%20Forms.md).  Vengono fornite informazioni sulla creazione e la programmazione di Windows Form.  
  
-   [Windows Forms Walkthroughs](http://msdn.microsoft.com/it-it/fd44d13d-4733-416f-aefc-32592e59e5d9).  Consente di visualizzare un elenco di argomenti in cui viene dettagliatamente descritto lo sviluppo di applicazioni Windows Form comunemente create in base a Windows Form.  
  
-   [Controlli per Windows Form](../Topic/Windows%20Forms%20Controls.md).  Raccolta di argomenti in cui viene dettagliatamente descritto l'utilizzo dei controlli Windows Form.  
  
-   [Windows Service Applications](../Topic/Developing%20Windows%20Service%20Applications.md).  Consente di visualizzare un elenco di argomenti in cui viene illustrato il modo in cui creare i servizi Windows.  
  
## Compilazione di interfacce utente complete e interattive  
 Windows Form è il componente Smart Client di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)], un insieme di librerie gestite che attivano le comuni attività dell'applicazione quali la lettura e la scrittura nel file system.  Utilizzando un ambiente di sviluppo come [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)], è possibile creare applicazioni Windows Form che visualizzano informazioni, richiedono l'input dagli utenti e comunicano con computer remoti tramite una rete.  
  
 In Windows Form, un modulo è una superficie visiva su cui possono essere visualizzate informazioni per l'utente.  Per compilare le applicazioni Windows Form, inserire i controlli sui moduli e sviluppare le risposte alle azioni utente, quali i clic con il mouse o la selezione di tasti.  Un *controllo* è un elemento separato dell'interfaccia utente \(UI\) utilizzato per visualizzare dati o accettare input di dati.  
  
### Eventi  
 Quando un utente esegue un'azione nel modulo o in uno dei controlli, genera un evento.  L'applicazione reagisce a tali eventi utilizzando il codice ed elabora gli eventi quando si verificano.  Per ulteriori informazioni, vedere [Creating Event Handlers in Windows Forms](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md).  
  
### Controlli  
 Windows Form contiene una serie di controlli da inserire nei moduli: i controlli che visualizzano le caselle di testo, i pulsanti, le caselle di riepilogo a discesa, i pulsanti di opzione e addirittura le pagine Web.  Per un elenco di tutti i controlli utilizzabili in un modulo, vedere [Controlli da utilizzare in Windows Form](../Topic/Controls%20to%20Use%20on%20Windows%20Forms.md).  Se un controllo esistente non soddisfare le proprie esigenze, Windows Form consente anche di creare controlli personalizzati utilizzando la classe <xref:System.Windows.Forms.UserControl>.  
  
 Windows Form dispone di controlli UI completi che simulano le funzioni delle applicazioni di fascia alta quali Microsoft Office.  Utilizzando <xref:System.Windows.Forms.ToolStrip> e il controllo<xref:System.Windows.Forms.MenuStrip>, è possibile creare barre degli strumenti e menu che contengono testo e immagini, visualizzare sottomenu e attivare altri controlli, quali caselle di testo e caselle combinate.  
  
 Utilizzando la funzionalità di trascinamento disponibile nella finestra di progettazione dei form di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] è possibile creare facilmente applicazioni Windows Form. È sufficiente selezionare i controlli con il cursore e posizionarli nel punto desiderato del form.  La finestra di progettazione contiene strumenti quali linee della griglia e "guide di allineamento" per facilitare i controlli dell'allineamento.  Sia che si utilizzi [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] o che si compili dalla riga di comando, è possibile utilizzare i controlli <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel> e <xref:System.Windows.Forms.SplitContainer> per creare layout di form avanzati con il minimo sforzo e nel minimo tempo.  
  
### Elementi della UI personalizzati  
 Infine, se è necessario creare propri elementi UI personalizzati, lo spazio nome <xref:System.Drawing> contiene tutte le classi necessarie per creare linee,cerchi e altre forme direttamente nel form.  
  
 Per informazioni dettagliate sull'utilizzo di tali funzioni, vedere i seguenti argomenti della Guida.  
  
|Per|Vedere|  
|---------|------------|  
|Creare una nuova applicazione Windows Form con [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)]|[Walkthrough: Creating a Simple Windows Form](http://msdn.microsoft.com/it-it/2d9daec0-0543-41d0-acb1-964f685bddbb)|  
|Utilizzare i controlli sui form|[Procedura: aggiungere controlli a un Windows Form](../Topic/How%20to:%20Add%20Controls%20to%20Windows%20Forms.md)|  
|Gestire gli eventi da un form e i relativi controlli|[How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/it-it/8461e9b8-14e8-406f-936e-3726732b23d2)|  
|Utilizzare il controllo <xref:System.Windows.Forms.ToolStrip>|[Procedura: creare un controllo ToolStrip di base con elementi standard utilizzando la finestra di progettazione](../Topic/How%20to:%20Create%20a%20Basic%20Windows%20Forms%20ToolStrip%20with%20Standard%20Items%20Using%20the%20Designer.md)|  
|Creare grafici con <xref:System.Drawing>|[Guida introduttiva alla programmazione grafica](../Topic/Getting%20Started%20with%20Graphics%20Programming.md)|  
|Creare controlli personalizzati|[Procedura: ereditare dalla classe UserControl](../Topic/How%20to:%20Inherit%20from%20the%20UserControl%20Class.md)|  
  
## Visualizzazione e manipolazione dei dati  
 Molte applicazioni devono visualizzare i dati da un database, da un file XML, servizi Web XML o altre origini di dati.  Windows Form fornisce un controllo flessibile denominato controllo <xref:System.Windows.Forms.DataGridView> per creare dati tabulari nel formato di una riga o di una colonna tradizionale, in modo che ciascun dato occupi una cella.  Utilizzando <xref:System.Windows.Forms.DataGridView> è possibile tra l'altro personalizzare l'aspetto delle singole celle, bloccare le righe e le colonne arbitrarie e visualizzare controlli complessi dentro le celle.  
  
 Il collegamento alle origini dati tramite una rete è un'attività semplice con gli smart client Windows Form.  Il componente <xref:System.Windows.Forms.BindingSource>, una novità di Windows Form in [!INCLUDE[vsprvslong](../../../csharp/misc/includes/vsprvslong-md.md)] e [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)], rappresenta una connessione a un'origine dati ed espone metodi per l'associazione di dati a controlli, lo spostamento ai record precedenti e successivi, la modifica di record e il salvataggio delle modifiche fino all'origine iniziale.  Il controllo <xref:System.Windows.Forms.BindingNavigator> fornisce un'interfaccia semplice tramite il componente <xref:System.Windows.Forms.BindingSource> per gli utenti per spostarsi tra i record.  
  
### Controlli associati ai dati  
 È possibile creare dei controlli associati ai dati utilizzando la finestra Data Sources in cui è possibile visualizzare le origini dati quali i database, i servizi Web e gli oggetti del progetto.  È possibile creare controlli associati a dati mediante il trascinamento di elementi da questa finestra nei form del progetto.  È inoltre possibile connettere i controlli esistenti ai dati mediante il trascinamento di oggetti dalla finestra Origini dati nei controlli esistenti.  
  
### Impostazioni  
 Un altro tipo di associazione di dati che è possibile gestire in Windows Form è l'impostazione.  Molte applicazioni smart client devono conservare informazioni sullo stato di runtime, quali l'ultima dimensione nota dei form, nonché i dati relativi alle preferenze dell'utente, quali le posizioni predefinite dei file salvati.  La funzione relativa alle impostazioni dell'applicazione consente di risolvere questi problemi fornendo un modo semplice per memorizzare entrambi i tipi di impostazione sul client.  Una volta definite mediante [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] o un editor di codice, tali impostazioni vengono mantenute come XML e lette automaticamente in memoria in fase di esecuzione.  
  
 Per informazioni dettagliate sull'utilizzo di tali funzioni, vedere i seguenti argomenti della Guida.  
  
|Per|Vedere|  
|---------|------------|  
|Utilizzare il componente <xref:System.Windows.Forms.BindingSource>|[Procedura: associare controlli Windows Form al componente BindingSource utilizzando la finestra di progettazione](../Topic/How%20to:%20Bind%20Windows%20Forms%20Controls%20with%20the%20BindingSource%20Component%20Using%20the%20Designer.md)|  
|Utilizzo delle origini dati di [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado-md.md)]|[Procedura: ordinare e filtrare i dati ADO.NET con il componente BindingSource Windows Form](../Topic/How%20to:%20Sort%20and%20Filter%20ADO.NET%20Data%20with%20the%20Windows%20Forms%20BindingSource%20Component.md)|  
|Utilizzare la finestra Origini dati|[Procedura dettagliata: visualizzazione di dati in un Windows Form](../Topic/Walkthrough:%20Displaying%20Data%20on%20a%20Windows%20Form.md)|  
|Utilizzare le impostazioni dell'applicazione|[How to: Create Application Settings Using the Designer](http://msdn.microsoft.com/it-it/53b3af80-1c02-4e35-99c6-787663148945)|  
  
## Distribuzione delle applicazioni ai client  
 Una volta scritta l'applicazione, è necessario inviarla agli utenti in modo che possano installarla ed eseguirla sui propri client.  Utilizzando la tecnologia [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)], è possibile distribuire le applicazioni dall'interno di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] con alcuni semplici clic e fornire agli utenti un indirizzo URL che punta all'applicazione sul Web o in una condivisione di file.  [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] consente di gestire tutti gli elementi e le dipendenze dell'applicazione e garantisce la corretta installazione dell'applicazione nel client.  
  
 Le applicazioni [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] possono essere configurate per essere eseguite solo quando l'utente è connesso alla rete oppure per essere eseguite sia online che offline.  Quando si specifica il supporto dell'esecuzione offline per un'operazione, in [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] viene aggiunto un collegamento all'applicazione nel menu **Start**, in modo che l'utente possa aprirlo senza utilizzare l'URL.  
  
 Quando si aggiorna l'applicazione, vengono pubblicati un nuovo manifesto di distribuzione e una nuova copia dell'applicazione sul server Web.  L'aggiornamento disponibile viene rilevato da [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)] e l'installazione viene aggiornata. Non è necessaria alcuna operazione di programmazione personalizzata per aggiornare gli assembly precedenti.  
  
 Per un'introduzione completa a [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)], vedere [ClickOnce Security and Deployment](/visual-studio/deployment/clickonce-security-and-deployment).  Per informazioni dettagliate sull'utilizzo di tali funzioni, vedere i seguenti argomenti della Guida:  
  
|Per|Vedere|  
|---------|------------|  
|Distribuire un'applicazione con [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)]|[How to: Publish a ClickOnce Application using the Publish Wizard](../Topic/How%20to:%20Publish%20a%20ClickOnce%20Application%20using%20the%20Publish%20Wizard.md)<br /><br /> [Walkthrough: Manually Deploying a ClickOnce Application](../Topic/Walkthrough:%20Manually%20Deploying%20a%20ClickOnce%20Application.md)|  
|Aggiornare una distribuzione di [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)]|[How to: Manage Updates for a ClickOnce Application](../Topic/How%20to:%20Manage%20Updates%20for%20a%20ClickOnce%20Application.md)|  
|Gestire la sicurezza con [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick-md.md)]|[How to: Enable ClickOnce Security Settings](../Topic/How%20to:%20Enable%20ClickOnce%20Security%20Settings.md)|  
  
## Altri controlli e funzionalità  
 Windows Form dispone di altre funzioni che rendono le comuni attività di implementazione estremamente semplici e rapide, quali il supporto per la creazione di caselle di dialogo, la stampa, l'aggiunta della Guida e la documentazione, la localizzazione dell'applicazione in diverse lingue.  Inoltre, il solido sistema di sicurezza di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] su cui poggia Windows Form consente di rilasciare applicazioni più sicure ai clienti.  
  
 Per informazioni dettagliate sull'utilizzo di tali funzioni, vedere i seguenti argomenti della Guida:  
  
|Per|Vedere|  
|---------|------------|  
|Stampa del contenuto di un form|[How to: Print Graphics in Windows Forms](../Topic/How%20to:%20Print%20Graphics%20in%20Windows%20Forms.md)<br /><br /> [How to: Print a Multi\-Page Text File in Windows Forms](../Topic/How%20to:%20Print%20a%20Multi-Page%20Text%20File%20in%20Windows%20Forms.md)|  
|Globalizzare un'applicazione Windows Form|[Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/it-it/9a96220d-a19b-4de0-9f48-01e5d82679e5)|  
|Richiamare informazioni aggiuntive sulla sicurezza di Windows Form|[Security in Windows Forms Overview](../Topic/Security%20in%20Windows%20Forms%20Overview.md)|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Panoramica sui Windows Form](../Topic/Windows%20Forms%20Overview.md)   
 [My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)