---
title: "Procedura: utilizzare i metodi di scorrimento del contenuto di ScrollViewer | Microsoft Docs"
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
  - "IScrollInfo (interfaccia)"
  - "metodi di scorrimento"
  - "ScrollViewer (controllo), metodi di scorrimento"
ms.assetid: 4708cc65-6510-45f8-82e6-30b0d3e30045
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: utilizzare i metodi di scorrimento del contenuto di ScrollViewer
In questo esempio viene illustrato come utilizzare i metodi di scorrimento dell'elemento <xref:System.Windows.Controls.ScrollViewer>.  Questi metodi consentono lo scorrimento incrementale del contenuto, per riga o per pagina, in un elemento <xref:System.Windows.Controls.ScrollViewer>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Controls.ScrollViewer> denominato `sv1`, che ospita un elemento <xref:System.Windows.Controls.TextBlock> figlio.  Poiché l'oggetto <xref:System.Windows.Controls.TextBlock> è più grande dell'elemento <xref:System.Windows.Controls.ScrollViewer> padre, vengono visualizzate le barre di scorrimento per abilitare lo scorrimento.  Gli elementi <xref:System.Windows.Controls.Button> che rappresentano i vari metodi di scorrimento sono ancorati sulla sinistra in un oggetto <xref:System.Windows.Controls.StackPanel> separato.  Ogni oggetto <xref:System.Windows.Controls.Button> nel file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] chiama un metodo personalizzato correlato che controlla il comportamento di scorrimento in <xref:System.Windows.Controls.ScrollViewer>.  
  
 [!code-xml[ScrollViewerMethods#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml#1)]  
  
 Nell'esempio riportato di seguito vengono utilizzati i metodi <xref:System.Windows.Controls.ScrollViewer.LineUp%2A> e <xref:System.Windows.Controls.ScrollViewer.LineDown%2A>.  
  
 [!code-csharp[ScrollViewerMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ScrollViewerMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewerMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.StackPanel>