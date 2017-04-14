---
title: "Procedura: scorrere il contenuto mediante l&#39;interfaccia IScrollInfo | Microsoft Docs"
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
  - "scorrimento di contenuto"
  - "ScrollViewer (controllo), scorrimento di contenuto"
ms.assetid: d8700bef-a3f8-4c12-9de2-fc3b79f32cd3
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: scorrere il contenuto mediante l&#39;interfaccia IScrollInfo
In questo esempio viene illustrato come scorrere il contenuto utilizzando l'interfaccia <xref:System.Windows.Controls.Primitives.IScrollInfo>.  
  
## Esempio  
 Nell'esempio seguente vengono illustrate le funzionalità dell'interfaccia <xref:System.Windows.Controls.Primitives.IScrollInfo>.  Viene creato un elemento <xref:System.Windows.Controls.StackPanel> in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] annidato in un elemento <xref:System.Windows.Controls.ScrollViewer> padre.  È possibile scorrere logicamente gli elementi figlio di <xref:System.Windows.Controls.StackPanel> utilizzando i metodi definiti dall'interfaccia <xref:System.Windows.Controls.Primitives.IScrollInfo>, nonché eseguirne il cast nell'istanza di <xref:System.Windows.Controls.StackPanel> \(`sp1`\) nel codice.  
  
 [!code-xml[IScrollInfoMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml#2)]  
  
 L'oggetto <xref:System.Windows.Controls.Button> nel file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] attiva un metodo personalizzato associato che controlla il comportamento dello scorrimento in <xref:System.Windows.Controls.StackPanel>.  Nell'esempio seguente viene illustrato come utilizzare i metodi <xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> e <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A> e viene illustrato genericamente come utilizzare tutti i metodi di posizionamento definiti dalla classe <xref:System.Windows.Controls.Primitives.IScrollInfo>.  
  
 [!code-csharp[IScrollInfoMethods#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.Primitives.IScrollInfo>   
 <xref:System.Windows.Controls.StackPanel>   
 [Cenni preliminari sull'elemento ScrollViewer](../../../../docs/framework/wpf/controls/scrollviewer-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/scrollviewer-how-to-topics.md)   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)