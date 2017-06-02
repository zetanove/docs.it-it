---
title: "Stili e modelli di ListBox | Microsoft Docs"
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
  - "ControlTemplate [WPF], ListBox"
  - "ListBox [WPF], stili e modelli"
  - "parti [WPF], ListBox"
  - "stati [WPF], ListBox"
  - "stili [WPF], ListBox"
  - "modelli [WPF], ListBox"
ms.assetid: fc5764cb-c27b-495b-88d4-d969a8213ccb
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Stili e modelli di ListBox
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.ListBox>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo ListBox  
 Il controllo <xref:System.Windows.Controls.ListBox> non include parti denominate.  
  
 Quando si crea <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.ListBox>, il modello potrebbe contenere <xref:System.Windows.Controls.ItemsPresenter> all'interno di <xref:System.Windows.Controls.ScrollViewer>.  L'oggetto <xref:System.Windows.Controls.ItemsPresenter> visualizza ogni elemento in <xref:System.Windows.Controls.ListBox>; <xref:System.Windows.Controls.ScrollViewer> consente lo scorrimento all'interno del controllo.  Se <xref:System.Windows.Controls.ItemsPresenter> non è l'elemento figlio diretto di <xref:System.Windows.Controls.ScrollViewer>, è necessario assegnare a <xref:System.Windows.Controls.ItemsPresenter> il nome `ItemsPresenter`.  
  
## Stati del controllo ListBox  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.ListBox>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Valid|ValidationStates|Il controllo è valido.|  
|InvalidFocused|ValidationStates|Il controllo non è valido e presenta lo stato attivo.|  
|InvalidUnfocused|ValidationStates|Il controllo non è valido e non presenta lo stato attivo.|  
  
## Parti del controllo ListBoxItem  
 Il controllo <xref:System.Windows.Controls.ListBoxItem> non include parti denominate.  
  
## Stati del controllo ListBoxItem  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.ListBox>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sul controllo.|  
|Disabled|CommonStates|L'elemento è disabilitato.|  
|Focused|FocusStates|L'elemento dispone dello stato attivo.|  
|Unfocused|FocusStates|L'elemento non dispone dello stato attivo.|  
|Non selezionato|SelectionStates|L'elemento è attualmente selezionato.|  
|Selezionato|SelectionStates|L'elemento non è attualmente selezionato.|  
|SelectedUnfocused|SelectionStates|L'elemento è selezionato, ma non dispone dello stato attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo ListBox  
 Nell'esempio seguente viene illustrato come definire <xref:System.Windows.Controls.ControlTemplate> per i controlli <xref:System.Windows.Controls.ListBox> e <xref:System.Windows.Controls.ListBoxItem>.  
  
 [!code-xml[ControlTemplateExamples#ListBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/listbox.xaml#listbox)]  
  
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