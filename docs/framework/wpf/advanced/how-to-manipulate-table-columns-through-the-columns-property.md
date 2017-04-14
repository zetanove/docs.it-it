---
title: "Procedura: modificare le colonne di una tabella tramite la propriet&#224; Columns | Microsoft Docs"
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
  - "Columns (proprietà)"
  - "documenti, modifica di colonne di tabella"
  - "proprietà, Colonne, modifica di colonne di tabella"
  - "tabelle, modifica di colonne"
ms.assetid: 3f8884f4-7e1f-456b-be06-fbd3cf469bf3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: modificare le colonne di una tabella tramite la propriet&#224; Columns
In questo esempio vengono illustrate alcune delle operazioni più comuni che è possibile eseguire sulle colonne di una tabella tramite la proprietà <xref:System.Windows.Documents.Table.Columns%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creata una nuova tabella e successivamente utilizzato il metodo <xref:System.Windows.Documents.TableColumnCollection.Add%2A> per aggiungere colonne alla raccolta <xref:System.Windows.Documents.Table.Columns%2A> della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Add](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_add)]
 [!code-vb[TableSnippets2#_Table_Columns_Add](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_add)]  
  
## Esempio  
 Nell'esempio seguente viene inserito un nuovo oggetto <xref:System.Windows.Documents.TableColumn>.  La nuova colonna viene inserita in corrispondenza della posizione di indice 0, rendendola così la prima colonna della tabella.  
  
> [!NOTE]
>  La raccolta <xref:System.Windows.Documents.TableColumnCollection> utilizza l'indicizzazione in base zero standard.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Insert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_insert)]
 [!code-vb[TableSnippets2#_Table_Columns_Insert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_insert)]  
  
## Esempio  
 Nell'esempio riportato di seguito si accede ad alcune proprietà arbitrarie sulle colonne nella raccolta <xref:System.Windows.Documents.TableColumnCollection>, con riferimento a particolari colonne tramite l'indice.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Manip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_manip)]
 [!code-vb[TableSnippets2#_Table_Columns_Manip](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_manip)]  
  
## Esempio  
 Nell'esempio riportato di seguito si ottiene il numero di colonne attualmente ospitate dalla tabella.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Count](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_count)]
 [!code-vb[TableSnippets2#_Table_Columns_Count](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_count)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene rimossa una colonna tramite riferimento.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_DelRef](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_delref)]
 [!code-vb[TableSnippets2#_Table_Columns_DelRef](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_delref)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene rimossa una colonna tramite indice.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_DelIndex](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_delindex)]
 [!code-vb[TableSnippets2#_Table_Columns_DelIndex](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_delindex)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono rimosse tutte le colonne dalla raccolta di colonne della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Clear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_clear)]
 [!code-vb[TableSnippets2#_Table_Columns_Clear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_clear)]  
  
## Vedere anche  
 [Cenni preliminari sull'elemento Table](../../../../docs/framework/wpf/advanced/table-overview.md)   
 [Definire un oggetto Table tramite XAML](../../../../docs/framework/wpf/advanced/how-to-define-a-table-with-xaml.md)   
 [Compilare oggetti Table a livello di codice](../../../../docs/framework/wpf/advanced/how-to-build-a-table-programmatically.md)   
 [Modificare i gruppi di righe di una tabella tramite la proprietà RowGroups](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)   
 [Modificare un oggetto FlowDocument tramite la proprietà Blocks](../../../../docs/framework/wpf/advanced/how-to-manipulate-a-flowdocument-through-the-blocks-property.md)   
 [Modificare i gruppi di righe di una tabella tramite la proprietà RowGroups](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)