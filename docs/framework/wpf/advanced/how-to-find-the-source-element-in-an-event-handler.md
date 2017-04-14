---
title: "Procedura: cercare l&#39;elemento di origine in un gestore eventi | Microsoft Docs"
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
  - "gestori eventi, ricerca di elemento di origine"
  - "elemento di origine nei gestori eventi"
ms.assetid: 85f71c5a-b714-4c65-9711-7d905c2bbe98
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: cercare l&#39;elemento di origine in un gestore eventi
In questo esempio viene mostrato come cercare l'elemento di origine in un gestore eventi.  
  
## Esempio  
 Nell'esempio seguente viene mostrato un gestore eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click> dichiarato in un file code\-behind.  Quando un utente fa clic sul pulsante a cui è collegato il gestore, quest'ultimo modifica un valore della proprietà.  Il codice di gestione utilizza la proprietà <xref:System.Windows.RoutedEventArgs.Source%2A> dei dati di eventi indirizzati segnalata negli argomenti dell'evento per modificare il valore della proprietà <xref:System.Windows.FrameworkElement.Width%2A> nell'elemento <xref:System.Windows.RoutedEventArgs.Source%2A>.  
  
 [!code-xml[RoutedEventSource#XAMLHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml#xamlhandler)]  
  
 [!code-csharp[RoutedEventSource#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventSource#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventSource/VisualBasic/default.xaml.vb#handler)]  
  
## Vedere anche  
 <xref:System.Windows.RoutedEventArgs>   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/events-how-to-topics.md)