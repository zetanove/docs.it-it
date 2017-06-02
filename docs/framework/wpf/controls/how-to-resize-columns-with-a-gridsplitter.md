---
title: "Procedura: ridimensionare le colonne con un GridSplitter | Microsoft Docs"
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
  - "colonne della griglia, ridimensionamento"
  - "GridSplitter (controllo), ridimensionamento delle colonne della griglia"
  - "ridimensionamento delle colonne della griglia"
ms.assetid: 47b20fe6-7adc-4aa6-9693-b4e184eef74b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: ridimensionare le colonne con un GridSplitter
In questo esempio viene illustrato come creare un oggetto <xref:System.Windows.Controls.GridSplitter> verticale per ridistribuire lo spazio tra due colonne in un oggetto <xref:System.Windows.Controls.Grid> senza modificare le dimensioni dell'oggetto <xref:System.Windows.Controls.Grid>.  
  
## Esempio  
 **Come creare un oggetto GridSplitter che si sovrapponga al bordo di una colonna**  
  
 Per specificare un oggetto <xref:System.Windows.Controls.GridSplitter> che ridimensiona colonne adiacenti in un oggetto <xref:System.Windows.Controls.Grid>, impostare la [proprietà connessa](GTMT) <xref:System.Windows.Controls.Grid.Column%2A> su una delle colonne da ridimensionare.  Se l'oggetto <xref:System.Windows.Controls.Grid> contiene più righe, impostare la proprietà associata <xref:System.Windows.Controls.Grid.RowSpan%2A> sul numero di righe.  Impostare quindi la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> su <xref:System.Windows.HorizontalAlignment> o su <xref:System.Windows.HorizontalAlignment> \(l'allineamento impostato dipende dalle due colonne che si desidera ridimensionare\).  Impostare infine la proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> su <xref:System.Windows.VerticalAlignment>.  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterColumnOverlay](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplittercolumnoverlay)]  
  
 Un oggetto <xref:System.Windows.Controls.GridSplitter> che non ha una propria colonna può essere nascosto da altri controlli nell'oggetto <xref:System.Windows.Controls.Grid>.  Per ulteriori informazioni su come evitare questo problema, vedere [Assicurarsi che GridSplitter sia visibile](../../../../docs/framework/wpf/controls/how-to-make-sure-that-a-gridsplitter-is-visible.md).  
  
 **Come creare un oggetto GridSplitter che occupa una colonna**  
  
 Per specificare un oggetto <xref:System.Windows.Controls.GridSplitter> che occupa una colonna in un oggetto <xref:System.Windows.Controls.Grid>, impostare la [proprietà connessa](GTMT) <xref:System.Windows.Controls.Grid.Column%2A> su una delle colonne da ridimensionare.  Se l'oggetto Grid contiene più righe, impostare la proprietà <xref:System.Windows.Controls.Grid.RowSpan%2A> associata sul numero di righe.  Impostare quindi la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> su <xref:System.Windows.HorizontalAlignment>, impostare la proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> su <xref:System.Windows.VerticalAlignment> e la proprietà <xref:System.Windows.Controls.ColumnDefinition.Width%2A> della colonna che contiene l'oggetto <xref:System.Windows.Controls.GridSplitter> su <xref:System.Windows.GridLength.Auto%2A>.  
  
 Nell'esempio riportato di seguito viene illustrato come definire un oggetto <xref:System.Windows.Controls.GridSplitter> verticale che occupa una colonna e ridimensiona le colonne ai lati.  
  
 [!code-xml[GridSplitterRowColumn#GridSplitterEntireColumnPart1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart1)]  
[!code-xml[GridSplitterRowColumn#GridSplitterEntireColumnPart2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.GridSplitter>   
 [Procedure relative](../../../../docs/framework/wpf/controls/gridsplitter-how-to-topics.md)