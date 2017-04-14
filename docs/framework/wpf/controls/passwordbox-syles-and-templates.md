---
title: "Stili e modelli di PasswordBox | Microsoft Docs"
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
  - "ControlTemplate [WPF], PasswordBox"
  - "parti [WPF], PasswordBox"
  - "PasswordBox [WPF], stili e modelli"
  - "stati [WPF], PasswordBox"
  - "stili [WPF], PasswordBox"
  - "modelli [WPF], PasswordBox"
ms.assetid: deb52107-959f-4a60-b303-d21a0a933060
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Stili e modelli di PasswordBox
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.PasswordBox>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo PasswordBox  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.PasswordBox>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_ContentHost|<xref:System.Windows.FrameworkElement>|Elemento visivo che può contenere un oggetto <xref:System.Windows.FrameworkElement>.  Il testo di <xref:System.Windows.Controls.PasswordBox> viene visualizzato in questo elemento.|  
  
## Stati del controllo PasswordBox  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.PasswordBox>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sul controllo.|  
|Disabled|CommonStates|Il controllo è disabilitato.|  
|Focused|FocusStates|Il controllo ha lo stato attivo.|  
|Unfocused|FocusStates|Il controllo non ha lo stato attivo.|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo PasswordBox  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.PasswordBox>.  
  
 [!code-xml[ControlTemplateExamples#PasswordBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/textbox.xaml#passwordbox)]  
  
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