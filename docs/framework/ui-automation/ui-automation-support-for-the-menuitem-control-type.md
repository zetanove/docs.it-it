---
title: "UI Automation Support for the MenuItem Control Type | Microsoft Docs"
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
  - "control types, Menu Item"
  - "Menu Item control type"
  - "UI Automation, Menu Item control type"
ms.assetid: 54bce311-3d23-40b9-ba90-1bdbdaf8fbba
caps.latest.revision: 23
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 23
---
# UI Automation Support for the MenuItem Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] per il tipo di controllo MenuItem. Viene descritta la struttura ad albero di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] del controllo e vengono descritte le proprietà e i pattern di controllo obbligatori per il tipo di controllo MenuItem.  
  
 Un controllo menu consente l'organizzazione gerarchica degli elementi associati a comandi e gestori eventi. In una tipica applicazione [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] una barra dei menu contiene più voci di menu \(ad esempio **File**, **Modifica** e **Finestra**\), mentre ogni voce di menu visualizza un menu. Un menu contiene una raccolta di voci di menu \(ad esempio **Nuovo**, **Apri** e **Chiudi**\), che può essere espansa per visualizzare altre voci di menu che, se selezionate, consentono di eseguire un'azione specifica. Una voce di menu può trovarsi in un menu, una barra dei menu o una barra degli strumenti.  
  
 Nelle sezioni seguenti vengono definiti la struttura ad albero, le proprietà, i pattern di controllo e gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo MenuItem. I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si applicano a tutti i controlli elenco, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente viene illustrata la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli MenuItem e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|MenuItem "?"<br /><br /> <ul><li>Menu \(sottomenu della voce di menu della Guida in linea\)<br /><br /> <ul><li>MenuItem "Guida in linea"</li><li>MenuItem "Informazioni su Blocco note"</li></ul></li></ul>|MenuItem "?"<br /><br /> -   MenuItem "Guida in linea"<br />-   MenuItem "Informazioni su Blocco note"|  
  
 La visualizzazione controlli del controllo MenuItem presenta la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sopra illustrata. Si noti che la voce di menu **?** è stata inclusa per illustrare più chiaramente la struttura di una tipica gerarchia menu\/sottomenu.  
  
 Per la visualizzazione contenuto, la voce Menu è assente dall'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] perché non apporta informazioni significative per l'utente finale.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per i controlli MenuItem. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà|Valore|Descrizione|  
|---------------|------------|-----------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vedere le note.|Supportata se è presente un rettangolo di delimitazione. Se non tutti i punti all'interno del rettangolo di delimitazione sono selezionabili ed è stato eseguito un processo di hit testing specializzato, eseguire l'override e implementare un punto selezionabile.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vedere le note.|Se il controllo può ricevere lo stato attivo, deve supportare questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|Il controllo MenuItem è incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ed è automaticamente associato a un nome.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Nessuna etichetta|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|MenuItem|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"menu item"|Stringa localizzata corrispondente al tipo di controllo MenuItem.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Il controllo MenuItem non viene mai incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo MenuItem deve essere sempre incluso nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo per l'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati dai controlli MenuItem. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Proprietà del pattern di controllo|Supporto|Note|  
|----------------------------------------|--------------|----------|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|A seconda dei casi|Se il controllo può essere espanso o compresso, implementare <xref:System.Windows.Automation.Provider.IExpandCollapseProvider>.|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|A seconda dei casi|Se il controllo esegue un singolo comando o una singola azione, implementare <xref:System.Windows.Automation.Provider.IInvokeProvider>.|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|A seconda dei casi|Se il controllo rappresenta un'opzione che può essere attivata o disattivata, implementare <xref:System.Windows.Automation.Provider.IToggleProvider>.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|A seconda dei casi|Se il controllo viene usato per effettuare una selezione da un elenco di opzioni tra voci di menu, implementare <xref:System.Windows.Automation.Provider.ISelectionItemProvider>.|  
  
<a name="UI_Automation_Events_for_Menu_Item"></a>   
## Eventi di automazione interfaccia utente per i controlli MenuItem  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] associati al controllo MenuItem.  
  
|Evento|Supporto|Descrizione|  
|------------|--------------|-----------------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|A seconda dei casi|Deve essere generato se il controllo supporta il pattern di controllo Invoke.|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>.|A seconda dei casi|Deve essere generato se il controllo supporta il pattern di controllo Toggle.|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>.|A seconda dei casi|Deve essere generato se il controllo supporta il pattern di controllo ExpandCollapse.|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|A seconda dei casi|Nessuno.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli MenuItem. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto\/valore|Note|  
|----------------------------------------------------------------------------------|----------------------|----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|A seconda dei casi|Nessuno|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|A seconda dei casi|Nessuno|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|A seconda dei casi|Nessuno|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|A seconda dei casi|Nessuno|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|Nessuno|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|Nessuno|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuno|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>.|A seconda dei casi|Nessuno|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>.|A seconda dei casi|Nessuno|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|Nessuno|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|Nessuno|  
  
<a name="Legacy_Issues"></a>   
## Problemi preesistenti  
 Il pattern Toggle è supportato solo quando la voce di menu [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] è selezionata e può essere determinato a livello di codice che è necessaria per il supporto del pattern Toggle. Poiché la voce di menu [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] non espone la possibilità di essere selezionata, il pattern Invoke è supportato quando la voce di menu non è selezionata. Il pattern Invoke verrà eccezionalmente supportato sempre per le voci di menu che devono solo supportare il pattern Toggle. Ciò consente di evitare confusione a livello di client quando un elemento che supporta il pattern Invoke \(quando una voce di menu non è selezionata\) non supporta più il pattern dopo essere stato selezionato.  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.MenuItem>   
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)