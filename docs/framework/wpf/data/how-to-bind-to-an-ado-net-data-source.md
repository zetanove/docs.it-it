---
title: "Procedura: eseguire l&#39;associazione a un&#39;origine dati ADO.NET | Microsoft Docs"
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
  - "ADO.NET (origini dati), associazione a"
  - "associazione, a origini dati ADO.NET"
  - "associazione dati, associazione a origini dati ADO.NET"
ms.assetid: a70c6d7b-7b38-4fdf-b655-4804db7c8315
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: eseguire l&#39;associazione a un&#39;origine dati ADO.NET
In questo esempio viene illustrato come associare un controllo <xref:System.Windows.Controls.ListBox> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] a un oggetto `DataSet` [!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)].  
  
## Esempio  
 Nell'esempio, viene utilizzato un oggetto `OleDbConnection` per la connessione all'origine dati, ovvero un file `Access MDB` specificato nella stringa di connessione.  Una volta stabilita la connessione, viene creato un oggetto `OleDbDataAdpater`,  che esegue un'istruzione [!INCLUDE[TLA#tla_sql](../../../../includes/tlasharptla-sql-md.md)] Select per recuperare il recordset dal database.  I risultati del comando [!INCLUDE[TLA2#tla_sql](../../../../includes/tla2sharptla-sql-md.md)] vengono archiviati in un oggetto `DataTable` dell'oggetto `DataSet` chiamando il metodo `Fill` di `OleDbDataAdapter`.  Il nome dell'oggetto `DataTable` dell'esempio è `BookTable`.  Viene quindi impostata la proprietà <xref:System.Windows.FrameworkElement.DataContext%2A> di <xref:System.Windows.Controls.ListBox> sull'oggetto `DataSet`.  
  
 [!code-csharp[ADODataSet#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ADODataSet#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ADODataSet/VisualBasic/Window1.xaml.vb#1)]  
  
 A questo punto è possibile associare la proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> di <xref:System.Windows.Controls.ListBox> su `BookTable` per l'oggetto `DataSet`:  
  
 [!code-xml[ADODataSet#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml#2)]  
  
 `BookItemTemplate` è l'oggetto <xref:System.Windows.DataTemplate> che definisce la modalità di visualizzazione dei dati:  
  
 [!code-xml[ADODataSet#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml#3)]  
  
 Il convertitore `IntColorConverter` consente di convertire un oggetto `int` in un colore.  Se si utilizza questo convertitore, il colore di <xref:System.Windows.Controls.TextBlock.Background%2A> del terzo oggetto <xref:System.Windows.Controls.TextBlock> sarà verde se il valore di `NumPages` è inferiore a 350; in caso contrario sarà rosso.  L'implementazione del convertitore non viene illustrata in questo argomento.  
  
## Vedere anche  
 <xref:System.Windows.Data.BindingListCollectionView>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)