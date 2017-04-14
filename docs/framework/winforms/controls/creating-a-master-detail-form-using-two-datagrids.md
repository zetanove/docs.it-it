---
title: "Procedura dettagliata: creazione di un form Master-Details mediante due controlli DataGridView Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "02/15/2017"
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
  - "DataGridView (controllo) [Windows Form], master - dettagli (form)"
  - "Master-Details (elenchi), visualizzazione su Windows Form"
  - "padre-figlio (tabelle), visualizzazione su Windows Form"
  - "procedure dettagliate [Windows Form], DataGridView (controllo)"
ms.assetid: c5fa29e8-47f7-4691-829b-0e697a691f36
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura dettagliata: creazione di un form Master-Details mediante due controlli DataGridView Windows Form
Uno degli scenari più comuni per l'utilizzo del controllo <xref:System.Windows.Forms.DataGridView> è il form *Master\-Details*, in cui viene visualizzata una relazione padre\-figlio tra tabelle di database.  Selezionando righe nella tabella master, la tabella dettagli viene aggiornata con i corrispondenti dati figlio.  
  
 L'implementazione di un form Master\-Details è semplice con l'interazione tra il controllo <xref:System.Windows.Forms.DataGridView> e il componente <xref:System.Windows.Forms.BindingSource>.  In questa procedura dettagliata verrà compilato il form utilizzando due controlli <xref:System.Windows.Forms.DataGridView> e due componenti <xref:System.Windows.Forms.BindingSource>.  Nel form verranno visualizzate due tabelle correlate nel database di esempio Northwind SQL Server: `Customers` e `Orders`.  Al termine si disporrà di un form in cui vengono visualizzati tutti i clienti contenuti nel database nel controllo <xref:System.Windows.Forms.DataGridView> master e tutti gli ordini di un cliente selezionato nel controllo <xref:System.Windows.Forms.DataGridView> dettagli.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: creare un form Master\-Details mediante due controlli DataGridView di Windows Form](../../../../docs/framework/winforms/controls/create-a-master-detail-form-using-two-datagrids.md).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Accesso a un server che dispone del database di esempio di SQL Server, Northwind.  
  
## Creazione del form  
  
#### Per creare un form Master\-Details  
  
1.  Creare una classe che deriva da <xref:System.Windows.Forms.Form> e contiene due controlli <xref:System.Windows.Forms.DataGridView> e due componenti <xref:System.Windows.Forms.BindingSource>.  Il codice riportato di seguito fornisce l'inizializzazione di base del form e include un metodo `Main`.  Se si utilizza la finestra di progettazione [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] per creare il form, è possibile sfruttare il codice generato dalla finestra di progettazione invece di questo codice, tuttavia è necessario assicurarsi di utilizzare i nomi indicati nelle dichiarazioni di variabili descritte di seguito.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#02)]  
  
2.  Implementare un metodo nella definizione di classe del form per la gestione dei dettagli della connessione al database.  In questo esempio viene utilizzato un metodo `GetData` che compila un oggetto <xref:System.Data.DataSet>, aggiunge un oggetto <xref:System.Data.DataRelation> al dataset ed esegue l'associazione dei componenti <xref:System.Windows.Forms.BindingSource>.  Accertarsi di impostare la variabile `connectionString` su un valore appropriato per il database in uso.  
  
    > [!IMPORTANT]
    >  L'archiviazione delle informazioni riservate, ad esempio la password, nella stringa di connessione può avere implicazioni sulla sicurezza dell'applicazione.  L'autenticazione di Windows, detta anche sicurezza integrata, consente di controllare l'accesso a un database in modo più sicuro.  Per ulteriori informazioni, vedere [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#20)]  
  
3.  Implementare un gestore per l'evento <xref:System.Windows.Forms.Form.Load> del form che associa i controlli <xref:System.Windows.Forms.DataGridView> ai componenti <xref:System.Windows.Forms.BindingSource> e chiama il metodo `GetData`.  Nell'esempio riportato di seguito è incluso il codice che ridimensiona le colonne <xref:System.Windows.Forms.DataGridView> adattandole ai dati visualizzati.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#10)]  
  
## Verifica dell'applicazione  
 È ora possibile verificare il form per assicurarsi che funzioni correttamente.  
  
#### Per eseguire il test del form  
  
-   Compilare l'applicazione ed eseguirla.  
  
     Verranno visualizzati due controlli <xref:System.Windows.Forms.DataGridView>, disposti verticalmente.  Nella parte superiore vi sono i clienti della tabella `Customers` di Northwind, mentre nella parte inferiore vi sono gli ordini della tabella `Orders` corrispondenti al cliente selezionato.  Selezionando righe diverse nel controllo <xref:System.Windows.Forms.DataGridView> superiore, il contenuto del controllo <xref:System.Windows.Forms.DataGridView> inferiore varia contestualmente.  
  
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
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: creare un form Master\-Details mediante due controlli DataGridView di Windows Form](../../../../docs/framework/winforms/controls/create-a-master-detail-form-using-two-datagrids.md)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)