---
title: "Modalit&#224; di selezione nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "DataGridView (controllo) [Windows Form], modalità di selezione"
  - "selezione, modalità nel controllo DataGridView"
ms.assetid: a3ebfd3d-0525-479d-9d96-d9e017289b36
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Modalit&#224; di selezione nel controllo DataGridView Windows Form
A volte è preferibile che l'applicazione esegua azioni in base alle selezioni effettuate dall'utente all'interno di un controllo <xref:System.Windows.Forms.DataGridView>.  A seconda delle azioni, può essere opportuno limitare i tipi di selezione possibili.  Si supponga ad esempio che l'applicazione consenta di stampare un report sul record correntemente selezionato.  In questo caso, può essere opportuno configurare il controllo <xref:System.Windows.Forms.DataGridView> in modo che, quando si fa clic in qualsiasi punto all'interno di una riga, venga selezionata sempre l'intera riga e sia possibile selezionare solo una riga alla volta.  
  
 È possibile specificare le selezioni consentite impostando la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> su uno dei seguenti valori dell'enumerazione <xref:System.Windows.Forms.DataGridViewSelectionMode>.  
  
|Valore di DataGridViewSelectionMode|Descrizione|  
|-----------------------------------------|-----------------|  
|<xref:System.Windows.Forms.DataGridViewSelectionMode>|La cella viene selezionata con un clic.  Per la selezione non possono essere utilizzate le intestazioni di riga e di colonna.|  
|<xref:System.Windows.Forms.DataGridViewSelectionMode>|La cella viene selezionata con un clic.  L'intera colonna viene selezionata facendo clic sull'intestazione di colonna.  Non è possibile utilizzare le intestazioni di colonna per l'ordinamento.|  
|<xref:System.Windows.Forms.DataGridViewSelectionMode>|L'intera colonna viene selezionata facendo clic sull'intestazione di colonna o su una cella.  Non è possibile utilizzare le intestazioni di colonna per l'ordinamento.|  
|<xref:System.Windows.Forms.DataGridViewSelectionMode>|L'intera riga viene selezionata facendo clic sull'intestazione di riga o su una cella.|  
|<xref:System.Windows.Forms.DataGridViewSelectionMode>|Modalità di selezione predefinita.  La cella viene selezionata con un clic.  L'intera riga viene selezionata facendo clic sull'intestazione di riga.|  
  
> [!NOTE]
>  Se si modifica la modalità di selezione in fase di esecuzione viene automaticamente annullata la selezione corrente.  
  
 Per impostazione predefinita, gli utenti possono selezionare più righe, colonne o celle trascinando il mouse e tenendo premuto CTRL o MAIUSC durante la selezione per estendere o modificare una selezione oppure facendo clic sulla cella di intestazione in alto a sinistra per selezionare tutte le celle del controllo.  Per impedire questo comportamento, impostare la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> su `false`.  
  
 Con le modalità <xref:System.Windows.Forms.DataGridViewSelectionMode> e <xref:System.Windows.Forms.DataGridViewSelectionMode> è possibile eliminare le righe selezionandole e premendo CANC.  Gli utenti possono eliminare righe solo quando la cella corrente non è in modalità di modifica, la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToDeleteRows%2A> è impostata su `true` e l'origine dati sottostante supporta l'eliminazione di righe eseguita dagli utenti.  Queste impostazioni, tuttavia, non impediscono l'eliminazione di righe a livello di codice.  
  
## Selezione a livello di codice  
 La modalità di selezione corrente limita il comportamento della selezione a livello di codice così come la selezione eseguita dall'utente.  È possibile modificare la selezione corrente a livello di codice impostando la proprietà `Selected` di tutte le celle, le righe o le colonne presenti nel controllo <xref:System.Windows.Forms.DataGridView>.  Inoltre è possibile selezionare tutte le celle del controllo attraverso il metodo <xref:System.Windows.Forms.DataGridView.SelectAll%2A>, in base alla modalità di selezione.  Per annullare la selezione, utilizzare il metodo <xref:System.Windows.Forms.DataGridView.ClearSelection%2A>.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `true`, è possibile aggiungere o rimuovere elementi <xref:System.Windows.Forms.DataGridView> dalla selezione modificando la proprietà `Selected` dell'elemento.  Diversamente, se si imposta la proprietà `Selected` su `true` di un elemento, gli altri elementi verranno rimossi automaticamente dalla selezione.  
  
 La modifica del valore della proprietà <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> non altera la selezione corrente.  
  
 È possibile recuperare una raccolta delle celle, delle righe o delle colonne correntemente selezionate mediante le proprietà <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>, <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> e <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> del controllo <xref:System.Windows.Forms.DataGridView>.  L'accesso a queste proprietà è inefficace quando ogni cella del controllo è selezionata.  Per evitare una lieve riduzione delle prestazioni in questo caso, utilizzare prima il metodo <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>.  Anche l'accesso a queste raccolte per determinare il numero di celle, righe o colonne selezionate può risultare inefficace.  Utilizzare invece il metodo <xref:System.Windows.Forms.DataGridView.GetCellCount%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.GetRowCount%2A> o <xref:System.Windows.Forms.DataGridViewColumnCollection.GetColumnCount%2A> e passare il valore <xref:System.Windows.Forms.DataGridViewElementStates>.  
  
> [!TIP]
>  Il codice di esempio in cui viene illustrato l'utilizzo a livello di codice delle celle selezionate è disponibile nei cenni preliminari sulla classe <xref:System.Windows.Forms.DataGridView>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A>   
 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>   
 <xref:System.Windows.Forms.DataGridViewSelectionMode>   
 [Utilizzo della selezione e degli Appunti con il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare la modalità di selezione del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-selection-mode-of-the-windows-forms-datagridview-control.md)