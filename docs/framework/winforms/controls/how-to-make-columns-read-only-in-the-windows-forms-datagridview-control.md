---
title: "Procedura: impostare le colonne come in sola lettura nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, colonne di sola lettura"
  - "DataGridView (controllo) [Windows Form], colonne di sola lettura"
ms.assetid: 2bb73ebb-1a55-4362-9fda-e50574c087d5
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: impostare le colonne come in sola lettura nel controllo DataGridView di Windows Form
Non tutti i dati sono concepiti per la modifica.  Nel controllo <xref:System.Windows.Forms.DataGridView>, il valore della proprietà <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A> di una colonna determina se gli utenti possono modificare le celle di tale colonna.  Per informazioni su come impostare il controllo come di sola lettura, vedere [Procedura: impedire l'aggiunta o l'eliminazione di righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md).  
  
 Questa attività è supportata in Visual Studio.  Vedere anche [Procedura: Rendere le colonne di sola lettura nel controllo DataGridView Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/xd4k3c7e\(v=vs.110\)).  
  
### Per impostare una colonna come di sola lettura a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A?displayProperty=fullName> su `true`.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#064](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#064)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#064](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#064)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un oggetto <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` con una colonna denominata `CompanyName`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.Columns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A?displayProperty=fullName>   
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [Procedura: impedire l'aggiunta o l'eliminazione di righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md)