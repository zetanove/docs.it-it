---
title: "Procedura: modificare elementi di contenuto del flusso tramite la propriet&#224; Blocks | Microsoft Docs"
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
  - "Blocks (proprietà), modifica di elementi di contenuto del flusso"
  - "documenti, modifica di elementi di contenuto del flusso tramite la proprietà Blocks"
  - "elementi di contenuto del flusso, modifica tramite la proprietà Blocks"
  - "proprietà, Blocchi, modifica di elementi di contenuto del flusso"
ms.assetid: aeda4ece-b979-4818-a093-ef938e908751
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: modificare elementi di contenuto del flusso tramite la propriet&#224; Blocks
In questi esempi vengono illustrate alcune delle operazioni più comuni che è possibile eseguire sugli elementi di contenuto del flusso tramite la proprietà **Blocks**.  Questa proprietà viene utilizzata per aggiungere e rimuovere elementi dalla classe <xref:System.Windows.Documents.BlockCollection>.  Gli elementi di contenuto del flusso che presentano una proprietà **Blocks** sono:  
  
-   <xref:System.Windows.Documents.Figure>  
  
-   <xref:System.Windows.Documents.Floater>  
  
-   <xref:System.Windows.Documents.ListItem>  
  
-   <xref:System.Windows.Documents.Section>  
  
-   <xref:System.Windows.Documents.TableCell>  
  
 In questi esempi si utilizza <xref:System.Windows.Documents.Section> come elemento di contenuto del flusso, tuttavia queste tecniche sono applicabili a tutti gli elementi in cui è presente una raccolta di elementi di contenuto del flusso.  
  
## Esempio  
 Nell'esempio seguente viene creato un nuovo oggetto <xref:System.Windows.Documents.Section> e viene quindi utilizzato il metodo **Add** per aggiungere un nuovo paragrafo al contenuto della **sezione**.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksAdd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksadd)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksAdd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksadd)]  
  
## Esempio  
 Nell’esempio seguente viene creato un nuovo elemento <xref:System.Windows.Documents.Paragraph> che viene inserito all'inizio dell'elemento <xref:System.Windows.Documents.Section>.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksInsert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksinsert)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksInsert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksinsert)]  
  
## Esempio  
 Nell'esempio seguente viene indicato il numero di elementi <xref:System.Windows.Documents.Block> di primo livello contenuti in <xref:System.Windows.Documents.Section>.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksCount](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblockscount)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksCount](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblockscount)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene eliminato l'ultimo elemento <xref:System.Windows.Documents.Block> di <xref:System.Windows.Documents.Section>.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksRemoveLast](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksremovelast)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksRemoveLast](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksremovelast)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene cancellato tutto il contenuto \(gli elementi <xref:System.Windows.Documents.Block>\) dall'oggetto <xref:System.Windows.Documents.Section>.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksClear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksclear)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksClear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksclear)]  
  
## Vedere anche  
 <xref:System.Windows.Documents.BlockCollection>   
 <xref:System.Windows.Documents.InlineCollection>   
 <xref:System.Windows.Documents.ListItemCollection>   
 [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [Modificare i gruppi di righe di una tabella tramite la proprietà RowGroups](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)   
 [Modificare le colonne di una tabella tramite la proprietà Columns](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-columns-through-the-columns-property.md)   
 [Modificare i gruppi di righe di una tabella tramite la proprietà RowGroups](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)