---
title: "UI Automation Support for the Window Control Type | Microsoft Docs"
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
  - "UI Automation, Window control type"
  - "Window control type"
  - "control types, Window"
ms.assetid: 53be78a6-cdcc-4af3-a464-5927d19c54e8
caps.latest.revision: 19
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 19
---
# UI Automation Support for the Window Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo Window. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e i pattern di controllo.  
  
 Il controllo finestra è costituito dalla cornice della finestra, che contiene oggetti figlio, ad esempio barra del titolo, oggetti client e altri oggetti.  
  
 I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] illustrati nelle sezioni seguenti si applicano a tutti i controlli che implementano il tipo di controllo Window, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente viene illustrata la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli finestra e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|Finestra|Finestra|  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per i controlli finestra. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vedere le note.|Il controllo finestra deve avere un punto selezionabile che genererà la selezione o deselezione della finestra.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Window|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo finestra deve essere sempre di tipo contenuto.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo finestra deve essere sempre un controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vedere le note.|Se il controllo può ricevere lo stato attivo, deve supportare questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`null`|I controlli finestra in genere non hanno un'etichetta statica.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"window"|Stringa localizzata corrispondente al tipo di controllo Window.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Il controllo finestra contiene sempre un elemento Window principale che fa riferimento all'elemento associato dall'utente come identificatore più significativo per l'elemento.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli finestra. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo|Supporto|Note|  
|--------------------------|--------------|----------|  
|<xref:System.Windows.Automation.Provider.IDockProvider>|Condizionale|Deve essere supportato se la finestra può essere ancorata.|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|Obbligatorio|Abilita lo spostamento, il ridimensionamento o la rotazione della finestra sullo schermo.|  
|<xref:System.Windows.Automation.Provider.IWindowProvider>|Obbligatorio|Abilita operazioni specifiche per la finestra.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli finestra. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto|Note|  
|----------------------------------------------------------------------------------|--------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>.|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty>.|A seconda dei casi|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty>.|A seconda dei casi|Nessuna|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent>|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.WindowPatternIdentifiers.WindowVisualStateProperty>.|A seconda dei casi|Nessuna|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.Window>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)