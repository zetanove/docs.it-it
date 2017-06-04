---
title: "Procedura: ridimensionare le righe con un GridSplitter | Microsoft Docs"
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
  - "righe della griglia, ridimensionamento"
  - "GridSplitter (controllo), ridimensionamento delle righe della griglia"
  - "ridimensionamento delle righe della griglia"
ms.assetid: 2413a9f2-1d81-46ed-95cb-95ec8233eea2
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ridimensionare le righe con un GridSplitter
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Controls.GridSplitter> orizzontale per ridistribuire lo spazio tra due righe in un oggetto <xref:System.Windows.Controls.Grid> senza modificare le dimensioni dell'oggetto <xref:System.Windows.Controls.Grid>.  
  
## Esempio  
 **Come creare un oggetto GridSplitter che si sovrapponga al bordo di una riga**  
  
 Per specificare un oggetto <xref:System.Windows.Controls.GridSplitter> che ridimensiona righe adiacenti in un oggetto <xref:System.Windows.Controls.Grid>, impostare la [proprietà connessa](GTMT) <xref:System.Windows.Controls.Grid.Row%2A> su una delle righe da ridimensionare.  Se l'oggetto <xref:System.Windows.Controls.Grid> contiene più colonne, impostare la proprietà <xref:System.Windows.Controls.Grid.ColumnSpan%2A> associata per specificare il numero di colonne.  Impostare quindi la proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> su <xref:System.Windows.VerticalAlignment> o <xref:System.Windows.VerticalAlignment> \(l'allineamento impostato dipende dalle due righe che si desidera ridimensionare\).  Impostare infine la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> su <xref:System.Windows.HorizontalAlignment>.  
  
 Nell'esempio riportato di seguito viene illustrato come definire un oggetto <xref:System.Windows.Controls.GridSplitter> orizzontale che ridimensiona righe adiacenti.  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterRowOverlay](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterrowoverlay)]  
  
 Un oggetto <xref:System.Windows.Controls.GridSplitter> che non occupa una riga specifica può essere nascosto da altri controlli nell'oggetto <xref:System.Windows.Controls.Grid>.  Per ulteriori informazioni su come evitare questo problema, vedere [Assicurarsi che GridSplitter sia visibile](../../../../docs/framework/wpf/controls/how-to-make-sure-that-a-gridsplitter-is-visible.md).  
  
 **Come creare un oggetto GridSplitter che occupa una riga**  
  
 Per specificare un oggetto <xref:System.Windows.Controls.GridSplitter> che occupa una riga in un oggetto <xref:System.Windows.Controls.Grid>, impostare la [proprietà connessa](GTMT) <xref:System.Windows.Controls.Grid.Row%2A> su una delle righe da ridimensionare.  Se l'oggetto <xref:System.Windows.Controls.Grid> contiene più colonne, impostare la proprietà <xref:System.Windows.Controls.Grid.ColumnSpan%2A> associata sul numero di colonne.  Impostare quindi la proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> su <xref:System.Windows.VerticalAlignment>, impostare la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> su <xref:System.Windows.HorizontalAlignment> e la proprietà <xref:System.Windows.Controls.RowDefinition.Height%2A> della riga che contiene l'oggetto <xref:System.Windows.Controls.GridSplitter> su <xref:System.Windows.GridLength.Auto%2A>.  
  
 Nell'esempio riportato di seguito viene illustrato come definire un oggetto <xref:System.Windows.Controls.GridSplitter> orizzontale che occupa una riga e ridimensiona le righe ai lati.  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterEntireRowPart1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart1)]  
[!code-xml[GridSplitterRowColumn#GridSplitterEntireRowPart2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirerowpart2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.GridSplitter>   
 [Procedure relative](../../../../docs/framework/wpf/controls/gridsplitter-how-to-topics.md)