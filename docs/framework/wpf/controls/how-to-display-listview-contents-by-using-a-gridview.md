---
title: "Procedura: visualizzare il contenuto di ListView utilizzando un oggetto GridView | Microsoft Docs"
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
  - "GridView, visualizzazione di contenuti ListView"
  - "ListView (controlli), visualizzazione di contenuti con GridView"
ms.assetid: 5bc1e767-ab46-4f14-bd41-3d5d39e1d000
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: visualizzare il contenuto di ListView utilizzando un oggetto GridView
In questo esempio viene illustrato come definire una modalità di visualizzazione <xref:System.Windows.Controls.GridView> per un controllo <xref:System.Windows.Controls.ListView>.  
  
## Esempio  
 È possibile definire la modalità di visualizzazione di <xref:System.Windows.Controls.GridView> specificando oggetti <xref:System.Windows.Controls.GridViewColumn>.  Nell’esempio riportato di seguito viene illustrato come definire gli oggetti <xref:System.Windows.Controls.GridViewColumn> associati al contenuto di dati specificato per il controllo <xref:System.Windows.Controls.ListView>.  In questo esempio di <xref:System.Windows.Controls.GridView> vengono specificati tre oggetti <xref:System.Windows.Controls.GridViewColumn> che eseguono il mapping ai campi `FirstName`, `LastName` e `EmployeeNumber` di `EmployeeInfoDataSource`, impostato come proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> del controllo <xref:System.Windows.Controls.ListView>.  
  
 [!code-xml[ListViewCode#ListViewEmployee](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 Nell’immagine riportata di seguito viene illustrato l’aspetto di questo esempio.  
  
 ![ListView con output GridView](../../../../docs/framework/wpf/controls/media/listviewgridview.png "ListViewGridView")  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)