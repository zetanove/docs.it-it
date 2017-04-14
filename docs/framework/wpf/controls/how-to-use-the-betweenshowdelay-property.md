---
title: "Procedura: utilizzare la propriet&#224; BetweenShowDelay | Microsoft Docs"
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
  - "BetweenShowDelay (proprietà temporale)"
  - "ToolTip (controllo), BetweenShowDelay (proprietà temporale)"
ms.assetid: 984ea76d-f2a2-4326-a02e-f97ec3d036d6
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: utilizzare la propriet&#224; BetweenShowDelay
In questo esempio viene illustrato come utilizzare la proprietà temporale <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> in modo che le descrizioni comandi vengano visualizzate rapidamente, quasi senza ritardo, quando l'utente sposta il puntatore del mouse direttamente da una descrizione comandi a un'altra.  
  
## Esempio  
 Nell'esempio seguente la proprietà <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> è impostata su un secondo \(1000 millisecondi\) e la proprietà <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> su due secondi \(2000 millisecondi\) per le descrizioni comandi di entrambi i controlli <xref:System.Windows.Shapes.Ellipse>.  Se si visualizza la descrizione comandi per una delle ellissi e quindi entro due secondi si sposta e si mantiene il puntatore del mouse su un'altra ellisse, la descrizione comandi della seconda ellisse viene visualizzata immediatamente.  
  
 In entrambi gli scenari seguenti viene applicata la proprietà <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>, che genera un'attesa di un secondo prima che venga visualizzata la descrizione comandi della seconda ellisse:  
  
-   Se il tempo richiesto per il passaggio al secondo pulsante è superiore a due secondi.  
  
-   Se la descrizione comandi non è visibile all'inizio dell'intervallo di tempo per la prima ellisse.  
  
 [!code-xml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
[!code-xml[ToolTipService#NoToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipService>   
 [Procedure relative](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)   
 [Panoramica sul controllo ToolTip](../../../../docs/framework/wpf/controls/tooltip-overview.md)