---
title: "Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "dati [Windows Form], gestione di set di dati di grandi dimensioni"
  - "DataGridView (controllo) [Windows Form], set di dati di grandi dimensioni"
  - "DataGridView (controllo) [Windows Form], modalità virtuale"
  - "esempi [Windows Form], caricamento di dati JIT"
  - "caricamento di dati JIT"
  - "modalità virtuale, caricamento di dati JIT"
ms.assetid: c2a052b9-423c-4ff7-91dc-d8c7c79345f6
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form
Uno dei motivi alla base dell'implementazione del modo virtuale nel controllo <xref:System.Windows.Forms.DataGridView> è quello di recuperare i dati solo secondo le necessità.  Questa operazione è detta *caricamento dati JIT*.  
  
 Se si utilizza una tabella di grandi dimensioni in un database remoto, ad esempio, è possibile evitare i ritardi di avvio mediante il recupero solo dei dati necessari per la visualizzazione e il recupero di dati aggiuntivi solo quando l'utente visualizza nuove righe durante lo scorrimento.  Se sui computer client su cui è in esecuzione l'applicazione è disponibile una quantità di memoria limitata per l'archiviazione dei dati, è inoltre possibile scartare i dati inutilizzati quando si recuperano nuovi valori dal database.  
  
 Nelle sezioni seguenti viene descritto come utilizzare un controllo <xref:System.Windows.Forms.DataGridView> con una cache JIT.  
  
 Per copiare il codice in questo argomento sotto forma di elenco unico, vedere [Procedura: implementare la modalità virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md).  
  
## Form  
 Nell'esempio di codice seguente viene definito un form contenente un controllo <xref:System.Windows.Forms.DataGridView> di sola lettura che interagisce con un oggetto `Cache` tramite un gestore eventi <xref:System.Windows.Forms.DataGridView.CellValueNeeded>.  L'oggetto `Cache` gestisce i valori archiviati localmente e utilizza un oggetto `DataRetriever` per recuperare i valori dalla tabella Orders del database Northwind di esempio.  L'oggetto `DataRetriever`, che implementa l'interfaccia `IDataPageRetriever` richiesta dalla classe `Cache`, viene inoltre utilizzato per inizializzare le righe e le colonne del controllo <xref:System.Windows.Forms.DataGridView>.  
  
 I tipi `IDataPageRetriever`, `DataRetriever` e `Cache` vengono descritti più avanti in questo argomento.  
  
