---
title: "Gestione predefinita di tastiera e mouse nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "griglie dei dati, gestione del mouse"
  - "DataGridView (controllo) [Windows Form], gestione della tastiera"
  - "DataGridView (controllo) [Windows Form], gestione del mouse"
  - "DataGridView (controllo) [Windows Form], tasti di navigazione"
  - "tastiere, gestione predefinita nel controllo DataGridView"
  - "mouse, gestione predefinita nel controllo DataGridView"
  - "tasti di navigazione, DataGridView (controllo)"
ms.assetid: 4519b928-bfc8-4e8b-bb9c-b1e76a0ca552
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Gestione predefinita di tastiera e mouse nel controllo DataGridView Windows Form
Nelle tabelle riportate di seguito viene descritto il modo in cui è possibile interagire con il controllo <xref:System.Windows.Forms.DataGridView> utilizzando una tastiera e un mouse.  
  
> [!NOTE]
>  Per personalizzare il comportamento della tastiera, è possibile gestire eventi di tastiera standard come <xref:System.Windows.Forms.Control.KeyDown>.  In modalità di modifica, tuttavia, il controllo di modifica ospitato riceve l'input della tastiera e gli eventi della tastiera non si verificano per il controllo <xref:System.Windows.Forms.DataGridView>.  Per gestire gli eventi del controllo di modifica, collegare i gestori al controllo di modifica in un gestore eventi <xref:System.Windows.Forms.DataGridView.EditingControlShowing>.  In alternativa, è possibile personalizzare il comportamento della tastiera in una sottoclasse <xref:System.Windows.Forms.DataGridView> eseguendo l'override dei metodi <xref:System.Windows.Forms.DataGridView.ProcessDialogKey%2A> e <xref:System.Windows.Forms.DataGridView.ProcessDataGridViewKey%2A>.  
  
## Gestione predefinita della tastiera  
  
### Tasti di navigazione e immissione di base  
  
