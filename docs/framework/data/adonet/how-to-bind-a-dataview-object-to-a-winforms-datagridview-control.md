---
title: "Procedura: associare un oggetto DataView a un controllo DataGridView di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b73d60a-6049-446a-85a7-3e5a68b183e2
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: associare un oggetto DataView a un controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> fornisce un sistema efficiente e flessibile per visualizzare i dati in formato tabulare.  Il controllo <xref:System.Windows.Forms.DataGridView> supporta il modello di associazione dati standard di Windows Form ed è quindi possibile associarlo a <xref:System.Data.DataView> e a varie altre origini dati.  Nella maggior parte dei casi, tuttavia, l'associazione viene eseguita a un componente <xref:System.Windows.Forms.BindingSource>, che gestisce i dettagli dell'interazione con l'origine dati.  
  
 Per altre informazioni sul controllo <xref:System.Windows.Forms.DataGridView>, vedere [Cenni preliminari sul controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md).  
  
### Per connettere un controllo DataGridView a un oggetto DataView  
  
1.  Implementare un metodo per gestire i dettagli del recupero di dati da un database.  Nell'esempio di codice seguente viene implementato un metodo `GetData` che inizializza un componente <xref:System.Data.SqlClient.SqlDataAdapter> e lo usa per compilare <xref:System.Data.DataSet>.  Assicurarsi di impostare la variabile `connectionString` su un valore appropriato per il database.  Sarà necessario disporre di accesso a un server in cui sia installato il database SQL Server di esempio AdventureWorks.  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1getdata)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1getdata)]  
  
2.  Nel gestore eventi <xref:System.Windows.Forms.Form.Load> del form associare il controllo <xref:System.Windows.Forms.DataGridView> al componente <xref:System.Windows.Forms.BindingSource> e chiamare il metodo `GetData` per recuperare i dati dal database.  L'oggetto <xref:System.Data.DataView> viene creato da una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] sull'oggetto <xref:System.Data.DataTable> Contact e viene quindi associato al componente <xref:System.Windows.Forms.BindingSource>.  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1formload)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1formload)]  
  
## Vedere anche  
 [Associazione dati e LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)