---
title: "Procedura: creare un elemento Grid | Microsoft Docs"
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
  - "Grid (controllo), creazione, istanza di griglia"
ms.assetid: b2f07626-9df8-43b8-8d36-492f3cb42837
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare un elemento Grid
## Esempio  
 Nell'esempio seguente viene illustrato come creare e utilizzare un'istanza dell'elemento <xref:System.Windows.Controls.Grid> utilizzando [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] o codice.  Nell'esempio vengono utilizzate tre oggetti <xref:System.Windows.Controls.ColumnDefinition> e tre oggetti <xref:System.Windows.Controls.RowDefinition> per creare una griglia con nove celle come in un foglio di lavoro.  Ogni cella contiene un elemento <xref:System.Windows.Controls.TextBlock> che rappresenta dati, mentre la riga superiore contiene un oggetto <xref:System.Windows.Controls.TextBlock> con la proprietà <xref:System.Windows.Controls.Grid.ColumnSpan%2A> applicata.  Per visualizzare i limiti di ogni cella, viene abilitata la proprietà <xref:System.Windows.Controls.Grid.ShowGridLines%2A>.  
  
 [!code-csharp[Grid#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Grid/CSharp/Grid_Code.cs#3)]
 [!code-vb[Grid#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Grid/VisualBasic/grid_vb.vb#3)]
 [!code-xml[Grid#3](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Grid/XAML/default.xaml#3)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Grid>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)