---
title: "Comportamento predefinito di tastiera e mouse nel controllo DataGrid | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "DataGrid [WPF], comportamento della tastiera"
  - "DataGrid [WPF], comportamento del mouse"
  - "comportamento della tastiera [WPF], DataGrid"
  - "comportamento del mouse [WPF], DataGrid"
ms.assetid: 563b8854-ca39-4d97-8235-17eaa0f93c8d
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Comportamento predefinito di tastiera e mouse nel controllo DataGrid
In questo argomento viene descritto in che modo gli utenti possono interagire con il controllo <xref:System.Windows.Controls.DataGrid> utilizzando la tastiera e il mouse.  
  
 Le interazioni tipiche con <xref:System.Windows.Controls.DataGrid> includono la navigazione, la selezione e la modifica.  Il comportamento della selezione è influenzato dalle proprietà <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> e <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A>.  I valori predefiniti che causano il comportamento descritto in questo argomento sono <xref:System.Windows.Controls.DataGridSelectionMode?displayProperty=fullName> e <xref:System.Windows.Controls.DataGridSelectionUnit?displayProperty=fullName>.  La modifica di questi valori potrebbe causare un comportamento diverso da quello descritto.  Quando una cella è in modalità di modifica, il controllo di modifica esegue l'override del comportamento della tastiera standard di <xref:System.Windows.Controls.DataGrid>.  
  
## Comportamento predefinito della tastiera  
 Nella tabella riportata di seguito viene illustrato il comportamento predefinito della tastiera per il controllo <xref:System.Windows.Controls.DataGrid>.  
  
