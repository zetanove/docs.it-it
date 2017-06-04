---
title: "Stili e modelli di ListView | Microsoft Docs"
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
  - "ControlTemplate [WPF], ListView"
  - "ListView [WPF], stili e modelli"
  - "parti [WPF], ListView"
  - "stati [WPF], ListView"
  - "stili [WPF], ListView"
  - "modelli [WPF], ListView"
ms.assetid: d2387356-2171-4785-822a-7247e024b4ee
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Stili e modelli di ListView
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.ListView>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo ListView  
 Il controllo <xref:System.Windows.Controls.ListView> non include parti denominate.  
  
 Quando si crea <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.ListView>, il modello potrebbe contenere <xref:System.Windows.Controls.ItemsPresenter> all'interno di <xref:System.Windows.Controls.ScrollViewer>.  L'oggetto <xref:System.Windows.Controls.ItemsPresenter> visualizza ogni elemento in <xref:System.Windows.Controls.ListView>; <xref:System.Windows.Controls.ScrollViewer> consente lo scorrimento all'interno del controllo.  Se <xref:System.Windows.Controls.ItemsPresenter> non è l'elemento figlio diretto di <xref:System.Windows.Controls.ScrollViewer>, è necessario assegnare a <xref:System.Windows.Controls.ItemsPresenter> il nome `ItemsPresenter`.  
  
## Stati del controllo ListView  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.ListView>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti del controllo ListViewItem  
 Il controllo <xref:System.Windows.Controls.ListViewItem> non include parti denominate.  
  
## Stati del controllo ListViewItem  
 Nella tabella seguente sono elencati gli stati per il controllo <xref:System.Windows.Controls.ListViewItem>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|Il controllo è disabilitato.|  
|MouseOver|CommonStates|Il puntatore del mouse si trova sopra il controllo <xref:System.Windows.Controls.ComboBox>.|  
|Focused|FocusStates|Il controllo ha lo stato attivo.|  
|Unfocused|FocusStates|Il controllo non ha lo stato attivo.|  
|Selezionato|SelectionStates|L'elemento è attualmente selezionato.|  
|Non selezionato|SelectionStates|L'elemento non è attualmente selezionato.|  
|SelectedUnfocused|SelectionStates|L'elemento è selezionato, ma non dispone dello stato attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempi di ControlTemplate del controllo ListView  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.ListView> e i tipi associati.  
  
 [!code-xml[ControlTemplateExamples#ListView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/listview.xaml#listview)]  
  
 Negli esempi di <xref:System.Windows.Controls.ControlTemplate> vengono utilizzate una o più delle risorse seguenti.  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Per l'esempio completo, vedere [Esempio di applicazione di stili con ControlTemplate](http://go.microsoft.com/fwlink/?LinkID=160041) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)