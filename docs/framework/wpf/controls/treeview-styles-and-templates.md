---
title: "Stili e modelli di TreeView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ControlTemplate [WPF], TreeView"
  - "parti [WPF], TreeView"
  - "stati [WPF], TreeView"
  - "stili [WPF], TreeView"
  - "modelli [WPF], TreeView"
  - "TreeView [WPF], stili e modelli"
ms.assetid: a49adb77-0202-4caa-b94a-8bb110d7fa9a
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Stili e modelli di TreeView
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.TreeView>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo TreeView  
 Il controllo <xref:System.Windows.Controls.TreeView> non include parti denominate.  
  
 Quando si crea <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.TreeView>, il modello potrebbe contenere <xref:System.Windows.Controls.ItemsPresenter> all'interno di <xref:System.Windows.Controls.ScrollViewer>.  L'oggetto <xref:System.Windows.Controls.ItemsPresenter> visualizza ogni elemento in <xref:System.Windows.Controls.TreeView>; <xref:System.Windows.Controls.ScrollViewer> consente lo scorrimento all'interno del controllo.  Se <xref:System.Windows.Controls.ItemsPresenter> non è l'elemento figlio diretto di <xref:System.Windows.Controls.ScrollViewer>, è necessario assegnare a <xref:System.Windows.Controls.ItemsPresenter> il nome `ItemsPresenter`.  
  
## Stati del controllo TreeView  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.TreeView>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti del controllo TreeViewItem  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.TreeViewItem>.  
  
|Parte|Type|Descrizione|  
|-----------|----------|-----------------|  
|PART\_Header|<xref:System.Windows.FrameworkElement>|Elemento visivo che include il contenuto dell'intestazione del controllo <xref:System.Windows.Controls.TreeView>.|  
  
## Stati del controllo TreeViewItem  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.TreeViewItem>.  
  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|----------------------|---------------------------|-----------------|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato su <xref:System.Windows.Controls.TreeViewItem>.|  
|Disabled|CommonStates|<xref:System.Windows.Controls.TreeViewItem> è disabilitato.|  
|Focused|FocusStates|<xref:System.Windows.Controls.TreeViewItem> ha lo stato attivo.|  
|Unfocused|FocusStates|<xref:System.Windows.Controls.TreeViewItem> non ha lo stato attivo.|  
|Espanso|ExpansionStates|Il controllo <xref:System.Windows.Controls.TreeViewItem> è espanso.|  
|Collapsed|ExpansionStates|Il controllo <xref:System.Windows.Controls.TreeViewItem> è compresso.|  
|HasItems|HasItemsStates|<xref:System.Windows.Controls.TreeViewItem> include elementi.|  
|NoItems|HasItemsStates|<xref:System.Windows.Controls.TreeViewItem> non include elementi.|  
|Selezionato|SelectionStates|L'oggetto <xref:System.Windows.Controls.TreeViewItem> è selezionato.|  
|SelectedInactive|SelectionStates|<xref:System.Windows.Controls.TreeViewItem> è selezionato ma non presenta lo stato attivo.|  
|Non selezionato|SelectionStates|L'oggetto <xref:System.Windows.Controls.TreeViewItem> non è selezionato.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo TreeView  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.TreeView> e i tipi associati.  
  
 [!code-xml[ControlTemplateExamples#TreeView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/treeview.xaml#treeview)]  
  
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