|Tasto o combinazione di tasti|Descrizione|  
|-----------------------------------|-----------------|  
|Freccia GIÙ|Consente di spostare lo stato attivo alla cella posta immediatamente sotto quella corrente.  Se lo stato attivo si trova nell'ultima riga, non viene eseguito alcuno spostamento.|  
|Freccia SINISTRA|Consente di spostare lo stato attivo alla cella precedente nella riga.  Se lo stato attivo si trova nella prima cella della riga, non viene eseguito alcuno spostamento.|  
|Freccia DESTRA|Consente di spostare lo stato attivo alla cella successiva nella riga.  Se lo stato attivo si trova nell'ultima cella della riga, non viene eseguito alcuno spostamento.|  
|Freccia SU|Consente di spostare lo stato attivo alla cella posta immediatamente sopra quella corrente.  Se lo stato attivo si trova nella prima riga, non viene eseguito alcuno spostamento.|  
|HOME|Consente di spostare lo stato attivo alla prima cella nella riga corrente.|  
|FINE|Consente di spostare lo stato attivo all'ultima cella nella riga corrente.|  
|PGGIÙ|Consente di scorrere il controllo verso il basso del numero di righe visualizzate in modo completo.  Lo stato attivo viene spostato all'ultima riga visualizzata in modo completo senza cambiamento di colonne.|  
|PGSU|Consente di scorrere il controllo verso l'alto del numero di righe visualizzate in modo completo.  Lo stato attivo viene spostato alla prima riga visualizzata senza cambiamento di colonne.|  
|TAB|Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `false`, consente di spostare lo stato attivo alla cella successiva nella riga corrente.  Se lo stato attivo si trova già nell'ultima cella della riga, viene spostato alla prima cella della riga successiva.  Se lo stato attivo si trova nell'ultima cella del controllo, viene spostato al controllo successivo nell'ordine di tabulazione del contenitore padre.<br /><br /> Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `true`, consente di spostare lo stato attivo al controllo successivo nell'ordine di tabulazione del contenitore padre.|  
|MAIUSC\+TAB|Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `false`, consente di spostare lo stato attivo alla cella precedente nella riga corrente.  Se lo stato attivo si trova già nella prima cella della riga, viene spostato all'ultima cella della riga precedente.  Se lo stato attivo si trova nella prima cella del controllo, viene spostato al controllo precedente nell'ordine di tabulazione del contenitore padre.<br /><br /> Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `true`, consente di spostare lo stato attivo al controllo precedente nell'ordine di tabulazione del contenitore padre.|  
|CTRL\+TAB|Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `false`, consente di spostare lo stato attivo al controllo successivo nell'ordine di tabulazione del contenitore padre.<br /><br /> Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `true`, consente di spostare lo stato attivo alla cella successiva nella riga corrente.  Se lo stato attivo si trova già nell'ultima cella della riga, viene spostato alla prima cella della riga successiva.  Se lo stato attivo si trova nell'ultima cella del controllo, viene spostato al controllo successivo nell'ordine di tabulazione del contenitore padre.|  
|CTRL\+MAIUSC\+TAB|Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `false`, consente di spostare lo stato attivo al controllo precedente nell'ordine di tabulazione del contenitore padre.<br /><br /> Se la proprietà <xref:System.Windows.Forms.DataGridView.StandardTab%2A> è impostata su `true`, consente di spostare lo stato attivo alla cella precedente nella riga corrente.  Se lo stato attivo si trova già nella prima cella della riga, viene spostato all'ultima cella della riga precedente.  Se lo stato attivo si trova nella prima cella del controllo, viene spostato al controllo precedente nell'ordine di tabulazione del contenitore padre.|  
|CTRL\+freccia|Consente di spostare lo stato attivo all'ultima cella in direzione della freccia.|  
|CTRL\+HOME|Consente di spostare lo stato attivo alla prima cella nel controllo.|  
|CTRL\+FINE|Consente di spostare lo stato attivo all'ultima cella nel controllo.|  
|CTRL\+PGGIÙ\/PGSU|Uguale a PGGIÙ o PGSU.|  
|F2|Consente di passare alla modalità di modifica della cella corrente se il valore della proprietà <xref:System.Windows.Forms.DataGridView.EditMode%2A> è <xref:System.Windows.Forms.DataGridViewEditMode> o <xref:System.Windows.Forms.DataGridViewEditMode>.|  
|F4|Se la cella corrente è una <xref:System.Windows.Forms.DataGridViewComboBoxCell>, consente di passare alla modalità di modifica della cella e di visualizzare l'elenco a discesa.|  
|ALT\+Freccia SU\/GIÙ|Se la cella corrente è una <xref:System.Windows.Forms.DataGridViewComboBoxCell>, consente di passare alla modalità di modifica della cella e di visualizzare l'elenco a discesa.|  
|BARRA SPAZIATRICE|Se la cella corrente è una <xref:System.Windows.Forms.DataGridViewButtonCell>, <xref:System.Windows.Forms.DataGridViewLinkCell> o <xref:System.Windows.Forms.DataGridViewCheckBoxCell>, vengono generati gli eventi <xref:System.Windows.Forms.DataGridView.CellClick> e <xref:System.Windows.Forms.DataGridView.CellContentClick>.  Se la cella corrente è una <xref:System.Windows.Forms.DataGridViewButtonCell>, viene inoltre premuto il pulsante.  Se la cella corrente è una <xref:System.Windows.Forms.DataGridViewCheckBoxCell>, viene inoltre modificato lo stato di selezione.|  
|INVIO|Consente di eseguire il commit di eventuali modifiche apportate alla cella e alla riga correnti e di spostare lo stato attivo alla cella posta immediatamente sotto quella corrente.  Se lo stato attivo si trova nell'ultima riga, le modifiche vengono applicate ma non avviene alcuno spostamento dello stato attivo.|  
|ESC|Se il controllo è in modalità di modifica, consente di annullarlo.  Se il controllo non è in modalità di modifica, verranno annullate le modifiche apportate alla riga corrente se il controllo è associato a un'origine dati che supporta la modifica o è stata implementata la modalità virtuale con ambito di commit a livello di riga.|  
|BACKSPACE|Consente di eliminare il carattere che precede il punto di inserimento durante la modifica di una cella.|  
|DELETE|Consente di eliminare il carattere che segue il punto di inserimento durante la modifica di una cella.|  
|CTRL\+INVIO|Consente di eseguire il commit di eventuali modifiche apportate alla cella corrente senza spostamento dello stato attivo.  Consente inoltre di eseguire il commit di eventuali modifiche apportate alla riga corrente se il controllo è associato a un'origine dati che supporta la modifica o è stata implementata la modalità virtuale con ambito di commit a livello di riga.|  
|CTRL\+0|Consente di immettere un valore <xref:System.DBNull.Value?displayProperty=fullName> nella cella corrente se questa ammette modifiche.  Per impostazione predefinita il valore visualizzato per <xref:System.DBNull> è il valore della proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> della classe <xref:System.Windows.Forms.DataGridViewCellStyle> che ha effetto per la cella corrente.|  
  
### Tasti di selezione  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `false` e la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> è impostata su <xref:System.Windows.Forms.DataGridViewSelectionMode>, la modifica della cella corrente mediante i tasti di navigazione comporta lo spostamento della selezione alla nuova cella.  I tasti MAIUSC, CTRL e ALT non influenzano tale comportamento.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> è impostata su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, si verifica lo stesso comportamento con gli ulteriori effetti riportati di seguito.  
  
