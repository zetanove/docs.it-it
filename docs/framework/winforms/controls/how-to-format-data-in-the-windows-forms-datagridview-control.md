---
title: "Procedura: formattare i dati nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "celle, allineamento testo"
  - "valori di valuta, formattazione nelle griglie di dati"
  - "dati [Windows Form], formattazione nel controllo DataGridView"
  - "griglie dei dati, valori di valuta"
  - "griglie dei dati, data (valori)"
  - "griglie dei dati, abilitazione del ritorno a capo automatico"
  - "griglie dei dati, formattazione di dati"
  - "griglie dei dati, allineamento testo"
  - "DataGridView (controllo) [Windows Form], formattazione di dati"
ms.assetid: 8c33543c-9c08-4636-a65a-fdf714a529b7
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: formattare i dati nel controllo DataGridView di Windows Form
Nelle procedure riportate di seguito vengono illustrate le operazioni di formattazione di base dei valori delle celle mediante la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> di un controllo <xref:System.Windows.Forms.DataGridView> e di colonne specifiche di un controllo.  Per informazioni sulla formattazione avanzata dei dati, vedere [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md).  
  
### Per formattare valori di valuta e di data  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>.  Nell'esempio di codice riportato di seguito viene impostato il formato di colonne specifiche utilizzando la proprietà <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> delle colonne.  I valori nella colonna  `UnitPrice`  verranno visualizzati nel formato di valuta specifico delle impostazioni cultura correnti, con i valori negativi riportati tra parentesi.  I valori nella colonna  `ShipDate`  verranno visualizzati nel formato di data breve specifico delle impostazioni cultura correnti.  Per ulteriori informazioni sui valori della proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A>, vedere [Formattazione di tipi](../../../../docs/standard/base-types/formatting-types.md).  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#071](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#071)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#071](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#071)]  
  
### Per personalizzare la visualizzazione dei valori Null del database  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>.  Nell'esempio di codice riportato di seguito viene utilizzata la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> per indicare l'assenza di dati in tutte le celle contenenti valori uguali a <xref:System.DBNull.Value?displayProperty=fullName>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#073](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#073)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#073](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#073)]  
  
### Per attivare il ritorno a capo automatico nelle celle contenenti testo  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> su uno dei valori dell'enumerazione <xref:System.Windows.Forms.DataGridViewTriState>.  Nell'esempio di codice riportato di seguito viene utilizzata la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> per impostare la modalità di ritorno a capo automatico per tutto il controllo.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#074](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#074)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#074](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#074)]  
  
### Per specificare l'allineamento del testo delle celle di un DataGridView  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> su uno dei valori di enumerazione <xref:System.Windows.Forms.DataGridViewContentAlignment>.  Nell'esempio di codice riportato di seguito viene impostato l'allineamento di una colonna specifica utilizzando la proprietà <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> della colonna.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#072](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#072)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#072](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#072)]  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#070](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#070)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#070](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#070)]  
  
## Compilazione del codice  
 Requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` contenente la colonna `UnitPrice`, la colonna `ShipDate` e la colonna `CustomerName`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Programmazione efficiente  
 A fini di scalabilità è consigliabile che gli oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> vengano condivisi da più righe, colonne o celle che utilizzano lo stesso stile anziché impostare le proprietà di stile separatamente per ciascun elemento.  Per ulteriori informazioni, vedere [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Formattazione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)   
 [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)   
 [Formattazione di tipi](../../../../docs/standard/base-types/formatting-types.md)