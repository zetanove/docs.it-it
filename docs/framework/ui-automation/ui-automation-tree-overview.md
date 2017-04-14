---
title: "Panoramica dell&#39;albero di automazione dell&#39;interfaccia utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "albero di automazione"
  - "Automazione interfaccia utente, struttura ad albero"
ms.assetid: 03b98058-bdb3-47a0-8ff7-45e6cdf67166
caps.latest.revision: 25
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 25
---
# Panoramica dell&#39;albero di automazione dell&#39;interfaccia utente
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare gestita [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classi definite nel <xref:System.Windows.Automation> dello spazio dei nomi. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Prodotti Assistive technology e script di test consentono di passare il [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struttura ad albero per raccogliere informazioni di [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] e i relativi elementi.  
  
 All'interno di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] albero vi è un elemento radice (<xref:System.Windows.Automation.AutomationElement.RootElement%2A>) che rappresenta il desktop corrente e i cui elementi figlio rappresentano le finestre dell'applicazione. Ognuno di questi elementi figlio può contenere elementi che rappresentano parti di [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] , ad esempio menu, pulsanti, barre degli strumenti e le caselle di riepilogo. Tali elementi, a loro volta, possono contenere altri elementi, ad esempio voci di elenco.  
  
 Il [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] albero non è una struttura fissa e viene raramente in modo completo perché potrebbe contenere migliaia di elementi. Parti dell'albero vengono compilate in base alle esigenze e la struttura può subire modifiche man mano che vengono aggiunti, spostati o rimossi elementi.  
  
 Provider di automazione interfaccia utente supportano il [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] albero mediante l'implementazione di spostamento tra gli elementi all'interno di un frammento, costituito da una radice (in genere ospitato in una finestra) e un sottoalbero. I provider, tuttavia, non sono interessati dallo spostamento da un controllo a un altro. Questa operazione viene gestita dal [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] di base, utilizzando le informazioni dai provider di finestra predefinita.  
  
<a name="uiautomation_tree_view"></a>   
## <a name="views-of-the-automation-tree"></a>Visualizzazioni dell'albero di automazione  
 Il [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] albero può essere filtrato per creare visualizzazioni che contengono solo gli <xref:System.Windows.Automation.AutomationElement> oggetti rilevanti per un particolare client. Questo approccio consente ai client di personalizzare la struttura presentata tramite [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per le loro esigenze.  
  
 Il client consente di personalizzare la visualizzazione in due modi: tramite ambito e tramite filtro. L'ambito consiste nel definire l'estensione della visualizzazione, a partire da un elemento di base. Ad esempio, è possibile che l'applicazione cerchi solo i figli diretti del desktop o tutti i discendenti di una finestra dell'applicazione. Il filtro consiste nel definire i tipi di elementi da includere nella visualizzazione.  
  
 Provider di automazione interfaccia utente supportano i filtri mediante la definizione di proprietà sugli elementi, inclusi il <xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty> e <xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty> proprietà.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]fornisce tre visualizzazioni predefinite. che sono definite dal tipo di filtro eseguito. L'ambito di qualsiasi visualizzazione è definito dall'applicazione. L'applicazione può inoltre applicare altri filtri sulle proprietà, ad esempio per includere solo i controlli abilitati in una visualizzazione controlli.  
  
<a name="uiautomation_raw_view"></a>   
### <a name="raw-view"></a>Visualizzazione non elaborata  
 La visualizzazione non elaborata di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struttura ad albero è l'intero albero di <xref:System.Windows.Automation.AutomationElement> oggetti per cui il desktop è la radice. La visualizzazione non elaborata riproduce la struttura a livello di codice nativa di un'applicazione ed è pertanto la visualizzazione più dettagliata disponibile. Costituisce inoltre la base sulla quale vengono compilate le altre visualizzazioni dell'albero. Poiché questa visualizzazione dipende sottostante [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] framework, la visualizzazione non elaborata di un [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] pulsante avrà una visualizzazione diversa non elaborata da un [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] pulsante.  
  
 La visualizzazione non elaborata viene ottenuta eseguendo una ricerca per gli elementi senza specificare proprietà o tramite il <xref:System.Windows.Automation.TreeWalker.RawViewWalker> per esplorare la struttura ad albero.  
  
<a name="uiautomation_control_view"></a>   
### <a name="control-view"></a>Visualizzazione controlli  
 Visualizzazione controlli di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] albero semplifica l'attività del prodotto tecnologici di descrivere la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] per l'utente finale e aiutarli a tale utente finale interagisce con l'applicazione poiché che mappa il [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] struttura percepito da un utente finale.  
  
 La visualizzazione controlli è un sottoinsieme della visualizzazione non elaborata. Include tutte [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] gli elementi della visualizzazione non elaborata che un utente finale potrebbe considerare interattivi o inerenti la struttura logica del controllo nel [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Esempi di [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] gli elementi che contribuiscono alla struttura logica del [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)], ma non interattiva, i contenitori di elementi, ad esempio le intestazioni della visualizzazione elenco, le barre degli strumenti, menu e barra di stato. Gli elementi non interattivi usati semplicemente a scopi di layout o decorativi non saranno presenti nella visualizzazione controlli. Ne è un esempio un pannello usato solo per il layout di controlli in una finestra di dialogo che non contiene alcuna informazione. Gli elementi non interattivi presenti nella visualizzazione controlli sono grafici con informazioni e testo statico in una finestra di dialogo. Gli elementi non interattivi inclusi nella visualizzazione controlli non possono ricevere lo stato attivo della tastiera.  
  
 La visualizzazione del controllo viene ottenuta eseguendo una ricerca per gli elementi che hanno il <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A> impostata su `true`, oppure utilizzando il <xref:System.Windows.Automation.TreeWalker.ControlViewWalker> per esplorare la struttura ad albero.  
  
<a name="uiautomation_content_view"></a>   
### <a name="content-view"></a>Visualizzazione contenuto  
 La visualizzazione del contenuto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struttura ad albero è un subset della visualizzazione control. Contiene [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] gli elementi che contengono le informazioni effettive in un'interfaccia utente, tra cui [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] gli elementi che possono ricevere tastiera e del testo che non è un'etichetta in un [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] elemento. Ad esempio, i valori in una casella combinata a discesa saranno presenti nella visualizzazione contenuto poiché rappresentano le informazioni usate da un utente finale. Nella visualizzazione di contenuto, una casella combinata e una casella di riepilogo sono entrambe rappresentate come una raccolta di [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] gli elementi in cui è possibile selezionare uno o più elementi. Il fatto che un elemento sia sempre aperto e un altro possa essere espanso o compresso è irrilevante nella visualizzazione contenuto, che è progettata per mostrare i dati, o il contenuto, presentato all'utente.  
  
 Visualizzazione di contenuto viene ottenuta eseguendo una ricerca per gli elementi che hanno il <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A> impostata su `true`, oppure utilizzando il <xref:System.Windows.Automation.TreeWalker.ContentViewWalker> per esplorare la struttura ad albero.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Automation.AutomationElement>   
 [Panoramica di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-overview.md)