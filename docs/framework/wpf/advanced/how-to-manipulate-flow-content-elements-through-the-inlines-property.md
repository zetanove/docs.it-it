---
title: "Procedura: modificare elementi di contenuto del flusso tramite la propriet&#224; Inlines | Microsoft Docs"
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
  - "documenti, modifica di elementi di contenuto del flusso tramite la proprietà Inlines"
  - "elementi di contenuto del flusso, modifica tramite la proprietà Inlines"
  - "Inlines (proprietà), modifica di elementi di contenuto del flusso"
  - "proprietà, Inlines, modifica di elementi di contenuto del flusso"
ms.assetid: 510780d2-3da1-4360-8763-7054bda22ea3
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: modificare elementi di contenuto del flusso tramite la propriet&#224; Inlines
In questi esempi vengono illustrate alcune delle operazioni più comuni che è possibile eseguire sugli elementi di contenuto del flusso inline e sui contenitori di tali elementi, ad esempio <xref:System.Windows.Controls.TextBlock>, tramite la proprietà **Inlines**.  Questa proprietà viene utilizzata per aggiungere e rimuovere elementi da <xref:System.Windows.Documents.InlineCollection>.  Tra gli elementi di contenuto del flusso che presentano una proprietà **Inlines** sono inclusi:  
  
-   <xref:System.Windows.Documents.Bold>  
  
-   <xref:System.Windows.Documents.Hyperlink>  
  
-   <xref:System.Windows.Documents.Italic>  
  
-   <xref:System.Windows.Documents.Paragraph>  
  
-   <xref:System.Windows.Documents.Span>  
  
-   <xref:System.Windows.Documents.Underline>  
  
 In questi esempi viene utilizzato l'oggetto <xref:System.Windows.Documents.Span> come elemento di contenuto del flusso, ma queste tecniche sono applicabili a tutti gli elementi o controlli che ospitano una raccolta <xref:System.Windows.Documents.InlineCollection>.  
  
## Esempio  
 Nell'esempio seguente viene creato un nuovo oggetto <xref:System.Windows.Documents.Span>, quindi viene utilizzato il metodo **Add** per aggiungere due sequenze di testo come elementi figlio di contenuto di <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
## Esempio  
 Nell'esempio seguente viene creato un nuovo elemento <xref:System.Windows.Documents.Run> che viene inserito all'inizio dell'oggetto <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
## Esempio  
 Nell'esempio seguente viene ottenuto il numero di elementi <xref:System.Windows.Documents.Inline> di livello superiore contenuti in <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesCount](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinescount)]
 [!code-vb[SpanSnippets#_SpanInlinesCount](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinescount)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene eliminato l'ultimo elemento <xref:System.Windows.Documents.Inline> di <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene cancellato tutto il contenuto \(gli elementi <xref:System.Windows.Documents.Inline>\) dall'oggetto <xref:System.Windows.Documents.Span>.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
## Vedere anche  
 <xref:System.Windows.Documents.BlockCollection>   
 <xref:System.Windows.Documents.InlineCollection>   
 <xref:System.Windows.Documents.ListItemCollection>   
 [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [Modificare un oggetto FlowDocument tramite la proprietà Blocks](../../../../docs/framework/wpf/advanced/how-to-manipulate-a-flowdocument-through-the-blocks-property.md)   
 [Modificare le colonne di una tabella tramite la proprietà Columns](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-columns-through-the-columns-property.md)   
 [Modificare i gruppi di righe di una tabella tramite la proprietà RowGroups](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)