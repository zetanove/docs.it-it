---
title: "Procedure consigliate per ridimensionare il controllo DataGridView Windows Form | Microsoft Docs"
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
  - "procedure ottimali, DataGridView (controllo)"
  - "griglie dei dati, procedure ottimali"
  - "DataGridView (controllo) [Windows Form], procedure ottimali"
  - "DataGridView (controllo) [Windows Form], condivisione di righe"
  - "DataGridView (controllo) [Windows Form], adattamento"
  - "DataGridView (controllo) [Windows Form], righe condivise"
ms.assetid: 8321a8a6-6340-4fd1-b475-fa090b905aaf
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# Procedure consigliate per ridimensionare il controllo DataGridView Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> è progettato per fornire la massima scalabilità.  Se è necessario visualizzare grandi quantità di dati, seguire le istruzioni riportate in questo argomento per evitare l'utilizzo di notevoli quantità di memoria o diminuire i tempi di risposta dell'interfaccia utente.  In questo argomento vengono illustrati i seguenti problemi:  
  
-   Utilizzo efficace degli stili di cella  
  
-   Utilizzo efficace dei menu di scelta rapida  
  
-   Utilizzo efficace del ridimensionamento automatico  
  
-   Utilizzo efficace di raccolte di celle, righe e colonne selezionate  
  
-   Utilizzo di righe condivise  
  
-   Come impedire la rimozione della condivisione delle righe  
  
 Se è necessario ottenere prestazioni speciali, è possibile implementare la modalità virtuale ed eseguire operazioni di gestione dei dati personalizzati.  Per ulteriori informazioni, vedere [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md).  
  
## Utilizzo efficace degli stili di cella  
 A ciascuna cella, riga e colonna sono associate informazioni di stile.  Le informazioni di stile vengono memorizzate negli oggetti <xref:System.Windows.Forms.DataGridViewCellStyle>.  La creazione di oggetti cella per molti singoli elementi del controllo \-<xref:System.Windows.Forms.DataGridView> può risultare inefficace, specie quando si utilizzano grandi quantità di dati.  Per evitare l'impatto sulle prestazioni, attenersi alle istruzioni riportate di seguito.  
  
-   Evitare di impostare le proprietà dello stile di cella per singoli oggetti <xref:System.Windows.Forms.DataGridViewCell> o <xref:System.Windows.Forms.DataGridViewRow>.  Questa condizione vale anche per l'oggetto riga specificato dalla proprietà <xref:System.Windows.Forms.DataGridView.RowTemplate%2A>.  Ciascuna nuova riga duplicata dal modello di riga riceverà una copia dello stile di cella del modello.  Per ottenere la massima scalabilità, impostare le proprietà dello stile di cella a livello del controllo <xref:System.Windows.Forms.DataGridView>.  Ad esempio, impostare la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> invece della proprietà <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>.  
  
-   Se per alcune celle è necessaria una formattazione diversa da quella predefinita, utilizzare la stessa istanza della proprietà <xref:System.Windows.Forms.DataGridViewCellStyle> in gruppi diversi di celle, righe o colonne.  Evitare di impostare direttamente proprietà di tipo <xref:System.Windows.Forms.DataGridViewCellStyle> su singole celle, righe e colonne.  Per un esempio di condivisione degli stili di cella, vedere [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md).  Mediante il gestore eventi <xref:System.Windows.Forms.DataGridView.CellFormatting> è anche possibile evitare la riduzione delle prestazioni durante l'impostazione dei singoli stili di cella.  Per un esempio, vedere [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md).  
  
-   Quando si determina uno stile di cella, utilizzare la proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=fullName> invece della proprietà <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>.  L'accesso alla proprietà <xref:System.Windows.Forms.DataGridViewCell.Style%2A> determina la creazione di una nuova istanza della classe <xref:System.Windows.Forms.DataGridViewCellStyle> se la proprietà non è stata ancora utilizzata.  Se alcuni stili sono ereditati dalla riga, dalla colonna o dal controllo, l'accesso all'oggetto potrebbe non contenere le informazioni sullo stile complete relative alla cella.  Per ulteriori informazioni sull'ereditarietà degli stili delle celle, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
## Utilizzo efficace dei menu di scelta rapida  
 A ciascuna cella, riga e colonna è associato un menu di scelta rapida.  I menu di scelta rapida nel controllo <xref:System.Windows.Forms.DataGridView> sono rappresentati dai controlli <xref:System.Windows.Forms.ContextMenuStrip>.  Come nel caso degli stili di cella, la creazione di menu di scelta rapida per molti singoli elementi <xref:System.Windows.Forms.DataGridView> ha un impatto negativo sulle prestazioni.  Per evitare questo problema, attenersi alle istruzioni riportate di seguito.  
  
