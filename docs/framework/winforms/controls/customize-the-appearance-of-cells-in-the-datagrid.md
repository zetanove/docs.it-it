---
title: "Procedura: personalizzare l&#39;aspetto delle celle nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "celle, personalizzazione nel controllo DataGridView"
  - "griglie dei dati, personalizzazione di celle"
  - "DataGridView (controllo) [Windows Form], personalizzazione di celle"
ms.assetid: 478b20c9-625c-4116-9c5c-5a16e6f4ec67
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: personalizzare l&#39;aspetto delle celle nel controllo DataGridView di Windows Form
È possibile personalizzare l'aspetto di qualsiasi cella gestendo l'evento <xref:System.Windows.Forms.DataGridView.CellPainting> del controllo <xref:System.Windows.Forms.DataGridView>.  È possibile estrarre la classe <xref:System.Drawing.Graphics> del controllo <xref:System.Windows.Forms.DataGridView>dalla proprietà <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs.Graphics%2A> di <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs>.  Mediante <xref:System.Drawing.Graphics> è possibile modificare l'aspetto dell'intero controllo <xref:System.Windows.Forms.DataGridView>, ma in genere si desidera modificare solo l'aspetto della cella attualmente disegnata.  La proprietà <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs.ClipBounds%2A> di <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs> consente di limitare le operazioni di disegno alla cella corrente.  
  
 Nell'esempio di codice riportato di seguito vengono disegnate tutte le celle nella colonna `ContactName` utilizzando la combinazione di colori del controllo <xref:System.Windows.Forms.DataGridView>.  Per il testo contenuto in ogni cella viene utilizzato il colore <xref:System.Drawing.Color.Crimson%2A> e viene disegnato un rettangolo interno nel colore specificato nella proprietà <xref:System.Windows.Forms.DataGridView.GridColor%2A> del controllo <xref:System.Windows.Forms.DataGridView>.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewCellPainting#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCellPainting/CS/form1.cs#10)]
 [!code-vb[System.Windows.Forms.DataGridViewCellPainting#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCellPainting/VB/form1.vb#10)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` con una colonna `ContactName` come quella della tabella Customers del database di esempio Northwind.  
  
-   Riferimenti agli assembly System, System.Windows.Forms e System.Drawing.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.CellPainting>   
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)