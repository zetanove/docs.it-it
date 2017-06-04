---
title: "Cenni preliminari sull&#39;elemento Table | Microsoft Docs"
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
  - "documenti, tabelle"
  - "contenuto dinamico (elementi) [WPF], Tabella"
  - "tabelle"
ms.assetid: 5e1105f4-8fc4-473a-ba55-88c8e71386e6
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Cenni preliminari sull&#39;elemento Table
<xref:System.Windows.Documents.Table> è un elemento a livello di blocco che supporta la presentazione basata su griglia del contenuto di documenti dinamici.  La flessibilità di questo elemento lo rende molto utile, ma al contempo ne complica la comprensione e l'utilizzo corretto.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento.  
  
-   [Introduzione all'elemento Table](#table_basics)  
  
-   [Differenze tra l'elemento Table e l'elemento Grid](#table_vs_Grid)  
  
-   [Struttura di base dell'elemento Table](#basic_table_structure)  
  
-   [Contenuto dell'elemento Table](#table_containment)  
  
-   [Raggruppamenti di righe](#row_groupings)  
  
-   [Precedenza del rendering dello sfondo](#rednering_precedence)  
  
-   [Estensione su più righe o colonne](#spanning_rows_or_columns)  
  
-   [Compilazione di un elemento Table con codice](#building_a_table_with_code)  
  
-   [Argomenti correlati](#see_also)  
  
<a name="table_basics"></a>   
## Introduzione all'elemento Table  
  
<a name="table_vs_Grid"></a>   
### Differenze tra l'elemento Table e l'elemento Grid  
 Gli elementi <xref:System.Windows.Documents.Table> e <xref:System.Windows.Controls.Grid> condividono alcune funzionalità comuni, ma ciascuno di essi si rivela più adatto per scenari diversi.  Un elemento <xref:System.Windows.Documents.Table> è progettato per l'utilizzo all'interno del contenuto di flusso \(per ulteriori informazioni sul contenuto di flusso, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)\).  Gli elementi Grid vengono utilizzati con maggior efficacia all'interno di form \(in generale all'esterno del contenuto di flusso\).  All'interno di un oggetto <xref:System.Windows.Documents.FlowDocument>, un elemento <xref:System.Windows.Documents.Table> supporta comportamenti del contenuto di flusso come impaginazione, riflusso di colonne e selezione di contenuto, a differenza di un elemento <xref:System.Windows.Controls.Grid>.  Un elemento <xref:System.Windows.Controls.Grid> viene invece utilizzato con maggior efficacia all'esterno di un oggetto <xref:System.Windows.Documents.FlowDocument> per diversi motivi, incluso il fatto che l'elemento <xref:System.Windows.Controls.Grid> aggiunge gli elementi in base a un indice di riga e di colonna, a differenza di <xref:System.Windows.Documents.Table>.  L'elemento <xref:System.Windows.Controls.Grid> consente la sovrapposizione di contenuti figlio, permettendo la presenza di più di un elemento all'interno di un'unica "cella". L'elemento <xref:System.Windows.Documents.Table> non supporta la sovrapposizione.  Gli elementi figlio di un elemento <xref:System.Windows.Controls.Grid> possono essere posizionati in modo assoluto rispetto all'area della relativa "cella".  <xref:System.Windows.Documents.Table> non supporta questa funzionalità.  Infine, poiché un elemento <xref:System.Windows.Controls.Grid> richiede un numero inferiore di risorse rispetto a <xref:System.Windows.Documents.Table>, è opportuno considerare l'utilizzo di <xref:System.Windows.Controls.Grid> per migliorare le prestazioni.  
  
<a name="basic_table_structure"></a>   
### Struttura di base dell'elemento Table  
 L'elemento <xref:System.Windows.Documents.Table> fornisce una presentazione basata su griglia costituita da colonne \(rappresentate da elementi <xref:System.Windows.Documents.TableColumn>\) e righe \(rappresentate da elementi <xref:System.Windows.Documents.TableRow>\).  Gli elementi <xref:System.Windows.Documents.TableColumn> non ospitano contenuto, ma definiscono semplicemente le colonne e le relative caratteristiche.  Gli elementi <xref:System.Windows.Documents.TableRow> devono essere ospitati in un elemento <xref:System.Windows.Documents.TableRowGroup> che definisce un raggruppamento di righe per la tabella.  Gli elementi <xref:System.Windows.Documents.TableCell>, che contengono il contenuto effettivo presentato dalla tabella, devono essere ospitati in un elemento <xref:System.Windows.Documents.TableRow>.  <xref:System.Windows.Documents.TableCell> può contenere solo elementi che derivano da <xref:System.Windows.Documents.Block>.  Tra gli elementi figlio validi per <xref:System.Windows.Documents.TableCell> sono inclusi:  
  
-   <xref:System.Windows.Documents.BlockUIContainer>  
  
-   <xref:System.Windows.Documents.List>  
  
-   <xref:System.Windows.Documents.Paragraph>  
  
-   <xref:System.Windows.Documents.Section>  
  
-   <xref:System.Windows.Documents.Table>  
  
> [!NOTE]
>  Gli elementi <xref:System.Windows.Documents.TableCell> non possono ospitare direttamente contenuto di testo.  Per ulteriori informazioni sulle regole di contenuto per gli elementi di contenuto dinamico come <xref:System.Windows.Documents.TableCell>, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md).  
  
> [!NOTE]
>  <xref:System.Windows.Documents.Table> è simile a <xref:System.Windows.Controls.Grid> ma offre maggiori funzionalità e, pertanto, richiede un sovraccarico di risorse maggiore.  
  
 Nell'esempio riportato di seguito viene definita una semplice tabella 2 x 3 con [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)].  
  
 [!code-xml[TableSnippets2#_Table_BasicLayout](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_basiclayout)]  
  
 Nella figura riportata di seguito viene illustrato il rendering di questo esempio.  
  
 ![Schermata: rendering di una tabella semplice](../../../../docs/framework/wpf/advanced/media/basictablerrender.png "BasicTablerRender")  
  
<a name="table_containment"></a>   
### Contenuto dell'elemento Table  
 <xref:System.Windows.Documents.Table> deriva dall'elemento <xref:System.Windows.Documents.Block> ed è conforme alle regole comuni per gli elementi a livello di <xref:System.Windows.Documents.Block>.  Un elemento <xref:System.Windows.Documents.Table> può essere contenuto da ognuno degli elementi riportati di seguito:  
  
-   <xref:System.Windows.Documents.FlowDocument>  
  
-   <xref:System.Windows.Documents.TableCell>  
  
-   <xref:System.Windows.Controls.ListBoxItem>  
  
-   <xref:System.Windows.Controls.ListViewItem>  
  
-   <xref:System.Windows.Documents.Section>  
  
-   <xref:System.Windows.Documents.Floater>  
  
-   <xref:System.Windows.Documents.Figure>  
  
<a name="row_groupings"></a>   
### Raggruppamenti di righe  
 L'elemento <xref:System.Windows.Documents.TableRowGroup> consente di raggruppare in modo arbitrario le righe in una tabella, ciascuna delle quali deve appartenere a un raggruppamento di righe.  Spesso, le righe appartenenti allo stesso gruppo condividono un intento comune ed è possibile utilizzare uno stile comune per il gruppo.  Un utilizzo tipico dei raggruppamenti di righe consiste nel separare le righe finalizzate a scopi specifici, ad esempio le righe di titolo, intestazione e piè di pagina, dal contenuto principale della tabella.  
  
 Nell'esempio riportato di seguito viene utilizzato [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] per definire una tabella con righe di intestazione e piè di pagina personalizzate con stili.  
  
 [!code-xml[TableSnippets2#_Table_RowGroups](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_rowgroups)]  
  
 Nella figura riportata di seguito viene illustrato il rendering di questo esempio.  
  
 ![Schermata: gruppi di righe di tabella](../../../../docs/framework/wpf/advanced/media/table-rowgroups.png "Table\_RowGroups")  
  
<a name="renderning_precedence"></a>   
### Precedenza del rendering dello sfondo  
 Il rendering di elementi Table viene eseguito nell'ordine seguente \([ordine z](GTMT) dal più basso al più alto\).  Questo ordine non può essere modificato.  Ad esempio, per questi elementi non esiste una proprietà "ordine Z" che è possibile utilizzare per l'override dell'ordine stabilito.  
  
1.  <xref:System.Windows.Documents.Table>  
  
2.  <xref:System.Windows.Documents.TableColumn>  
  
3.  <xref:System.Windows.Documents.TableRowGroup>  
  
4.  <xref:System.Windows.Documents.TableRow>  
  
5.  <xref:System.Windows.Documents.TableCell>  
  
 Nell'esempio riportato di seguito vengono definiti i colori di sfondo per ciascun elemento all'interno di una tabella.  
  
 [!code-xml[TableSnippets2#_Table_ZOrder](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_zorder)]  
  
 Nella figura riportata di seguito viene illustrato il rendering dell'esempio \(visualizzazione dei soli colori di sfondo\).  
  
 ![Schermata: ordine Z della tabella](../../../../docs/framework/wpf/advanced/media/table-zorder.png "Table\_ZOrder")  
  
<a name="spanning_rows_or_columns"></a>   
### Estensione su più righe o colonne  
 Le celle della tabella possono essere configurate per estendersi su più righe o colonne utilizzando rispettivamente gli attributi <xref:System.Windows.Documents.TableCell.RowSpan%2A> o <xref:System.Windows.Documents.TableCell.ColumnSpan%2A>.  
  
 Nell'esempio riportato di seguito una cella si estende su tre colonne.  
  
 [!code-xml[TableSnippets2#_Table_ColumnSpan](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_columnspan)]  
  
 Nella figura riportata di seguito viene illustrato il rendering di questo esempio.  
  
 ![Schermata: cella che si estende su tutte e tre colonne](../../../../docs/framework/wpf/advanced/media/table-columnspan.png "Table\_ColumnSpan")  
  
<a name="building_a_table_with_code"></a>   
## Compilazione di un elemento Table con codice  
 Negli esempi riportati di seguito viene illustrato come creare un elemento <xref:System.Windows.Documents.Table> a livello di codice e compilarlo con contenuto.  Il contenuto della tabella è ripartito in cinque righe \(rappresentate da oggetti <xref:System.Windows.Documents.TableRow> contenuti in un oggetto <xref:System.Windows.Documents.Table.RowGroups%2A>\) e sei colonne \(rappresentate da oggetti <xref:System.Windows.Documents.TableColumn>\).  Le righe vengono utilizzate per scopi di presentazione diversi, ad esempio una riga è destinata a contenere il titolo dell'intera tabella, una riga di intestazione a descrivere le colonne di dati nella tabella e una riga di piè di pagina a fornire informazioni di riepilogo.  Si noti che i concetti di righe del "titolo", "intestazione" e "piè di pagina" non sono inerenti la tabella, ma fanno semplicemente riferimento a righe con caratteristiche diverse.  Le celle della tabella ospitano il contenuto effettivo, che può essere costituito da testo, immagini o qualsiasi altro elemento [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  
  
 Viene innanzitutto creato un oggetto <xref:System.Windows.Documents.FlowDocument> per ospitare l'elemento <xref:System.Windows.Documents.Table>, quindi viene creato un nuovo elemento <xref:System.Windows.Documents.Table> e aggiunto al contenuto di <xref:System.Windows.Documents.FlowDocument>.  
  
 [!code-csharp[TableSnippets#_TableCreate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
 Successivamente, vengono creati sei oggetti <xref:System.Windows.Documents.TableColumn> e aggiunti alla raccolta <xref:System.Windows.Documents.Table.Columns%2A> della tabella, con l'applicazione di alcuni elementi di formattazione.  
  
> [!NOTE]
>  Si noti che la raccolta <xref:System.Windows.Documents.Table.Columns%2A> della tabella utilizza un'indicizzazione a base zero standard.  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
 Viene quindi creata una riga del titolo e aggiunta alla tabella con l'applicazione di alcuni elementi di formattazione.  La riga del titolo può contenere una sola cella che si estende su tutte e sei le colonne della tabella.  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
 Viene quindi creata e aggiunta alla tabella una riga di intestazione, per la quale vengono create celle in cui viene inserito contenuto.  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
 In seguito, viene creata e aggiunta alla tabella una riga per i dati, per la quale vengono create celle in cui viene inserito contenuto.  La compilazione di questa riga è simile alla compilazione della riga di intestazione, con l'applicazione di una formattazione leggermente diversa.  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
 Infine, viene creata, aggiunta e formattata una riga a piè di pagina.  Analogamente alla riga del titolo, il piè di pagina contiene una sola cella che si estende su tutte e sei colonne della tabella.  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## Vedere anche  
 [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [Definire un oggetto Table tramite XAML](../../../../docs/framework/wpf/advanced/how-to-define-a-table-with-xaml.md)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Utilizzare elementi di contenuto del flusso](../../../../docs/framework/wpf/advanced/how-to-use-flow-content-elements.md)