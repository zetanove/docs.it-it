---
title: "Procedura: ottenere le celle, righe e colonne selezionate nel controllo DataGridView di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DataGridView (controllo) [Windows Form], recupero della selezione"
  - "recupero della selezione, DataGridView (controllo) [Windows Form]"
  - "selezione, DataGridView (controllo) [Windows Form]"
ms.assetid: d93c4b5b-498e-49bc-982a-2229d61778e4
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: ottenere le celle, righe e colonne selezionate nel controllo DataGridView di Windows Form
È possibile ottenere le celle, righe o colonne selezionate da un controllo <xref:System.Windows.Forms.DataGridView> mediante l'utilizzo delle proprietà corrispondenti: <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>, <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> e <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>.  Nelle procedure seguenti viene descritto come ottenere le celle selezionate e visualizzarne gli indici di riga e colonna in una classe <xref:System.Windows.Forms.MessageBox>.  
  
### Per ottenere le celle selezionate in un controllo DataGridView  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>.  
  
    > [!NOTE]
    >  Utilizzare il metodo <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A> per evitare di visualizzare una grande quantità di celle.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#10)]  
  
### Per ottenere le righe selezionate in un controllo DataGridView  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>.  Per consentire agli utenti di selezionare le righe, è necessario impostare la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode> o <xref:System.Windows.Forms.DataGridViewSelectionMode>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#20)]  
  
### Per ottenere le colonne selezionate in un controllo DataGridView  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>.  Per consentire agli utenti di selezionare le colonne, è necessario impostare la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode> o <xref:System.Windows.Forms.DataGridViewSelectionMode>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#30)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   I controlli <xref:System.Windows.Forms.Button> denominati `selectedCellsButton`, `selectedRowsButton` e `selectedColumnsButton`, ciascuno con gestori per l'evento <xref:System.Windows.Forms.Control.Click> associato.  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Windows.Forms?displayProperty=fullName> e <xref:System.Text?displayProperty=fullName>.  
  
## Programmazione efficiente  
 Le raccolte descritte in questo argomento non funzionano efficientemente quando vengono selezionate numerose celle, righe o colonne.  Per ulteriori informazioni sull'uso di queste raccolte con grandi quantità di dati, vedere [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>   
 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>   
 [Utilizzo della selezione e degli Appunti con il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)