---
title: "Procedura: impostare la modalit&#224; di selezione del controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, modalità di selezione"
  - "DataGridView (controllo) [Windows Form], modalità di selezione"
  - "selezione, modalità nel controllo DataGridView"
ms.assetid: 2f241643-7f82-4583-8757-03494f63b465
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: impostare la modalit&#224; di selezione del controllo DataGridView di Windows Form
Nell'esempio di codice riportato di seguito viene illustrato come configurare un controllo <xref:System.Windows.Forms.DataGridView> in modo che, quando si fa clic in qualsiasi punto all'interno di una riga, venga automaticamente selezionata tutta la riga e sia possibile selezionare solo una riga alla volta.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#065](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#065)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#065](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#065)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>   
 <xref:System.Windows.Forms.DataGridViewSelectionMode>   
 [Utilizzo della selezione e degli Appunti con il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)   
 [Modalità di selezione nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)