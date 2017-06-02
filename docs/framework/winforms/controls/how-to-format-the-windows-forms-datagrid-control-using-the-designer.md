---
title: "Procedura: formattare il controllo DataGrid Windows Form mediante la finestra di progettazione | Microsoft Docs"
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
  - "colori, applicazione a controlli DataGrid"
  - "colonne [Windows Form], controlli DataGrid"
  - "DataGrid (controllo) [Windows Form], stili predefiniti"
  - "DataGrid (controllo) [Windows Form], formattazione"
  - "formattazione [Windows Form]"
  - "tabelle [Windows Form], formattazione nel controllo DataGrid"
ms.assetid: 533b9814-6124-49dc-9fda-085f1502609f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: formattare il controllo DataGrid Windows Form mediante la finestra di progettazione
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 L'utilizzo di colori diversi per le parti di un controllo <xref:System.Windows.Forms.DataGrid> può contribuire ad agevolare la lettura e l'interpretazione delle informazioni in esso contenute.  È possibile applicare i colori alle righe e alle colonne.  La visualizzazione delle righe e delle colonne può inoltre essere attivata o disattivata a discrezione dell'utente.  
  
 La formattazione del controllo <xref:System.Windows.Forms.DataGrid> è caratterizzata da tre aspetti di base:  
  
-   È possibile impostare proprietà per stabilire uno stile predefinito da utilizzare per la visualizzazione dei dati.  
  
-   A partire da tale base, è quindi possibile personalizzare l'aspetto di alcune tabelle visualizzate in fase di esecuzione.  
  
-   È infine possibile modificare le colonne da visualizzare nella griglia dei dati, nonché i colori e gli altri attributi di formattazione.  
  
 Il primo passaggio per la formattazione di una griglia dei dati può prevedere l'impostazione delle proprietà del controllo <xref:System.Windows.Forms.DataGrid>.  Le selezioni relative al colore e al formato costituiscono la base di partenza per apportare modifiche sulla base delle tabelle e delle colonne dati visualizzate.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGrid>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  Per impostazione predefinita, in [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] il controllo <xref:System.Windows.Forms.DataGrid> non si trova nella **Casella degli strumenti**.  Per ulteriori informazioni, vedere [How to: Add Items to the Toolbox](http://msdn.microsoft.com/it-it/458e119e-17fe-450b-b889-e31c128bd7e0).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per stabilire uno stile predefinito per il controllo DataGrid  
  
1.  Fare clic sul controllo <xref:System.Windows.Forms.DataGrid>.  
  
