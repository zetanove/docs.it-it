---
title: "Procedura: gestire l&#39;evento ScrollChanged | Microsoft Docs"
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
  - "ScrollChanged (eventi)"
  - "ScrollViewer (controllo), generazione di eventi ScrollChanged"
ms.assetid: 42c695d8-ee28-49d4-80fd-fc71e9be7f29
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: gestire l&#39;evento ScrollChanged
## Esempio  
 In questo esempio viene illustrato come gestire l'evento <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> di un oggetto <xref:System.Windows.Controls.ScrollViewer>.  
  
 Un elemento <xref:System.Windows.Documents.FlowDocument> con parti <xref:System.Windows.Documents.Paragraph> viene definito in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Quando si verifica l'evento <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> a causa dell'interazione dell'utente, viene richiamato un gestore e viene immesso testo in un controllo <xref:System.Windows.Controls.TextBlock> per indicare il verificarsi dell'evento.  
  
 [!code-xml[scrollchangedeventargsLayout#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml#1)]  
[!code-xml[scrollchangedeventargsLayout#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[scrollchangedeventargsLayout#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml.cs#3)]
 [!code-vb[scrollchangedeventargsLayout#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/scrollchangedeventargsLayout/VisualBasic/Window1.xaml.vb#3)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.ScrollViewer.ScrollChanged>   
 <xref:System.Windows.Controls.ScrollChangedEventHandler>   
 <xref:System.Windows.Controls.ScrollChangedEventArgs>