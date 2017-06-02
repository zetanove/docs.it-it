---
title: "Opzioni di ridimensionamento nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "griglie dei dati, ridimensionamento di colonne"
  - "griglie dei dati, ridimensionamento di righe"
  - "griglie dei dati, opzioni di ridimensionamento"
  - "DataGridView (controllo) [Windows Form], ridimensionamento di colonne"
  - "DataGridView (controllo) [Windows Form], ridimensionamento di righe"
  - "DataGridView (controllo) [Windows Form], opzioni di ridimensionamento"
ms.assetid: a5620a9c-0d06-41e3-8934-c25ddb16c9e6
caps.latest.revision: 29
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# Opzioni di ridimensionamento nel controllo DataGridView Windows Form
Le dimensioni di righe, colonne e intestazioni del controllo <xref:System.Windows.Forms.DataGridView> possono variare in seguito a diverse occorrenze.  Tali occorrenze sono illustrate nella tabella che segue.  
  
|Occorrenza|Descrizione|  
|----------------|-----------------|  
|Ridimensionamento effettuato dall'utente|Gli utenti possono effettuare ridimensionamenti trascinando o facendo doppio clic sui divisori di righe, colonne o intestazioni.|  
|Ridimensionamento dei controlli|In modalità di riempimento di colonna, la larghezza delle colonne cambia al variare della larghezza del controllo, ad esempio quando il controllo è ancorato al form padre e l'utente ridimensiona il form.|  
|Modifica del valore della cella|Nelle modalità di ridimensionamento automatico basato sul contenuto, le dimensioni variano in funzione dei nuovi valori visualizzati.|  
|Chiamata ai metodi|Il ridimensionamento in base al contenuto a livello di codice consente di effettuare ridimensionamenti opportunistici in base ai valori delle celle al momento della chiamata ai metodi.|  
|Impostazione di proprietà|È possibile anche impostare valori specifici di altezza e larghezza.|  
  
 Per impostazione predefinita, è abilitato il ridimensionamento effettuato dall'utente, è disabilitato il ridimensionamento automatico e i valori delle celle più ampi delle rispettive colonne vengono troncati.  
  
 Nella tabella seguente sono illustrati gli scenari utilizzabili per adattare il comportamento predefinito o utilizzare specifiche opzioni di ridimensionamento per ottenere effetti particolari.  
  
