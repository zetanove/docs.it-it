---
title: "Procedura dettagliata: gestione degli errori che si verificano durante l&#39;immissione di dati nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "immissione di dati, gestione errori"
  - "griglie dei dati, gestione errori"
  - "DataGridView (controllo) [Windows Form], gestione errori"
  - "gestione errori, immissione di dati"
  - "gestione errori, DataGridView (controllo)"
  - "procedure dettagliate [Windows Form], DataGridView (controllo)"
ms.assetid: 30a68b85-d3af-4946-83c1-1e2d010d0511
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura dettagliata: gestione degli errori che si verificano durante l&#39;immissione di dati nel controllo DataGridView Windows Form
La gestione degli errori derivanti dall'archivio dati sottostante è una funzionalità necessaria per un'applicazione di immissione dati.  Il controllo <xref:System.Windows.Forms.DataGridView> di Windows Form semplifica questa attività esponendo l'evento <xref:System.Windows.Forms.DataGridView.DataError>, che viene generato quando nell'archivio dati viene rilevata una violazione dei vincoli o di una regola business.  
  
 In questa procedura dettagliata verranno recuperate righe dalla tabella `Customers` del database di esempio Northwind e verranno visualizzate in un controllo <xref:System.Windows.Forms.DataGridView>.  Quando viene rilevato un valore di riga duplicata `CustomerID` in una nuova riga o in una riga già presente e modificata, viene generato l'evento <xref:System.Windows.Forms.DataGridView.DataError>, la cui gestione è possibile mediante la visualizzazione della classe <xref:System.Windows.Forms.MessageBox> in cui è descritta l'eccezione.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: gestire gli errori che si verificano durante l'immissione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/handle-errors-that-occur-during-data-entry-in-the-datagrid.md).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Accesso a un server che dispone del database di esempio di SQL Server, Northwind.  
  
## Creazione del form  
  
#### Per gestire gli errori di immissione dei dati nel controllo DataGridView  
  
1.  Creare una classe che deriva da <xref:System.Windows.Forms.Form> e contiene un controllo <xref:System.Windows.Forms.DataGridView> e un componente <xref:System.Windows.Forms.BindingSource>.  
  
     L'esempio di codice riportato di seguito fornisce l'inizializzazione di base del form e include un metodo `Main`.  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridView.DataError#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#02)]  
  
2.  Implementare un metodo nella definizione di classe del form per la gestione dei dettagli della connessione al database.  
  
     In questo esempio di codice viene utilizzato un metodo  `GetData` che restituisce un oggetto <xref:System.Data.DataTable> popolato.  Accertarsi di avere impostato la variabile `connectionString` su un valore appropriato per il database in uso.  
  
    > [!IMPORTANT]
    >  L'archiviazione delle informazioni riservate, ad esempio la password, nella stringa di connessione può avere implicazioni sulla sicurezza dell'applicazione.  L'autenticazione di Windows, detta anche sicurezza integrata, consente di controllare l'accesso a un database in modo più sicuro.  Per ulteriori informazioni, vedere [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#30)]  
  
3.  Implementare un gestore per l'evento <xref:System.Windows.Forms.Form.Load> del form che inizializza le classi <xref:System.Windows.Forms.DataGridView> e <xref:System.Windows.Forms.BindingSource> e configura l'associazione dei dati.  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#10)]  
  
4.  Gestire l'evento <xref:System.Windows.Forms.DataGridView.DataError> nella classe <xref:System.Windows.Forms.DataGridView>.  
  
     Se il contesto dell'errore è un'operazione di commit, visualizzare l'errore in una classe <xref:System.Windows.Forms.MessageBox>.  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#20)]  
  
## Verifica dell'applicazione  
 È ora possibile verificare il form per assicurarsi che funzioni correttamente.  
  
#### Per eseguire il test del form  
  
-   ‎Premere F5 per eseguire l'applicazione.  
  
     Verrà visualizzato un controllo <xref:System.Windows.Forms.DataGridView> in cui sono presenti i dati della tabella Customers.  Se si inserisce un valore duplicato per `CustomerID` e si esegue il commit della modifica, il valore della cella verrà annullato automaticamente e verrà visualizzata una classe <xref:System.Windows.Forms.MessageBox> in cui è presente l'errore di immissione dati.  
  
## Passaggi successivi  
 Questa applicazione fornisce un'idea di massima delle capacità del controllo <xref:System.Windows.Forms.DataGridView>.  È possibile personalizzare l'aspetto e il comportamento del controllo <xref:System.Windows.Forms.DataGridView> in diversi modi:  
  
-   Modificare gli stili di bordi e intestazioni.  Per ulteriori informazioni, vedere [Procedura: modificare gli stili dei bordi e delle linee della griglia nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md).  
  
-   Consentire o limitare l'input utente nel controllo <xref:System.Windows.Forms.DataGridView>.  Per ulteriori informazioni, vedere [Procedura: impedire l'aggiunta o l'eliminazione di righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md) e [Procedura: impostare le colonne come in sola lettura nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md).  
  
-   Convalidare l'input utente nel controllo <xref:System.Windows.Forms.DataGridView>.  Per ulteriori informazioni, vedere [Procedura dettagliata: convalida di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/walkthrough-validating-data-in-the-windows-forms-datagridview-control.md).  
  
-   Gestire dataset di grandi dimensioni utilizzando la modalità virtuale.  Per ulteriori informazioni, vedere [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
-   Personalizzare l'aspetto delle celle.  Per ulteriori informazioni, vedere [Procedura: personalizzare l'aspetto delle celle nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md) e [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [Immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [Procedura: gestire gli errori che si verificano durante l'immissione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/handle-errors-that-occur-during-data-entry-in-the-datagrid.md)   
 [Procedura dettagliata: convalida di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)