---
title: "Procedura: applicare un oggetto FocusVisualStyle a un controllo | Microsoft Docs"
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
  - "FocusVisualStyle (proprietà)"
  - "proprietà, FocusVisualStyle"
ms.assetid: 363de99e-8ecc-438c-ac4a-f9147432ebd6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: applicare un oggetto FocusVisualStyle a un controllo
In questo esempio viene illustrato come creare un stile di visualizzazione dello stato attivo nelle risorse e applicare lo stile a un controllo, utilizzando la proprietà <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene definito uno stile che crea una composizione del controllo aggiuntiva che si applica solo quando tale controllo presenta lo stato attivo della tastiera in [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  Questa operazione viene esguita definendo un stile con <xref:System.Windows.Controls.ControlTemplate>, quindi facendo riferimento a quello stile come una risorsa quando si imposta la proprietà <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>.  
  
 Un rettangolo esterno che assomiglia a un bordo viene posizionato all’esterno dell’area rettangolare.  In assenza di modificato divere, il ridimensionamento dello stile utilizza <xref:System.Windows.FrameworkElement.ActualHeight%2A> e <xref:System.Windows.FrameworkElement.ActualWidth%2A> del controllo rettangolare in cui viene applicato lo stile di visualizzazione dello stato attivo.  In questo esempio vengono impostati valori negativi per <xref:System.Windows.FrameworkElement.Margin%2A> affinché il bordo venga visualizzato leggermente fuori dal controllo con lo stato attivo.  
  
 [!code-xml[FEFocusVisualStyle#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEFocusVisualStyle/CS/page1.xaml#xaml)]  
  
 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> è aggiuntivo a qualsiasi stile di modello di controllo che deriva da un stile esplicito o da un stile del tema; lo stile primario per un controllo può comunque essere creato utilizzando <xref:System.Windows.Controls.ControlTemplate> e impostando tale stile nella proprietà <xref:System.Windows.FrameworkElement.Style%2A>.  
  
 Gli stili di visualizzazione dello stato attivo devono essere utilizzati coerentemente in un tema o in un’interfaccia utente, piuttosto che utilizzarne uno diverso per ciascun elemento attivabile.  Per informazioni dettagliate, vedere [Applicazione di stili per lo stato attivo nei controlli e FocusVisualStyle](../../../../docs/framework/wpf/advanced/styling-for-focus-in-controls-and-focusvisualstyle.md).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Applicazione di stili per lo stato attivo nei controlli e FocusVisualStyle](../../../../docs/framework/wpf/advanced/styling-for-focus-in-controls-and-focusvisualstyle.md)