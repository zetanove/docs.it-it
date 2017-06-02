---
title: "Stili e modelli di DatePicker | Microsoft Docs"
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
  - "ControlTemplate [WPF], DatePicker"
  - "DatePicker [WPF], stili e modelli"
  - "parti [WPF], DatePicker"
  - "stati [WPF], DatePicker"
  - "stili [WPF], DatePicker"
  - "modelli [WPF], DatePicker"
ms.assetid: c430a657-692f-44bd-a549-2341f92d6115
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Stili e modelli di DatePicker
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.DatePicker>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo DatePicker  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.DatePicker>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_Root|<xref:System.Windows.Controls.Grid>|Radice del controllo.|  
|PART\_Button|<xref:System.Windows.Controls.Button>|Pulsante che consente di aprire e chiudere l'oggetto <xref:System.Windows.Controls.Calendar>.|  
|PART\_TextBox|<xref:System.Windows.Controls.Primitives.DatePickerTextBox>|Casella di testo che consente di inserire una data.|  
|PART\_Popup|<xref:System.Windows.Controls.Primitives.Popup>|Popup del controllo <xref:System.Windows.Controls.DatePicker>.|  
  
## Stati del controllo DatePicker  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.DatePicker>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|<xref:System.Windows.Controls.DatePicker> è disabilitato.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti di DatePickerTextBox  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.Primitives.DatePickerTextBox>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_Watermark|<xref:System.Windows.Controls.ContentControl>|Elemento che contiene il testo iniziale nell'oggetto <xref:System.Windows.Controls.DatePicker>.|  
|PART\_ContentElement|<xref:System.Windows.FrameworkElement>|Elemento visivo che può contenere un oggetto <xref:System.Windows.FrameworkElement>.  Il testo di <xref:System.Windows.Controls.TextBox> viene visualizzato in questo elemento.|  
  
## Stati di DatePickerTextBox  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Primitives.DatePickerTextBox>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|<xref:System.Windows.Controls.Primitives.DatePickerTextBox> è disabilitato.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato su <xref:System.Windows.Controls.Primitives.DatePickerTextBox>.|  
|ReadOnly|CommonStates|L'utente non può modificare il testo in <xref:System.Windows.Controls.Primitives.DatePickerTextBox>.|  
|Focused|FocusStates|Il controllo ha lo stato attivo.|  
|Unfocused|FocusStates|Il controllo non ha lo stato attivo.|  
|Watermarked|WatermarkStates|Nel controllo viene visualizzato il testo iniziale.  L'oggetto <xref:System.Windows.Controls.Primitives.DatePickerTextBox> si trova nello stato in cui l'utente non ha immesso testo né selezionato una data.|  
|Unwatermarked|WatermarkStates|L'utente ha immesso testo in <xref:System.Windows.Controls.Primitives.DatePickerTextBox> o selezionato una data in <xref:System.Windows.Controls.DatePicker>.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo DatePicker  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.DatePicker>.  
  
 [!code-xml[ControlTemplateExamples#DatePicker](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datepicker.xaml#datepicker)]  
  
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