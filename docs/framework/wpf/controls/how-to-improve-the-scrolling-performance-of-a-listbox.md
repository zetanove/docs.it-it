---
title: "Procedura: migliorare le prestazioni di scorrimento di un controllo ListBox | Microsoft Docs"
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
  - "ListBox (controllo) [WPF], miglioramento delle prestazioni di scorrimento"
  - "ListBox (controllo) [WPF], riutilizzo dei contenitori di elementi"
ms.assetid: 1e2bf8f3-c8ce-47f7-a400-a7fe11d1a848
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: migliorare le prestazioni di scorrimento di un controllo ListBox
Se un controllo <xref:System.Windows.Controls.ListBox> contiene molti elementi, la risposta dell'interfaccia utente può essere lenta quando un utente scorre <xref:System.Windows.Controls.ListBox> tramite la rotellina del mouse o trascinando il cursore di una barra di scorrimento.  È possibile migliorare le prestazioni di <xref:System.Windows.Controls.ListBox> quando l'utente scorre la visualizzazione impostando la proprietà associata <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> su <xref:System.Windows.Controls.VirtualizationMode>.  
  
## Esempio  
  
## Descrizione  
 Nell'esempio seguente viene creato un controllo <xref:System.Windows.Controls.ListBox> e la proprietà <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> viene impostata su <xref:System.Windows.Controls.VirtualizationMode> per migliorare le prestazioni durante lo scorrimento.  
  
## Codice  
 [!code-xml[RecycleItemContainerShippets#VirtualizationMode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizationmode)]  
  
 Nell'esempio seguente vengono illustrati i dati utilizzati nell'esempio precedente.  
  
 [!code-csharp[RecycleItemContainerShippets#ListBoxData](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#listboxdata)]
 [!code-vb[RecycleItemContainerShippets#ListBoxData](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#listboxdata)]