---
title: "Stili e modelli di DataGrid | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ControlTemplate [WPF], DataGrid"
  - "DataGrid [WPF], stili e modelli"
  - "parti [WPF], DataGrid"
  - "stati [WPF], DataGrid"
  - "stili [WPF], DataGrid"
  - "modelli [WPF], DataGrid"
ms.assetid: 9cb31d63-f148-4d25-b079-816e73f988c7
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Stili e modelli di DataGrid
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.DataGrid>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti di DataGrid  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.DataGrid>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_ColumnHeadersPresenter|<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>|Riga che contiene le intestazioni di colonna.|  
  
 Quando si crea <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.DataGrid>, il modello potrebbe contenere <xref:System.Windows.Controls.ItemsPresenter> all'interno di <xref:System.Windows.Controls.ScrollViewer>.  L'oggetto <xref:System.Windows.Controls.ItemsPresenter> visualizza ogni elemento in <xref:System.Windows.Controls.DataGrid>; <xref:System.Windows.Controls.ScrollViewer> consente lo scorrimento all'interno del controllo.  Se <xref:System.Windows.Controls.ItemsPresenter> non è l'elemento figlio diretto di <xref:System.Windows.Controls.ScrollViewer>, è necessario assegnare a <xref:System.Windows.Controls.ItemsPresenter> il nome `ItemsPresenter`.  
  
 Il modello predefinito per <xref:System.Windows.Controls.DataGrid> contiene n controllo <xref:System.Windows.Controls.ScrollViewer>.  Per ulteriori informazioni sulle parti definite da <xref:System.Windows.Controls.ScrollViewer>, vedere [Stili e modelli di ScrollViewer](../../../../docs/framework/wpf/controls/scrollviewer-styles-and-templates.md).  
  
## Stati di DataGrid  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.DataGrid>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|Il controllo è disabilitato.|  
|InvalidFocused|ValidationStates|Il controllo non è valido e presenta lo stato attivo.|  
|InvalidUnfocused|ValidationStates|Il controllo non è valido e non presenta lo stato attivo.|  
|Valid|ValidationStates|Il controllo è valido.|  
  
## Parti di DataGridCell  
 L'elemento <xref:System.Windows.Controls.DataGridCell> non include parti denominate.  
  
## Stati di DataGridCell  
 Nella tabella seguente sono elencati gli stati di visualizzazione per l'elemento <xref:System.Windows.Controls.DataGridCell>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sulla cella.|  
|Focused|FocusStates|La cella ha lo stato attivo.|  
|Unfocused|FocusStates|La cella non ha lo stato attivo.|  
|Corrente|CurrentStates|La cella è la cella attiva.|  
|Regolare|CurrentStates|La cella non è la cella attiva.|  
|Visualizzazione|InteractionStates|La cella è in modalità di visualizzazione.|  
|Modifica|InteractionStates|La cella è in modalità di modifica.|  
|Selezionato|SelectionStates|La cella è selezionata.|  
|Non selezionato|SelectionStates|La cella non è selezionata.|  
|InvalidFocused|ValidationStates|La cella non è valida e ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La cella non è valida e non ha lo stato attivo.|  
|Valid|ValidationStates|La cella è valida.|  
  
## Parti di DataGridRow  
 L'elemento <xref:System.Windows.Controls.DataGridRow> non include parti denominate.  
  
## Stati di DataGridRow  
 Nella tabella seguente sono elencati gli stati di visualizzazione per l'elemento <xref:System.Windows.Controls.DataGridRow>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sulla riga.|  
|MouseOver\_Editing|CommonStates|Il puntatore del mouse è posizionato sulla riga e la riga è in modalità di modifica.|  
|MouseOver\_Selected|CommonStates|Il puntatore del mouse è posizionato sulla riga e la riga è selezionata.|  
|MouseOver\_Unfocused\_Editing|CommonStates|Il puntatore del mouse è posizionato sulla riga, la riga è in modalità di modifica e non ha lo stato attivo.|  
|MouseOver\_Unfocused\_Selected|CommonStates|Il puntatore del mouse è posizionato sulla riga, la riga è selezionata e non ha lo stato attivo.|  
|Normal\_AlternatingRow|CommonStates|La riga è una riga alterna.|  
|Normal\_Editing|CommonStates|La riga è in modalità di modifica.|  
|Normal\_Selected|CommonStates|La riga è selezionata.|  
|Unfocused\_Editing|CommonStates|La riga è in modalità di modifica e non ha lo stato attivo.|  
|Unfocused\_Selected|CommonStates|La riga è selezionata e non ha lo stato attivo.|  
|InvalidFocused|ValidationStates|Il controllo non è valido e presenta lo stato attivo.|  
|InvalidUnfocused|ValidationStates|Il controllo non è valido e non presenta lo stato attivo.|  
|Valid|ValidationStates|Il controllo è valido.|  
  
