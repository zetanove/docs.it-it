---
title: "Procedura: modificare l&#39;ordine delle colonne nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], modifica dell'ordine"
  - "griglie dei dati, modifica dell'ordine delle colonne"
  - "DataGridView (controllo) [Windows Form], ordine di colonne"
ms.assetid: 5e9ac3bc-b0f0-48cb-a3d5-b005af905395
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: modificare l&#39;ordine delle colonne nel controllo DataGridView di Windows Form
Quando si usa <xref:System.Windows.Forms.DataGridView> per visualizzare i dati di un'origine dati, a volte le colonne nello schema dell'origine dati non appaiono nell'ordine desiderato.  È possibile modificare l'ordine di visualizzazione delle colonne usando la proprietà <xref:System.Windows.Forms.DataGridViewColumn.DisplayIndex%2A> della classe <xref:System.Windows.Forms.DataGridViewColumn>.  
  
 L'esempio di codice seguente riposiziona alcune colonne generate automaticamente durante il binding alla tabella Customers nel database di esempio Northwind.  Per altre informazioni su come associare il controllo <xref:System.Windows.Forms.DataGridView> a una tabella di un database, vedere [Procedura: associare dati al controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md).  
  
 Questa attività è supportata in Visual Studio.  Vedere anche [Procedura: Modificare l'ordine delle colonne nel controllo DataGridView Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/hb1dk7ax\(v=vs.110\)).  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#040](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#040)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#040](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#040)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `customersDataGridView` associato a una tabella con indicati i nomi di colonna, ad esempio la tabella `Customers` nel database di esempio Northwind.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Windows.Forms?displayProperty=fullName>, <xref:System.Data?displayProperty=fullName> e <xref:System.Xml?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 <xref:System.Windows.Forms.DataGridViewColumn.DisplayIndex%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A?displayProperty=fullName>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: associare dati al controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md)