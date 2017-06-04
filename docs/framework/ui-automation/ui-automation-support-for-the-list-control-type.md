---
title: "UI Automation Support for the List Control Type | Microsoft Docs"
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
  - "control types, List"
  - "List control type"
  - "UI Automation, List control type"
ms.assetid: 0e959fcb-50f2-413b-948d-7167d279bc11
caps.latest.revision: 20
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 20
---
# UI Automation Support for the List Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo elenco. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e i pattern di controllo.  
  
 Il tipo di controllo elenco consente di organizzare uno o più gruppi di elementi permettendo a un utente di selezionare uno o più elementi. Il tipo di controllo elenco prevede una restrizione ampia sui tipi di elementi figlio che può contenere. I provider di automazione interfaccia utente sono quindi in grado di supportare un elemento noto per i contenitori di selezione.  
  
 I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] illustrati nelle sezioni seguenti si applicano a tutti i controlli che implementano il tipo di controllo elenco, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]. I controlli contenitore elenco sono un esempio di controlli che implementano il tipo di controllo elenco.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente vengono illustrate due visualizzazioni dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativamente ai controlli elenco e viene descritto il possibile contenuto di ogni visualizzazione. Nella visualizzazione controlli sono contenuti solo elementi controllo e nella visualizzazione contenuto vengono rimosse le informazioni ridondanti dell'albero. Ad esempio, un controllo testo usato come etichetta di una casella combinata sarà esposto come `ComboBox NameProperty`. Poiché il controllo testo è già esposto in questo modo tramite la visualizzazione controlli, non è necessario che venga esposto due volte e, pertanto, viene rimosso dalla visualizzazione contenuto. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|Contiene elementi che corrispondono ai controlli.|Rimuove le informazioni ridondanti dell'albero in modo che i prodotti di assistive technology dispongano di un insieme ridotto di informazioni significative per l'utente finale.|  
|Elenco<br /><br /> -   DataItem \(0 o più\)<br />-   ListItem \(0 o più\)<br />-   Group \(0 o più\)<br />-   ScrollBar \(0, 1 o 2\)|Elenco<br /><br /> -   DataItem \(0 o più\)<br />-   ListItem \(0 o più\)<br />-   Group \(0 o più\)|  
  
 La visualizzazione controlli per un controllo che implementa il tipo di controllo elenco \(ad esempio un controllo elenco\) contiene:  
  
-   Zero o più elementi nel controllo elenco \(gli elementi possono essere basati sui tipi di controllo ListItem o DataItem\)  
  
-   Zero o più controlli gruppo in un controllo elenco  
  
-   Zero, uno o due controlli barra di scorrimento  
  
-  
  
 La visualizzazione contenuto di un controllo che implementa il tipo di controllo elenco \(ad esempio un controllo elenco\) contiene:  
  
-   Zero o più elementi nel controllo elenco \(gli elementi possono essere basati sui tipi di controllo ListItem o DataItem\)  
  
-   Zero o più gruppi nel controllo elenco  
  
 Un controllo elenco non deve contenere elementi con una relazione gerarchica diversa dal raggruppamento. Se gli elementi hanno figli nell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], il contenitore elenco deve essere basato sul tipo di controllo Tree.  
  
 Gli elementi selezionabili nel controllo elenco sono disponibili dai discendenti nell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] del controllo elenco. Tutti gli elementi nel controllo elenco devono appartenere allo stesso gruppo di selezione. Gli elementi selezionabili nell'elenco devono essere esposti come tipi di controllo ListItem \(anziché DataItem\).  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per i controlli elenco. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vedere le note.|Se l'elenco ha un punto selezionabile, ovvero un punto su cui è possibile fare clic affinché l'elenco assuma lo stato attivo, tale punto deve essere esposto tramite questa proprietà.<br /><br /> Se il valore della proprietà `IsOffScreen` è True, verrà generato l'oggetto <xref:System.Windows.Automation.NoClickablePointException>.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vedere le note.|Se il controllo può ricevere lo stato attivo, deve supportare questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Il valore della proprietà Name di un controllo elenco deve fornire la categoria di opzioni da cui l'utente effettua la selezione. Questa proprietà deriva in genere il nome da un'etichetta di testo statico. Se non è presente alcuna etichetta di testo statico, lo sviluppatore dell'applicazione deve esporre un valore per la proprietà Name.<br /><br /> L'unico caso in cui questa proprietà non è obbligatoria per i controlli elenco è quando si usa il controllo all'interno del sottoalbero di un altro controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Vedere le note.|Se è presente un'etichetta di testo statico, questa proprietà deve esporre un riferimento a tale controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Elenco|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"elenco"|Stringa localizzata corrispondente al tipo di controllo elenco.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo elenco è sempre incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo elenco è sempre incluso nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|Se il contenitore può accettare input da tastiera, il valore di questa proprietà deve essere True.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Vedere le note.|Il testo della Guida per i controlli elenco deve illustrare il motivo per cui viene chiesto all'utente di effettuare una selezione da un elenco di opzioni. Ad esempio, "La selezione di un elemento dall'elenco consente di impostare la risoluzione per il monitor".|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo e proprietà obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo per l'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati dai controlli elenco. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo\/proprietà del pattern|Supporto\/valore|Note|  
|-------------------------------------------------|----------------------|----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Obbligatorio|Tutti i controlli che supportano il tipo di controllo elenco devono implementare `ISelectionProvider` quando viene gestito uno stato di selezione tra gli elementi nel controllo. Se gli elementi all'interno del contenitore non sono selezionabili, usare il tipo di controllo Group.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|A seconda dei casi|Nei controlli elenco non è necessario che un elemento sia sempre selezionato.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|A seconda dei casi|I controlli elenco possono essere contenitori per una o più selezioni.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|A seconda dei casi|Implementare questo pattern di controllo se gli elementi nel contenitore sono scorrevoli.|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|A seconda dei casi|Implementare questo pattern quando è necessario rendere disponibile lo spostamento nella griglia elemento per elemento.|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|A seconda dei casi|Implementare questo pattern di controllo se il controllo può supportare più visualizzazioni degli elementi nel contenitore.|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|Mai|`ITableProvider` non è mai supportato per il tipo di controllo elenco. Se il controllo deve supportare questo pattern di controllo, deve essere basato sul tipo del controllo DataGrid.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli elenco. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto\/valore|Note|  
|----------------------------------------------------------------------------------|----------------------|----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty>.|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|Nessuna|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.List>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)