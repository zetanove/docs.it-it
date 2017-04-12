---
title: Nozioni fondamentali sull&quot;applicazione (Visual Basic) di Windows Form | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Windows applications
- Windows Forms, Visual Basic
ms.assetid: 0b919d30-7fd6-42db-85c8-543d15312441
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8275d3c06ebd89254a07127b4850d32ef0580830
ms.lasthandoff: 03/13/2017

---
# <a name="windows-forms-application-basics-visual-basic"></a>Nozioni fondamentali relative alle applicazioni Windows Forms (Visual Basic)
Una parte importante di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è la possibilità di creare applicazioni Windows Form eseguite localmente sui computer degli utenti. È possibile utilizzare Visual Studio per creare l'interfaccia utente e di applicazione Windows Form. Un'applicazione Windows Form è basata sulle classi di <xref:System.Windows.Forms>dello spazio dei nomi.</xref:System.Windows.Forms>  
  
## <a name="designing-windows-forms-applications"></a>Applicazioni Progettazione Windows Form  
 È possibile creare Windows Form e applicazioni di servizio Windows con [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]. Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Guida introduttiva a Windows Form](https://msdn.microsoft.com/library/ms229601.aspx). Fornisce informazioni su come creare e programmare i Windows Form.  
   
-   [Controlli Windows Form](https://msdn.microsoft.com/library/ettb6e2a.aspx). Raccolta di argomenti che riporta in dettaglio l'utilizzo di controlli Windows Form.  
  
-   [Applicazioni di servizio Windows](https://msdn.microsoft.com/library/y817hyb6.aspx). Vengono elencati argomenti che illustrano come creare servizi Windows.  
  
## <a name="building-rich-interactive-user-interfaces"></a>Compilazione di interfacce utente complete e interattive  
 Windows Form è il componente smart client di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], un set di librerie gestite che consentono l'esecuzione di attività comuni quali la lettura e scrittura nel file System. Utilizzando un ambiente di sviluppo come [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], è possibile creare applicazioni Windows Form che visualizzano informazioni, richiedono l'input dagli utenti e comunicano con computer remoti tramite una rete.  
  
 In Windows Form, un modulo è una superficie visiva sulla quale è possibile visualizzare informazioni all'utente. Per compilare applicazioni Windows Form, controlli nei form e sviluppare le risposte alle azioni dell'utente, ad esempio clic del mouse o pressioni dei tasti. Oggetto *controllo* è un elemento di interfaccia utente discreti che visualizza dati o accetta input di dati.  
  
### <a name="events"></a>Eventi  
 Quando un utente esegue un'azione nel form o uno dei relativi controlli, viene generato un evento. L'applicazione reagisce a tali eventi usando il codice ed elabora gli eventi quando si verificano. Per ulteriori informazioni, vedere [creazione di gestori eventi in Windows Form](https://msdn.microsoft.com/library/dacysss4.aspx).  
  
### <a name="controls"></a>Controlli  
 Windows Form contiene diversi controlli che è possibile inserire nel form: controlli che visualizzano caselle di testo, pulsanti, caselle di riepilogo a discesa, pulsanti di opzione e persino pagine Web. Per un elenco di tutti i controlli utilizzabili in un form, vedere [controlli da usare in Windows Form](https://msdn.microsoft.com/library/3xdhey7w.aspx). Se un controllo esistente non soddisfa le proprie esigenze, Windows Form consente anche di creare controlli personalizzati utilizzando la <xref:System.Windows.Forms.UserControl>classe.</xref:System.Windows.Forms.UserControl>  
  
 Windows Form dispone di controlli UI completi che simulano le funzionalità delle applicazioni di fascia alta quali Microsoft Office. Utilizzo di <xref:System.Windows.Forms.ToolStrip>e <xref:System.Windows.Forms.MenuStrip>controllo, è possibile creare barre degli strumenti e menu contengono testo e immagini, visualizzare sottomenu nonché includere altri controlli quali caselle di testo e caselle combinate.</xref:System.Windows.Forms.MenuStrip> </xref:System.Windows.Forms.ToolStrip>  
  
 Con il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] progettazione form di trascinamento e rilascio, è possibile creare facilmente applicazioni Windows Form: è sufficiente selezionare i controlli con il cursore e inserirli nella posizione desiderata nel modulo. La finestra di progettazione vengono forniti strumenti quali linee della griglia e "snap" per facilitare l'allineamento di controlli. Sia che si usi [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] o di compilazione dalla riga di comando, è possibile utilizzare il <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel>e <xref:System.Windows.Forms.SplitContainer>i controlli per creare avanzate costituiscono layout con meno tempo.</xref:System.Windows.Forms.SplitContainer> </xref:System.Windows.Forms.TableLayoutPanel> </xref:System.Windows.Forms.FlowLayoutPanel>  
  
### <a name="custom-ui-elements"></a>Elementi dell'interfaccia utente personalizzata  
 Infine, se è necessario creare elementi dell'interfaccia utente personalizzati, il <xref:System.Drawing>dello spazio dei nomi contiene tutte le classi necessarie per eseguire il rendering di linee, cerchi e altre forme direttamente in un form.</xref:System.Drawing>  
  
 Per informazioni dettagliate sull'utilizzo di queste funzionalità, vedere i seguenti argomenti della Guida.  
  
|Per|Vedere|  
|--------|---------|  
|Creare una nuova applicazione Windows Form con[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]|[Procedura dettagliata: Creazione di un Windows Form semplice](http://msdn.microsoft.com/en-us/2d9daec0-0543-41d0-acb1-964f685bddbb)|  
|Utilizzare i controlli nei form|[Procedura: aggiungere controlli Windows Form](https://msdn.microsoft.com/library/0h5y8567.aspx)|   
|Creare la grafica con<xref:System.Drawing></xref:System.Drawing>|[Introduzione alla programmazione grafica](https://msdn.microsoft.com/library/da0f23z7.aspx)|  
|Creazione di controlli personalizzati|[Procedura: ereditare dalla classe UserControl](https://msdn.microsoft.com/library/00ctb4z0.aspx)|  
  
## <a name="displaying-and-manipulating-data"></a>Visualizzazione e modifica dei dati  
 Molte applicazioni devono visualizzare i dati da un database, da un file XML, servizi Web XML o altre origini di dati. Windows Form fornisce un controllo flessibile denominato il <xref:System.Windows.Forms.DataGridView>controllo per il rendering di dati tabulari in un formato tradizionale basato su riga e colonna, in modo che ciascun blocco di dati occupi una cella.</xref:System.Windows.Forms.DataGridView> Utilizzando <xref:System.Windows.Forms.DataGridView>è possibile personalizzare l'aspetto delle singole celle, bloccare le colonne e righe arbitrarie e visualizzare controlli complessi all'interno delle celle, tra le altre funzionalità.</xref:System.Windows.Forms.DataGridView>  
  
 Il collegamento alle origini dati tramite una rete è un'attività semplice con gli smart client Windows Form. Il <xref:System.Windows.Forms.BindingSource>componente novità di Windows Form in [!INCLUDE[vsprvslong](../../../csharp/misc/includes/vsprvslong_md.md)] e [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)], rappresenta una connessione a un'origine dati ed espone metodi per l'associazione dati ai controlli, spostamento ai record precedenti e successive, la modifica di record e salvare le modifiche nell'origine originale.</xref:System.Windows.Forms.BindingSource> Il <xref:System.Windows.Forms.BindingNavigator>controllo fornisce un'interfaccia semplice tramite il <xref:System.Windows.Forms.BindingSource>componente agli utenti di spostarsi tra i record.</xref:System.Windows.Forms.BindingSource> </xref:System.Windows.Forms.BindingNavigator>  
  
### <a name="data-bound-controls"></a>Controlli con associazione a dati  
 È possibile creare controlli associati a dati con facilità tramite la finestra Origini dati, che consente di visualizzare origini dati quali database, servizi Web e oggetti nel progetto. È possibile creare controlli associati a dati mediante il trascinamento di elementi da questa finestra nei form del progetto. È anche possibile connettere i controlli esistenti ai dati mediante il trascinamento di oggetti dalla finestra Origini dati nei controlli esistenti.  
  
### <a name="settings"></a>Impostazioni  
 Un altro tipo di associazione dati che è possibile gestire in Windows Form sono le impostazioni. La maggior parte delle applicazioni smart client devono conservare alcune informazioni relative al proprio stato in fase di esecuzione, ad esempio le ultime dimensioni note dei form e conservare i dati di preferenze dell'utente, ad esempio le posizioni predefinite per i file salvati. La funzionalità Impostazioni applicazione risolve queste problematiche offrendo un modo semplice per archiviare entrambi i tipi di impostazioni nel computer client. Una volta definite mediante [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] o un editor di codice, queste impostazioni vengono mantenute come XML e lette automaticamente in memoria in fase di esecuzione.  
  
 Per informazioni dettagliate sull'utilizzo di queste funzionalità, vedere i seguenti argomenti della Guida.  
  
|Per|Vedere|  
|--------|---------|  
|Utilizzare il <xref:System.Windows.Forms.BindingSource>componente</xref:System.Windows.Forms.BindingSource>|[Procedura: associare controlli Windows Form al componente BindingSource utilizzando la finestra di progettazione](https://msdn.microsoft.com/library/801dxw2t.aspx)|  
|Lavorare con [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] origini dati|[Procedura: ordinare e filtrare i dati ADO.NET con il componente BindingSource Windows Form](https://msdn.microsoft.com/library/ya3sah92.aspx)|  
|Utilizzare la finestra Origini dati|[Procedura dettagliata: visualizzazione di dati in un Windows Form](https://docs.microsoft.com/visualstudio/data-tools/accessing-data-in-visual-studio)|  
  
## <a name="deploying-applications-to-client-computers"></a>Distribuzione delle applicazioni ai client  
 Dopo aver scritto l'applicazione, è necessario inviarlo agli utenti in modo che possano installarla ed eseguirla sui propri computer client. Utilizzo di [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] tecnologia, è possibile distribuire le applicazioni dall'interno [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] con pochi clic e fornire agli utenti con un URL che punta all'applicazione sul Web. [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]gestisce tutti gli elementi e le dipendenze dell'applicazione e garantisce che l'applicazione sia installato correttamente nel computer client.  
  
 Le applicazioni [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] possono essere configurate per essere eseguite solo quando l'utente è connesso alla rete oppure per essere eseguite sia online che offline. Quando si specifica che un'applicazione deve supportare l'operazione non in linea, [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] aggiunge un collegamento all'applicazione dell'utente **avviare** menu, in modo che l'utente possa aprirlo senza utilizzare l'URL.  
  
 Quando si aggiorna l'applicazione, vengono pubblicati un nuovo manifesto della distribuzione e una nuova copia dell'applicazione sul server Web. [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]rileva la presenza di un aggiornamento e aggiorna l'installazione dell'utente. programmazione personalizzata non è necessario per aggiornare gli assembly precedenti.  
  
 Per un'introduzione completa a [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)], vedere [protezione di applicazioni ClickOnce](https://docs.microsoft.com/visualstudio/deployment/clickonce-security-and-deployment). Per informazioni dettagliate sull'utilizzo di queste funzionalità, vedere i seguenti argomenti:  
  
|Per|Vedere|  
|--------|---------|  
|Distribuire un'applicazione con[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]|[Procedura: Pubblicare un'applicazione ClickOnce mediante la Pubblicazione guidata](https://docs.microsoft.com/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [Procedura dettagliata: distribuzione manuale di un'applicazione ClickOnce](https://docs.microsoft.com/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|  
|Aggiornamento un [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] distribuzione|[Procedura: Gestire gli aggiornamenti per un'applicazione ClickOnce](https://docs.microsoft.com/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|  
|Gestire la sicurezza con[!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)]|[Procedura: Abilitare le impostazioni di sicurezza ClickOnce](https://docs.microsoft.com/visualstudio/deployment/how-to-enable-clickonce-security-settings)|  
  
## <a name="other-controls-and-features"></a>Altri controlli e funzionalità  
 Windows Form dispone di altre funzioni che rendono le comuni attività di implementazione estremamente semplici e rapide, quali il supporto per la creazione di caselle di dialogo, la stampa, l'aggiunta della Guida e la documentazione, la localizzazione dell'applicazione in diverse lingue. Inoltre, Windows Form si basa sull'infrastruttura di sicurezza del [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], che consente di rilasciare applicazioni più sicure ai clienti.  
  
 Per informazioni dettagliate sull'utilizzo di queste funzionalità, vedere i seguenti argomenti:  
  
|Per|Vedere|  
|--------|---------|  
|Stampare il contenuto di un form|[Procedura: stampare grafica in Windows Form](https://msdn.microsoft.com/library/741a0ktc.aspx)<br /><br /> [Procedura: stampare un File di testo con più pagine in Windows Form](https://msdn.microsoft.com/library/cwbe712d.aspx)|   
|Altre informazioni sulla sicurezza di Windows Form|[Sicurezza nella panoramica sui Windows Form](https://msdn.microsoft.com/library/90k49ccb.aspx)|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Panoramica sui Windows Form](https://msdn.microsoft.com/library/8bxxy49h.aspx)   
 [Oggetto My.Forms](../../../visual-basic/language-reference/objects/my-forms-object.md)
