---
title: "Procedura: bloccare le colonne nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], blocco"
  - "DataGridView (controllo) [Windows Form], colonne sempre visualizzate"
  - "DataGridView (controllo) [Windows Form], blocco di colonne"
ms.assetid: 2ef8b1de-782e-4867-af8d-58171ab5c106
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: bloccare le colonne nel controllo DataGridView di Windows Form
Quando gli utenti visualizzano i dati contenuti in un controllo <xref:System.Windows.Forms.DataGridView> Windows Form, a volte devono fare spesso riferimento a una sola colonna o a un set di colonne.  Ad esempio, quando si visualizza una tabella di informazioni sui clienti che contiene molte colonne, è utile visualizzare il nome del cliente in qualsiasi momento, anche mentre le altre colonne scorrono all'esterno dell'area visibile.  
  
 A tale scopo, è possibile bloccare le colonne nel controllo.  Quando si blocca una colonna, vengono bloccate anche tutte le colonne alla sua sinistra \(o alla sua destra, nelle lingue scritte da destra a sinistra\).  Le colonne bloccate rimangono ferme mentre tutte le altre colonne possono scorrere.  
  
> [!NOTE]
>  Se viene abilitato il riordinamento delle colonne, le colonne bloccate vengono considerate come un gruppo distinto dalle colonne non bloccate.  Gli utenti possono riposizionare le colonne in entrambi i gruppi, ma non possono spostare una colonna da un gruppo all'altro.  
  
 La proprietà <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A> di una colonna determina se la colonna è sempre visibile nella griglia.  
  
 Questa attività è supportata in Visual Studio.  Vedere anche [Procedura: Bloccare le colonne nel controllo DataGridView Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/717ss6s6\(v=vs.110\)).  
  
### Per bloccare una colonna a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=fullName> su `true`.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#061](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#061)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#061](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#061)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` contenente una colonna denominata `AddToCartButton`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView>   
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [Procedura: abilitare il riordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-enable-column-reordering-in-the-windows-forms-datagridview-control.md)