-   Evitare di creare menu di scelta rapida per singole celle e righe.  Questa condizione vale anche per il modello di riga duplicato assieme al menu di scelta rapida quando nuove righe vengono aggiunte al controllo.  Per ottenere la massima scalabilità, utilizzare solo la proprietà <xref:System.Windows.Forms.Control.ContextMenuStrip%2A> del controllo per specificare un singolo menu di scelta rapida per l'intero controllo.  
  
-   Se sono necessari più menu di scelta rapida per più righe o celle, gestire l'evento <xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded> o l'evento <xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded>.  Questi eventi consentono di gestire i menu di scelta rapida manualmente, consentendo di regolare le prestazioni.  
  
## Utilizzo efficace del ridimensionamento automatico  
 Righe, colonne e intestazioni possono essere ridimensionate automaticamente quando il contenuto della cella viene modificato, in modo da visualizzare l'intero contenuto delle celle senza che vengano eseguiti tagli.  Le modalità di modifica delle dimensioni possono comportare anche il ridimensionamento di righe, colonne e intestazioni.  Per determinare le dimensioni corrette, il controllo <xref:System.Windows.Forms.DataGridView> deve esaminare il valore di ciascuna cella nella quale dovrà essere disposto il contenuto.  Se si lavora con grandi quantità di dati, questa analisi può avere un effetto negativo sulle prestazioni del controllo quando si verifica il ridimensionamento automatico.  Per evitare questo problema di prestazioni, attenersi alle istruzioni riportate di seguito.  
  
-   Evitare di utilizzare il ridimensionamento su un controllo <xref:System.Windows.Forms.DataGridView> con un insieme ampio di righe.  Se si utilizza il ridimensionamento automatico, ridimensionare solo le righe visualizzate.  Utilizzare solo le righe visualizzate anche in modalità virtuale.  
  
    -   Per righe e colonne, utilizzare il campo `DisplayedCells` o il campo `DisplayedCellsExceptHeaders` delle enumerazioni <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>, <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode> e <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>.  
  
    -   Per le intestazioni di riga, utilizzare il campo <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode> o il campo <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode> dell'enumerazione <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>.  
  
-   Per ottenere la massima scalabilità, disattivare il ridimensionamento automatico e utilizzare il ridimensionamento a livello di codice.  
  
 Per ulteriori informazioni, vedere [Opzioni di ridimensionamento nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md).  
  
## Utilizzo efficace di raccolte di celle, righe e colonne selezionate  
 La raccolta <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> non viene eseguita in modo efficace in presenza di selezioni di notevoli dimensioni.  Anche le raccolte <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> e <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> possono risultare inefficaci, sebbene in maniera minore, in quanto in un controllo <xref:System.Windows.Forms.DataGridView> normale vi sono molte meno righe che celle e molte meno colonne che righe.  Per evitare la riduzione delle prestazioni quando si utilizzano queste raccolte, attenersi alle istruzioni riportate di seguito.  
  
-   Per determinare se tutte le celle presenti in un controllo <xref:System.Windows.Forms.DataGridView> sono state selezionate prima dell'accesso al contenuto della raccolta <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>, verificare il valore restituito del metodo <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>.  Notare, tuttavia, che questo metodo può provocare la rimozione della condivisione delle righe.  Per ulteriori informazioni, vedere la sezione successiva.  
  
-   Evitare di utilizzare la proprietà <xref:System.Collections.ICollection.Count%2A> della classe <xref:System.Windows.Forms.DataGridViewSelectedCellCollection?displayProperty=fullName> per determinare il numero delle celle selezionate.  Utilizzare invece il metodo <xref:System.Windows.Forms.DataGridView.GetCellCount%2A?displayProperty=fullName> e passare il valore <xref:System.Windows.Forms.DataGridViewElementStates?displayProperty=fullName>.  Analogamente, utilizzare i metodi <xref:System.Windows.Forms.DataGridViewRowCollection.GetRowCount%2A?displayProperty=fullName> e <xref:System.Windows.Forms.DataGridViewColumnCollection.GetColumnCount%2A?displayProperty=fullName> per determinare il numero di elementi selezionati invece di accedere alle raccolte di righe e colonne selezionate.  
  
-   Evitare le modalità di selezione basate sulle celle.  Impostare invece la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> su <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName> o <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName>.  
  