|Tasto o combinazione di tasti|Descrizione|  
|-----------------------------------|-----------------|  
|MAIUSC\+BARRA SPAZIATRICE|Consente di selezionare la riga o colonna intera \(come se si facesse clic sull'intestazione della riga o colonna\).|  
|tasto di navigazione \(tasto di direzione, PGSU\/PGGIÙ, HOME, FINE\)|Se è selezionata una riga o colonna intera, il passaggio dalla cella corrente a una nuova riga o colonna comporta lo spostamento della selezione alla nuova riga o colonna intera \(a seconda della modalità di selezione\).|  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `false` e la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, il passaggio dalla cella corrente a una nuova riga o colonna mediante la tastiera comporta lo spostamento della selezione alla nuova riga o colonna intera.  I tasti MAIUSC, CTRL e ALT non influenzano tale comportamento.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `true`, l'effetto della navigazione non muta ma se la navigazione avviene tramite tastiera mentre è premuto il tasto MAIUSC \(CTRL\+MAIUSC compreso\), viene modificata la selezione di più celle.  Prima della navigazione, il controllo contrassegna la cella corrente come cella di partenza.  Durante lo spostamento con pressione del tasto MAIUSC, vengono selezionate tutte le celle comprese tra la cella di partenza e quella corrente.  Altre celle del controllo, se già selezionate, mantengono tale stato ma potrebbero essere deselezionate se la navigazione tramite tastiera le inserisce temporaneamente tra la cella di partenza e la cella corrente.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `true` e la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, il comportamento della cella di partenza e di quella corrente è identico con la differenza che solo le righe o colonne intere vengono selezionate o deselezionate.  
  
## Gestione predefinita del mouse  
  
### Gestione di base del mouse  
  
> [!NOTE]
>  Se si fa clic su una cella con il pulsante sinistro del mouse, viene sempre modificata la cella corrente.  Se si fa clic su una cella con il pulsante destro del mouse, viene aperto un menu di scelta rapida, se disponibile.  
  
|Azione del mouse|Descrizione|  
|----------------------|-----------------|  
|Pulsante sinistro del mouse premuto|La cella su cui si è fatto clic è la cella corrente e viene generato l'evento <xref:System.Windows.Forms.DataGridView.CellMouseDown?displayProperty=fullName>.|  
|Pulsante sinistro del mouse sollevato|Genera l'evento <xref:System.Windows.Forms.DataGridView.CellMouseUp?displayProperty=fullName>|  
|Clic con il pulsante sinistro del mouse|Vengono generati gli eventi <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName> e <xref:System.Windows.Forms.DataGridView.CellMouseClick?displayProperty=fullName>.|  
|Pulsante sinistro del mouse premuto e trascinamento su una cella di intestazione di colonna|Se la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=fullName> è impostata su `true`, la colonna viene spostata affinché sia possibile rilasciarla in una nuova posizione.|  
  
### Selezione con il mouse  
 Il pulsante centrale e la rotellina del mouse non consentono di effettuare alcuna selezione.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `false` e la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode>, si verificano gli effetti riportati di seguito.  
  
|Azione del mouse|Descrizione|  
|----------------------|-----------------|  
|Clic con il pulsante sinistro del mouse|Consente di selezionare solo la cella corrente se si fa clic su una cella.  Se si fa clic su un'intestazione di riga o colonna, non viene effettuata alcuna selezione.|  
|Clic con il pulsante destro del mouse|Viene visualizzato un menu di scelta rapida, se disponibile.|  
  
 Si verificano gli stessi effetti quando la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> è impostata su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, con l'eccezione che, in funzione della modalità di selezione, se si fa clic su un'intestazione di riga o colonna viene selezionata la riga o colonna intera e la prima cella della riga o colonna viene impostata come cella corrente.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> è impostata su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, se si fa clic su una cella qualsiasi in una riga o colonna viene selezionata la riga o colonna intera.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `true`, se si fa clic su una cella tenendo premuto il tasto CTRL o MAIUSC viene modificata la selezione di più celle.  
  
 Quando si fa clic su una cella tenendo premuto il tasto CTRL, lo stato di selezione della cella viene modificato mentre viene mantenuto quello corrente di tutte le altre celle.  
  
 Quando si fa clic su una cella o una serie di celle tenendo premuto il tasto MAIUSC, vengono selezionate tutte le celle comprese tra la cella corrente e una cella di partenza posizionata in corrispondenza della cella corrente prima del primo clic.  Quando si fa clic e si trascina il puntatore su più celle, la cella di partenza corrisponde a quella su cui si è fatto clic all'inizio dell'operazione.  Se si fanno altri clic tenendo premuto il tasto MAIUSC, la cella corrente viene cambiata ma non quella di partenza.  Altre celle del controllo, se già selezionate, mantengono tale stato ma potrebbero essere deselezionate se la navigazione tramite mouse le inserisce temporaneamente tra la cella di partenza e la cella corrente.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `true` e la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, se si fa clic su un'intestazione di riga o colonna \(in funzione della modalità di selezione\) tenendo premuto il tasto MAIUSC, viene modificata una selezione esistente di righe o colonne intere, se tale selezione esiste.  In caso contrario la selezione viene annullata e vengono selezionate altre righe o colonne intere.  Se si fa clic su un'intestazione di riga o colonna tenendo premuto il tasto CTRL, tuttavia, la riga o colonna su cui si è fatto clic viene aggiunta o rimossa dalla selezione corrente senza ulteriori modifiche della stessa.  
  
 Se la proprietà <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> è impostata su `true` e la proprietà <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> su <xref:System.Windows.Forms.DataGridViewSelectionMode> o su <xref:System.Windows.Forms.DataGridViewSelectionMode>, se si fa clic su una cella tenendo premuto il tasto MAIUSC o CTRL si verificano gli stessi effetti con l'eccezione che sono interessate solo righe e colonne intere.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)