---
title: "Procedura: creare una griglia complessa | Microsoft Docs"
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
  - "calendario, creazione"
  - "Grid (controllo), creazione, griglia complessa"
  - "calendario mensile, creazione"
ms.assetid: 4ce3040a-a156-4364-9596-98ca1eca5550
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare una griglia complessa
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Controls.Grid> per creare un layout simile a un calendario mensile.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono definite otto righe e otto colonne utilizzando le classi <xref:System.Windows.Controls.RowDefinition> e <xref:System.Windows.Controls.ColumnDefinition>.  Vengono utilizzate le proprietà <xref:System.Windows.Controls.Grid.ColumnSpan%2A?displayProperty=fullName> e <xref:System.Windows.Controls.Grid.RowSpan%2A?displayProperty=fullName> associate, insieme agli elementi <xref:System.Windows.Shapes.Rectangle>, che riempiono gli sfondi delle varie colonne e righe.  Questa progettazione è resa possibile da fatto che in ogni cella di un oggetto <xref:System.Windows.Controls.Grid> possono essere presenti più elementi, una differenza essenziale tra <xref:System.Windows.Controls.Grid> e <xref:System.Windows.Documents.Table>.  
  
 Nell'esempio vengono utilizzate sfumature verticali nella proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> per riempire le colonne e le righe al fine di migliorare l'aspetto e la leggibilità del calendario.  Gli elementi con stile <xref:System.Windows.Controls.TextBlock> rappresentano le date e i giorni della settimana.  Gli elementi <xref:System.Windows.Controls.TextBlock> sono posizionati in modo assoluto all'interno delle celle utilizzando la proprietà <xref:System.Windows.FrameworkElement.Margin%2A> e proprietà di allineamento definite all'interno dello stile per l'applicazione.  
  
 [!code-xml[GridComplex#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridComplex/CS/default.xaml#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.Documents.TableCell>   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Cenni preliminari sull'elemento Table](../../../../docs/framework/wpf/advanced/table-overview.md)