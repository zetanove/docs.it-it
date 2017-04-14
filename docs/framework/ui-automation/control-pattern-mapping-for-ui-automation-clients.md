---
title: "Control Pattern Mapping for UI Automation Clients | Microsoft Docs"
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
  - "control patterns, for UI Automation clients"
  - "UI Automation, clients, control patterns for"
ms.assetid: 8b81645b-8be3-4e26-9c98-4fb0fceca06b
caps.latest.revision: 18
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 18
---
# Control Pattern Mapping for UI Automation Clients
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono elencati i tipi di controllo e i pattern di controllo associati.  
  
 Nella tabella seguente i pattern di controllo sono organizzati nelle categorie seguenti:  
  
-   Supportato. Il controllo deve supportare questo il pattern di controllo.  
  
-   Supporto condizionale. Il controllo può supportare questo pattern di controllo a seconda dello stato del controllo.  
  
-   Non supportato. Il controllo non supporta questo pattern di controllo. I controlli personalizzati possono supportare questo pattern di controllo.  
  
> [!NOTE]
>  Alcuni controlli sono caratterizzati dal supporto condizionale per diversi pattern di controllo a seconda della funzionalità del controllo. Ad esempio, il controllo voce di menu prevede il supporto condizionale per il pattern di controllo <xref:System.Windows.Automation.InvokePattern>, <xref:System.Windows.Automation.ExpandCollapsePattern>, <xref:System.Windows.Automation.TogglePattern> o <xref:System.Windows.Automation.SelectionItemPattern> a seconda della relativa funzione nel controllo menu.  
  
<a name="control_mapping_clients"></a>   
## Pattern di controllo di automazione interfaccia utente per i client  
  
|Tipo di controllo|Supportato|Supporto condizionale|Non supportato|  
|-----------------------|----------------|---------------------------|--------------------|  
|Button|Nessuno|Invoke, Toggle, ExpandCollapse|Nessuno|  
|Calendar|Grid, Table|Selection, Scroll|Value|  
|CheckBox|Toggle|Nessuno|Nessuno|  
|ComboBox|ExpandCollapse|Selection, Value|Scroll|  
|DataGrid|Grid|Scroll, Selection, Table|Nessuno|  
|DataItem|SelectionItem|ExpandCollapse, GridItem, ScrollItem, Table, Toggle, Value|Nessuno|  
|Document|Text|Scroll, Value|Nessuno|  
|Edit|Nessuno|Text, RangeValue, Value|None|  
|Group|Nessuno|ExpandCollapse|Nessuno|  
|Header|Nessuno|Transform|Nessuno|  
|HeaderItem|Nessuno|Transform, Invoke|Nessuno|  
|Hyperlink|Invoke|Value|Nessuno|  
|Image|Nessuno|GridItem, TableItem|Invoke, SelectionItem|  
|List|Nessuno|Grid, MultipleView, Scroll, Selection|Table|  
|ListItem|Item|ExpandCollapse, GridItem, Invoke, ScrollItem, Toggle, Value|Nessuno|  
|Menu|Nessuno|Nessuno|Nessuno|  
|MenuBar|Nessuno|ExpandCollapse, Dock, Transform|Nessuno|  
|MenuItem|Nessuno|ExpandCollapse, Invoke, SelectionItem, Toggle|Nessuno|  
|Pane|Nessuno|Dock Scroll, Transform|Window|  
|ProgressBar|Nessuno|RangeValue, Value|Nessuno|  
|RadioButton|SelectionItem|Nessuno|Toggle|  
|ScrollBar|Nessuno|RangeValue|Scroll|  
|Separator|Nessuno|Nessuno|Nessuno|  
|Slider|Nessuno|RangeValue, Selection, Value|Nessuno|  
|Spinner|Nessuno|RangeValue, Selection, Value|Nessuno|  
|Pulsante di menu combinato|Invoke, ExpandCollapse|Nessuno|Nessuno|  
|StatusBar|Nessuno|Grid|Nessuno|  
|Tab|Selection|Scroll|Nessuno|  
|TabItem|SelectionItem|Nessuno|Invoke|  
|Table|Grid, GridItem, Table, TableItem|Nessuno|Nessuno|  
|Text|Nessuno|GridItem, TableItem, Text|Valore|  
|Thumb|Transform|Nessuno|Nessuno|  
|TitleBar|Nessuno|Nessuno|Nessuno|  
|ToolBar|Nessuno|Dock, ExpandCollapse, Transform|Nessuno|  
|ToolTip|Nessuno|Text, Window|Nessuno|  
|Tree|Nessuno|Scroll, Selection|Nessuno|  
|TreeItem|ExpandCollapse|Invoke, ScrollItem, SelectionItem, Toggle|Nessuno|  
|Window|Transform, Window|Dock|Nessuno|  
  
> [!NOTE]
>  Se un tipo di controllo non dispone di pattern di controllo supportati ma ha uno o più pattern di controllo supportati in modo condizionale, uno dei pattern di controllo condizionali risulterà sempre supportato.  
  
## Vedere anche  
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)