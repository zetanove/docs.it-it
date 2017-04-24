---
title: "Panoramica sul controllo ListView | Microsoft Docs"
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
  - "controlli, ListView"
  - "ListView (controlli) [WPF], informazioni sul controllo ListView"
ms.assetid: 989e12b0-260e-4570-95c6-489284003ce2
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Panoramica sul controllo ListView
Il controllo <xref:System.Windows.Controls.ListView> fornisce l'infrastruttura per la visualizzazione di un insieme di elementi dei dati in layout o visualizzazioni diverse.  Ad esempio, un utente può scegliere di visualizzare gli elementi dei dati in una tabella e anche di ordinare le relative colonne.  
  
   
  
<a name="WhatisaListView"></a>   
## Definizione di ListView  
 Il controllo <xref:System.Windows.Controls.ListView> è un oggetto <xref:System.Windows.Controls.ItemsControl> derivato da <xref:System.Windows.Controls.ListBox>.  In genere, i relativi elementi sono membri di una raccolta dati e sono rappresentati come oggetti <xref:System.Windows.Controls.ListViewItem>.  Un oggetto <xref:System.Windows.Controls.ListViewItem> è un oggetto <xref:System.Windows.Controls.ContentControl> e può contenere solo un singolo elemento figlio.  Tuttavia, tale elemento figlio può essere qualsiasi elemento visuale.  
  
