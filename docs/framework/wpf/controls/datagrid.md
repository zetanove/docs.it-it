---
title: "DataGrid | Microsoft Docs"
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
  - "controlli [WPF], DataGrid"
  - "DataGrid [WPF], attività comuni"
  - "DataGrid [WPF], personalizzazione dell'aspetto"
  - "DataGrid (tipi di colonne) [WPF]"
  - "DataGrid (colonne) [WPF], utilizzo"
  - "DataGrid (controllo) [WPF]"
  - "DataGrid (scenari) [WPF]"
ms.assetid: bf89ea63-79b6-422b-bc9f-0485ad803216
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# DataGrid
Il controllo <xref:System.Windows.Controls.DataGrid> consente di visualizzare e modificare dati da molte origini diverse, ad esempio da un database SQL, una query LINQ o qualsiasi altra origine dati associabile.  Per ulteriori informazioni, vedere [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md).  
  
 Nelle colonne è possibile visualizzare testo, controlli, ad esempio <xref:System.Windows.Controls.ComboBox>, o qualsiasi altro contenuto WPF, ad esempio immagini, pulsanti o qualsiasi contenuto presente in un modello.  È possibile utilizzare un oggetto <xref:System.Windows.Controls.DataGridTemplateColumn> per visualizzare i dati definiti in un modello.  Nella tabella riportata di seguito sono elencati i tipi di colonna forniti per impostazione predefinita.  
  
|Tipo di colonna generata|Tipo di dati|  
|------------------------------|------------------|  
|<xref:System.Windows.Controls.DataGridTextColumn>|<xref:System.String>|  
|<xref:System.Windows.Controls.DataGridCheckBoxColumn>|<xref:System.Boolean>|  
|<xref:System.Windows.Controls.DataGridComboBoxColumn>|<xref:System.Enum>|  
|<xref:System.Windows.Controls.DataGridHyperlinkColumn>|<xref:System.Uri>|  
  
 <xref:System.Windows.Controls.DataGrid> può essere personalizzato nell'aspetto, ad esempio il tipo di carattere di cella, il colore e la dimensione.  <xref:System.Windows.Controls.DataGrid> supporta tutte le funzionalità di applicazione di stili e modelli degli altri controlli WPF.  In <xref:System.Windows.Controls.DataGrid> sono inoltre inclusi i comportamenti predefiniti e personalizzabili per la modifica, l'ordinamento e la convalida.  
  
 Nella tabella seguente sono elencate alcune delle attività comuni per <xref:System.Windows.Controls.DataGrid> e viene descritto come eseguirle.  Visualizzando l'API correlata, è possibile ottenere maggiori informazioni e codice di esempio.  
  
