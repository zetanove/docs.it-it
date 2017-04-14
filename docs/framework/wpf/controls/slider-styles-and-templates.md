---
title: "Stili e modelli di Slider | Microsoft Docs"
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
  - "ControlTemplate [WPF], Dispositivo di scorrimento"
  - "parti [WPF], Dispositivo di scorrimento"
  - "Slider [WPF], stili e modelli"
  - "stati [WPF], Dispositivo di scorrimento"
  - "stili [WPF], Dispositivo di scorrimento"
  - "modelli [WPF], Dispositivo di scorrimento"
ms.assetid: d89aa97b-075a-4752-9c41-9679df65c491
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Stili e modelli di Slider
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.Slider>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo Slider  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.Slider>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_Track|<xref:System.Windows.Controls.Primitives.Track>|Contenitore dell'elemento che indica la posizione dell'oggetto <xref:System.Windows.Controls.Slider>.|  
|PART\_SelectionRange|<xref:System.Windows.FrameworkElement>|Elemento che consente di visualizzare un intervallo di selezione in <xref:System.Windows.Controls.Slider>.  L'intervallo di selezione è visibile soltanto se la proprietà <xref:System.Windows.Controls.Slider.IsSelectionRangeEnabled%2A> è `true`.|  
  
## Stati di Slider  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Slider>.  
  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|----------------------|---------------------------|-----------------|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sul controllo.|  
|Disabled|CommonStates|Il controllo è disabilitato.|  
|Focused|FocusStates|Il controllo ha lo stato attivo.|  
|Unfocused|FocusStates|Il controllo non ha lo stato attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo Slider  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.Slider>.  
  
 [!code-xml[ControlTemplateExamples#Slider](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/slider.xaml#slider)]  
  
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