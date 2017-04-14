---
title: "UI Automation Support for the ComboBox Control Type | Microsoft Docs"
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
  - "control types, Combo Box"
  - "UI Automation, Combo Box control type"
  - "ComboBox controls"
ms.assetid: bb321126-4770-41da-983a-67b7b89d45dd
caps.latest.revision: 23
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 23
---
# UI Automation Support for the ComboBox Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo ComboBox. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i pattern di controllo e gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
 Una casella combinata è un casella di riepilogo combinata con un controllo statico o un controllo di modifica che visualizza l'elemento attualmente selezionato nel componente casella di riepilogo della casella combinata. Il componente casella di riepilogo del controllo viene visualizzato ogni volta o solo quando l'utente seleziona la freccia a discesa \(un pulsante di comando\) accanto al controllo. Se il campo di selezione è un controllo di modifica, l'utente può immettere informazioni non presenti nell'elenco. In caso contrario, l'utente può solo selezionare gli elementi nell'elenco.  
  
 Nelle sezioni seguenti vengono definiti la struttura ad albero necessaria di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], le proprietà, i pattern di controllo e gli eventi per il tipo di controllo ComboBox. I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si applicano a tutti i controlli casella combinata, in [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente vengono illustrate la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli casella combinata e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|ComboBox<br /><br /> -   Edit \(0 o 1\)<br />-   List \(1\)<br />-   List Item \(elemento figlio di List; da 0 a molti\)<br />-   Button \(1\)|ComboBox<br /><br /> -   List Item \(da 0 a molti\)|  
  
 Il controllo di modifica nella visualizzazione controlli della casella combinata è necessario solo se la casella combinata può essere modificata in modo che accetti qualsiasi input, come nel caso della casella combinata nella finestra di dialogo Esegui.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per i controlli casella combinata. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vedere le note.|Supportata se è presente un rettangolo di delimitazione. Se non tutti i punti all'interno del rettangolo di delimitazione sono selezionabili ed è stato eseguito un processo di hit testing specializzato, eseguire l'override e implementare un punto selezionabile.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ComboBox|Questo valore è uguale per tutti i framework dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Vedere le note.|Il testo della Guida per i controlli casella combinata deve spiegare perché all'utente viene chiesto di scegliere un'opzione dalla casella combinata. Il testo è simile a quello delle informazioni presentate in una descrizione comando. Ad esempio, "Selezionare un'opzione per impostare la risoluzione dello schermo".|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo casella combinata viene sempre incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo casella combinata viene sempre incluso nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|I controlli casella combinata espongono un set di elementi da un contenitore di selezione. Il controllo casella combinata può ricevere lo stato attivo, anche se, quando un client di automazione interfaccia utente imposta lo stato attivo su una casella combinata, tutti gli elementi nel sottoalbero della casella combinata possono ricevere lo stato attivo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Vedere le note.|I controlli casella combinata in genere includono un'etichetta di testo statico a cui questa proprietà fa riferimento.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"combo box"|Stringa localizzata corrispondente al tipo di controllo ComboBox.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Il controllo casella combinata in genere ricava il proprio nome da un controllo di testo statico.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli casella combinata. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo|Supporto|Note|  
|--------------------------|--------------|----------|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Sì|Il controllo casella combinata, per essere tale, deve sempre contenere il pulsante a discesa.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Sì|Visualizza la selezione corrente nella casella combinata. Questo supporto viene delegato alla casella di riepilogo sotto la casella combinata.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|A seconda dei casi|Se la casella combinata può accettare valori di testo arbitrari, il pattern Value deve essere supportato. Questo pattern consente di impostare a livello di codice i contenuti delle stringhe della casella combinata. Se il pattern Value non è supportato, significa che l'utente deve effettuare una selezione tra gli elementi elenco nel sottoalbero della casella combinata.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|Never|Il pattern Scroll non è mai direttamente supportato in una casella combinata. È supportato se è possibile scorrere una casella di riepilogo contenuta in una casella combinata. Può essere supportato solo quando la casella di riepilogo è visibile sullo schermo.|  
  
<a name="Required_Events"></a>   
## Eventi obbligatori  
 La tabella seguente elenca gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli casella combinata. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto|Note|  
|----------------------------------------------------------------------------------|--------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>.|Obbligatorio|None|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty>.|A seconda dei casi|Se il controllo supporta il pattern Value, deve supportare questo evento.|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.ComboBox>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)