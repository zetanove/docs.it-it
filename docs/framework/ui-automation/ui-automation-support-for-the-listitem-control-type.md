---
title: "UI Automation Support for the ListItem Control Type | Microsoft Docs"
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
  - "List Item control type"
  - "UI Automation, List Item control type"
ms.assetid: 34f533bf-fc14-4e78-8fee-fb7107345fab
caps.latest.revision: 24
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 24
---
# UI Automation Support for the ListItem Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo <xref:System.Windows.Automation.ControlType.ListItem>. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e i pattern di controllo.  
  
 I controlli elemento elenco sono un esempio di controlli che implementano il tipo di controllo ListItem.  
  
 Nelle sezioni seguenti vengono definiti la struttura ad albero, le proprietà, i pattern di controllo e gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo ListItem. I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si applicano a tutti i controlli elenco, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente viene illustrata la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli elemento elenco e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|ListItem<br /><br /> -   Image \(0 o più\)<br />-   Text \(0 o più\)<br />-   Edit \(0 o più\)|ListItem|  
  
 Gli elementi figlio di un controllo elemento elenco all'interno della visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] deve sempre essere "0". Se la struttura del controllo è tale che altri elementi sono contenuti sotto il controllo elemento elenco, tale struttura deve soddisfare i requisiti per il tipo di controllo [UI Automation Support for the TreeItem Control Type](../../../docs/framework/ui-automation/ui-automation-support-for-the-treeitem-control-type.md).  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per i controlli elemento elenco. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il valore di questa proprietà include l'area dei contenuti immagine e testo dell'elemento dell'elenco.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|A seconda dei casi|Se l'elenco ha un punto selezionabile ovvero un punto su cui è possibile fare clic affinché l'elenco assuma lo stato attivo, tale punto deve essere esposto tramite questa proprietà. Se l'elenco è completamente coperto da elementi elenco discendenti, verrà generata un'eccezione <xref:System.Windows.Automation.NoClickablePointException> per indicare che il client deve richiedere un elemento all'interno dell'elenco come punto selezionabile.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Il valore della proprietà name di un controllo elemento elenco deriva dal contenuto di testo dell'elemento.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Vedere le note.|Se è presente un'etichetta di testo statico, questa proprietà deve esporre un riferimento a tale controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ListItem|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"list item"|Stringa localizzata corrispondente al tipo di controllo ListItem.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo elenco è sempre incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo elenco è sempre incluso nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|Se il contenitore può accettare input da tastiera, il valore di questa proprietà deve essere true.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|""|Il testo della Guida per gli elenchi deve spiegare il motivo per cui all'utente viene chiesto di effettuare una selezione da un elenco di opzioni, che è in genere lo stesso tipo di informazioni visualizzate tramite una descrizione comando. Ad esempio, "Selezionare un'opzione per impostare la risoluzione dello schermo".|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemTypeProperty>|A seconda dei casi|Questa proprietà deve essere esposta per i controlli elemento elenco che rappresentano un oggetto sottostante. In genere, questi controlli elemento elenco includono un'icona associato al controllo che gli utenti associano all'oggetto sottostante.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|A seconda dei casi|Questa proprietà deve restituire un valore indicante se l'elemento elenco viene attualmente visualizzato tramite scorrimento all'interno del contenitore padre che implementa il pattern di controllo Scroll.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo per l'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati dai controlli elemento elenco. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo|Supporto|Note|  
|--------------------------|--------------|----------|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Sì|Il controllo elemento elenco deve implementare questo pattern di controllo. Ciò consente ai controlli elemento elenco di indicare quando sono selezionati.|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|A seconda dei casi|Se l'elemento elenco è contenuto in un contenitore scorrevole, è necessario implementare questo pattern di controllo.|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|A seconda dei casi|Se l'elemento elenco è selezionabile e l'azione non comporta una modifica dello stato di selezione, è necessario implementare questo pattern di controllo.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|A seconda dei casi|Se l'elemento può essere modificato per visualizzare o nascondere informazioni, è necessario implementare questo pattern di controllo.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|A seconda dei casi|Se l'elemento può essere modificato, è necessario implementare questo pattern di controllo. Le modifiche al controllo elemento elenco vengono apportate modifiche ai valori di <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> e <xref:System.Windows.Automation.Provider.IValueProvider.Value%2A>.|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|A seconda dei casi|Se è supportato lo spostamento spaziale tra elementi all'interno del contenitore elenco e il contenitore è organizzato in righe e colonne, è necessario implementare il pattern di controllo GridItem.|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|A seconda dei casi|Se l'elemento include un comando che può essere eseguito su di esso, oltre alla selezione, è necessario implementare questo pattern. In genere si tratta di un'azione associata all'esecuzione del doppio clic sul controllo elemento elenco. Un esempio di queste azioni è l'avvio di un documento da [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)] o la riproduzione di un file audio in [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)].|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli elemento elenco. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto|Note|  
|----------------------------------------------------------------------------------|--------------|----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|A seconda dei casi|Nessuno|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|Obbligatorio|Nessuno|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuno|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty>.|A seconda dei casi|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>.|A seconda dei casi|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty>.|A seconda dei casi|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>.|A seconda dei casi|Nessuno|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|Nessuno|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.ListItem>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)