---
title: "Procedura: modificare i gruppi di righe di una tabella tramite la propriet&#224; RowGroups | Microsoft Docs"
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
  - "documenti, modifica di gruppi di righe tramite la proprietà RowGroups"
  - "proprietà, RowGroups, modifica di gruppi di righe"
  - "gruppi di righe, modifica tramite la proprietà RowGroups"
  - "RowGroups (proprietà), modifica di gruppi di righe"
ms.assetid: ea61440f-08ae-44ed-b314-5716aaaae3ed
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: modificare i gruppi di righe di una tabella tramite la propriet&#224; RowGroups
In questo esempio vengono illustrate alcune delle operazioni più comuni che è possibile eseguire sui gruppi di righe di una tabella tramite la proprietà <xref:System.Windows.Documents.Table.RowGroups%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creata una nuova tabella e successivamente utilizzato il metodo <xref:System.Windows.Documents.TableRowGroupCollection.Add%2A> per aggiungere colonne alla raccolta <xref:System.Windows.Documents.Table.RowGroups%2A> della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Add](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_add)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Add](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_add)]  
  
## Esempio  
 Nell'esempio seguente viene inserito un nuovo oggetto <xref:System.Windows.Documents.TableRowGroup>.  La nuova colonna viene inserita in corrispondenza della posizione di indice 0, in modo da trasformarla nel nuovo primo gruppo di righe della tabella.  
  
> [!NOTE]
>  La raccolta <xref:System.Windows.Documents.TableRowGroupCollection> utilizza l'indicizzazione a base zero standard.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Insert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_insert)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Insert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_insert)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono aggiunte diverse righe a un oggetto <xref:System.Windows.Documents.TableRowGroup> particolare \(specificato tramite l'indice\) della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_AddRows](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_addrows)]
 [!code-vb[TableSnippets2#_Table_RowGroups_AddRows](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_addrows)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene effettuato l'accesso ad alcune proprietà arbitrarie disponibili nelle righe del primo gruppo di righe della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_ManipRows](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_maniprows)]
 [!code-vb[TableSnippets2#_Table_RowGroups_ManipRows](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_maniprows)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono aggiunte diverse celle a un oggetto <xref:System.Windows.Documents.TableRow> particolare \(specificato tramite l'indice\) della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_AddCells](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_addcells)]
 [!code-vb[TableSnippets2#_Table_RowGroups_AddCells](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_addcells)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene effettuato l'accesso ad alcuni metodi e proprietà arbitrari disponibili nelle celle della prima riga del primo gruppo di righe.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_ManipCells](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_manipcells)]
 [!code-vb[TableSnippets2#_Table_RowGroups_ManipCells](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_manipcells)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene restituito il numero di elementi <xref:System.Windows.Documents.TableRowGroup> ospitati dalla tabella.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Count](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_count)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Count](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_count)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene rimosso un particolare gruppo di righe tramite riferimento.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_DelRef](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_delref)]
 [!code-vb[TableSnippets2#_Table_RowGroups_DelRef](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_delref)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene rimosso un particolare gruppo di righe tramite l'indice.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_DelIndex](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_delindex)]
 [!code-vb[TableSnippets2#_Table_RowGroups_DelIndex](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_delindex)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono rimossi tutti i gruppi di righe dalla raccolta di gruppi di righe della tabella.  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Clear](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_clear)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Clear](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_clear)]  
  
## Vedere anche  
 [How\-to: Manipulate Flow Content Elements through the Inlines Property](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)   
 [Modificare un oggetto FlowDocument tramite la proprietà Blocks](../../../../docs/framework/wpf/advanced/how-to-manipulate-a-flowdocument-through-the-blocks-property.md)   
 [Modificare le colonne di una tabella tramite la proprietà Columns](../../../../docs/framework/wpf/advanced/how-to-manipulate-table-columns-through-the-columns-property.md)