|Tasto o combinazione di tasti|Descrizione|  
|-----------------------------------|-----------------|  
|Freccia GIÙ|Consente di spostare lo stato attivo alla cella posta immediatamente sotto quella corrente.  Se lo stato attivo si trova nell'ultima riga, la pressione del tasto Freccia GIÙ non produce alcun effetto.|  
|Freccia SU|Consente di spostare lo stato attivo alla cella posta immediatamente sopra quella corrente.  Se lo stato attivo si trova nella prima riga, la pressione del tasto Freccia SU non produce alcun effetto.|  
|Freccia SINISTRA|Consente di spostare lo stato attivo alla cella precedente nella riga.  Se lo stato attivo si trova nella prima cella della riga, la pressione del tasto Freccia SINISTRA non produce alcun effetto.|  
|Freccia DESTRA|Consente di spostare lo stato attivo alla cella successiva nella riga.  Se lo stato attivo si trova nell'ultima cella della riga, la pressione del tasto Freccia DESTRA non produce alcun effetto.|  
|HOME|Consente di spostare lo stato attivo alla prima cella nella riga corrente.|  
|FINE|Consente di spostare lo stato attivo all'ultima cella nella riga corrente.|  
|PGGIÙ|Se le righe non sono raggruppate, consente di scorrere il controllo verso il basso del numero di righe visualizzate in modo completo.  Lo stato attivo viene spostato all'ultima riga visualizzata in modo completo senza cambiamento di colonne.<br /><br /> Se la riga sono raggruppate, muove lo stato attivo all'ultima riga in <xref:System.Windows.Controls.DataGrid> senza modificare le colonne.|  
|PGSU|Se le righe non sono raggruppate, consente di scorrere il controllo verso l'alto del numero di righe visualizzate in modo completo.  Lo stato attivo viene spostato alla prima riga visualizzata senza cambiamento di colonne.<br /><br /> Se la riga sono raggruppate, muove lo stato attivo alla prima riga in <xref:System.Windows.Controls.DataGrid> senza modificare le colonne.|  
|TAB|Consente di spostare lo stato attivo alla cella successiva nella riga corrente.  Se lo stato attivo si trova nell'ultima cella della riga, viene spostato alla prima cella della riga successiva.  Se lo stato attivo si trova nell'ultima cella del controllo, viene spostato al controllo successivo nell'ordine di tabulazione del contenitore padre.<br /><br /> Se la cella corrente si trova in modalità di modifica e premere il pulsante di tabulazione sposta lo stato attivo via dalla riga corrente, tutte le modifiche apportate alla riga vengono confermate prima che lo stato attivo venga modificato.|  
|MAIUSC\+TAB|Consente di spostare lo stato attivo alla cella precedente nella riga corrente.  Se lo stato attivo si trova già nella prima cella della riga, viene spostato all'ultima cella della riga precedente.  Se lo stato attivo si trova nella prima cella del controllo, viene spostato al controllo precedente nell'ordine di tabulazione del contenitore padre.<br /><br /> Se la cella corrente si trova in modalità di modifica e premere il pulsante di tabulazione sposta lo stato attivo via dalla riga corrente, tutte le modifiche apportate alla riga vengono confermate prima che lo stato attivo venga modificato.|  
|CTRL\+freccia GIÙ|Consente di spostare lo stato attivo all'ultima cella nella colonna corrente.|  
|CTRL\+FRECCIA SU|Consente di spostare lo stato attivo alla prima cella nella colonna corrente.|  
|CTRL\+freccia DESTRA|Consente di spostare lo stato attivo all'ultima cella nella riga corrente.|  
|CTRL\+freccia SINISTRA|Consente di spostare lo stato attivo alla prima cella nella riga corrente.|  
|CTRL\+HOME|Consente di spostare lo stato attivo alla prima cella nel controllo.|  
|CTRL\+FINE|Consente di spostare lo stato attivo all'ultima cella nel controllo.|  
|CTRL\+PGGIÙ|Equivale a PGGIÙ.|  
|CTRL\+PGSU|Equivale a PGSU.|  
|F2|Se il valore della proprietà <xref:System.Windows.Controls.DataGrid.IsReadOnly%2A?displayProperty=fullName> è `false` e quello della proprietà <xref:System.Windows.Controls.DataGridColumn.IsReadOnly%2A?displayProperty=fullName> è `false` per la colonna corrente, consente di passare alla modalità di modifica della cella corrente.|  
|INVIO|Consente di eseguire il commit di eventuali modifiche apportate alla cella e alla riga correnti e di spostare lo stato attivo alla cella posta immediatamente sotto quella corrente.  Se lo stato attivo si trova nell'ultima riga, le modifiche vengono applicate ma non avviene alcuno spostamento dello stato attivo.|  
|ESC|Se il controllo è in modalità di modifica, consente di annulla la modifica e di ripristinare le eventuali modifica apportate nel controllo.  Se l'origine dati sottostante implementa <xref:System.ComponentModel.IEditableObject>, premendo ESC una seconda volta verrà annullata la modalità di modifica per la riga intera.|  
|BACKSPACE|Consente di eliminare il carattere che precede il cursore durante la modifica di una cella.|  
|DELETE|Consente di eliminare il carattere che segue il cursore durante la modifica di una cella.|  
|CTRL\+INVIO|Consente di eseguire il commit di eventuali modifiche apportate alla cella corrente senza spostamento dello stato attivo.|  
|CTRL\+A|Se <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> è impostato su <xref:System.Windows.Controls.DataGridSelectionMode>, selezionare tutte le righe in <xref:System.Windows.Controls.DataGrid>.|  
  
## Tasti di selezione  
 Se la proprietà <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> è impostata su <xref:System.Windows.Controls.DataGridSelectionMode>, il comportamento di navigazione non cambia, ma se la navigazione viene eseguita con la tastiera mentre è premuto il tasto MAIUSC \(inclusa la combinazione CTRL\+MAIUSC\), verrà modificata una selezione di più celle.  Prima della navigazione, il controllo contrassegna la riga corrente come riga di ancoraggio.  Quando si esegue la navigazione tenendo premuto MAIUSC, la selezione include tutte le righe comprese la riga di ancoraggio e la riga corrente.  
  
 I tasti di selezione seguenti consentono di modificare la selezione di più righe.  
  
-   MAIUSC\+freccia GIÙ  
  
-   MAIUSC\+freccia SU  
  
-   MAIUSC\+PGGIÙ  
  
-   MAIUSC\+PGSU  
  
-   CTRL\+MAIUSC\+freccia GIÙ  
  
-   CTRL\+MAIUSC\+freccia SU  
  
-   CTRL\+MAIUSC\+HOME  
  
-   CTRL\+MAIUSC\+FINE  
  
## Comportamento predefinito del mouse  
 Nella tabella riportata di seguito viene illustrato il comportamento predefinito del mouse per il controllo <xref:System.Windows.Controls.DataGrid>.  
  
