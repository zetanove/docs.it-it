---
title: "Stili e modelli di ScrollViewer | Microsoft Docs"
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
  - "ControlTemplate [WPF], ScrollViewer"
  - "parti [WPF], ScrollViewer"
  - "ScrollViewer [WPF], stili e modelli"
  - "stati [WPF], ScrollViewer"
  - "stili [WPF], ScrollViewer"
  - "modelli [WPF], ScrollViewer"
ms.assetid: dffdd822-ae69-4946-abaf-710860cd65b2
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Stili e modelli di ScrollViewer
In questo argomento vengono descritti gli stili e i modelli per il controllo <xref:System.Windows.Controls.ScrollViewer>.  È possibile modificare l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito per conferire al controllo un aspetto univoco.  Per ulteriori informazioni, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## Parti del controllo ScrollViewer  
 Nella tabella seguente sono elencate le parti denominate del controllo <xref:System.Windows.Controls.ScrollViewer>.  
  
||||  
|-|-|-|  
|Parte|Type|Descrizione|  
|PART\_ScrollContentPresenter|<xref:System.Windows.Controls.ScrollContentPresenter>|Segnaposto per il contenuto nell'oggetto <xref:System.Windows.Controls.ScrollViewer>.|  
|PART\_HorizontalScrollBar|<xref:System.Windows.Controls.Primitives.ScrollBar>|Oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> utilizzato per scorrere il contenuto in senso orizzontale.|  
|PART\_VerticalScrollBar|<xref:System.Windows.Controls.Primitives.ScrollBar>|Oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> utilizzato per scorrere il contenuto in senso verticale.|  
  
## Stati del controllo ScrollViewer  
 Nella tabella seguente sono elencati gli stati visivi per il controllo <xref:System.Windows.Controls.ScrollViewer>.  
  
||||  
|-|-|-|  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|Valid|ValidationStates|Il controllo utilizza la classe <xref:System.Windows.Controls.Validation> e la proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `false`.|  
|InvalidFocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo ha lo stato attivo.|  
|InvalidUnfocused|ValidationStates|La proprietà associata <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=fullName> è `true` e il controllo non ha lo stato attivo.|  
  
## Esempio di ControlTemplate del controllo ScrollViewer  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo <xref:System.Windows.Controls.ScrollViewer>.  
  
 [!code-xml[ControlTemplateExamples#ScrollViewer](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/scrollviewer.xaml#scrollviewer)]  
  
 Nell'esempio precedente vengono utilizzate una o più delle risorse seguenti.  
  
 [!code-xml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Per l'esempio completo, vedere [Esempio di applicazione di stili con ControlTemplate](http://go.microsoft.com/fwlink/?LinkID=160041) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.Style%2A>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)