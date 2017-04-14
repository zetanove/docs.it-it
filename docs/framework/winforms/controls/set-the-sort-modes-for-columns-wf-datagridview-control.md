---
title: "Procedura: impostare le modalit&#224; di ordinamento delle colonne nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, ordinamento dei dati"
  - "DataGridView (controllo) [Windows Form], modalità di ordinamento"
  - "ordinamento, griglie dei dati"
ms.assetid: 57dfed60-a608-40d5-86f9-d65686ffb325
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare le modalit&#224; di ordinamento delle colonne nel controllo DataGridView di Windows Form
Nel controllo <xref:System.Windows.Forms.DataGridView>, per impostazione predefinita, per le colonne di caselle di testo viene utilizzato l'ordinamento automatico mentre gli altri tipi di colonna non vengono ordinati automaticamente.  Talvolta potrebbe essere preferibile ignorare tali impostazioni predefinite.  Ad esempio, se si visualizzano immagini anziché testo, numeri o valori di celle di enumerazione,  sebbene non sia possibile ordinare le immagini, è possibile eseguire l'ordinamento in base ai valori sottostanti rappresentati dalle immagini.  
  
 Nel controllo <xref:System.Windows.Forms.DataGridView> il valore della proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> di una colonna determina la relativa modalità di ordinamento.  
  
 Nella procedura riportata di seguito viene utilizzata la colonna `Priority` creata in [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md) che è di tipo image e per impostazione predefinita non può essere ordinata.  Tuttavia, poiché i valori effettivi delle celle sono stringhe, può essere ordinata automaticamente.  
  
### Per impostare la modalità di ordinamento per una colonna  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=fullName>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#066](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#066)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#066](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#066)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` contenente una colonna denominata `Priority`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=fullName>   
 [Ordinamento dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)   
 [Modalità di ordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-sort-modes-in-the-windows-forms-datagridview-control.md)   
 [Procedura: personalizzare l'ordinamento nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)