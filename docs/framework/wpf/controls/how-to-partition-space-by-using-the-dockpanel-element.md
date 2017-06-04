---
title: "Procedura: partizionare lo spazio utilizzando l&#39;elemento DockPanel | Microsoft Docs"
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
  - "controlli [WPF], DockPanel"
  - "DockPanel (controllo), partizionamento dello spazio"
  - "partizionamento dello spazio"
ms.assetid: a219b9e5-b205-4438-89b5-0a137ac463ab
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: partizionare lo spazio utilizzando l&#39;elemento DockPanel
Nell'esempio seguente viene creato un semplice framework di [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] utilizzando un elemento <xref:System.Windows.Controls.DockPanel>.  L'oggetto <xref:System.Windows.Controls.DockPanel> partiziona lo spazio disponibile ai propri elementi figlio.  
  
## Esempio  
 In questo esempio viene utilizzata la proprietà <xref:System.Windows.Controls.DockPanel.Dock%2A>, che è una [proprietà connessa](GTMT), per ancorare due elementi <xref:System.Windows.Controls.Border> identici in corrispondenza dell'elemento <xref:System.Windows.Controls.Dock> dello spazio partizionato.  Un terzo elemento <xref:System.Windows.Controls.Border> viene ancorato all'elemento <xref:System.Windows.Controls.Dock>, con la larghezza impostata su 200 pixel.  Un quarto <xref:System.Windows.Controls.Border> è ancorato al <xref:System.Windows.Controls.Dock> dello schermo.  L'ultimo elemento <xref:System.Windows.Controls.Border> riempie automaticamente lo spazio rimanente.  
  
 [!code-cpp[DockPanelOvwSample#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xml[DockPanelOvwSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
> [!NOTE]
>  Per impostazione predefinita, l'ultimo elemento figlio di un elemento <xref:System.Windows.Controls.DockPanel> riempie lo spazio rimanente non allocato.  Se non si desidera ottenere questo comportamento, impostare `LastChildFill="False"`.  
  
 L'applicazione compilata produce una nuova interfaccia utente simile alla seguente.  
  
 ![Tipo scenario DockPanel](../../../../docs/framework/wpf/controls/media/panel-intro-dockpanel.png "panel\_intro\_dockpanel")  
  
## Vedere anche  
 <xref:System.Windows.Controls.DockPanel>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)