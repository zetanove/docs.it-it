---
title: "Modo virtuale nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "DataGridView (controllo) [Windows Form], modalità virtuale"
ms.assetid: feae5d43-2848-4b1a-8ea7-77085dc415b5
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Modo virtuale nel controllo DataGridView di Windows Form
La modalità virtuale consente di gestire l'interazione tra il controllo <xref:System.Windows.Forms.DataGridView> e una cache di dati personalizzata.  Per implementare la modalità virtuale, impostare la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> su `true` e gestire uno o più eventi tra quelli descritti in questo argomento.  In genere è necessario gestire almeno l'evento `CellValueNeeded`, che consente al controllo di cercare i valori nella cache dei dati.  
  
## Modalità associata e modalità virtuale  
 La modalità virtuale è necessaria solo quando si deve integrare o sostituire la modalità associata.  Nella modalità associata impostare la proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A>. Il controllo caricherà automaticamente i dati dall'origine specificata e vi invierà le modifiche dell'utente.  È possibile controllare quali colonne associate vengono visualizzate. Normalmente è l'origine di dati che gestisce le operazioni quale l'ordinamento.  
  
## Integrazione della modalità associata  
 È possibile integrare la modalità associata mediante la visualizzazione di colonne non associate insieme alle colonne associate.  A volte questa modalità è detta "modalità mista" ed è utile per visualizzare, ad esempio, i valori calcolati o i controlli dell'interfaccia utente.  
  
 Poiché le colonne non associate non rientrano nell'origine di dati, vengono ignorate dalle operazioni di ordinamento di quest'ultima.  Pertanto, quando si attiva l'ordinamento nella modalità mista, è necessario gestire i dati non associati in una cache locale e implementare la modalità virtuale per consentire al controllo <xref:System.Windows.Forms.DataGridView> di interagire con essi.  
  
 Per ulteriori informazioni su come utilizzare la modalità virtuale per mantenere i valori nelle colonne non associate, vedere gli esempi nella proprietà <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A?displayProperty=fullName> e gli argomenti di riferimento della classe <xref:System.Windows.Forms.DataGridViewComboBoxColumn?displayProperty=fullName>.  
  
## Sostituzione della modalità associata  
 Se la modalità associata non soddisfa le esigenze a livello di prestazioni, è possibile gestire tutti i dati in una cache personalizzata tramite i gestori evento in modalità virtuale.  Ad esempio, è possibile utilizzare la modalità virtuale per implementare un meccanismo di caricamento dati JIT che recuperi solo i dati di un database in rete che sono necessari per ottenere prestazioni ottimali.  Questo scenario è particolarmente utile quando si usano grandi quantità di dati su una connessione di rete lenta o computer client che dispongono di una quantità limitata di RAM o spazio di archiviazione.  
  
 Per ulteriori informazioni sull'utilizzo della modalità virtuale in uno scenario JIT, vedere [Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md).  
  
## Eventi in modalità virtuale  
 Se si tratta di dati in sola lettura, è possibile che l'evento `CellValueNeeded` sia l'unico a dover essere gestito.  Altri eventi in modalità virtuale consentono di attivare funzionalità specifiche, quali le modifiche da parte dell'utente, l'aggiunta e l'eliminazione di righe e le transazioni a livello di riga.  
  
 Alcuni eventi <xref:System.Windows.Forms.DataGridView> standard \(ad esempio, gli eventi che si verificano quando gli utenti aggiungono o eliminano righe o quando i valori delle celle vengono modificati, analizzati, convalidati o formattati\) sono utili anche nella modalità virtuale.  È inoltre possibile gestire gli eventi che consentono di mantenere i valori che normalmente non sono archiviati in un'origine dati associata, quali il testo di descrizione comandi delle celle, il testo di errore delle celle e delle righe, i dati dei menu di scelta rapida delle celle e delle righe e i dati di altezza delle righe.  
  
 Per ulteriori informazioni sull'implementazione della modalità virtuale per la gestione dei dati di lettura\/scrittura con un ambito di commit a livello di riga, vedere [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
 Per un esempio di implementazione della modalità virtuale con un ambito di commit a livello di cella, vedere l'argomento di riferimento della proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>.  
  
 Gli eventi seguenti si verificano solo quando la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `true`.  
  
