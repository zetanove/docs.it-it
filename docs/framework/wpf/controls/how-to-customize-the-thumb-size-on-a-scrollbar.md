---
title: "Procedura: personalizzare le dimensioni del cursore in una barra di scorrimento | Microsoft Docs"
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
  - "personalizzazione delle dimensioni del cursore"
  - "ScrollBar (controllo)"
  - "dimensioni del cursore"
ms.assetid: fa32b866-5ca1-4e73-85e7-2ac64b80d194
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: personalizzare le dimensioni del cursore in una barra di scorrimento
In questo argomento viene illustrato come impostare <xref:System.Windows.Controls.Primitives.Thumb> di un oggetto<xref:System.Windows.Controls.Primitives.ScrollBar> su dimensioni fisse e come specificare la dimensione minima per <xref:System.Windows.Controls.Primitives.Thumb> di un oggetto <xref:System.Windows.Controls.Primitives.ScrollBar>.  
  
## Esempio  
  
## Descrizione  
 Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> che include un oggetto <xref:System.Windows.Controls.Primitives.Thumb> con dimensioni fisse.  Viene quindi impostata la proprietà <xref:System.Windows.Controls.Primitives.Track.ViewportSize%2A> dell'oggetto <xref:System.Windows.Controls.Primitives.Thumb> su <xref:System.Double.NaN> e l'altezza dell'oggetto <xref:System.Windows.Controls.Primitives.Thumb>.  Per creare un oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> orizzontale con un oggetto <xref:System.Windows.Controls.Primitives.Thumb> con larghezza fissa, impostare la larghezza dell'oggetto <xref:System.Windows.Controls.Primitives.Thumb>.  
  
## Codice  
 [!code-xml[ScrollBarCustomThumbSize#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#1)]  
  
## Descrizione  
 Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> che include un oggetto <xref:System.Windows.Controls.Primitives.Thumb> con una dimensione minima.  Viene quindi impostato il valore dell'oggetto <xref:System.Windows.SystemParameters.VerticalScrollBarButtonHeightKey%2A>.  Per creare un oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> orizzontale con un oggetto <xref:System.Windows.Controls.Primitives.Thumb> con larghezza minima, impostare <xref:System.Windows.SystemParameters.HorizontalScrollBarButtonWidthKey%2A>.  
  
## Codice  
 [!code-xml[ScrollBarCustomThumbSize#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#2)]  
  
## Vedere anche  
 [Stili e modelli di ScrollBar](../../../../docs/framework/wpf/controls/scrollbar-styles-and-templates.md)