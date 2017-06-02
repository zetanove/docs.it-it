---
title: "Panoramica sui modelli e sugli stili di intestazione delle colonne in GridView | Microsoft Docs"
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
  - "intestazioni di colonna, personalizzazione"
  - "controlli, ListView"
  - "GridView (modalità di visualizzazione), personalizzazione delle intestazioni di colonne"
  - "intestazioni, personalizzazione"
  - "ListView (controlli) [WPF], GridView (stili delle intestazioni delle colonne)"
ms.assetid: 74835674-a39e-4ab5-9418-ad7f6ab7b956
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Panoramica sui modelli e sugli stili di intestazione delle colonne in GridView
In questa sezione viene descritto l'ordine di precedenza delle proprietà utilizzate per personalizzare un'intestazione di colonna nella modalità di visualizzazione <xref:System.Windows.Controls.GridView> di un controllo <xref:System.Windows.Controls.ListView>.  
  
## Personalizzazione di un'intestazione di colonna in GridView  
 Le proprietà che definiscono il contenuto, il layout e lo stile di un'intestazione di colonna in un oggetto <xref:System.Windows.Controls.GridView> sono disponibili in molte classi correlate.  Alcune di queste proprietà hanno funzionalità analoghe o identiche.  
  
 Nelle righe della tabella seguente sono illustrati gruppi di proprietà che eseguono la stessa funzione.  È possibile utilizzare queste proprietà per personalizzare le intestazioni di colonna in un oggetto <xref:System.Windows.Controls.GridView>.  L'ordine di precedenza per le proprietà correlate è da destra a sinistra, dove la proprietà nella colonna all'estrema destra ha la massima precedenza.  Ad esempio, se per l'oggetto <xref:System.Windows.Controls.GridViewColumnHeader> è impostata una proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> e per l'oggetto <xref:System.Windows.Controls.GridViewColumn> associato è impostata la proprietà <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A>, la proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> ha la precedenza.  In questo scenario la proprietà <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A> non ha effetto.  
  
 **Proprietà correlate per le intestazioni di colonna in GridView**  
  
|||||  
|-|-|-|-|  
|**Classi**|<xref:System.Windows.Controls.GridView>|<xref:System.Windows.Controls.GridViewColumn>|<xref:System.Windows.Controls.GridViewColumnHeader>|  
|**Proprietà dei menu di scelta rapida**|<xref:System.Windows.Controls.GridView.ColumnHeaderContextMenu%2A>|Non applicabile|<xref:System.Windows.FrameworkElement.ContextMenu%2A>|  
|**ToolTip**<br /><br /> **Proprietà**|<xref:System.Windows.Controls.GridView.ColumnHeaderToolTip%2A>|Non applicabile|<xref:System.Windows.FrameworkElement.ToolTip%2A>|  
|**Proprietà dei**<br /><br /> **Proprietà**|<xref:System.Windows.Controls.GridView.ColumnHeaderTemplate%2A> <sup>1</sup>\/<br /><br /> <xref:System.Windows.Controls.GridView.ColumnHeaderTemplateSelector%2A>|<xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> <sup>1</sup>\/<br /><br /> <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A>|<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> <sup>1</sup>\/<br /><br /> <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A>|  
|**Proprietà di stile**|<xref:System.Windows.Controls.GridView.ColumnHeaderContainerStyle%2A>|<xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A>|<xref:System.Windows.FrameworkElement.Style%2A>|  
  
 <sup>1</sup>Per le**proprietà dei modelli di intestazione**, se si impostano sia la proprietà del modello che la proprietà di selezione modello, la proprietà del modello ha la precedenza.  Ad esempio, se si impostano entrambe le proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> e <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A>, la proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> avrà la precedenza.  
  
## Vedere anche  
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)