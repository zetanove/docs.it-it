---
title: "UI Automation Support for the Image Control Type | Microsoft Docs"
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
  - "UI Automation, Image control type"
  - "control types, Image"
  - "Image control type"
ms.assetid: 4e0eeefb-e09b-46d2-b83b-0a7e35543ab8
caps.latest.revision: 21
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 21
---
# UI Automation Support for the Image Control Type
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono fornite informazioni sul supporto di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo Image. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] un tipo di controllo è un set di condizioni che un controllo deve soddisfare per usare la proprietà <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Le condizioni includono linee guida specifiche per la struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], i valori delle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e i pattern di controllo.  
  
 I controlli Image usati come icone, grafica informativa e grafici supportano il tipo di controllo Image. I controlli usati come immagini di sfondo o filigrana non supportano il tipo di controllo Image.  
  
 Nelle sezioni seguenti vengono definiti la struttura ad albero, le proprietà, i pattern di controllo e gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per il tipo di controllo Image. I requisiti di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si applicano a tutti i controlli immagine, ovvero [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Struttura ad albero di automazione interfaccia utente obbligatoria  
 Nella tabella seguente viene illustrata la visualizzazione controlli e la visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] relativo ai controlli immagine e viene descritto il possibile contenuto di ogni visualizzazione. Per altre informazioni sull'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Visualizzazione controlli|Visualizzazione contenuto|  
|-------------------------------|-------------------------------|  
|Immagine|Immagine \(a seconda che l'immagine contenga informazioni \(in base al valore della proprietà `IsContentElement`\)\)|  
  
<a name="Required_UI_Automation_Properties"></a>   
## Proprietà di automazione interfaccia utente obbligatorie  
 La tabella seguente elenca le proprietà [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] il cui valore o la cui definizione è particolarmente rilevante per il tipo di controllo Image. Per altre informazioni sulle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valore|Note|  
|----------------------------------------------------------------------------------------|------------|----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vedere le note.|Il valore di questa proprietà deve essere univoco in tutti i controlli in un'applicazione.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vedere le note.|Il rettangolo più esterno che contiene l'intero controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vedere le note.|Il punto selezionabile del controllo immagine deve essere un punto all'interno del rettangolo di delimitazione del controllo immagine.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vedere le note.|Se il controllo può ricevere lo stato attivo, deve supportare questa proprietà.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vedere le note.|La proprietà Name deve essere esposta per tutti i controlli immagine che contengono informazioni. L'accesso a livello di codice a queste informazioni richiede che venga specificato un equivalente testuale dell'immagine. Se il controllo immagine è puramente decorativo, deve essere visualizzato solo nella visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e non deve necessariamente avere un nome. I framework dell'interfaccia utente devono supportare una proprietà ALT o testo alternativo sulle immagini, in grado di essere impostata dall'interno del relativo framework. Per questa proprietà verrà quindi eseguito il mapping alla proprietà Name dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Vedere le note.|Se è presente un'etichetta di testo statico, questa proprietà deve esporre un riferimento a tale controllo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Immagine|Questo valore è uguale per tutti i framework dell'interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"image"|Stringa localizzata corrispondente al tipo di controllo Image.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Vedere le note.|Il controllo immagine deve essere incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] quando contiene informazioni significative non ancora esposte all'utente finale.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Il controllo immagine viene sempre incluso nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Vedere le note.|La proprietà HelpText espone una stringa localizzata che descrive l'aspetto visivo effettivo del controllo \(ad esempio, un quadrato rosso con una 'X' bianca\) o altre informazioni sulla descrizione comandi associate all'immagine.<br /><br /> Questa proprietà deve essere supportata quando è necessaria una descrizione lunga per fornire altre informazioni sul controllo immagine, ad esempio in un grafico o diagramma complesso. Questa proprietà esegue il mapping al tag HTML LongDesc e al tag Scalable Vector Graphics \(SVG\) Desc. Gli strumenti di sviluppo che usano i controlli immagine devono supportare una proprietà che consenta la descrizione visiva da impostare per il controllo. È necessario eseguire il mapping di questa proprietà alla proprietà VisualDescription di automazione interfaccia utente.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty>|Vedere le note.|Se il controllo immagine rappresenta le informazioni sullo stato relative a un particolare elemento sullo schermo, il controllo deve essere contenuto all'interno dell'elemento. Quando l'immagine è contenuta in un elemento, tale elemento deve supportare la proprietà Status e generare le notifiche appropriate quando lo stato viene modificato.<br /><br /> Se un'immagine è un controllo autonomo che visualizza lo stato, questa proprietà deve essere supportata.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Pattern di controllo obbligatori per l'automazione interfaccia utente  
 La tabella seguente elenca i pattern di controllo per l'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli immagine. Per altre informazioni sui pattern di controllo, vedere [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Pattern di controllo|Supporto|Note|  
|--------------------------|--------------|----------|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|A seconda dei casi|Se il controllo si trova all'interno di un contenitore della griglia, il controllo immagine supporta il pattern GridItem.|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider>|A seconda dei casi|Se il controllo si trova all'interno di un contenitore con controlli intestazione, il controllo immagine supporta il pattern TableItem.|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Mai|Se il controllo immagine contiene un'immagine selezionabile, il controllo deve supportare un tipo di controllo che supporta il pattern Invoke, ad esempio il tipo di controllo Button.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Mai|I controlli immagine non devono supportare il pattern SelectionItem.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventi di automazione interfaccia utente obbligatori  
 La tabella seguente elenca gli eventi dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] che devono essere supportati da tutti i controlli immagine. Per altre informazioni sugli eventi, vedere [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Supporto|Note|  
|----------------------------------------------------------------------------------|--------------|----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|Mai|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|Mai|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|Mai|Nessuna|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|Mai|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obbligatorio|Nessuna|  
|Evento di modifica della proprietà <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>.|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obbligatorio|Nessuna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obbligatorio|Nessuna|  
  
## Vedere anche  
 <xref:System.Windows.Automation.ControlType.Image>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)