|Scenario|Implementazione|  
|--------------|---------------------|  
|Utilizzare la modalità di riempimento di colonna per visualizzare dati di dimensioni simili in un numero di colonne relativamente ridotto che occupa l'intera larghezza del controllo senza visualizzare la barra di scorrimento orizzontale.|Impostare la proprietà <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>.|  
|Utilizzare la modalità di riempimento di colonna con valori visualizzati di dimensioni diverse.|Impostare la proprietà <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>.  Inizializzare la larghezza relativa delle colonne impostando le proprietà <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> delle colonne o chiamando il metodo <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> del controllo dopo aver popolato il controllo con i dati.|  
|Utilizzare la modalità di riempimento di colonna con valori di importanza diversa.|Impostare la proprietà <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>.  Impostare valori ampi per la proprietà <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> delle colonne in cui devono sempre essere visualizzati dei dati o utilizzare un'opzione di ridimensionamento diversa dalla modalità di riempimento per colonne specifiche.|  
|Utilizzare la modalità di riempimento di colonna per evitare la visualizzazione dello sfondo del controllo.|Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> dell'ultima colonna su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> e utilizzare altre opzioni di ridimensionamento per le altre colonne.  Se le altre colonne utilizzano una quantità eccessiva dello spazio disponibile, impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> dell'ultima colonna.|  
|Visualizzare una colonna di larghezza fissa, ad esempio una colonna di icone o di ID.|Impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> su <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> e la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> su <xref:System.Windows.Forms.DataGridViewTriState> per la colonna.  Inizializzare la larghezza della colonna impostando la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> o chiamando il metodo <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A> del controllo dopo aver popolato il controllo con i dati.|  
|Adattare automaticamente le dimensioni ogni volta che varia il contenuto delle celle per evitarne il troncamento e ottimizzare l'utilizzo dello spazio.|Impostare una proprietà di ridimensionamento automatico su un valore che rappresenta una modalità di ridimensionamento basato sul contenuto.  Per evitare una riduzione delle prestazioni durante l'utilizzo di grandi quantità di dati, utilizzare una modalità di ridimensionamento che prenda in considerazione solo le righe visualizzate.|  
|Adattare le dimensioni ai valori nelle righe visualizzate per evitare riduzioni di prestazioni con un numero di righe elevato.|Utilizzare i valori di enumerazione appropriati della modalità di ridimensionamento automatico o a livello di codice.  Per adattare le dimensioni ai valori nelle righe appena visualizzate durante lo scorrimento, effettuare una chiamata a un metodo di ridimensionamento in un gestore eventi <xref:System.Windows.Forms.DataGridView.Scroll>.  Per personalizzare il ridimensionamento con doppio clic in modo da determinare le nuove dimensioni solo con i valori nelle righe visualizzate, effettuare una chiamata a un metodo di ridimensionamento in un gestore eventi <xref:System.Windows.Forms.DataGridView.RowDividerDoubleClick> o <xref:System.Windows.Forms.DataGridView.ColumnDividerDoubleClick>.|  
|Adattare le dimensioni al contenuto delle celle solo in specifici momenti per evitare riduzioni di prestazioni o consentire il ridimensionamento effettuato dall'utente.|Effettuare una chiamata a un metodo di ridimensionamento basato sul contenuto in un gestore eventi.  Utilizzare ad esempio l'evento <xref:System.Windows.Forms.DataGridView.DataBindingComplete> per inizializzare le dimensioni dopo l'associazione e gestire l'evento <xref:System.Windows.Forms.DataGridView.CellValidated> o <xref:System.Windows.Forms.DataGridView.CellValueChanged> per compensare le dimensioni nelle modifiche effettuate dall'utente in un'origine dati associata.|  
|Adattare l'altezza delle righe al contenuto di celle su più righe.|Accertarsi che la larghezza delle colonne sia appropriata per la visualizzazione di paragrafi di testo e utilizzare il ridimensionamento di riga automatico o a livello di codice basato sul contenuto per adattare l'altezza.  Assicurarsi inoltre che le celle con contenuto su più righe vengano visualizzate con un valore di stile <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> pari a <xref:System.Windows.Forms.DataGridViewTriState>.<br /><br /> Di solito si utilizza una modalità di ridimensionamento automatico delle colonne per conservare la larghezza delle colonne o impostarle su una larghezza specifica prima che venga adattata l'altezza delle righe.|  
  
## Ridimensionamento con il mouse  
 Per impostazione predefinita, gli utenti possono ridimensionare righe, colonne e intestazioni che non utilizzano una modalità di ridimensionamento automatico basato sui valori delle celle.  Per impedire agli utenti il ridimensionamento con altre modalità, come ad esempio la modalità di riempimento di colonna, impostare almeno una delle seguenti proprietà del controllo <xref:System.Windows.Forms.DataGridView>:  
  
-   <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
 È inoltre possibile impedire il ridimensionamento di singole righe o colonne impostando le rispettive proprietà <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>.  Per impostazione predefinita, il valore della proprietà <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> si basa sul valore della proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A> delle colonne e sul valore della proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A> delle righe.  Se tuttavia si imposta in maniera esplicita la proprietà <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> su <xref:System.Windows.Forms.DataGridViewTriState> o su <xref:System.Windows.Forms.DataGridViewTriState>, il valore specificato avrà la precedenza sul valore del controllo di tale riga o colonna.  Impostare <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> su <xref:System.Windows.Forms.DataGridViewTriState> per ripristinare l'ereditarietà.  
  
 Poiché <xref:System.Windows.Forms.DataGridViewTriState> ripristina l'ereditarietà dei valori, la proprietà <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> non restituirà mai un valore <xref:System.Windows.Forms.DataGridViewTriState> a meno che la riga o la colonna non sia stata aggiunta a un controllo <xref:System.Windows.Forms.DataGridView>.  Quando è necessario stabilire se il valore della proprietà <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> di una riga o di una colonna è ereditato, esaminare la proprietà <xref:System.Windows.Forms.DataGridViewElement.State%2A> corrispondente.  Se il valore <xref:System.Windows.Forms.DataGridViewElement.State%2A> include il flag <xref:System.Windows.Forms.DataGridViewElementStates>, il valore della proprietà <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> non è ereditato.  
  
