---
title: "Procedura: creare un controllo Expander con un controllo ScrollViewer | Microsoft Docs"
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
  - "controlli [WPF], Expander"
  - "controlli [WPF], ScrollViewer"
  - "Expander (controllo), creazione"
  - "ScrollViewer (controllo), con controllo Expander"
ms.assetid: 2ad124d2-2406-4157-aaf2-64e067298f01
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare un controllo Expander con un controllo ScrollViewer
In questo esempio viene illustrato come creare un controllo <xref:System.Windows.Controls.Expander> che contenga contenuto complesso, ad esempio un immagine e del testo.  Nell'esempio è incluso anche il contenuto di <xref:System.Windows.Controls.Expander> in un controllo <xref:System.Windows.Controls.ScrollViewer>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come creare un oggetto <xref:System.Windows.Controls.Expander>.  Nell'esempio viene utilizzato un controllo <xref:System.Windows.Controls.Primitives.BulletDecorator> che contiene un'immagine e del testo, per definire la proprietà <xref:System.Windows.Controls.HeaderedContentControl.Header%2A>.  Un controllo <xref:System.Windows.Controls.ScrollViewer> fornisce un metodo per scorrere il contenuto espanso.  
  
 Nell'esempio viene impostata la proprietà <xref:System.Windows.FrameworkElement.Height%2A> sul controllo <xref:System.Windows.Controls.ScrollViewer> e non sul contenuto.  Se la proprietà <xref:System.Windows.FrameworkElement.Height%2A> viene impostata sul contenuto, il controllo <xref:System.Windows.Controls.ScrollViewer> non consente all'utente di scorrere il contenuto.  La proprietà <xref:System.Windows.FrameworkElement.Width%2A> viene impostata sul controllo <xref:System.Windows.Controls.Expander>. Questa impostazione si applica alla proprietà <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> e al contenuto espanso.  
  
 [!code-xml[ExpanderRichContent#CreateExpander](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#createexpander)]  
  
 [!code-csharp[ExpanderRichContent#CreateExpanderCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#createexpandercode)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Expander>   
 [Cenni preliminari sul controllo Expander](../../../../docs/framework/wpf/controls/expander-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/expander-how-to-topics.md)