---
title: "Stili e modelli di Calendar | Microsoft Docs"
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
  - "Calendar [WPF], stili e modelli"
  - "ControlTemplate [WPF], Calendar"
  - "parti [WPF], Calendar"
  - "stati [WPF], Calendar"
  - "stili [WPF], Calendar"
  - "modelli [WPF], Calendar"
ms.assetid: f4fcf046-7a8f-41b8-b5a8-534b64e0345c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Stili e modelli di Calendar
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.Calendar>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo Calendar  
 Nella tabella seguente sono elencate le parti denominate per il controllo <xref:System.Windows.Controls.Calendar>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_CalendarItem|<xref:System.Windows.Controls.Primitives.CalendarItem>|Mese o anno attualmente visualizzato nell'oggetto <xref:System.Windows.Controls.Calendar>.|  
|PART\_Root|<xref:System.Windows.Controls.Panel>|Pannello che contiene l'oggetto <xref:System.Windows.Controls.Primitives.CalendarItem>.|  
  
## Stati del controllo Calendar  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Calendar>.  
  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|----------------------|---------------------------|-----------------|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti del controllo CalendarItem  
 Nella tabella seguente sono elencate le parti denominate per il controllo <xref:System.Windows.Controls.Primitives.CalendarItem>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_Root|<xref:System.Windows.FrameworkElement>|Radice del controllo.|  
|PART\_PreviousButton|<xref:System.Windows.Controls.Button>|Pulsante che quando viene selezionato consente di visualizzare la pagina precedente del calendario.|  
|PART\_NextButton|<xref:System.Windows.Controls.Button>|Pulsante che quando viene selezionato consente di visualizzare la pagina successiva del calendario.|  
|PART\_HeaderButton|<xref:System.Windows.Controls.Button>|Pulsante che consente di passare tra la modalità mensile, quella annuale e quella decennale.|  
|PART\_MonthView|<xref:System.Windows.Controls.Grid>|Ospita il contenuto in modalità mensile.|  
|PART\_YearView|<xref:System.Windows.Controls.Grid>|Ospita il contenuto in modalità annuale o decennale.|  
|PART\_DisabledVisual|<xref:System.Windows.FrameworkElement>|Sovrapposizione per lo stato disabilitato.|  
|DayTitleTemplate|<xref:System.Windows.DataTemplate>|Oggetto <xref:System.Windows.DataTemplate> che descrive la struttura visiva.|  
  
## Stati del controllo CalendarItem  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Primitives.CalendarItem>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|Stato del calendario quando la proprietà <xref:System.Windows.UIElement.IsEnabled%2A> è `false`.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti di CalendarDayButton  
 Il controllo <xref:System.Windows.Controls.Primitives.CalendarDayButton> non include parti denominate.  
  
## Stati di CalendarDayButton  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Primitives.CalendarDayButton>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> è disabilitato.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato su <xref:System.Windows.Controls.Primitives.CalendarDayButton>.|  
|Pressed|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> viene premuto.|  
|Selezionato|SelectionStates|Il pulsante è selezionato.|  
|Non selezionato|SelectionStates|Il pulsante non è selezionato.|  
|CalendarButtonFocused|CalendarButtonFocusStates|Il pulsante ha lo stato attivo.|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|Il pulsante non ha lo stato attivo.|  
|Focused|FocusStates|Il pulsante ha lo stato attivo.|  
|Unfocused|FocusStates|Il pulsante non ha lo stato attivo.|  
|Active|ActiveStates|Il pulsante è attivo.|  
|Inattivo|ActiveStates|Il pulsante non è attivo.|  
|RegularDay|DayStates|Il pulsante non rappresenta <xref:System.DateTime.Today%2A?displayProperty=fullName>.|  
|Today|DayStates|Il pulsante rappresenta <xref:System.DateTime.Today%2A?displayProperty=fullName>.|  
|NormalDay|BlackoutDayStates|Il pulsante rappresenta un giorno che può essere selezionato.|  
|BlackoutDay|BlackoutDayStates|Il pulsante rappresenta un giorno che non può essere selezionato.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti di CalendarButton  
 Il controllo <xref:System.Windows.Controls.Primitives.CalendarButton> non include parti denominate.  
  
## Stati di CalendarButton  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Primitives.CalendarButton>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|Disabled|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> è disabilitato.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato su <xref:System.Windows.Controls.Primitives.CalendarButton>.|  
|Pressed|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> viene premuto.|  
|Selezionato|SelectionStates|Il pulsante è selezionato.|  
|Non selezionato|SelectionStates|Il pulsante non è selezionato.|  
|CalendarButtonFocused|CalendarButtonFocusStates|Il pulsante ha lo stato attivo.|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|Il pulsante non ha lo stato attivo.|  
|Focused|FocusStates|Il pulsante ha lo stato attivo.|  
|Unfocused|FocusStates|Il pulsante non ha lo stato attivo.|  
|Active|ActiveStates|Il pulsante è attivo.|  
|Inattivo|ActiveStates|Il pulsante non è attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo Calendar  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.Calendar> e i tipi associati.  
  
 [!code-xml[ControlTemplateExamples#Calendar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/calendar.xaml#calendar)]  
  
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