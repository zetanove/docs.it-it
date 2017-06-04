---
title: "Procedura: posizionare un oggetto ToolTip | Microsoft Docs"
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
  - "posizionamento di controlli ToolTip"
  - "ToolTip (controllo), posizionamento"
ms.assetid: cddf3757-9e5f-4ce3-a6eb-44489cf3804a
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: posizionare un oggetto ToolTip
In questo esempio viene illustrato come specificare la posizione di una descrizione comandi sullo schermo.  
  
## Esempio  
 È possibile posizionare una descrizione comandi utilizzando un insieme di cinque proprietà definite sia nella classe <xref:System.Windows.Controls.ToolTip> sia nella classe <xref:System.Windows.Controls.ToolTipService>.  Nella tabella seguente sono riportati questi due insiemi di cinque proprietà e vengono forniti i collegamenti alla relativa documentazione di riferimento in base alla classe.  
  
### Proprietà delle descrizioni comandi corrispondenti in base alla classe  
  
|Proprietà della classe <xref:System.Windows.Controls.ToolTip?displayProperty=fullName>|Proprietà della classe <xref:System.Windows.Controls.ToolTipService?displayProperty=fullName>|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.ToolTip.Placement%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.Placement%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.PlacementTarget%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.PlacementTarget%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.PlacementRectangle%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.PlacementRectangle%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.HorizontalOffset%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.HorizontalOffset%2A?displayProperty=fullName>|  
|<xref:System.Windows.Controls.ToolTip.VerticalOffset%2A?displayProperty=fullName>|<xref:System.Windows.Controls.ToolTipService.VerticalOffset%2A?displayProperty=fullName>|  
  
 Se si definisce il contenuto di una descrizione comandi utilizzando un oggetto <xref:System.Windows.Controls.ToolTip>, è possibile utilizzare le proprietà di una delle due classi. Tuttavia le proprietà della classe <xref:System.Windows.Controls.ToolTipService> hanno la precedenza.  Utilizzare le proprietà della classe <xref:System.Windows.Controls.ToolTipService> per le descrizioni comandi che non sono definite come oggetti <xref:System.Windows.Controls.ToolTip>.  
  
 Nelle illustrazioni seguenti viene mostrato come posizionare una descrizione comandi utilizzando queste proprietà.  Anche se negli esempi di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] di queste illustrazioni viene mostrato come impostare le proprietà definite dalla classe <xref:System.Windows.Controls.ToolTip>, le proprietà corrispondenti della classe <xref:System.Windows.Controls.ToolTipService> seguono le stesse regole di layout.  Per ulteriori informazioni sui possibili valori della proprietà Placement, vedere [Comportamento del controllo Popup in relazione al posizionamento](../../../../docs/framework/wpf/controls/popup-placement-behavior.md).  
  
 ![Posizionamento di ToolTip](../../../../docs/framework/wpf/controls/media/tooltipplacement.png "ToolTipPlacement")  
Posizionamento dell'oggetto ToolTip tramite la proprietà Placement  
  
 ![Posizionamento di ToolTip mediante un rettangolo di posizionamento](../../../../docs/framework/wpf/controls/media/tooltipplacementrectangle.png "ToolTipPlacementRectangle")  
Posizionamento dell'oggetto ToolTip tramite le proprietà Placement e PlacementRectangle  
  
 ![Diagramma di posizionamento di ToolTip](../../../../docs/framework/wpf/controls/media/tooltipplacementprhv.png "ToolTipPlacementPRHV")  
Posizionamento dell'oggetto ToolTip tramite le proprietà Placement, PlacementRectangle e Offset  
  
 Nell'esempio seguente viene illustrato come utilizzare le proprietà della classe <xref:System.Windows.Controls.ToolTip> per specificare la posizione di una descrizione comandi il cui contenuto è un oggetto <xref:System.Windows.Controls.ToolTip>.  
  
 [!code-xml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
 [!code-csharp[ToolTipService#ToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#tooltipcode)]
 [!code-vb[ToolTipService#ToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#tooltipcode)]  
  
 Nell'esempio seguente viene illustrato come utilizzare le proprietà della classe <xref:System.Windows.Controls.ToolTipService> per specificare la posizione di una descrizione comandi il cui contenuto non è un oggetto <xref:System.Windows.Controls.ToolTip>.  
  
 [!code-xml[ToolTipService#NoToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
 [!code-csharp[ToolTipService#NoToolTipCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml.cs#notooltipcode)]
 [!code-vb[ToolTipService#NoToolTipCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipService/visualbasic/pane1.xaml.vb#notooltipcode)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipService>   
 [Procedure relative](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)   
 [Panoramica sul controllo ToolTip](../../../../docs/framework/wpf/controls/tooltip-overview.md)   
 [Use the ContextMenuService and ToolTipService](http://msdn.microsoft.com/it-it/809b0e9c-d612-4cda-b8af-1a698c68f4d1)