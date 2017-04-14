---
title: "Procedura: visualizzare i dati utilizzando GridViewRowPresenter | Microsoft Docs"
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
  - "visualizzazione di dati con GridViewRowPresenter"
  - "GridViewRowPresenter"
ms.assetid: bdb785a5-a262-44d5-a517-ea14383e5f70
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: visualizzare i dati utilizzando GridViewRowPresenter
In questo esempio viene illustrato come utilizzare gli oggetti <xref:System.Windows.Controls.GridViewRowPresenter> e <xref:System.Windows.Controls.GridViewHeaderRowPresenter> per visualizzare dati in colonne.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare un oggetto <xref:System.Windows.Controls.GridViewColumnCollection> che visualizza le proprietà <xref:System.DateTime.DayOfWeek%2A> e <xref:System.DateTime.Year%2A> di un oggetto <xref:System.DateTime> utilizzando gli oggetti <xref:System.Windows.Controls.GridViewRowPresenter> e <xref:System.Windows.Controls.GridViewHeaderRowPresenter>.  Viene inoltre definito un oggetto <xref:System.Windows.Style> per la proprietà <xref:System.Windows.Controls.GridViewColumn.Header%2A> di un oggetto <xref:System.Windows.Controls.GridViewColumn>.  
  
 [!code-xml[GridViewRowPresenterSample#GridViewRowPresenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewRowPresenterSample/CS/Window1.xaml#gridviewrowpresenter)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.GridViewHeaderRowPresenter>   
 <xref:System.Windows.Controls.GridViewRowPresenter>   
 <xref:System.Windows.Controls.GridViewColumnCollection>   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)