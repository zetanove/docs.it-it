---
title: "UI Automation Support for the TreeItem Control Type | Microsoft Docs"
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
  - "control types, Tree Item"
  - "Tree Item control type"
  - "UI Automation, Tree Item control type"
ms.assetid: 229f341a-477f-434e-b877-4db9973068eb
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# UI Automation Support for the TreeItem Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo TreeItem. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e i pattern di controllo.  
  
 Il tipo di controllo TreeItem rappresenta un nodo all'interno di un contenitore dell'albero. Ciascun nodo può contenere altri nodi, denominati nodi figlio. I nodi padre, ovvero i nodi contenenti nodi figlio, possono essere visualizzati in formato espanso o compresso.  
  
 Nelle sezioni seguenti vengono definiti la struttura ad albero, le proprietà, i pattern di controllo e gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo TreeItem. I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si applicano a tutti i controlli TreeItem, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente viene illustrata la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli TreeItem e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|TreeItem<br /><br /> -   CheckBox \(0 o 1\)<br />-   Image \(0 o 1\)<br />-   Button \(0 o 1\)<br />-   TreeItem \(0 o più\)|TreeItem<br /><br /> -   TreeItem \(0 o più\)|  
  
 I controlli TreeItem possono avere zero o più controlli TreeItem figlio nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Se il controllo TreeItem ha altre funzionalità oltre a quelle esposte nei pattern di controllo elencati di seguito, il controllo deve basarsi sul tipo di controllo DataItem.  
  
 Gli elementi compressi dell'albero vengono visualizzati nella visualizzazione contenuto o visualizzazione controlli solo dopo essere stati espansi e resi visibili oppure visualizzati mediante lo scorrimento.  
  
 La visualizzazione controlli può contenere dettagli aggiuntivi per un controllo, tra cui un'immagine associata o un pulsante. Ad esempio, un elemento in una visualizzazione Struttura potrebbe contenere un'immagine e un pulsante per espandere o comprimere la struttura. Questi oggetti dettagliati non vengono visualizzati nella visualizzazione contenuto perché le informazioni sono già rappresentate dall'elemento padre dell'albero. Gli elementi dell'albero esclusi dalla visualizzazione tramite lo scorrimento saranno visualizzati sia nella visualizzazione controlli che nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] devono avere la proprietà <xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> impostata su true.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per i controlli elenco. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vedere le note.|Questa proprietà deve restituire il percorso dell'elemento che causa la modifica dello stato di selezione dell'elemento oppure ne determina lo stato attivo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|TreeItem|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo elenco è sempre incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo elenco è sempre incluso nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|Vedere le note.|Questa proprietà è impostata per indicare quando un controllo TreeItem viene escluso dalla visualizzazione mediante lo scorrimento.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vedere le note.|Se il controllo può ricevere lo stato attivo, deve supportare questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemTypeProperty>|Vedere le note.|Se il controllo TreeItem usa un'icona per indicare che si tratta di un particolare tipo di oggetto, questa proprietà deve essere supportata e indicare il tipo di oggetto.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Per i controlli TreeItem l'etichetta viene definita automaticamente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"tree item"|Stringa localizzata corrispondente al tipo di controllo TreeItem.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Questa proprietà espone il testo visualizzato per ogni controllo TreeItem.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo per l'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati dai controlli elenco. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo\/proprietà del pattern|Supporto\/valore|Note|  
|-------------------------------------------------|----------------------|----------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|A seconda dei casi|Implementare questo pattern di controllo se il controllo TreeItem dispone di un comando separato su cui è possibile eseguire azioni.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Sì|Tutti i controlli TreeItem possono essere espansi o compressi.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider.ExpandCollapseState%2A>|Espanso, compresso o nodo foglia|I controlli TreeItem saranno nodi foglia quando non sono espansi o compressi.|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|A seconda dei casi|Implementare questo pattern di controllo se il contenitore dell'albero supporta il pattern di controllo Scroll.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|A seconda dei casi|Implementare questo pattern di controllo se è possibile disporre di una selezione attiva che viene mantenuta quando l'utente torna al contenitore dell'albero.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider.SelectionContainer%2A>|Sì|Questa proprietà espone lo stesso contenitore per tutti gli elementi all'interno del contenitore.|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|A seconda dei casi|Implementare questo pattern di controllo se il controllo TreeItem è associato a una casella di controllo.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli TreeItem. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto|Note|  
|----------------------------------------------------------------------------------|--------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>.|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>.|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty>.|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty>.|A seconda dei casi|Nessuna|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.TreeItem>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)