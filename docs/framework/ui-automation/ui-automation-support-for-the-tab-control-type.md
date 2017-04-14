---
title: "UI Automation Support for the Tab Control Type | Microsoft Docs"
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
  - "TabControl type"
  - "UI Automation, Tab control type"
  - "control types, Tab"
ms.assetid: f8be2732-836d-4e4d-85e2-73aa39479bf4
caps.latest.revision: 20
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 20
---
# UI Automation Support for the Tab Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo Tab. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. .  
  
 Un controllo Struttura a schede è simile ai separatori in un blocco per appunti o alle etichette in un archivio. L'uso del controllo Struttura a schede consente a un'applicazione di definire più pagine per la stessa area di una finestra o una finestra di dialogo.  
  
 Nelle sezioni seguenti vengono definiti la struttura ad albero, le proprietà, i pattern di controllo e gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo Tab. I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si applicano a tutti i controlli Struttura a schede, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente viene illustrata la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli Struttura a schede e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|Tab<br /><br /> <ul><li>TabItem \(1 o più\)</li><li>ScrollBar \(0 o 1\)<br /><br /> <ul><li>Button \(0 o 2\)</li></ul></li></ul>|Tab<br /><br /> -   TabItem \(1 o più\)|  
  
 I controlli Struttura a schede includono elementi figlio di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] in base al tipo di controllo TabItem. Quando gli elementi della struttura a schede vengono raggruppati, ad esempio nelle applicazioni di Microsoft Office 2007, il tipo di controllo Tab può ospitare anche tipi di controllo Groups per gli elementi della struttura a schede raggruppati, come illustrato nella struttura ad albero seguente.  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|Tab<br /><br /> <ul><li>TabItem \(1 o più\)</li><li>Group \(0 o più\)<br /><br /> <ul><li>TabItem \(0 o più\)</li></ul></li><li>ScrollBar \(0 o più\)<br /><br /> <ul><li>Button \(0 o 2\)</li></ul></li></ul>|Tab<br /><br /> <ul><li>TabItem \(1 o più\)</li><li>Group \(0 o più\)<br /><br /> <ul><li>TabItem \(0 o più\)</li></ul></li></ul>|  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per il tipo di controllo Tab. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vedere le note.|Se il controllo può ricevere lo stato attivo, deve supportare questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Il controllo Struttura a schede raramente richiede una proprietà Name.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|No|Il controllo Struttura a schede non dispone di un punto selezionabile.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Vedere le note.|I controlli Struttura a schede in genere includono un'etichetta di testo statico che viene esposta tramite questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Tab|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"tab"|Stringa localizzata corrispondente al tipo di controllo Tab.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|Il tipo di controllo Tab deve essere in grado di ricevere lo stato attivo. In genere, un client di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] chiama la proprietà SetFocus su un controllo Struttura a schede e uno dei relativi elementi inoltra lo stato attivo al controllo Struttura a schede. È possibile che alcuni contenitori di schede assumano lo stato attivo senza che lo stato attivo venga impostato su uno dei relativi elementi.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo Struttura a schede viene sempre incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo Struttura a schede viene sempre incluso nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.OrientationProperty>|Vedere le note.|Il controllo Struttura a schede deve sempre indicare se è posizionato orizzontalmente o verticalmente.|  
  
<a name="Required_UI_Automation_Control_Patterns_and_Properties"></a>   
## Pattern di controllo e proprietà obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli Struttura a schede. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo\/proprietà del pattern|Supporto\/valore|Note|  
|-------------------------------------------------|----------------------|----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Sì|Tutti i controlli Struttura a schede devono supportare il pattern Selection.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|True|I controlli Struttura a schede richiedono sempre una selezione.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|False|I controlli Struttura a schede sono sempre contenitori a selezione singola.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|A seconda dei casi|Il pattern Scroll deve essere supportato nel controllo Struttura a schede contenente widget che consentono lo scorrimento di un set di elementi della struttura a schede.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli Struttura a schede. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto|Note|  
|----------------------------------------------------------------------------------|--------------|----------|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty>.|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|Nessuna|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.Tab>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)