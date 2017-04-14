---
title: "Tasti di scelta rapida per il controllo DataGrid Windows Form | Microsoft Docs"
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
  - "DataGrid (controllo) [Windows Form], tasti di navigazione"
  - "tasti di scelta rapida, controllo DataGrid"
ms.assetid: a01780f9-20d5-4f5f-808f-c790c9a007a5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Tasti di scelta rapida per il controllo DataGrid Windows Form
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Nella seguente tabella sono elencati i tasti di scelta rapida che è possibile utilizzare per navigare all'interno del controllo <xref:System.Windows.Forms.DataGrid> Windows Form:  
  
|Azione|Tasto di scelta rapida|  
|------------|----------------------------|  
|Completamento dell'immissione di dati in una cella e spostamento nella cella successiva verso il basso.<br /><br /> Se lo stato attivo si trova sul collegamento a una tabella figlio, viene eseguito il passaggio a questa tabella.|INVIO|  
|Annullamento della modifica della cella se si è in modalità di modifica della cella.<br /><br /> Se si sta effettuando la selezione di testo scorrevole, viene eseguito l'annullamento della modifica della riga.|ESC|  
|Eliminazione del carattere che precede il punto di inserimento durante la modifica di una cella.|BACKSPACE|  
|Eliminazione del carattere che segue il punto di inserimento durante la modifica di una cella.|DELETE|  
|Spostamento nella prima cella della riga corrente.|HOME|  
|Spostamento nell'ultima cella della riga corrente.|FINE|  
|Evidenziazione dei caratteri della cella corrente e collocamento del punto di inserimento alla fine della riga corrente.  Si tratta dello stesso effetto del doppio clic all'interno di una cella.|F2|  
|Se lo stato attivo si trova in una cella, viene eseguito il passaggio alla cella successiva della riga.<br /><br /> Se lo stato attivo si trova nell'ultima cella di una riga, vengono eseguiti il passaggio al primo collegamento alla tabella figlio della riga e l'espansione di tale collegamento.<br /><br /> Se lo stato attivo si trova su un collegamento figlio, viene eseguito il passaggio al collegamento figlio successivo.<br /><br /> Se lo stato attivo si trova sull'ultimo collegamento figlio, viene eseguito il passaggio alla prima cella della riga successiva.|TAB|  
|Se lo stato attivo si trova in una cella, viene eseguito il passaggio alla cella precedente della riga.<br /><br /> Se lo stato attivo si trova nella prima cella di una riga, viene eseguito passaggio al passaggio all'ultimo collegamento a una tabella figlio che è stato espanso nella riga precedente oppure viene eseguito il passaggio all'ultima cella della riga precedente.<br /><br /> Se lo stato attivo si trova su un collegamento figlio, viene eseguito il passaggio al collegamento figlio precedente.<br /><br /> Se lo stato attivo si trova sul primo collegamento figlio, viene eseguito il passaggio all'ultima cella della riga precedente.|MAIUSC\+TAB|  
|Passaggio al controllo successivo nell'ordine di tabulazione.|CTRL\+TAB|  
|Passaggio al controllo precedente nell'ordine di tabulazione.|CTRL\+MAIUSC\+TAB|  
|Passaggio alla tabella padre se lo stato attivo all'interno di una tabella figlio.  Si tratta dello stesso effetto del clic sul pulsante Indietro.|ALT\+freccia SINISTRA|  
|Espansione dei collegamenti della tabella figlio.  ALT\+freccia GIÙ per l'espansione di tutti i collegamenti, non solo quelli selezionati.|ALT\+freccia GIÙ o CTRL\+segno PIÙ|  
|Compressione dei collegamenti della tabella figlio.  ALT\+freccia SU per la compressione di tutti i collegamenti, non solo quelli selezionati.|ALT\+freccia SU o CTRL\+segno MENO|  
|Passaggio all'ultima cella non vuota in direzione della freccia.|CTRL\+freccia|  
|Estensione della selezione avanzando di una riga in direzione della freccia \(esclusi i collegamenti alle tabelle figlio\).|MAIUSC\+freccia SU\/GIÙ|  
|Estensione della selezione all'ultima riga non vuota in direzione della freccia \(esclusi i collegamenti alle tabelle figlio\).|CTRL\+MAIUSC\+freccia SU\/GIÙ|  
|Passaggio alla cella superiore sinistra.|CTRL\+HOME|  
|Passaggio alla cella inferiore destra.|CTRL\+FINE|  
|Estensione della selezione alla riga superiore.|CTRL\+MAIUSC\+HOME|  
|Estensione della selezione alla riga inferiore.|CTRL\+MAIUSC\+FINE|  
|Selezione della riga corrente \(esclusi i collegamenti alle tabelle figlio\).|MAIUSC\+BARRA SPAZIATRICE|  
|Selezione dell'intera griglia \(esclusi i collegamenti alle tabelle figlio\).|CTRL\+A|  
|Visualizzazione della riga padre dall'interno di una tabella figlio.|CTRL\+PGGIÙ|  
|Nascondere la riga padre dall'interno di una tabella figlio.|CTRL\+PGSU|  
|Estensione della selezione verso il basso avanzando di una schermata \(esclusi i collegamenti alle tabelle figlio\).|MAIUSC\+PGGIÙ|  
|Estensione della selezione verso l'alto avanzando di una schermata \(esclusi i collegamenti alle tabelle figlio\).|MAIUSC\+PGSU|  
|Chiamata del metodo <xref:System.Windows.Forms.DataGrid.EndEdit%2A> per la riga corrente.|CTRL\+INVIO|  
|Immissione di un valore <xref:System.DBNull.Value?displayProperty=fullName> in una cella in modalità di modifica.|CTRL\+0|  
  
## Vedere anche  
 [Cenni preliminari sul controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)