> [!NOTE]
>  L'archiviazione delle informazioni riservate, ad esempio la password, nella stringa di connessione può avere implicazioni sulla sicurezza dell'applicazione.  L'autenticazione di Windows, detta anche sicurezza integrata, consente di controllare l'accesso a un database in modo più sicuro.  Per ulteriori informazioni, vedere [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#100)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#100)]  
  
## Interfaccia IDataPageRetriever  
 Nell'esempio di codice seguente viene definita l'interfaccia `IDataPageRetriever`, che viene implementata dalla classe `DataRetriever`.  L'unico metodo dichiarato in questa interfaccia è il metodo `SupplyPageOfData`, che richiede un indice di riga iniziale e un conteggio del numero di righe in un'unica pagina di dati.  Questi valori vengono utilizzati dall'implementatore per recuperare un sottoinsieme di dati da un'origine dati.  
  
 Un oggetto `Cache` utilizza un'implementazione di questa interfaccia durante la costruzione per caricare due pagine iniziali di dati.  Ogni volta che è necessario un valore non memorizzato nella cache, la cache scarta una di queste pagine e richiede una nuova pagina contenente il valore dall'interfaccia `IDataPageRetriever`.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#201](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#201)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#201](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#201)]  
  
## Classe DataRetriever  
 Nell'esempio di codice seguente viene definita la classe `DataRetriever`, che implementa l'interfaccia `IDataPageRetriever` per recuperare le pagine di dati da un server.  La classe `DataRetriever` comprende inoltre le proprietà `Columns` e `RowCount`, che il controllo <xref:System.Windows.Forms.DataGridView> utilizza per creare le colonne necessarie e per aggiungere il numero corretto di righe vuote alla raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A>.  L'aggiunta di righe vuote è necessaria affinché il controllo si comporti come se contenesse tutti i dati della tabella.  Ciò significa che la casella di scorrimento nella barra di scorrimento avrà le dimensioni corrette e l'utente sarà in grado di accedere a qualsiasi riga nella tabella.  Le righe vengono compilate dal gestore eventi <xref:System.Windows.Forms.DataGridView.CellValueNeeded> solo quando vengono visualizzate durante lo scorrimento.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#200](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#200)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#200](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#200)]  
  
## Classe Cache  
 Nell'esempio di codice seguente viene definita la classe `Cache`, che gestisce due pagine di dati compilate tramite un'implementazione dell'interfaccia `IDataPageRetriever`.  La classe `Cache` definisce una struttura `DataPage` interna, che contiene una classe <xref:System.Data.DataTable> per l'archiviazione dei valori in un'unica pagina di cache e che calcola gli indici di riga che rappresentano i limiti superiore e inferiore della pagina.  
  
 La classe `Cache` carica due pagine di dati in fase di costruzione.  Ogni volta che l'evento <xref:System.Windows.Forms.DataGridView.CellValueNeeded> richiede un valore, l'oggetto `Cache` verifica se il valore è disponibile in una delle due pagine e, in caso positivo, lo restituisce.  Se il valore non è disponibile localmente, l'oggetto `Cache` determina quale delle due pagine è la più lontana dalle righe visualizzate e la sostituisce con una nuova contenente il valore richiesto, che quindi restituisce.  
  
 Se si presuppone che il numero di righe in una pagina di dati corrisponda al numero di righe che possono essere visualizzate contemporaneamente sullo schermo, questo modello consente agli utenti che scorrono le pagine della tabella di restituire in modo efficiente la pagina visualizzata più di recente.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#300](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#300)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#300](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#300)]  
  
## Considerazioni aggiuntive  
 Gli esempi di codice precedenti vengono forniti per illustrare il caricamento dati JIT.  Per la massima efficienza è necessario modificare il codice in base alle esigenze.  Come minimo è necessario scegliere un valore appropriato per il numero di righe per pagina di dati nella cache.  Questo valore viene passato al costruttore `Cache`.  Il numero di righe per pagina non deve essere inferiore al numero di righe che possono essere visualizzate contemporaneamente nel controllo <xref:System.Windows.Forms.DataGridView>.  
  
 Per risultati ottimali è necessario eseguire la verifica delle prestazioni e dell'utilizzabilità per determinare i requisiti del sistema e degli utenti.  Tra i diversi fattori che è necessario prendere in considerazione figurano la quantità di memoria sui computer client su cui è in esecuzione l'applicazione, la larghezza di banda disponibile della connessione di rete utilizzata e la latenza del server in uso.  La larghezza di banda e la latenza vanno determinate in condizioni di picco.  
  
 Per migliorare le prestazioni di scorrimento dell'applicazione, è necessario aumentare la quantità di dati archiviati localmente.  Per migliorare i tempi di avvio, tuttavia, si consiglia di evitare di caricare troppi dati inizialmente.  È possibile modificare la classe `Cache` per aumentare il numero di pagine di dati archiviabili.  Se si utilizzano più pagine di dati, è possibile migliorare le prestazioni di scorrimento, ma è necessario determinare il numero ideale di righe in una pagina di dati a seconda della larghezza di banda disponibile e della latenza del server.  Nel caso delle pagine più piccole l'accesso al server è più frequente, ma il server impiega meno tempo a restituire i dati richiesti.  Se la latenza è più problematica rispetto alla larghezza di banda, è possibile utilizzare pagine di dati più grandi.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>   
 [Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [Modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)   
 [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)   
 [Procedura: implementare la modalità virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)