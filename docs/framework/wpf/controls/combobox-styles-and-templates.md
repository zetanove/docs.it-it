---
title: "Stili e modelli di ComboBox | Microsoft Docs"
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
  - "ComboBox [WPF], stili e modelli"
  - "ControlTemplate [WPF], ComboBox"
  - "parti [WPF], ComboBox"
  - "stati [WPF], ComboBox"
  - "stili [WPF], ComboBox"
  - "modelli [WPF], ComboBox"
ms.assetid: b0662fa1-16d7-4320-b26b-c1804e565a44
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Stili e modelli di ComboBox
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.ComboBox>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo ComboBox  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.ComboBox>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_EditableTextBox|<xref:System.Windows.Controls.TextBox>|Contiene il testo dell'oggetto <xref:System.Windows.Controls.ComboBox>.|  
|PART\_Popup|<xref:System.Windows.Controls.Primitives.Popup>|Elenco a discesa che contiene gli elementi della casella combinata.|  
  
 Quando si crea <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.ComboBox>, il modello potrebbe contenere <xref:System.Windows.Controls.ItemsPresenter> all'interno di <xref:System.Windows.Controls.ScrollViewer>.  L'oggetto <xref:System.Windows.Controls.ItemsPresenter> visualizza ogni elemento in <xref:System.Windows.Controls.ComboBox>; <xref:System.Windows.Controls.ScrollViewer> consente lo scorrimento all'interno del controllo.  Se <xref:System.Windows.Controls.ItemsPresenter> non è l'elemento figlio diretto di <xref:System.Windows.Controls.ScrollViewer>, è necessario assegnare a <xref:System.Windows.Controls.ItemsPresenter> il nome `ItemsPresenter`.  
  
## Stati del controllo ComboBox  
 Nella tabella seguente sono elencati gli stati per il controllo <xref:System.Windows.Controls.ComboBox>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|Il controllo è disabilitato.|  
|MouseOver|CommonStates|Il puntatore del mouse si trova sopra il controllo <xref:System.Windows.Controls.ComboBox>.|  
|Focused|FocusStates|Il controllo ha lo stato attivo.|  
|Unfocused|FocusStates|Il controllo non ha lo stato attivo.|  
|FocusedDropDown|FocusStates|L'elenco a discesa per <xref:System.Windows.Controls.ComboBox> ha lo stato attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
|Editable|EditStates|La proprietà <xref:System.Windows.Controls.ComboBox.IsEditable%2A> è `true`.|  
|Non modificabile|EditStates|La proprietà <xref:System.Windows.Controls.ComboBox.IsEditable%2A> è `false`.|  
  
## Parti del controllo ComboBoxItem  
 Il controllo <xref:System.Windows.Controls.ComboBoxItem> non include parti denominate.  
  
## Stati del controllo ComboBoxItem  
 Nella tabella riportata di seguito sono elencati gli stati per il controllo <xref:System.Windows.Controls.ComboBoxItem>.  
  
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
  
## Esempio di ControlTemplate del controllo ComboBox  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.ComboBox> e i tipi associati.  
  
 [!code-xml[ControlTemplateExamples#ComboBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/combobox.xaml#combobox)]  
  
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