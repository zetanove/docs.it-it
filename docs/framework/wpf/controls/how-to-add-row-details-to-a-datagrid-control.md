---
title: "Procedura: aggiungere dettagli di riga un controllo DataGrid | Microsoft Docs"
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
  - "DataGrid [WPF], dettagli riga"
  - "DataTemplate [WPF], DataGrid"
  - "dettagli riga [WPF], DataGrid"
ms.assetid: 0bdc6f50-9b4c-483f-9df6-a47a1fde998b
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: aggiungere dettagli di riga un controllo DataGrid
Quando si utilizza il controllo <xref:System.Windows.Controls.DataGrid>, è possibile personalizzare la presentazione dei dati aggiungendo una sezione dei dettagli di riga.  L'aggiunta di una sezione dei dettagli di riga consente di raggruppare i dati in un modello che è possibile rendere visibile o compresso.  È ad esempio possibile aggiungere dettagli di riga a un oggetto <xref:System.Windows.Controls.DataGrid> che includa solo un riepilogo dei dati per ogni riga in <xref:System.Windows.Controls.DataGrid>, ma che presenti più campi dati quando l'utente seleziona una riga.  Il modello per i dettagli di riga viene definito nella proprietà <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>.  Nella figura seguente viene illustrato un esempio di una sezione dei dettagli di riga.  
  
 ![DataGrid con i dettagli della riga](../../../../docs/framework/wpf/controls/media/ndp-rowdetails.png "NDP\_RowDetails")  
  
 Il modello dei dettagli di riga può essere definito sia come codice XAML inline sia come risorsa.  Entrambi gli approcci vengono illustrati nelle procedure seguenti.  Un modello di dati aggiunto come risorsa può essere utilizzato in tutto il progetto senza che sia necessario ricreare il modello.  Un modello di dati aggiunto come codice XAML inline è invece accessibile solo dal controllo in cui viene definito.  
  
### Per visualizzare dettagli della riga tramite codice XAML inline  
  
1.  Creare un oggetto <xref:System.Windows.Controls.DataGrid> che determini la visualizzazione di dati da un'origine dati.  
  
2.  Nell'elemento <xref:System.Windows.Controls.DataGrid> aggiungere un elemento <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>.  
  
3.  Creare un oggetto <xref:System.Windows.DataTemplate> che definisca l'aspetto della sezione dei dettagli di riga.  
  
     Nel codice XAML seguente vengono illustrati <xref:System.Windows.Controls.DataGrid> e come definire l'oggetto <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> inline.  L'oggetto <xref:System.Windows.Controls.DataGrid> determina la visualizzazione di tre valori in ogni riga e di tre ulteriori valori quando la riga viene selezionata.  
  
     [!code-xml[DataGrid_RowDetails#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml#1)]  
  
     Nel codice seguente viene illustrata la query utilizzata per selezionare i dati visualizzati in <xref:System.Windows.Controls.DataGrid>.  In questo esempio la query seleziona dati da un'entità contenente informazioni sul cliente.  
  
     [!code-csharp[DataGrid_RowDetails#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml.cs#2)]
     [!code-vb[DataGrid_RowDetails#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_rowdetails/vb/mainwindow.xaml.vb#2)]  
  
### Per visualizzare dettagli di riga tramite una risorsa  
  
1.  Creare un oggetto <xref:System.Windows.Controls.DataGrid> che determini la visualizzazione di dati da un'origine dati.  
  
2.  Aggiungere un elemento <xref:System.Windows.FrameworkElement.Resources%2A> all'elemento radice, ad esempio un controllo <xref:System.Windows.Window> o un controllo <xref:System.Windows.Controls.Page> oppure aggiunge un elemento <xref:System.Windows.Application.Resources%2A> alla classe <xref:System.Windows.Application> nel file App.xaml \(o Application.xaml\).  
  
3.  Nell'elemento delle risorse creare un oggetto <xref:System.Windows.DataTemplate> che definisca l'aspetto della sezione dei dettagli di riga.  
  
     Nel codice XAML seguente viene illustrata la proprietà <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> definita nella classe <xref:System.Windows.Application>.  
  
     [!code-xml[DataGrid_RowDetails#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/app.xaml#3)]  
  
4.  Sull'oggetto <xref:System.Windows.DataTemplate> impostare [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md) su un valore che identifichi in modo univoco il modello di dati.  
  
5.  Nell'elemento <xref:System.Windows.Controls.DataGrid> impostare la proprietà <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> sulla risorsa definita nei passaggi precedenti.  Assegnare la risorsa come risorsa statica.  
  
     Nel codice XAML seguente viene illustrata la proprietà <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> impostata sulla risorsa dell'esempio precedente.  
  
     [!code-xml[DataGrid_RowDetails#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/window2.xaml#4)]  
  
### Per impostare la visibilità e impedire lo scorrimento orizzontale per i dettagli di riga  
  
1.  Se necessario, impostare la proprietà <xref:System.Windows.Controls.DataGrid.RowDetailsVisibilityMode%2A> su un valore di <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode>.  
  
     Per impostazione predefinita, il valore viene impostato su <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode>.  È possibile impostarlo su <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> per visualizzare i dettagli per tutte le righe oppure su <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> per nascondere i dettagli per tutte le righe.  
  
2.  Se necessario, impostare la proprietà <xref:System.Windows.Controls.DataGrid.AreRowDetailsFrozen%2A> su `true` per impedire lo scorrimento orizzontale della sezione dei dettagli di riga.