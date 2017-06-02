---
title: "Procedura: compilare oggetti Table a livello di codice | Microsoft Docs"
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
  - "creazione, tabelle (a livello di codice)"
  - "documenti, creazione di tabelle a livello di codice"
  - "tabelle, creazione a livello di codice"
ms.assetid: e3ca88f3-6e94-4b61-82fc-42104c10b761
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: compilare oggetti Table a livello di codice
Negli esempi riportati di seguito viene illustrato come creare un elemento <xref:System.Windows.Documents.Table> a livello di codice e compilarlo con contenuto.  Il contenuto della tabella è ripartito in cinque righe \(rappresentate da oggetti <xref:System.Windows.Documents.TableRow> contenuti in un oggetto <xref:System.Windows.Documents.Table.RowGroups%2A>\) e sei colonne \(rappresentate da oggetti <xref:System.Windows.Documents.TableColumn>\).  Le righe vengono utilizzate per scopi di presentazione diversi, ad esempio una riga è destinata a contenere il titolo dell'intera tabella, una riga di intestazione a descrivere le colonne di dati nella tabella e una riga di piè di pagina a fornire informazioni di riepilogo.  Si noti che i concetti di righe del "titolo", "intestazione" e "piè di pagina" non sono inerenti la tabella, ma fanno semplicemente riferimento a righe con caratteristiche diverse.  Le celle della tabella ospitano il contenuto effettivo, che può essere costituito da testo, immagini o qualsiasi altro elemento [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  
  
## Esempio  
 Viene innanzitutto creato un oggetto <xref:System.Windows.Documents.FlowDocument> per ospitare l'elemento <xref:System.Windows.Documents.Table>, quindi viene creato un nuovo elemento <xref:System.Windows.Documents.Table> e aggiunto al contenuto di <xref:System.Windows.Documents.FlowDocument>.  
  
 [!code-csharp[TableSnippets#_TableCreate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
## Esempio  
 Successivamente, vengono creati sei oggetti <xref:System.Windows.Documents.TableColumn> e aggiunti alla raccolta <xref:System.Windows.Documents.Table.Columns%2A> della tabella, con l'applicazione di alcuni elementi di formattazione.  
  
> [!NOTE]
>  Si noti che la raccolta <xref:System.Windows.Documents.Table.Columns%2A> della tabella utilizza un'indicizzazione a base zero standard.  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
## Esempio  
 Viene quindi creata una riga del titolo e aggiunta alla tabella con l'applicazione di alcuni elementi di formattazione.  La riga del titolo può contenere una sola cella che si estende su tutte e sei le colonne della tabella.  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
## Esempio  
 Viene quindi creata e aggiunta alla tabella una riga di intestazione, per la quale vengono create celle in cui viene inserito contenuto.  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
## Esempio  
 In seguito, viene creata e aggiunta alla tabella una riga per i dati, per la quale vengono create celle in cui viene inserito contenuto.  La compilazione di questa riga è simile alla compilazione della riga di intestazione, con l'applicazione di una formattazione leggermente diversa.  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
## Esempio  
 Infine, viene creata, aggiunta e formattata una riga a piè di pagina.  Analogamente alla riga del titolo, il piè di pagina contiene una sola cella che si estende su tutte e sei colonne della tabella.  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## Vedere anche  
 [Cenni preliminari sull'elemento Table](../../../../docs/framework/wpf/advanced/table-overview.md)