## Utilizzo di righe condivise  
 La condivisione delle righe consente di sfruttare in modo efficace la memoria nel controllo <xref:System.Windows.Forms.DataGridView>.  La condivisione delle istanze della classe <xref:System.Windows.Forms.DataGridViewRow> determina la condivisione nelle righe di tutte le informazioni possibili sul relativo aspetto e comportamento.  
  
 La condivisione delle istanze della riga consente di utilizzare una quantità minore di memoria, ma la condivisione delle righe può essere facilmente rimossa.  Ad esempio, ogni volta che un utente interagisce direttamente con una cella, la condivisione della relativa riga viene rimossa.  Poiché non è possibile evitare questa condizione, le istruzioni riportate in questo argomento sono utili solo quando si utilizzano quantità di dati molto grandi e solo quando gli utenti interagiscono con una parte relativamente piccola dei dati ogni volta che il programma viene eseguito.  
  
 Non è possibile condividere una riga in un controllo <xref:System.Windows.Forms.DataGridView> non associato se in una delle celle sono presenti valori.  Quando il controllo <xref:System.Windows.Forms.DataGridView> viene associato a un'origine dati esterna o quando si implementa la modalità virtuale e si fornisce un'origine dati personalizzata, i valori della cella vengono memorizzati al di fuori del controllo invece che negli oggetti cella, consentendo la condivisione delle righe.  
  
 Una riga può essere condivisa solo se lo stato di tutte le relative celle può essere determinato dallo stato della riga e dagli stati delle colonne che contengono le celle.  Se si modifica lo stato di una cella in modo tale che non possa più essere determinato dallo stato della relativa riga e colonna, la riga non può essere condivisa.  
  
 Ad esempio, una riga non può essere condivisa in una delle seguenti situazioni:  
  
-   La riga contiene una singola cella selezionata che non si trova in una colonna selezionata.  
  
-   La riga contiene una cella in cui è impostata la proprietà <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> o la proprietà <xref:System.Windows.Forms.DataGridViewCell.ContextMenuStrip%2A>.  
  
-   La riga contiene una proprietà <xref:System.Windows.Forms.DataGridViewComboBoxCell> in cui è impostata la proprietà <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A>.  
  
 In modalità associata o in modalità virtuale, è possibile fornire descrizioni comandi e menu di scelta rapida per singole celle gestendo gli eventi <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded> e <xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded>.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> tenta automaticamente di utilizzare le righe condivise ogni volta che vengono aggiunte righe alla classe <xref:System.Windows.Forms.DataGridViewRowCollection>.  Attenersi alle seguenti istruzioni per verificare che le righe siano condivise:  
  
-   Evitare di chiamare l'overload `Add(Object[])` del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> e l'overload `Insert(Object[])` del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> della raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName>.  Questi overload creano automaticamente righe non condivise.  
  
-   Verificare che la riga specificata nella proprietà <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=fullName> possa essere condivisa nei seguenti casi:  
  
    -   Quando viene chiamato l'overload `Add()` o l'overload `Add(Int32)` del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> oppure l'overload `Insert(Int32,Int32)` del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> della raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName>.  
  
    -   Quando viene incrementato il valore della proprietà <xref:System.Windows.Forms.DataGridView.RowCount%2A?displayProperty=fullName>.  
  
    -   Quando viene impostata la proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=fullName>.  
  
-   Verificare che la riga indicata dal parametro `indexSource` possa essere condivisa quando vengono chiamati i metodi <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopy%2A> e <xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopies%2A> della raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName>.  
  
-   Verificare che la riga o le righe specificate possano essere condivise quando si chiama l'overload `Add(DataGridViewRow)` del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>, il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.AddRange%2A>, l'overload `Insert(Int32,DataGridViewRow)` del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> e il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.InsertRange%2A> della raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=fullName>.  
  
 Per determinare se una riga è condivisa, utilizzare il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=fullName> per recuperare l'oggetto riga, quindi verificare la proprietà <xref:System.Windows.Forms.DataGridViewBand.Index%2A> dell'oggetto.  Il valore della proprietà <xref:System.Windows.Forms.DataGridViewBand.Index%2A> delle righe condivise è sempre uguale a \-1.  
  
## Come impedire la rimozione della condivisione delle righe  
 La condivisione delle righe può essere rimossa a seguito dell'utilizzo di codice o di un'operazione di un utente.  Per evitare effetti negativi sulle prestazioni, è necessario evitare che la condivisione delle righe venga rimossa.  Durante lo sviluppo dell'applicazione, è possibile gestire l'evento <xref:System.Windows.Forms.DataGridView.RowUnshared> per individuare il momento in cui la condivisione delle righe viene rimossa.  Questa operazione è utile durante il debug dei problemi di condivisione delle righe.  
  
 Per impedire la rimozione della condivisione delle righe, attenersi alle istruzioni riportate di seguito.  
  
