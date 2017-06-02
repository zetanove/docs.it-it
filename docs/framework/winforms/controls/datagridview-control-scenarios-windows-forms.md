---
title: "Scenari del controllo DataGridView (Windows Form) | Microsoft Docs"
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
  - "dati [Windows Form], visualizzazione in formato tabella"
  - "griglie dei dati, informazioni sulle griglie dei dati"
  - "DataGridView (controllo) [Windows Form], scenari"
ms.assetid: 09a5fd05-3447-47ec-a4ec-6082a2b7f0dd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Scenari del controllo DataGridView (Windows Form)
Con il controllo <xref:System.Windows.Forms.DataGridView> è possibile visualizzare i dati in formato tabulare da una serie di origini dati.  Per le operazioni semplici, è possibile inserire manualmente i dati all'interno della classe <xref:System.Windows.Forms.DataGridView> e modificarli direttamente mediante il controllo.  In genere, tuttavia, verranno memorizzati dati in un'origine dati esterna e il controllo verrà associato tramite il componente <xref:System.Windows.Forms.BindingSource>.  
  
 In questo argomento vengono descritti alcuni scenari comuni che comportano l'impiego del controllo <xref:System.Windows.Forms.DataGridView>.  
  
## Scenario 1: visualizzazione di piccole quantità di dati  
 Non è necessario memorizzare i dati in un'origine dati esterna per visualizzarli all'interno del controllo <xref:System.Windows.Forms.DataGridView>.  Se si utilizza una piccola quantità di dati, è possibile popolare il controllo manualmente e modificare i dati tramite il controllo.  Questo meccanismo è denominato *modalità svincolata*.  Per ulteriori informazioni, vedere [Procedura: creare un controllo DataGridView di Windows Form non associato](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md).  
  
### Punti chiave dello scenario  
  
-   Nella modalità svincolata, il controllo viene popolato manualmente.  
  
-   La modalità svincolata è particolarmente adatta per piccole quantità di dati in sola lettura.  
  
-   Tale modalità è anche adatta per tabelle simili a fogli di calcolo o tabelle con un numero limitato di dati.  
  
## Scenario 2: visualizzazione e aggiornamento dei dati memorizzati in un'origine dati esterna  
 È possibile utilizzare il controllo <xref:System.Windows.Forms.DataGridView> come interfaccia utente tramite cui gli utenti possono accedere ai dati presenti in un'origine dati come una tabella di database o una raccolta di oggetti business.  Per ulteriori informazioni, vedere [Procedura: associare dati al controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md).  
  
### Punti chiave dello scenario  
  
-   La modalità associata consente di eseguire la connessione a un'origine dati, la generazione automatica di colonne sulla base delle proprietà dell'origine dati o di colonne del database e l'inserimento automatico di dati nel controllo.  
  
-   La modalità associata è adatta nei casi di stretta interazione dell'utente con i dati.  I dati possono essere formattati per la visualizzazione e i dati specificati dall'utente possono essere analizzati nel formato previsto nell'origine dati.  È possibile rilevare gli errori di formattazione nell'immissione dei dati e gli errori derivanti da vincoli del database in modo che gli utenti possano essere avvertiti e sia possibile correggere le celle in cui si è verificato l'errore.  
  
-   Funzionalità aggiuntive come l'ordinamento, il blocco e il riordinamento delle colonne consentono agli utenti di visualizzare i dati nel modo più idoneo per il loro flusso di lavoro.  
  
-   Il supporto per gli Appunti consente agli utenti di copiare i dati dalle applicazioni in altre applicazioni.  
  
## Scenario 3: dati avanzati  
 Se non è possibile soddisfare esigenze speciali mediante il modello standard di associazione dati, è possibile gestire l'interazione tra il controllo e i dati implementando la *modalità virtuale*.  L'implementazione della modalità virtuale è l'implementazione di uno o più gestori eventi che consentono al controllo di richiedere informazioni sulle celle quando tali informazioni sono necessarie.  
  
 Ad esempio, se si utilizzano grandi quantità di dati, è possibile implementare la modalità virtuale per garantire un livello ottimale di efficacia.  La modalità virtuale è anche utile per mantenere i valori delle colonne non associate visualizzate con le colonne recuperate da un'altra origine dati.  
  
 Per ulteriori informazioni sulla modalità virtuale, vedere [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
### Punti chiave dello scenario  
  
-   La modalità virtuale è adatta per la visualizzazione di quantità di dati molto grandi quando è necessario ottimizzare le prestazioni.  
  
## Scenario 4: ridimensionamento automatico di righe e colonne  
 Quando si visualizzano dati aggiornati regolarmente, è possibile ridimensionare automaticamente righe e colonne per accertarsi che tutto il contenuto sia visibile.  Il controllo <xref:System.Windows.Forms.DataGridView> fornisce diverse opzioni che consentono di attivare o disabilitare il ridimensionamento manuale, eseguire il ridimensionamento a livello di codice a una data\/ora specifica oppure ogni volta che il contenuto cambia.  Per ulteriori informazioni, vedere [Opzioni di ridimensionamento nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md).  
  
### Punti chiave dello scenario  
  
-   Il ridimensionamento manuale consente agli utenti di regolare l'altezza e la larghezza delle celle.  
  
-   Il ridimensionamento automatico consente di gestire le dimensioni delle celle in modo che il contenuto non venga tagliato.  
  
-   Il ridimensionamento a livello di codice consente di ridimensionare le celle a una data\/ora specifica per evitare la riduzione delle prestazioni dovuta al continuo ridimensionamento automatico.  
  
## Scenario 5: personalizzazione semplice  
 Il controllo <xref:System.Windows.Forms.DataGridView> fornisce molti modi per modificare il relativo aspetto e il comportamento di base.  Per ulteriori informazioni, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
### Punti chiave dello scenario  
  
-   Mediante gli oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> è possibile fornire informazioni sul colore, il tipo di carattere, la formattazione e il posizionamento a più livelli e per singoli elementi del controllo.  
  
-   Gli stili delle celle possono essere suddivisi in livelli e condivisi tra più elementi, consentendo il riutilizzo del codice.  
  
## Scenario 6: personalizzazione avanzata  
 Il controllo <xref:System.Windows.Forms.DataGridView> fornisce molti modi per personalizzare il relativo aspetto e il comportamento.  
  
### Punti chiave dello scenario  
  
-   È possibile fornire codice per il disegno della cella personalizzata.  Per ulteriori informazioni, vedere [Procedura: personalizzare l'aspetto delle celle nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md).  
  
-   È possibile fornire il disegno della riga personalizzata.  Questa caratteristica è utile, ad esempio, per creare righe il cui contenuto si estende su più colonne.  Per ulteriori informazioni, vedere [Procedura: personalizzare l'aspetto delle righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md).  
  
-   È possibile implementare classi personalizzate di celle e colonne per personalizzare l'aspetto delle celle.  Per ulteriori informazioni, vedere [Procedura: personalizzare celle e colonne nel controllo DataGridView di Windows Form estendendone il comportamento e l'aspetto](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md).  
  
-   È possibile implementare classi personalizzate di celle e colonne per l'inserimento di controlli diversi da quelli forniti dai tipi di colonne incorporati.  Per ulteriori informazioni, vedere [Procedura: inserire controlli in celle del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Cenni preliminari sul controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)