## Parti di DataGridRowHeader  
 Nella tabella seguente sono elencate le parti denominate dell'elemento <xref:System.Windows.Controls.Primitives.DataGridRowHeader>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_TopHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|Elemento utilizzato per ridimensionare l'intestazione di riga dalla parte superiore.|  
|PART\_BottomHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|Elemento utilizzato per ridimensionare l'intestazione di riga dalla parte inferiore.|  
  
## Stati di DataGridRowHeader  
 Nella tabella seguente sono elencati gli stati di visualizzazione per l'elemento <xref:System.Windows.Controls.Primitives.DataGridRowHeader>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sulla riga.|  
|MouseOver\_CurrentRow|CommonStates|Il puntatore del mouse è posizionato sulla riga e la riga è la riga attiva.|  
|MouseOver\_CurrentRow\_Selected|CommonStates|Il puntatore del mouse è posizionato sulla riga e la riga è attiva e selezionata.|  
|MouseOver\_EditingRow|CommonStates|Il puntatore del mouse è posizionato sulla riga e la riga è in modalità di modifica.|  
|MouseOver\_Selected|CommonStates|Il puntatore del mouse è posizionato sulla riga e la riga è selezionata.|  
|MouseOver\_Unfocused\_CurrentRow\_Selected|CommonStates|Il puntatore del mouse è posizionato sulla riga, la riga è attiva e selezionata e non ha lo stato attivo.|  
|MouseOver\_Unfocused\_EditingRow|CommonStates|Il puntatore del mouse è posizionato sulla riga, la riga è in modalità di modifica e non ha lo stato attivo.|  
|MouseOver\_Unfocused\_Selected|CommonStates|Il puntatore del mouse è posizionato sulla riga, la riga è selezionata e non ha lo stato attivo.|  
|Normal\_CurrentRow|CommonStates|La riga è la riga attiva.|  
|Normal\_CurrentRow\_Selected|CommonStates|La riga è la riga attiva ed è selezionata.|  
|Normal\_EditingRow|CommonStates|La riga è in modalità di modifica.|  
|Normal\_Selected|CommonStates|La riga è selezionata.|  
|Unfocused\_CurrentRow\_Selected|CommonStates|La riga è la riga attiva, è selezionata e non ha lo stato attivo.|  
|Unfocused\_EditingRow|CommonStates|La riga è in modalità di modifica e non ha lo stato attivo.|  
|Unfocused\_Selected|CommonStates|La riga è selezionata e non ha lo stato attivo.|  
|InvalidFocused|ValidationStates|Il controllo non è valido e presenta lo stato attivo.|  
|InvalidUnfocused|ValidationStates|Il controllo non è valido e non presenta lo stato attivo.|  
|Valid|ValidationStates|Il controllo è valido.|  
  
## Parti di DataGridColumnHeadersPresenter  
 Nella tabella seguente sono elencate le parti denominate dell'elemento <xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_FillerColumnHeader|<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>|Segnaposto per le intestazioni di colonna.|  
  
## Stati di DataGridColumnHeadersPresenter  
 Nella tabella seguente sono elencati gli stati di visualizzazione per l'elemento <xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|InvalidFocused|ValidationStates|La cella non è valida e ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La cella non è valida e non ha lo stato attivo.|  
|Valid|ValidationStates|La cella è valida.|  
  
## Parti di DataGridColumnHeader  
 Nella tabella seguente sono elencate le parti denominate dell'elemento <xref:System.Windows.Controls.Primitives.DataGridColumnHeader>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_LeftHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|Elemento utilizzato per ridimensionare l'intestazione di colonna dalla sinistra.|  
|PART\_RightHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|Elemento utilizzato per ridimensionare l'intestazione di colonna dalla destra.|  
  
## Stati di DataGridColumnHeader  
 Nella tabella seguente sono elencati gli stati di visualizzazione per l'elemento <xref:System.Windows.Controls.Primitives.DataGridColumnHeader>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sul controllo.|  
|Pressed|CommonStates|Il controllo viene premuto.|  
|SortAscending|SortStates|La colonna è ordinata in ordine crescente.|  
|SortDescending|SortStates|La colonna è ordinata in ordine decrescente.|  
|Unsorted|SortStates|La colonna non è ordinata.|  
|InvalidFocused|ValidationStates|Il controllo non è valido e presenta lo stato attivo.|  
|InvalidUnfocused|ValidationStates|Il controllo non è valido e non presenta lo stato attivo.|  
|Valid|ValidationStates|Il controllo è valido.|  
  
## Esempio di ControlTemplate del controllo DataGrid  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.DataGrid> e i tipi associati.  
  
 [!code-xml[ControlTemplateExamples#DataGrid](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datagrid.xaml#datagrid)]  
  
 Nell'esempio precedente vengono utilizzate una o più delle risorse seguenti.  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Per l'esempio completo, vedere          [Esempio di applicazione di stili con ControlTemplates](http://go.microsoft.com/fwlink/?LinkID=160041) .  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)