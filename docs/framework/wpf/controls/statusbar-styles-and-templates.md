---
title: "Stili e modelli di StatusBar | Microsoft Docs"
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
  - "ControlTemplate [WPF], StatusBar"
  - "parti [WPF], StatusBar"
  - "stati [WPF], StatusBar"
  - "StatusBar [WPF], stili e modelli"
  - "stili [WPF], StatusBar"
  - "modelli [WPF], StatusBar"
ms.assetid: 9f5e1c25-81eb-4756-a0ac-d9e1fbe33ee2
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Stili e modelli di StatusBar
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.Primitives.StatusBar>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti di StatusBar  
 Il controllo <xref:System.Windows.Controls.Primitives.StatusBar> non include parti denominate.  
  
## Stati di StatusBar  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Primitives.StatusBar>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Parti di StatusBarItem  
 Il controllo <xref:System.Windows.Controls.Primitives.StatusBarItem> non include parti denominate.  
  
## Stati di StatusBar  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.Primitives.StatusBarItem>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo StatusBar  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.Primitives.StatusBar>.  
  
 [!code-xml[ControlTemplateExamples#StatusBar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/statusbar.xaml#statusbar)]  
  
 <xref:System.Windows.Controls.ControlTemplate> utilizza una o più delle risorse seguenti.  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Per l'esempio completo, vedere [Esempio di applicazione di stili con ControlTemplate](http://go.microsoft.com/fwlink/?LinkID=160041) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)