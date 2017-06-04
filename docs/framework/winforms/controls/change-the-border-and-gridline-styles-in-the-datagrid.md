---
title: "Procedura: modificare gli stili dei bordi e delle linee della griglia nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, modifica degli stili dei bordi"
  - "griglie dei dati, modifica degli stili delle linee della griglia"
  - "DataGridView (controllo) [Windows Form], stili dei bordi"
  - "DataGridView (controllo) [Windows Form], stili delle linee della griglia"
  - "linee della griglia, modifica degli stili"
ms.assetid: 2f413c7a-4025-4171-8e3a-66ef908ea583
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: modificare gli stili dei bordi e delle linee della griglia nel controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> consente di personalizzare l'aspetto dei bordi e delle linee della griglia del controllo per migliorare l'interazione degli utenti.  È possibile modificare il colore delle linee della griglia e lo stile del bordo del controllo oltre agli stili dei bordi delle celle all'interno del controllo.  È inoltre possibile applicare stili dei bordi diversi alle celle normali e alle celle di intestazione di riga e di colonna.  
  
> [!NOTE]
>  Il colore delle linee della griglia viene utilizzato solo con i valori <xref:System.Windows.Forms.DataGridViewCellBorderStyle>, <xref:System.Windows.Forms.DataGridViewCellBorderStyle> e <xref:System.Windows.Forms.DataGridViewCellBorderStyle> dell'enumerazione <xref:System.Windows.Forms.DataGridViewCellBorderStyle> e il valore <xref:System.Windows.Forms.DataGridViewHeaderBorderStyle> dell'enumerazione <xref:System.Windows.Forms.DataGridViewHeaderBorderStyle>.  Gli altri valori delle enumerazioni utilizzano colori specificati dal sistema operativo.  Inoltre, se gli stili visivi sono attivati in Windows XP e nei sistemi della famiglia Windows Server 2003 mediante il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName>, il valore della proprietà <xref:System.Windows.Forms.DataGridView.GridColor%2A> non viene utilizzato.  
  
### Per modificare il colore delle linee della griglia a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.GridColor%2A>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#031](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#031)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#031](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#031)]  
  
### Per modificare lo stile dei bordi dell'intero controllo DataGridView a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.BorderStyle%2A> su uno dei valori dell'enumerazione <xref:System.Windows.Forms.BorderStyle>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#032](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#032)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#032](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#032)]  
  
### Per modificare gli stili dei bordi delle celle di DataGridView a livello di codice  
  
-   Impostare le proprietà <xref:System.Windows.Forms.DataGridView.CellBorderStyle%2A>, <xref:System.Windows.Forms.DataGridView.RowHeadersBorderStyle%2A> e <xref:System.Windows.Forms.DataGridView.ColumnHeadersBorderStyle%2A>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#033](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#033)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#033](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#033)]  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#030](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#030)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#030](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#030)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Windows.Forms?displayProperty=fullName> e <xref:System.Drawing?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.BorderStyle>   
 <xref:System.Windows.Forms.DataGridView.BorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellBorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersBorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.GridColor%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersBorderStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellBorderStyle>   
 <xref:System.Windows.Forms.DataGridViewHeaderBorderStyle>   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)