2.  Nella finestra **Proprietà** impostare le proprietà indicate di seguito in base alle esigenze.  
  
    |Proprietà|Descrizione|  
    |---------------|-----------------|  
    |<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>|La proprietà `BackColor` consente di definire il colore delle righe pari della griglia.  Quando si imposta la proprietà <xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A> su un colore diverso, tutte le righe dispari vengono impostate sul nuovo colore \(righe 1, 3, 5 e così via\).|  
    |<xref:System.Windows.Forms.DataGrid.BackColor%2A>|Colore di sfondo delle righe pari della griglia \(righe 0, 2, 4, 6 e così via\).|  
    |<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>|Mentre le proprietà <xref:System.Windows.Forms.DataGrid.BackColor%2A> e <xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A> determinano il colore delle righe della griglia, la proprietà <xref:System.Windows.Forms.DataGrid.BackgroundColor%2A> consente di stabilire il colore dell'area esterna a quella delle righe, visibile solo quando si scorre la griglia fino alla fine, oppure se la griglia comprende solo poche righe.|  
    |<xref:System.Windows.Forms.DataGrid.BorderStyle%2A>|Stile del bordo della griglia; uno dei valori di enumerazione di <xref:System.Windows.Forms.BorderStyle>.|  
    |<xref:System.Windows.Forms.DataGrid.CaptionBackColor%2A>|Colore di sfondo della didascalia della finestra della griglia, visualizzata appena sopra la griglia.|  
    |<xref:System.Windows.Forms.DataGrid.CaptionFont%2A>|Carattere della didascalia nella parte superiore della griglia.|  
    |<xref:System.Windows.Forms.DataGrid.CaptionForeColor%2A>|Colore di sfondo della didascalia della finestra della griglia.|  
    |<xref:System.Windows.Forms.Control.Font%2A>|Carattere utilizzato per visualizzare il testo nella griglia.|  
    |<xref:System.Windows.Forms.DataGrid.ForeColor%2A>|Colore del carattere utilizzato per la visualizzazione dei dati nelle righe della griglia.|  
    |<xref:System.Windows.Forms.DataGrid.GridLineColor%2A>|Colore delle linee della griglia dei dati.|  
    |<xref:System.Windows.Forms.DataGrid.GridLineStyle%2A>|Stile delle linee di separazione delle celle nella griglia; uno dei valori di enumerazione di <xref:System.Windows.Forms.DataGridLineStyle>.|  
    |<xref:System.Windows.Forms.DataGrid.HeaderBackColor%2A>|Colore di sfondo delle intestazioni di riga e colonna.|  
    |<xref:System.Windows.Forms.DataGrid.HeaderFont%2A>|Carattere utilizzato per le intestazioni di colonna.|  
    |<xref:System.Windows.Forms.DataGrid.HeaderForeColor%2A>|Colore di primo piano delle intestazioni di colonna della griglia, compreso il testo dell'intestazione e i segni più \(\+\) e meno \(\-\) che consentono di espandere e comprimere le righe quando vengono visualizzate più tabelle correlate.|  
    |<xref:System.Windows.Forms.DataGrid.LinkColor%2A>|Colore del testo di tutti i collegamenti presenti nella griglia dei dati, compresi quelli alle tabelle figlio, al nome della relazione e così via.|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsBackColor%2A>|Colore di sfondo delle righe padre in una tabella figlio.|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsForeColor%2A>|Colore di primo piano delle righe padre in una tabella figlio.|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsLabelStyle%2A>|Consente di stabilire se i nomi della tabella e delle colonne vengono visualizzati nella riga padre tramite l'enumerazione <xref:System.Windows.Forms.DataGridParentRowsLabelStyle>.|  
    |<xref:System.Windows.Forms.DataGrid.PreferredColumnWidth%2A>|Larghezza predefinita \(in pixel\) delle colonne della griglia.  Impostare questa proprietà prima di reimpostare le proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A> e <xref:System.Windows.Forms.DataGrid.DataMember%2A> \(singolarmente o tramite il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>\). In caso contrario, la proprietà non avrà effetto.<br /><br /> Specificare un valore superiore a 0.|  
    |<xref:System.Windows.Forms.DataGrid.PreferredRowHeight%2A>|Altezza predefinita \(in pixel\) delle righe della griglia.  Impostare questa proprietà prima di reimpostare le proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A> e <xref:System.Windows.Forms.DataGrid.DataMember%2A> \(singolarmente o tramite il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>\). In caso contrario, la proprietà non avrà effetto.<br /><br /> Specificare un valore superiore a 0.|  
    |<xref:System.Windows.Forms.DataGrid.RowHeaderWidth%2A>|Larghezza delle intestazioni di riga della griglia.|  
    |<xref:System.Windows.Forms.DataGrid.SelectionBackColor%2A>|Colore di sfondo quando si seleziona una cella o una riga.|  
    |<xref:System.Windows.Forms.DataGrid.SelectionForeColor%2A>|Colore di primo piano quando si seleziona una cella o una riga.|  
  
    > [!NOTE]
    >  Durante la personalizzazione dei colori dei controlli, il controllo potrebbe risultare inaccessibile se il numero di colori disponibili è limitato, ad esempio a rosso e verde.  Per ovviare a questo problema, utilizzare i colori disponibili nella tavolozza **Colori di sistema**.  
  
     Nella seguente procedura è richiesto un controllo <xref:System.Windows.Forms.DataGrid> associato a una tabella di dati.  Per ulteriori informazioni, vedere [Procedura: associare il controllo DataGrid Windows Form a un'origine dati](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md).  
  
### Per impostare lo stile di tabella e colonna di una tabella dati in fase di progettazione  
  
1.  Selezionare il controllo <xref:System.Windows.Forms.DataGrid> nel form.  
  
2.  Nella finestra **Proprietà**, selezionare la proprietà <xref:System.Windows.Forms.DataGrid.TableStyles%2A> e fare clic sul pulsante con i **puntini di sospensione** \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\).  
  
3.  Nella finestra **Editor della raccolta DataGridTableStyle** fare clic su **Aggiungi** per aggiungere uno stile di tabella alla raccolta.  
  
     Con l'**Editor della raccolta DataGridTableStyle** è possibile aggiungere e rimuovere stili di tabella, impostare proprietà relative alla visualizzazione e al layout, nonché impostare il nome di mapping per gli stili di tabella.  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> sul nome di mapping di ciascuno stile di tabella.  
  
     Il nome di mapping viene utilizzato per specificare lo stile da utilizzare con ogni singola tabella.  
  
5.  Nell'**Editor della raccolta DataGridTableStyle** selezionare la proprietà <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> e fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\).  
  
6.  Nella finestra **Editor della raccolta DataGridColumnStyle** aggiungere gli stili di colonna allo stile di tabella creato.  
  
     Con l'**Editor della raccolta DataGridColumnStyle** è possibile aggiungere e rimuovere stili di colonna, impostare proprietà relative alla visualizzazione e al layout, nonché impostare il nome di mapping e le stringhe di formattazione per le colonne dei dati.  
  
    > [!NOTE]
    >  Per ulteriori informazioni sulla stringhe di formattazione, vedere [Formattazione di tipi](../../../../docs/standard/base-types/formatting-types.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.GridTableStylesCollection>   
 <xref:System.Windows.Forms.GridColumnStylesCollection>   
 <xref:System.Windows.Forms.DataGrid>   
 [Procedura: eliminare o nascondere colonne nel controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)   
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)