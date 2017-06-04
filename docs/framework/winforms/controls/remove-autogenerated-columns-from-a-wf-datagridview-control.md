---
title: "Procedure: rimuovere le colonne generate automaticamente da un controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], rimozione"
  - "DataGridView (controllo) [Windows Form], rimozione di colonne"
ms.assetid: 92e28d98-95a3-446c-9150-41b7c7e5be15
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedure: rimuovere le colonne generate automaticamente da un controllo DataGridView di Windows Form
Quando il controllo <xref:System.Windows.Forms.DataGridView> è impostato in modo da generare automaticamente le colonne in base ai dati provenienti dall'origine dati, è possibile omettere selettivamente alcune colonne  chiamando il metodo <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A> sulla raccolta <xref:System.Windows.Forms.DataGridView.Columns%2A>.  In alternativa, è possibile nascondere le colonne impostando la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> su `false`.  Questa tecnica risulta utile se si desidera visualizzare le colonne nascoste in condizioni particolari o se è necessario accedere ai dati presenti nelle colonne senza visualizzarli.  
  
### Per rimuovere le colonne generate automaticamente  
  
-   Chiamare il metodo <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A> sulla raccolta <xref:System.Windows.Forms.DataGridView.Columns%2A>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#111](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#111)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#111](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#111)]  
  
### Per nascondere le colonne generate automaticamente  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> della colonna su `false`.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#112](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#112)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#112](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#112)]  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#110)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#110)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` associato a una tabella contenente le colonne `Fax` e `CustomerID`, ad esempio la tabella `Customers` del database di esempio Northwind.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.Columns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A?displayProperty=fullName>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)