|Scenario|Approccio|  
|--------------|---------------|  
|Colori di sfondo alternati|Impostare la proprietà <xref:System.Windows.Controls.ItemsControl.AlternationIndex%2A> su 2 o un valore superiore, quindi assegnare un oggetto <xref:System.Windows.Media.Brush> alle proprietà <xref:System.Windows.Controls.DataGrid.RowBackground%2A> e <xref:System.Windows.Controls.DataGrid.AlternatingRowBackground%2A>.|  
|Definire il comportamento di selezione per celle e righe|Impostare le proprietà <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> e <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A>.|  
|Personalizzare l'aspetto visivo di intestazioni, celle e righe|Applicare un nuovo oggetto <xref:System.Windows.Style> alle proprietà <xref:System.Windows.Controls.DataGrid.ColumnHeaderStyle%2A>, <xref:System.Windows.Controls.DataGrid.RowHeaderStyle%2A>, <xref:System.Windows.Controls.DataGrid.CellStyle%2A> o <xref:System.Windows.Controls.DataGrid.RowStyle%2A>.|  
|Impostare le opzioni di dimensionamento|Impostare le proprietà <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A>, <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.FrameworkElement.MaxWidth%2A> o <xref:System.Windows.FrameworkElement.MinWidth%2A>.  Per ulteriori informazioni, vedere [Opzioni di ridimensionamento nel controllo DataGrid](../../../../docs/framework/wpf/controls/sizing-options-in-the-datagrid-control.md).|  
|Accedere agli elementi selezionati|Controllare la proprietà <xref:System.Windows.Controls.DataGrid.SelectedCells%2A> per ottenere le celle selezionate e la proprietà <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems%2A> per ottenere le righe selezionate.  Per ulteriori informazioni, vedere <xref:System.Windows.Controls.DataGrid.SelectedCells%2A>.|  
|Personalizzare le interazioni dell'utente finale|Impostare le proprietà <xref:System.Windows.Controls.DataGrid.CanUserAddRows%2A>, <xref:System.Windows.Controls.DataGrid.CanUserDeleteRows%2A>, <xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A>, <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A>, <xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A> e <xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A>.|  
|Annullare o modificare le colonne generate automaticamente|Gestire l'evento <xref:System.Windows.Controls.DataGrid.AutoGeneratingColumn>.|  
|Bloccare una colonna|Impostare la proprietà <xref:System.Windows.Controls.DataGrid.FrozenColumnCount%2A> su 1 e spostare la colonna nella posizione all'estrema sinistra impostando la proprietà <xref:System.Windows.Controls.DataGridColumn.DisplayIndex%2A> su 0.|  
|Utilizzare i dati XML come origine dati|Associare <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> in <xref:System.Windows.Controls.DataGrid> alla query XPath che rappresenta la raccolta di elementi.  Creare ogni colonna in <xref:System.Windows.Controls.DataGrid>.  Associare ogni colonna impostando XPath nell'associazione sulla query che ottiene la proprietà nell'origine dell'elemento.  Per un esempio, vedere <xref:System.Windows.Controls.DataGridTextColumn>.|  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Procedura dettagliata: aggiunta di dati di un database di SQL Server in un controllo DataGrid](../../../../docs/framework/wpf/controls/walkthrough-display-data-from-a-sql-server-database-in-a-datagrid-control.md)|Viene descritto come impostare un nuovo progetto WPF, aggiungere un elemento Entity Framework, impostare l'origine e visualizzare i dati in un oggetto <xref:System.Windows.Controls.DataGrid>.|  
|[Procedura: aggiungere dettagli di riga un controllo DataGrid](../../../../docs/framework/wpf/controls/how-to-add-row-details-to-a-datagrid-control.md)|Viene descritto come creare dettagli riga per un oggetto <xref:System.Windows.Controls.DataGrid>.|  
|[Procedura: implementare la convalida con il controllo DataGrid](../../../../docs/framework/wpf/controls/how-to-implement-validation-with-the-datagrid-control.md)|Viene descritto come convalidare valori in celle e righe <xref:System.Windows.Controls.DataGrid> e visualizzare commenti e suggerimenti di convalida.|  
|[Comportamento predefinito di tastiera e mouse nel controllo DataGrid](../../../../docs/framework/wpf/controls/default-keyboard-and-mouse-behavior-in-the-datagrid-control.md)|Viene descritto come interagire con il controllo <xref:System.Windows.Controls.DataGrid> utilizzando la tastiera e il mouse.|  
|[Procedura: raggruppare, ordinare e filtrare dati nel controllo DataGrid](../../../../docs/framework/wpf/controls/how-to-group-sort-and-filter-data-in-the-datagrid-control.md)|Viene descritto come visualizzare dati in un oggetto <xref:System.Windows.Controls.DataGrid> in diversi modi attraverso il raggruppamento, l'ordinamento e il filtro di dati.|  
|[Opzioni di ridimensionamento nel controllo DataGrid](../../../../docs/framework/wpf/controls/sizing-options-in-the-datagrid-control.md)|Viene descritto come controllare il ridimensionamento assoluto e automatico in <xref:System.Windows.Controls.DataGrid>.|  
  
## Vedere anche  
 <xref:System.Windows.Controls.DataGrid>   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [Controlli](../../../../docs/framework/wpf/controls/index.md)   
 [Modello di contenuto WPF](../../../../docs/framework/wpf/controls/wpf-content-model.md)