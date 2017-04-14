---
title: "Procedura: utilizzare i modelli per applicare uno stile a un ListView che utilizza una GridView | Microsoft Docs"
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
  - "ListView (controlli), applicazione di stili"
ms.assetid: 94bf964b-96c8-4bdf-a0c3-f5271b7cb565
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: utilizzare i modelli per applicare uno stile a un ListView che utilizza una GridView
In questo esempio viene illustrato come utilizzare gli oggetti <xref:System.Windows.DataTemplate> e <xref:System.Windows.Style> per specificare l'aspetto di un controllo <xref:System.Windows.Controls.ListView> che utilizza una modalità di visualizzazione <xref:System.Windows.Controls.GridView>.  
  
## Esempio  
 Negli esempi seguenti vengono illustrati gli oggetti <xref:System.Windows.Style> e <xref:System.Windows.DataTemplate> che personalizzano l'aspetto di un'intestazione di colonna per un controllo <xref:System.Windows.Controls.GridViewColumn>.  
  
 [!code-xml[ListViewTemplate#GridViewHeaderStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheaderstyle)]  
  
 [!code-xml[ListViewTemplate#GridViewHeaderTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheadertemplate)]  
  
 Nell'esempio seguente viene illustrato come utilizzare questi oggetti <xref:System.Windows.Style> e <xref:System.Windows.DataTemplate> per impostare le proprietà <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> e <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> di un controllo <xref:System.Windows.Controls.GridViewColumn>.  La proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> definisce il contenuto delle celle delle colonne.  
  
 [!code-xml[ListViewTemplate#GridViewColumnTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcolumntemplate)]  
  
 <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> e <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> sono solo due delle numerose proprietà che è possibile utilizzare per personalizzare l'aspetto delle intestazioni di colonna di un controllo <xref:System.Windows.Controls.GridView>.  Per ulteriori informazioni, vedere [Panoramica sui modelli e sugli stili di intestazione delle colonne in GridView](../../../../docs/framework/wpf/controls/gridview-column-header-styles-and-templates-overview.md).  
  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.DataTemplate> che personalizza l'aspetto delle celle in un controllo <xref:System.Windows.Controls.GridViewColumn>.  
  
 [!code-xml[ListViewTemplate#GridViewCellTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 Nell'esempio seguente viene illustrato come utilizzare questo oggetto <xref:System.Windows.DataTemplate> per definire il contenuto di una cella di un controllo <xref:System.Windows.Controls.GridViewColumn>.  Questo modello viene utilizzato al posto della proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> mostrata nell'esempio di <xref:System.Windows.Controls.GridViewColumn> precedente.  
  
 [!code-xml[ListViewTemplate#CellTemplateProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)