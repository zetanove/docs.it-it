---
title: "Procedura: abilitare il riordinamento delle colonne nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], riordino"
  - "griglie dei dati, riordinamento di colonne"
  - "DataGridView (controllo) [Windows Form], ordine di colonne"
ms.assetid: cc20eae3-e4db-493f-95ce-a4215e29472a
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: abilitare il riordinamento delle colonne nel controllo DataGridView di Windows Form
Quando si abilita il riordinamento delle colonne nel controllo <xref:System.Windows.Forms.DataGridView>, gli utenti possono spostare una colonna in una nuova posizione trascinandone l'intestazione con il mouse.  Nel controllo <xref:System.Windows.Forms.DataGridView> il valore della proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=fullName> determina se gli utenti possono spostare le colonne in posizioni diverse.  
  
 Questa attività è supportata in Visual Studio.  Vedere anche [Procedura: Bloccare le colonne nel controllo DataGridView Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/8xwtyc86\(v=vs.110\)).  
  
### Per abilitare il riordinamento delle colonne a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=fullName> su `true`.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#060](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#060)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#060](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#060)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=fullName>   
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [Procedura: bloccare le colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-freeze-columns-in-the-windows-forms-datagridview-control.md)