|Evento|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Forms.DataGridView.CellValueNeeded>|Utilizzato dal controllo per recuperare un valore di cella dalla cache di dati per la visualizzazione.  Questo evento si verifica solo per le celle nelle colonne non associate.|  
|<xref:System.Windows.Forms.DataGridView.CellValuePushed>|Utilizzato dal controllo per applicare l'input dell'utente per una cella alla cache di dati.  Questo evento si verifica solo per le celle nelle colonne non associate.<br /><br /> Richiamare il metodo <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> quando si modifica un valore memorizzato nella cache al di fuori di un gestore dell'evento <xref:System.Windows.Forms.DataGridView.CellValuePushed> per garantire che il valore corrente sia visualizzato nel controllo e per applicare qualsiasi modalità di dimensionamento automatico attualmente in vigore.|  
|<xref:System.Windows.Forms.DataGridView.NewRowNeeded>|Utilizzato dal controllo per indicare l'esigenza di una nuova riga nella cache di dati.|  
|<xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>|Utilizzato dal controllo per determinare se una riga contiene modifiche non applicate.|  
|<xref:System.Windows.Forms.DataGridView.CancelRowEdit>|Utilizzato dal controllo per indicare che devono essere ripristinati i valori memorizzati nella cache di una riga.|  
  
 Gli eventi seguenti sono utili nella modalità virtuale, ma possono essere utilizzati indipendentemente dall'impostazione della proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>.  
  
|Eventi|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Forms.DataGridView.UserDeletingRow><br /><br /> <xref:System.Windows.Forms.DataGridView.UserDeletedRow><br /><br /> <xref:System.Windows.Forms.DataGridView.RowsRemoved><br /><br /> <xref:System.Windows.Forms.DataGridView.RowsAdded>|Utilizzato dal controllo per indicare l'aggiunta o l'eliminazione di righe e consentire di conseguenza l'aggiornamento della cache di dati.|  
|<xref:System.Windows.Forms.DataGridView.CellFormatting><br /><br /> <xref:System.Windows.Forms.DataGridView.CellParsing><br /><br /> <xref:System.Windows.Forms.DataGridView.CellValidating><br /><br /> <xref:System.Windows.Forms.DataGridView.CellValidated><br /><br /> <xref:System.Windows.Forms.DataGridView.RowValidating><br /><br /> <xref:System.Windows.Forms.DataGridView.RowValidated>|Utilizzato dal controllo per formattare i valori di cella per la visualizzazione e per analizzare e convalidare l'input dell'utente.|  
|<xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded>|Utilizzato dal controllo per recuperare il testo di descrizione comandi delle celle quando è impostata la proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A> o quando la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `true`.<br /><br /> Le descrizioni comandi delle celle vengono visualizzate solo quando il valore della proprietà <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A> è `true`.|  
|<xref:System.Windows.Forms.DataGridView.CellErrorTextNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowErrorTextNeeded>|Utilizzato dal controllo per recuperare il testo di errore delle celle o delle righe quando è impostata la proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A> o la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `true`.<br /><br /> Richiamare il metodo <xref:System.Windows.Forms.DataGridView.UpdateCellErrorText%2A> o il metodo <xref:System.Windows.Forms.DataGridView.UpdateRowErrorText%2A> quando si modifica il testo di errore delle celle o delle righe per garantire che il valore corrente sia visualizzato nel controllo.<br /><br /> Le icone di errore delle celle e delle righe vengono visualizzate quando i valori delle proprietà <xref:System.Windows.Forms.DataGridView.ShowCellErrors%2A> e <xref:System.Windows.Forms.DataGridView.ShowRowErrors%2A> sono `true`.|  
|<xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded>|Utilizzato dal controllo per recuperare una cella o una riga <xref:System.Windows.Forms.ContextMenuStrip> quando è impostata la proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A> del controllo o la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `true`.|  
|<xref:System.Windows.Forms.DataGridView.RowHeightInfoNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowHeightInfoPushed>|Utilizzato dal controllo per recuperare o archiviare i dati di altezza delle righe nella cache di dati.  Richiamare il metodo <xref:System.Windows.Forms.DataGridView.UpdateRowHeightInfo%2A> quando si modificano i dati di altezza delle righe archiviati nella cache al di fuori di un gestore dell'evento <xref:System.Windows.Forms.DataGridView.RowHeightInfoPushed> per garantire che il valore corrente sia visualizzato nel controllo.|  
  
## Suggerimenti per la modalità virtuale  
 Se si implementa la modalità virtuale per utilizzare efficientemente grandi quantità di dati, è necessario garantire anche un uso efficiente del controllo <xref:System.Windows.Forms.DataGridView> stesso.  Per ulteriori informazioni sull'utilizzo efficiente degli stili delle celle, del dimensionamento automatico, delle selezioni e della condivisione di righe, vedere [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>   
 [Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)   
 [Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)