## Ridimensionamento automatico  
 Sono disponibili due tipi di ridimensionamento automatico nel controllo <xref:System.Windows.Forms.DataGridView>: modalità di riempimento di colonna e ridimensionamento automatico basato sul contenuto.  
  
 Con la modalità di riempimento di colonna, le colonne visibili nel controllo occuperanno l'intera larghezza dell'area di visualizzazione del controllo.  Per ulteriori informazioni su questa modalità, vedere [Modalità di riempimento di colonna nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/column-fill-mode-in-the-windows-forms-datagridview-control.md).  
  
 È possibile anche configurare righe, colonne e intestazioni per adattarne automaticamente le dimensioni al contenuto delle celle.  In questo caso, il ridimensionamento viene eseguito ad ogni variazione del contenuto delle celle.  
  
> [!NOTE]
>  Se si conservano i valori delle celle in una cache di dati personalizzata utilizzando la modalità virtuale, il ridimensionamento automatico viene eseguito ogni volta che l'utente modifica il valore di una cella, mentre non viene eseguito quando si modifica un valore memorizzato nella cache all'esterno di un gestore eventi <xref:System.Windows.Forms.DataGridView.CellValuePushed>.  In questo caso, effettuare una chiamata al metodo <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> per costringere il controllo ad aggiornare la visualizzazione della cella e ad applicare le modalità di ridimensionamento automatico correnti.  
  
 Se il ridimensionamento automatico basato sul contenuto viene abilitato per una sola dimensione, ovvero solo per le righe e non per le colonne o viceversa, e anche la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> è abilitata, il ridimensionamento automatico verrà eseguito ogni volta che varia anche l'altra dimensione.  Se ad esempio le righe, e non le colonne, sono configurate per il ridimensionamento automatico e la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> è abilitata, gli utenti potranno trascinare i divisori di colonne per modificare le dimensioni di una colonna. Contemporaneamente, l'altezza delle righe verrà adattata automaticamente per consentire la visualizzazione completa del contenuto delle celle.  
  
 Se si configurano sia le righe che le colonne al ridimensionamento automatico basato sul contenuto e la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> è abilitata, il controllo <xref:System.Windows.Forms.DataGridView> adatterà le dimensioni ogni volta che cambia il contenuto delle celle e utilizzerà un rapporto ideale di altezza per larghezza delle celle nel calcolo delle nuove dimensioni.  
  
 Per configurare la modalità di ridimensionamento per intestazioni e righe e per colonne che non superano il valore del controllo, impostare almeno una delle seguenti proprietà di <xref:System.Windows.Forms.DataGridView>:  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A>  
  
 Per ignorare la modalità di ridimensionamento di colonna del controllo per una singola colonna, impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> corrispondente su un valore diverso da <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>.  La modalità di ridimensionamento di una colonna è in realtà determinato dalla relativa proprietà <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A>.  Il valore di questa proprietà si basa sul valore della proprietà <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> della colonna, a meno che tale valore non sia <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>, nel qual caso viene ereditato il valore della proprietà <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> del controllo.  
  
 Utilizzare con cautela il ridimensionamento automatico basato sul contenuto quando si ha a che fare con grandi quantità di dati.  Per evitare riduzioni di prestazioni, utilizzare le modalità di ridimensionamento automatico che calcolano le dimensioni in base alle sole righe visualizzate anziché analizzare ogni riga del controllo.  Per ottenere prestazioni ottimali, utilizzare invece il ridimensionamento a livello di codice in modo da poter eseguire il ridimensionamento in momenti specifici, ad esempio immediatamente dopo il caricamento di nuovi dati.  
  
 Le modalità di ridimensionamento automatico basato sul contenuto non hanno effetto su righe, colonne o intestazioni nascoste con l'impostazione della proprietà <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> di righe o colonne o delle proprietà <xref:System.Windows.Forms.DataGridView.RowHeadersVisible%2A> o <xref:System.Windows.Forms.DataGridView.ColumnHeadersVisible%2A> del controllo su `false`.  Se ad esempio una colonna viene nascosta dopo averla ridimensionata automaticamente per adattarla a un valore elevato di cella, le dimensioni di tale colonna nascosta non varieranno se la riga contenente il valore elevato di cella viene eliminata.  Poiché il ridimensionamento automatico non viene eseguito quando cambia la visibilità, il ripristino della proprietà <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> della colonna su `true` non implicherà l'esecuzione di un nuovo calcolo delle dimensioni in base al contenuto corrente.  
  
 Il ridimensionamento basato sul contenuto a livello di codice non ha effetto su righe, colonne e intestazioni, a prescindere dalla loro visibilità.  
  
