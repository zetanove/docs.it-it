---
title: "Stili e modelli di ProgressBar | Microsoft Docs"
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
  - "ControlTemplate [WPF], ProgressBar"
  - "parti [WPF], ProgressBar"
  - "ProgressBar [WPF], stili e modelli"
  - "stati [WPF], ProgressBar"
  - "stili [WPF], ProgressBar"
  - "modelli [WPF], ProgressBar"
ms.assetid: 935aa600-16e6-4947-a905-37a189a583dd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Stili e modelli di ProgressBar
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.ProgressBar>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo ProgressBar  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.ProgressBar>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_Indicator|<xref:System.Windows.FrameworkElement>|Oggetto che indica lo stato di avanzamento.|  
|PART\_Track|<xref:System.Windows.FrameworkElement>|Oggetto che definisce il percorso dell'indicatore di stato.|  
|PART\_GlowRect|<xref:System.Windows.FrameworkElement>|Oggetto che abbellisce l'indicatore di stato.|  
  
## Stati del controllo ProgressBar  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.ProgressBar>.  
  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|----------------------|---------------------------|-----------------|  
|Determinate|CommonStates|<xref:System.Windows.Controls.ProgressBar> restituisce lo stato di avanzamento in base alla proprietà <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A>.|  
|Indeterminate|CommonStates|<xref:System.Windows.Controls.ProgressBar> restituisce lo stato di avanzamento generico con un motivo ripetuto.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo ProgressBar  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.ProgressBar>.  
  
 [!code-xml[ControlTemplateExamples#ProgressBar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/progressbar.xaml#progressbar)]  
  
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