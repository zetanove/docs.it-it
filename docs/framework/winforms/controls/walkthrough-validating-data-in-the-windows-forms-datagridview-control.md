---
title: "Procedura dettagliata: convalida di dati nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "dati [Windows Form], convalida"
  - "griglie dei dati, convalida dei dati"
  - "convalida dei dati, Windows Form"
  - "DataGridView (controllo) [Windows Form], convalida dei dati"
  - "convalida dei dati, Windows Form"
  - "procedure dettagliate [Windows Form], DataGridView (controllo)"
ms.assetid: a4f1d015-2969-430c-8ea2-b612d179c290
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Procedura dettagliata: convalida di dati nel controllo DataGridView Windows Form
Quando la funzionalità di immissione dei dati viene resa disponibile agli utenti, è necessario che i dati immessi nel form vengano convalidati frequentemente.  La classe <xref:System.Windows.Forms.DataGridView> consente di eseguire agevolmente la convalida prima del commit dei dati nell'archivio dati.  È possibile convalidare i dati gestendo l'evento <xref:System.Windows.Forms.DataGridView.CellValidating>, generato dalla classe <xref:System.Windows.Forms.DataGridView> al variare della cella corrente.  
  
 In questa procedura dettagliata verranno recuperate righe dalla tabella `Customers` del database di esempio Northwind e verranno visualizzate in un controllo <xref:System.Windows.Forms.DataGridView>.  Quando un utente modifica una cella nella colonna `CompanyName` e prova a lasciare la cella, il gestore eventi <xref:System.Windows.Forms.DataGridView.CellValidating> esaminerà la nuova stringa del nome della società per accertarsi che non sia vuota. Se il nuovo valore è una stringa vuota, la classe <xref:System.Windows.Forms.DataGridView> impedirà al cursore dell'utente di lasciare la cella senza prima avere immesso una stringa non vuota.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: convalidare dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control.md).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Accesso a un server che dispone del database di esempio di SQL Server, Northwind.  
  
## Creazione del form  
  
#### Per convalidare i dati immessi in una classe DataGridView  
  
1.  Creare una classe che deriva da <xref:System.Windows.Forms.Form> e contiene un controllo <xref:System.Windows.Forms.DataGridView> e un componente <xref:System.Windows.Forms.BindingSource>.  
  
     L'esempio di codice riportato di seguito fornisce l'inizializzazione di base del form e include un metodo `Main`.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#02)]  
  
2.  Implementare un metodo nella definizione di classe del form per la gestione dei dettagli della connessione al database.  
  
     In questo esempio di codice viene utilizzato un metodo  `GetData` che restituisce un oggetto <xref:System.Data.DataTable> popolato.  Accertarsi di avere impostato la variabile `connectionString` su un valore appropriato per il database in uso.  
  
    > [!IMPORTANT]
    >  L'archiviazione delle informazioni riservate, ad esempio la password, nella stringa di connessione può avere implicazioni sulla sicurezza dell'applicazione.  L'autenticazione di Windows, detta anche sicurezza integrata, consente di controllare l'accesso a un database in modo più sicuro.  Per ulteriori informazioni, vedere [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#30)]  
  
3.  Implementare un gestore per l'evento <xref:System.Windows.Forms.Form.Load> del form che inizializza le classi <xref:System.Windows.Forms.DataGridView> e <xref:System.Windows.Forms.BindingSource> e configura l'associazione dei dati.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#10)]  
  
4.  Implementare i gestori per gli eventi <xref:System.Windows.Forms.DataGridView.CellValidating> e <xref:System.Windows.Forms.DataGridView.CellEndEdit> del controllo <xref:System.Windows.Forms.DataGridView>.  
  
     Il gestore eventi <xref:System.Windows.Forms.DataGridView.CellValidating> è l'elemento che consente di determinare se il valore di una cella nella colonna `CompanyName` è vuoto.  Se il valore della cella non supera la convalida, impostare la proprietà <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> della classe <xref:System.Windows.Forms.DataGridViewCellValidatingEventArgs?displayProperty=fullName> su `true`.  In questo modo, il controllo <xref:System.Windows.Forms.DataGridView> impedirà al cursore di lasciare la cella.  Impostare la proprietà <xref:System.Windows.Forms.DataGridViewRow.ErrorText%2A> della riga su una stringa descrittiva.  Verrà visualizzata un'icona di errore con una descrizione comandi contenente il testo dell'errore.  Nel gestore eventi <xref:System.Windows.Forms.DataGridView.CellEndEdit>, impostare la proprietà <xref:System.Windows.Forms.DataGridViewRow.ErrorText%2A> della riga sulla stringa vuota.  L'evento <xref:System.Windows.Forms.DataGridView.CellEndEdit> si verifica solo quando la cella esce dalla modalità di modifica. Ciò non avviene se la convalida non è riuscita.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#20)]  
  
## Verifica dell'applicazione  
 È ora possibile verificare il form per assicurarsi che funzioni correttamente.  
  
#### Per eseguire il test del form  
  
-   Compilare l'applicazione ed eseguirla.  
  
     Verrà visualizzato un controllo <xref:System.Windows.Forms.DataGridView> popolato con dati dalla tabella `Customers`.  Quando si fa doppio clic su una cella nella colonna `CompanyName`, è possibile modificare il valore.  Se si eliminano tutti i caratteri e si preme TAB per uscire dalla cella, il controllo <xref:System.Windows.Forms.DataGridView> ne impedisce l'uscita.  Quando si digita una stringa non vuota nella cella, il controllo <xref:System.Windows.Forms.DataGridView> consente di lasciare la cella.  
  
## Passaggi successivi  
 Questa applicazione fornisce un'idea di massima delle capacità del controllo <xref:System.Windows.Forms.DataGridView>.  È possibile personalizzare l'aspetto e il comportamento del controllo <xref:System.Windows.Forms.DataGridView> in diversi modi:  
  
-   Modificare gli stili di bordi e intestazioni.  Per ulteriori informazioni, vedere [Procedura: modificare gli stili dei bordi e delle linee della griglia nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md).  
  
-   Consentire o limitare l'input utente nel controllo <xref:System.Windows.Forms.DataGridView>.  Per ulteriori informazioni, vedere [Procedura: impedire l'aggiunta o l'eliminazione di righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md) e [Procedura: impostare le colonne come in sola lettura nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md).  
  
-   Verificare eventuali errori relativi al database nell'input utente.  Per ulteriori informazioni, vedere [Procedura dettagliata: gestione degli errori che si verificano durante l'immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/handling-errors-that-occur-during-data-entry-in-the-datagrid.md).  
  
-   Gestire dataset di grandi dimensioni utilizzando la modalità virtuale.  Per ulteriori informazioni, vedere [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
-   Personalizzare l'aspetto delle celle.  Per ulteriori informazioni, vedere [Procedura: personalizzare l'aspetto delle celle nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md) e [Procedura: impostare gli stili di carattere e colore nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [Immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [Procedura: convalidare dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura dettagliata: gestione degli errori che si verificano durante l'immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/handling-errors-that-occur-during-data-entry-in-the-datagrid.md)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)