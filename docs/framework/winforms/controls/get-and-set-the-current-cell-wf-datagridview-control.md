---
title: "Procedura: ottenere e impostare la cella corrente nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "celle, recupero e impostazione della cella corrente"
  - "DataGridView (controllo) [Windows Form], recupero della cella corrente"
  - "DataGridView (controllo) [Windows Form], impostazione della cella corrente"
ms.assetid: b0e41e57-493a-4bd0-9376-a6f76723540c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ottenere e impostare la cella corrente nel controllo DataGridView di Windows Form
L'interazione con il controllo <xref:System.Windows.Forms.DataGridView> spesso richiede il rilevamento a livello di codice della cella attiva.  Potrebbe inoltre essere necessario modificare la cella corrente.  La proprietà <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> consente di eseguire queste attività.  
  
> [!NOTE]
>  Non è possibile impostare la cella corrente in una riga o una colonna con la proprietà <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> impostata su `false`.  
  
 A seconda della modalità di selezione del controllo <xref:System.Windows.Forms.DataGridView>, la modifica della cella corrente può modificare la selezione.  Per ulteriori informazioni, vedere [Modalità di selezione nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md).  
  
### Per ottenere la cella corrente a livello di codice  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> del controllo <xref:System.Windows.Forms.DataGridView>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#080](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#080)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#080](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#080)]  
  
### Per impostare la cella corrente a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> del controllo <xref:System.Windows.Forms.DataGridView>.  Nell'esempio di codice seguente la cella corrente è impostata sulla riga 0 e sulla colonna 1.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#085](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#085)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#085](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#085)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Controlli <xref:System.Windows.Forms.Button> denominati `getCurrentCellButton` e `setCurrentCellButton`.  In [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] è necessario aggiungere gli eventi <xref:System.Windows.Forms.Control.Click> per ciascun pulsante al gestore eventi associato nel codice di esempio.  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.CurrentCell%2A?displayProperty=fullName>   
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [Modalità di selezione nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)