## Ridimensionamento a livello di codice  
 Quando è disabilitato il ridimensionamento automatico, è possibile impostare a livello di codice la larghezza o l'altezza esatta di righe, colonne o intestazioni attraverso le seguenti proprietà:  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>  
  
 È inoltre possibile ridimensionare a livello di codice righe, colonne e intestazioni per adattarne il contenuto utilizzando i seguenti metodi:  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A>  
  
 Questi metodi permettono di ridimensionare righe, colonne o intestazioni una sola volta anziché configurarle per il ridimensionamento continuo.  Le nuove dimensioni vengono calcolate automaticamente per visualizzare il contenuto di tutte le celle senza troncamenti.  Quando tuttavia a livello di codice si ridimensionano le colonne i cui valori della proprietà <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> sono uguali a <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>, viene utilizzata la larghezza calcolata in base al contenuto per adattare in maniera proporzionale i valori della proprietà <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> delle colonne, quindi viene calcolata la larghezza effettiva delle colonne in base a queste nuove proporzioni affinché tutte le colonne occupino l'area di visualizzazione disponibile del controllo.  
  
 Il ridimensionamento automatico a livello di codice è utile per evitare riduzioni di prestazioni dovute al ridimensionamento continuo.  È inoltre utile per fornire le dimensioni iniziali per righe, colonne e intestazioni modificabili dall'utente e per la modalità di riempimento di colonna.  
  
 Di solito si effettuano chiamate ai metodi di ridimensionamento a livello di codice in momenti specifici.  È possibile ad esempio ridimensionare a livello di codice tutte le colonne subito dopo il caricamento dei dati oppure ridimensionare a livello di codice una specifica riga dopo aver modificato un particolare valore di cella.  
  
## Personalizzazione del ridimensionamento basato sul contenuto  
 È possibile personalizzare il ridimensionamento di tipi di celle, righe e colonne del controllo <xref:System.Windows.Forms.DataGridView> derivato effettuando l'override dei metodi <xref:System.Windows.Forms.DataGridViewCell.GetPreferredSize%2A?displayProperty=fullName>, <xref:System.Windows.Forms.DataGridViewRow.GetPreferredHeight%2A?displayProperty=fullName> o <xref:System.Windows.Forms.DataGridViewColumn.GetPreferredWidth%2A?displayProperty=fullName> oppure effettuando chiamate agli overload di metodi di ridimensionamento protetti in un controllo <xref:System.Windows.Forms.DataGridView> derivato.  Gli overload di metodi di ridimensionamento protetti sono progettati per il funzionamento abbinato, in modo da ottenere un rapporto ideale di altezza per larghezza delle celle ed evitare la sovrapposizione di celle con larghezza o altezza maggiore.  Se ad esempio si effettua una chiamata all'overload `AutoResizeRows(DataGridViewAutoSizeRowsMode,Boolean)` del metodo <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A> e si passa un valore di `false` per il parametro <xref:System.Boolean>, l'overload calcolerà l'altezza e la larghezza ideali delle celle della riga, ma adatterà solo l'altezza delle righe.  Sarà quindi necessario effettuare una chiamata al metodo <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> per adattare la larghezza delle colonne al valore calcolato ideale.  
  
## Opzioni di ridimensionamento basato sul contenuto  
 Le enumerazioni utilizzate dalle proprietà e dai metodi di ridimensionamento presentano valori simili per il ridimensionamento basato sul contenuto.  Con questi valori, è possibile limitare le celle da utilizzare per il calcolo delle dimensioni preferite.  Nel caso di tutte le enumerazioni di ridimensionamento, i valori i cui nomi fanno riferimento alle celle visualizzate limiteranno il calcolo alle celle presenti nelle righe visualizzate.  L'esclusione delle righe è utile per evitare una riduzione delle prestazioni quando si utilizzano grandi quantità di righe.  È inoltre possibile limitare i calcoli ai valori delle celle con o senza intestazioni.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeRowMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>   
 <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>   
 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>   
 [Ridimensionamento di colonne e righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)   
 [Modalità di riempimento di colonna nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/column-fill-mode-in-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare le modalità dimensionamento del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control.md)