|Azione del mouse|Descrizione|  
|----------------------|-----------------|  
|Clic su una riga deselezionata|Rende la riga su cui si è fatto clic la riga corrente e la cella su cui si è fatto clic quella corrente.|  
|Fare clic sulla cella corrente|Pone la cella corrente in modalità di modifica.|  
|Trascinamento di una cella di intestazione di colonna|Se il valore della proprietà <xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A?displayProperty=fullName> è `true` e quello della proprietà <xref:System.Windows.Controls.DataGridColumn.CanUserReorder%2A?displayProperty=fullName> è `true` per la colonna corrente, la colonna viene spostata affinché sia possibile rilasciarla in una nuova posizione.|  
|Trascinamento di un separatore di intestazione di colonna|Se il valore della proprietà <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=fullName> è `true` e quello della proprietà <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=fullName> è `true` per la colonna corrente, la colonna viene ridimensionata.|  
|Fare doppio clic su un separatore di intestazione della colonna|Se la proprietà <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=fullName> è `true` e la proprietà <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=fullName> è `true` per la colonna corrente, ridimensiona automaticamente la colonna mediante la modalità di ridimensionamento <xref:System.Windows.Controls.DataGridLength.Auto%2A>.|  
|Clic su una cella di intestazione di colonna|Se il valore della proprietà <xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A?displayProperty=fullName> è `true` e quello della proprietà <xref:System.Windows.Controls.DataGridColumn.CanUserSort%2A?displayProperty=fullName> è `true` per la colonna corrente, viene eseguito l'ordinamento della colonna.<br /><br /> Quando si fa clic sull'intestazione di una colonna già ordinata, il tipo di ordinamento della colonna viene invertito.<br /><br /> Quando si fa clic su più intestazioni di colonna tenendo premuto MAIUSC, viene eseguito l'ordinamento di più colonne nell'ordine in cui si è fatto clic.|  
|CTRL\+clic su una riga|Se la proprietà <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> è impostata su <xref:System.Windows.Controls.DataGridSelectionMode>, viene modificata una selezione di più righe non contigue.<br /><br /> Se la riga è già selezionata, la riga verrà deselezionata.|  
|MAIUSC\+clic su una riga|Se la proprietà <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> è impostata su <xref:System.Windows.Controls.DataGridSelectionMode>, viene modificata una selezione di più righe contigue.|  
|Fare clic su un'intestazione di un gruppo di righe|Consente di espandere o comprimere il gruppo.|  
|Fare clic sul pulsante Seleziona tutto nell'angolo in alto a sinistra di <xref:System.Windows.Controls.DataGrid>|Se <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> è impostato su <xref:System.Windows.Controls.DataGridSelectionMode>, selezionare tutte le righe in <xref:System.Windows.Controls.DataGrid>.|  
  
## Selezione con il mouse  
 Se la proprietà <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> è impostata su <xref:System.Windows.Controls.DataGridSelectionMode>, quando si fa clic su una riga tenendo premuto CTRL o MAIUSC verrà modificata una selezione di più celle.  
  
 Quando si fa clic su una riga tenendo premuto CTRL, lo stato di selezione della riga viene modificato mentre viene mantenuto quello corrente di tutte le altre righe.  Eseguire questa operazione per selezionare righe non adiacenti.  
  
 Quando si fa clic su una riga o una serie di righe tenendo premuto MAIUSC, vengono selezionate tutte le righe comprese tra la riga corrente e una riga di ancoraggio posizionata in corrispondenza della riga corrente prima del clic.  I successivi clic effettuati tendendo premuto MAIUSC determinano la modifica della riga corrente ma non della riga di ancoraggio.  Eseguire questa operazione per selezionare un intervallo di righe adiacenti.  
  
 È possibile digitare la combinazione CTRL\+SHIFT per selezionare gli intervalli non adiacenti di righe adiacenti.  Per eseguire questa operazione, selezionare il primo intervallo premendo MAIUSC\+clic come descritto in precedenza.  Dopo aver selezionato il primo intervallo di righe, utilizzare CTRL\+clic per selezionare la prima riga nell'intervallo successivo, quindi fare clic sull'ultima riga nell'intervallo successivo tenendo premuto CTRL\+MAIUSC.  
  
## Vedere anche  
 <xref:System.Windows.Controls.DataGrid>   
 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A>