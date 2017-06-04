---
title: "Procedura: aggiungere descrizioni comandi a singole celle in un controllo DataGridView di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "griglie dei dati, aggiunta di descrizioni comandi"
  - "DataGridView (controllo) [Windows Form], aggiunta di descrizioni comandi"
  - "descrizioni comandi [Windows Form], aggiunta alle griglie di dati"
ms.assetid: 2a81f9de-d58b-4ea8-bc0b-8d93c2f4cf78
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: aggiungere descrizioni comandi a singole celle in un controllo DataGridView di Windows Form
Per impostazione predefinita, per visualizzare i valori delle celle di un controllo <xref:System.Windows.Forms.DataGridView> che sono troppo piccole per consentire la visualizzazione di tutto il contenuto, vengono utilizzate descrizioni comandi.   È tuttavia possibile eseguire l'override di questo comportamento e impostare valori di testo di descrizione comandi per le singole celle.  Ciò risulta utile per visualizzare ulteriori informazioni sulla cella o per fornire agli utenti una descrizione alternativa del contenuto della cella.  Se ad esempio una riga visualizza icone di stato, è possibile fornire descrizioni testuali tramite la funzionalità descritta.  
  
 È inoltre possibile disabilitare la visualizzazione delle descrizioni comandi a livello di cella impostando la proprietà <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A?displayProperty=fullName> su `false`.  
  
### Per aggiungere una descrizione comandi a una cella  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A?displayProperty=fullName>.  
  
     [!code-cpp[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/cpp/datagridviewcell.tooltiptext.cpp#1)]
     [!code-csharp[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/CS/datagridviewcell.tooltiptext.cs#1)]
     [!code-vb[System.Windows.Forms.DataGridViewCell.ToolTipText#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCell.ToolTipText/VB/datagridviewcell.tooltiptext.vb#1)]  
  
## Compilazione del codice  
  
-   L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1` contenente una colonna denominata `Rating` per la visualizzazione di valori di stringa contenenti da uno a quattro simboli asterisco \("\*"\).  L'evento <xref:System.Windows.Forms.DataGridView.CellFormatting> del controllo deve essere associato al metodo del gestore eventi mostrato nell'esempio.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Programmazione efficiente  
 Quando si associa il controllo <xref:System.Windows.Forms.DataGridView> a un'origine dati esterna o si fornisce una propria origine dati implementando la modalità virtuale, è possibile che si verifichino problemi di prestazioni.  Per evitare cali di prestazioni quando si utilizzano grandi quantità di dati, gestire l'evento <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded> anziché impostare la proprietà <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> di più celle.  Quando si gestisce l'evento, il recupero del valore della proprietà <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> di una cella genera l'evento e restituisce il valore della proprietà <xref:System.Windows.Forms.DataGridViewCellToolTipTextNeededEventArgs.ToolTipText%2A?displayProperty=fullName> come specificato nel gestore eventi.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell>   
 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A?displayProperty=fullName>   
 [Programmazione con celle, righe e colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/programming-with-cells-rows-and-columns-in-the-datagrid.md)