-   Non indicizzare la raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A> o scorrerne gli elementi mediante un ciclo `foreach`.  In genere, non è necessario accedere direttamente alle righe.  I metodi <xref:System.Windows.Forms.DataGridView> che operano sulle righe estraggono gli argomenti di indice della riga invece delle istanze di riga.  Inoltre, i gestori degli eventi collegati alle righe ricevono oggetti di argomento dell'evento con proprietà delle righe che è possibile utilizzare per modificare le righe senza che ne venga rimossa la condivisione.  
  
-   Se è necessario accedere a una riga, utilizzare il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=fullName> e passare il valore di indice reale della riga.  La modifica di un oggetto riga condivisa recuperata mediante questo metodo sarà estesa tuttavia a tutte le righe che condividono l'oggetto.  Ad ogni modo, la riga relativa ai nuovi record non viene condivisa con le altre righe, per cui la modifica di altre righe non ha effetto su tale riga.  Inoltre, righe diverse rappresentate da una riga condivisa possono disporre di menu di scelta rapida diversi.  Per recuperare il menu di scelta rapida corretto dall'istanza di una riga condivisa, utilizzare il metodo <xref:System.Windows.Forms.DataGridViewRow.GetContextMenuStrip%2A> e passare il valore di indice reale della riga.  Se invece si accede alla proprietà <xref:System.Windows.Forms.DataGridViewRow.ContextMenuStrip%2A> della riga condivisa, verrà utilizzato il valore di indice della riga condivisa di \-1 e non verrà recuperato il menu di scelta rapida corretto.  
  
-   Evitare di indicizzare la raccolta <xref:System.Windows.Forms.DataGridViewRow.Cells%2A?displayProperty=fullName>.  L'accesso diretto a una cella provocherà la rimozione della condivisione della riga padre e determinerà la creazione di una nuova istanza della classe <xref:System.Windows.Forms.DataGridViewRow>.  I gestori degli eventi collegati alle celle ricevono oggetti di argomento dell'evento con proprietà delle celle che è possibile utilizzare per modificare le celle senza che venga rimossa la condivisione delle righe.  È anche possibile utilizzare la proprietà <xref:System.Windows.Forms.DataGridView.CurrentCellAddress%2A> per recuperare i valori di indice della riga e della colonna della cella corrente senza accedere direttamente alla cella.  
  
-   Evitare le modalità di selezione basate sulle celle.  Queste modalità provocano la rimozione della condivisione delle righe.  Impostare invece la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> su <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName> o <xref:System.Windows.Forms.DataGridViewSelectionMode?displayProperty=fullName>.  
  
-   Non gestire l'evento <xref:System.Windows.Forms.DataGridViewRowCollection.CollectionChanged?displayProperty=fullName> o l'evento <xref:System.Windows.Forms.DataGridView.RowStateChanged?displayProperty=fullName>.  Questi eventi provocano la rimozione della condivisione delle righe.  Inoltre, non chiamare il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.OnCollectionChanged%2A?displayProperty=fullName> o il metodo <xref:System.Windows.Forms.DataGridView.OnRowStateChanged%2A?displayProperty=fullName> per la generazione di questi eventi.  
  
-   Non accedere alla raccolta <xref:System.Windows.Forms.DataGridView.SelectedCells%2A?displayProperty=fullName> quando il valore della proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> è <xref:System.Windows.Forms.DataGridViewSelectionMode>, <xref:System.Windows.Forms.DataGridViewSelectionMode>, <xref:System.Windows.Forms.DataGridViewSelectionMode> o <xref:System.Windows.Forms.DataGridViewSelectionMode>.  In questo modo viene rimossa la condivisione di tutte le righe selezionate.  
  
-   Non chiamare il metodo <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A?displayProperty=fullName>.  Questo metodo può provocare la rimozione della condivisione di tutte le righe.  
  
-   Non chiamare il metodo <xref:System.Windows.Forms.DataGridView.SelectAll%2A?displayProperty=fullName> quando il valore della proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=fullName> è <xref:System.Windows.Forms.DataGridViewSelectionMode>.  In questo modo viene rimossa la condivisione di tutte le righe.  
  
-   Non impostare la proprietà <xref:System.Windows.Forms.DataGridViewCell.ReadOnly%2A> o la proprietà <xref:System.Windows.Forms.DataGridViewCell.Selected%2A> di una cella su `false` quando la corrispondente proprietà della relativa colonna è impostata su `true`.  In questo modo viene rimossa la condivisione di tutte le righe.  
  
-   Non accedere alla proprietà <xref:System.Windows.Forms.DataGridViewRowCollection.List%2A?displayProperty=fullName>.  In questo modo viene rimossa la condivisione di tutte le righe.  
  
-   Non chiamare l'overload `Sort(IComparer)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A>.  L'ordinamento eseguito mediante operatori di confronto personalizzati provoca la rimozione della condivisione di tutte le righe.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [Modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)   
 [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)   
 [Opzioni di ridimensionamento nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)