<a name="DefiningaListViewView"></a>   
## Definizione di una modalità di visualizzazione per un controllo ListView  
 Per specificare una modalità di visualizzazione per il contenuto di un controllo <xref:System.Windows.Controls.ListView>, impostare la proprietà <xref:System.Windows.Controls.ListView.View%2A>.  Una modalità di visualizzazione disponibile in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è <xref:System.Windows.Controls.GridView>, che visualizza una raccolta di elementi dei dati in una tabella con colonne personalizzabili.  
  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.GridView> per un controllo <xref:System.Windows.Controls.ListView> che visualizza informazioni sui dipendenti.  
  
 [!code-xml[ListViewCode#ListViewEmployee](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 Nell'immagine seguente viene illustrato come vengono visualizzati i dati per l'esempio precedente.  
  
 ![ListView con output GridView](../../../../docs/framework/wpf/controls/media/listviewgridview.png "ListViewGridView")  
  
 È possibile creare una modalità di visualizzazione personalizzata definendo una classe che eredita dalla classe <xref:System.Windows.Controls.ViewBase>.  La classe <xref:System.Windows.Controls.ViewBase> fornisce l'infrastruttura necessaria per creare una visualizzazione personalizzata.  Per ulteriori informazioni sulla creazione di una visualizzazione personalizzata, vedere [Creare una modalità di visualizzazione personalizzata per un oggetto ListView](../../../../docs/framework/wpf/controls/how-to-create-a-custom-view-mode-for-a-listview.md).  
  
<a name="BindingDatatoaListView"></a>   
## Associazione di dati a un controllo ListView  
 Utilizzare le proprietà <xref:System.Windows.Controls.ItemsControl.Items%2A> e <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> per specificare gli elementi per un controllo <xref:System.Windows.Controls.ListView>.  Nell'esempio seguente la proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> viene impostata su una raccolta dati denominata `EmployeeInfoDataSource`.  
  
 [!code-xml[ListViewCode#ItemsSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#itemssource)]  
  
 In un oggetto <xref:System.Windows.Controls.GridView> gli oggetti <xref:System.Windows.Controls.GridViewColumn> vengono associati ai campi dati specificati.  Nell'esempio seguente viene associato un oggetto <xref:System.Windows.Controls.GridViewColumn> a un campo dati specificando un oggetto <xref:System.Windows.Data.Binding> per la proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>.  
  
 [!code-csharp[ListViewCode#GridViewColumnProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml.cs#gridviewcolumnproperties)]
 [!code-vb[ListViewCode#GridViewColumnProperties](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCode/visualbasic/window1.xaml.vb#gridviewcolumnproperties)]
 [!code-xml[ListViewCode#GridViewColumnProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#gridviewcolumnproperties)]  
  
 È anche possibile specificare un oggetto <xref:System.Windows.Data.Binding> come parte della definizione di un oggetto <xref:System.Windows.DataTemplate> utilizzata per applicare uno stile alle celle di una colonna.  Nell'esempio seguente l'oggetto <xref:System.Windows.DataTemplate> identificato con un oggetto <xref:System.Windows.ResourceKey> imposta l'oggetto <xref:System.Windows.Data.Binding> per un oggetto <xref:System.Windows.Controls.GridViewColumn>.  Si noti che in questo esempio non viene definita la proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>, perché altrimenti verrebbe eseguito l'override dell'associazione specificata da <xref:System.Windows.DataTemplate>.  
  
 [!code-xml[ListViewTemplate#GridViewCellTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 [!code-xml[ListViewTemplate#CellTemplateProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
<a name="StylingaListView"></a>   
## Applicazione di uno stile a un controllo ListView che implementa una GridView  
 Il controllo <xref:System.Windows.Controls.ListView> contiene gli oggetti <xref:System.Windows.Controls.ListViewItem>, che rappresentano gli elementi dei dati visualizzati.  È possibile utilizzare le proprietà seguenti per definire il contenuto e lo stile degli elementi di dati:  
  
-   Sul controllo <xref:System.Windows.Controls.ListView> utilizzare le proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>, <xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A> e <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>.  
  
-   Sul controllo <xref:System.Windows.Controls.ListViewItem> utilizzare le proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> e <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A>.  
  
 Per evitare problemi di allineamento tra le celle in un controllo <xref:System.Windows.Controls.GridView>, non utilizzare la proprietà <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> per impostare proprietà o aggiungere contenuto che influisce sulla larghezza di un elemento in un controllo <xref:System.Windows.Controls.ListView>.  Ad esempio, può verificarsi un problema di allineamento quando si imposta la proprietà <xref:System.Windows.FrameworkElement.Margin%2A> in <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>.  Per specificare proprietà o definire contenuto che influisce sulla larghezza degli elementi in un controllo <xref:System.Windows.Controls.GridView>, utilizzare le proprietà della classe <xref:System.Windows.Controls.GridView> e le classi correlate, ad esempio <xref:System.Windows.Controls.GridViewColumn>.  
  
 Per ulteriori informazioni su come utilizzare <xref:System.Windows.Controls.GridView> e le relative classi di supporto, vedere [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md).  
  
 Se si definisce una proprietà <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> per un controllo <xref:System.Windows.Controls.ListView> e si definisce anche una proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>, è necessario includere un oggetto <xref:System.Windows.Controls.ContentPresenter> nello stile affinché la proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> funzioni correttamente.  
  
 Non utilizzare le proprietà <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> e <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> per il contenuto <xref:System.Windows.Controls.ListView> visualizzato utilizzando un oggetto <xref:System.Windows.Controls.GridView>.  Per specificare l'allineamento del contenuto in una colonna di un oggetto <xref:System.Windows.Controls.GridView>, definire una proprietà <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>.  
  
<a name="UsingtheSameViewMoreThanOnce"></a>   
## Condivisione della stessa modalità di visualizzazione  
 Due controlli <xref:System.Windows.Controls.ListView> non possono condividere contemporaneamente la stessa modalità di visualizzazione.  Se si tenta di utilizzare la stessa modalità di visualizzazione con più di un controllo <xref:System.Windows.Controls.ListView>, viene generata un'eccezione.  
  
 Per specificare una modalità di visualizzazione che può essere utilizzata simultaneamente da più controlli <xref:System.Windows.Controls.ListView>, utilizzare i modelli o gli stili.  Per un esempio su come definire le visualizzazioni come <xref:System.Windows.FrameworkElement.Resources%2A>, vedere [Esempio di ListView con più visualizzazioni](http://go.microsoft.com/fwlink/?LinkID=160013) \(la pagina potrebbe essere in inglese\).  
  
<a name="CreatingaCustomView"></a>   
## Creazione di una modalità di visualizzazione personalizzata  
 Le visualizzazioni personalizzate come <xref:System.Windows.Controls.GridView> vengono derivate dalla classe astratta <xref:System.Windows.Controls.ViewBase>, che rende disponibili gli strumenti per visualizzare gli elementi di dati rappresentati come oggetti <xref:System.Windows.Controls.ListViewItem>.  
  
 Per un esempio di una modalità di visualizzazione personalizzata, vedere [Esempio di ListView con più visualizzazioni](http://go.microsoft.com/fwlink/?LinkID=160013) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Controls.GridView>   
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.ListViewItem>   
 <xref:System.Windows.Data.Binding>   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Controlli](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)