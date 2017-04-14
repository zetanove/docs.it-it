---
title: "Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel | Microsoft Docs"
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
  - "controlli [Windows Form], disposizione con TableLayoutPanel"
  - "TableLayoutPanel (controllo) [Windows Form], procedure dettagliate"
  - "controlli Windows Form, disposizione"
ms.assetid: d474885e-12cc-4ab7-b997-2a23a643049b
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 28
---
# Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel
Alcune applicazioni richiedono che il form abbia un layout in grado di adattarsi automaticamente alle eventuali modifiche alle dimensioni del form o del contenuto del form.  Per utilizzare un layout dinamico senza gestire gli eventi <xref:System.Windows.Forms.Control.Layout> in modo esplicito nel codice è possibile usare un pannello layout.  
  
 I controlli <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel> offrono modalità intuitive per disporre i controlli nel form.  Entrambi i controlli forniscono una funzionalità configurabile e automatica per la verifica delle posizioni relative dei controlli figlio contenuti e funzionalità di layout dinamico in fase di esecuzione in modo che i controlli figlio possano essere ridimensionati e riposizionati quando le dimensioni del form padre cambiano.  I pannelli layout possono essere annidati in altri pannelli layout in modo da consentire la realizzazione di interfacce utente sofisticate.  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> dispone il contenuto secondo una specifica direzione di flusso, orizzontale o verticale.  Il contenuto può andare a capo da una riga a quella successiva o da una colonna a quella successiva.  In alternativa, è possibile troncare il contenuto invece di utilizzare il ritorno a capo.  Per ulteriori informazioni, vedere [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md).  
  
 <xref:System.Windows.Forms.TableLayoutPanel> dispone il contenuto in una griglia fornendo funzionalità simili all'elemento \<table\> HTML.  Il controllo <xref:System.Windows.Forms.TableLayoutPanel> permette di inserire i controlli in un layout di griglia senza dover specificare precisamente la posizione di ogni singolo controllo.  Le celle sono disposte in righe e colonne che possono anche avere dimensioni differenti.  È possibile unire le celle di più righe e colonne.  Le celle possono contenere tutto ciò che può essere incluso in un form, comportandosi per quasi tutti gli altri aspetti come contenitori.  
  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> inoltre fornisce una funzionalità di ridimensionamento proporzionale in fase di esecuzione, in modo che il layout possa cambiare facilmente in base al ridimensionamento del form.  Di conseguenza, il controllo <xref:System.Windows.Forms.TableLayoutPanel> è molto adatto per i form per l'immissione dei dati e le applicazioni localizzate.  Per ulteriori informazioni, vedere [Walkthrough: Creating a Resizable Windows Form for Data Entry](http://msdn.microsoft.com/it-it/e193b4fc-912a-4917-b036-b76c7a6f58ab) e [Walkthrough: Creating a Localizable Windows Form](http://msdn.microsoft.com/it-it/c5240b6e-aaca-4286-9bae-778a416edb9c).  
  
 Di norma, il controllo <xref:System.Windows.Forms.TableLayoutPanel> non deve essere utilizzato come un contenitore per l'intero layout.  Usare i controlli <xref:System.Windows.Forms.TableLayoutPanel> per fornire le funzionalità di ridimensionamento proporzionale alle parti del layout.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione di un progetto Windows Form  
  
-   Disposizione dei controlli in righe e colonne  
  
-   Impostazione delle proprietà di righe e colonne  
  
-   Estensione di un controllo su righe e colonne  
  
-   Gestione automatica degli overflow  
  
-   Inserimento dei controlli tramite doppio clic nella Casella degli strumenti  
  
-   Inserimento di un controllo tramite il trascinamento della struttura  
  
-   Riassegnazione dei controlli esistenti a un differente padre  
  
 Al termine, si saranno acquisite le informazioni circa il ruolo delle importanti funzionalità di layout.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare il progetto  
  
1.  Creare un progetto Applicazione Windows chiamato "TableLayoutPanelExample".  Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Selezionare il form in **Progettazione** **Windows Form**.  
  
## Disposizione dei controlli in righe e colonne  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> consente di disporre facilmente i controlli in righe e colonne.  
  
#### Per disporre i controlli in righe e colonne utilizzando TableLayoutPanel  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  Per impostazione predefinita, il controllo <xref:System.Windows.Forms.TableLayoutPanel> contiene quattro celle.  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel controllo <xref:System.Windows.Forms.TableLayoutPanel> e rilasciarlo in una delle quattro celle.  Il controllo <xref:System.Windows.Forms.Button> viene creato all'interno della cella selezionata.  
  
3.  Trascinare altri tre controlli <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel controllo <xref:System.Windows.Forms.TableLayoutPanel> in modo che ogni cella contenga un pulsante.  
  
4.  Agganciare il quadratino di ridimensionamento verticale tra le due colonne e spostarlo verso sinistra.  Si noti come il controllo <xref:System.Windows.Forms.Button> nella prima colonna venga ridimensionato in una larghezza inferiore mentre la dimensione dei controlli <xref:System.Windows.Forms.Button> nella seconda colonna resta invariata.  
  
5.  Agganciare il quadratino di ridimensionamento verticale tra le due colonne e spostarlo verso destra.  Per i controlli <xref:System.Windows.Forms.Button> nella prima colonna viene ripristinata la dimensione originale mentre i controlli <xref:System.Windows.Forms.Button> nella seconda colonna vengono spostati verso destra.  
  
6.  Spostare il quadratino di ridimensionamento orizzontale verso l'alto e verso il basso per osservarne gli effetti sui controlli del pannello.  
  
## Posizionamento dei controlli utilizzando l'ancoraggio e l'aggancio  
 Il comportamento dell'aggancio dei controlli figlio in un <xref:System.Windows.Forms.TableLayoutPanel> è differente rispetto a quello di altri controlli contenitore.  Il comportamento dell'ancoraggio dei controlli figlio è uguale a quello di altri controlli contenitore.  
  
#### Posizionamento dei controlli all'interno delle celle  
  
1.  Selezionare il primo controllo <xref:System.Windows.Forms.Button>.  Modificare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  Il controllo <xref:System.Windows.Forms.Button> si espande in modo da occupare la cella.  
  
2.  Selezionare uno degli altri controlli <xref:System.Windows.Forms.Button>.  Modificare il valore della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> su <xref:System.Windows.Forms.AnchorStyles>.  Si noti come viene spostato in modo che il bordo destro sia vicino al bordo destro della cella.  La distanza tra i bordi corrisponde alla somma dei valori della proprietà <xref:System.Windows.Forms.Control.Margin%2A> del controllo <xref:System.Windows.Forms.Button> e della proprietà <xref:System.Windows.Forms.Control.Padding%2A> del pannello.  
  
3.  Modificare il valore della proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del controllo <xref:System.Windows.Forms.Button> su <xref:System.Windows.Forms.AnchorStyles> e <xref:System.Windows.Forms.AnchorStyles>.  Si noti come il controllo viene ridimensionato nella larghezza della cella in base ai valori di <xref:System.Windows.Forms.Control.Margin%2A> e <xref:System.Windows.Forms.Control.Padding%2A>.  
  
4.  Ripetere i passaggi 2 e 3 con gli stili <xref:System.Windows.Forms.AnchorStyles> e <xref:System.Windows.Forms.AnchorStyles>.  
  
## Impostazione delle proprietà di righe e colonne  
 È possibile impostare singole proprietà di righe e colonne utilizzando le raccolte <xref:System.Windows.Forms.TableLayoutPanel.RowStyles%2A> e <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A>.  
  
#### Per impostare le proprietà di righe e colonne  
  
1.  Selezionare il controllo <xref:System.Windows.Forms.TableLayoutPanel> in **Progettazione Windows Form**.  
  
2.  Nella finestra **Proprietà**, aprire la raccolta <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> facendo clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla voce **Colonne**.  
  
3.  Selezionare la prima colonna e modificare il valore della proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> su <xref:System.Windows.Forms.SizeType>.  Scegliere **OK** per confermare la modifica.  La larghezza della prima colonna viene ridotta per adattarsi al controllo <xref:System.Windows.Forms.Button>.  Si noti inoltre che la larghezza della colonna non è ridimensionabile.  
  
4.  Nella finestra **Proprietà**, aprire la raccolta <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> e selezionare la prima colonna.  Modificare il valore della proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> su <xref:System.Windows.Forms.SizeType>.  Scegliere **OK** per confermare la modifica.  Ridimensionare il controllo <xref:System.Windows.Forms.TableLayoutPanel> su una larghezza maggiore e notare come si espande la larghezza della prima colonna.  Ridimensionare il controllo <xref:System.Windows.Forms.TableLayoutPanel> su una larghezza inferiore e notare come vengono ridimensionati i pulsanti della prima colonna per adattarsi alla cella.  Si noti inoltre che la larghezza della colonna è ridimensionabile.  
  
5.  Nella finestra **Proprietà**, aprire la raccolta <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> e selezionare tutte le colonne dell'elenco.  Impostare il valore di ogni proprietà <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> su <xref:System.Windows.Forms.SizeType>.  Scegliere **OK** per confermare la modifica.  Ripetere le operazioni per la raccolta <xref:System.Windows.Forms.TableLayoutPanel.RowStyles%2A>.  
  
6.  Agganciare uno dei quadratini di ridimensionamento presenti negli angoli e ridimensionare la larghezza e l'altezza del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Le righe e le colonne vengono ridimensionate in base alle dimensioni modificate del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Si noti inoltre che le righe e le colonne sono ridimensionabili tramite i quadratini di ridimensionamento orizzontale e verticale.  
  
## Estensione di un controllo su righe e colonne  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> aggiunge diverse proprietà ai controlli in fase di progettazione.  `RowSpan` e `ColumnSpan` sono due di queste proprietà.  È possibile utilizzare le proprietà per estendere un controllo su più righe o colonne.  
  
#### Per estendere un controllo su righe e colonne  
  
1.  Selezionare il controllo <xref:System.Windows.Forms.Button> nella prima riga della prima colonna.  
  
2.  Nella finestra **Proprietà** modificare il valore della proprietà `ColumnSpan` su 2.  Il controllo <xref:System.Windows.Forms.Button> occupa la prima e la seconda colonna.  Viene inoltre aggiunta una ulteriore riga per inserire la modifica.  
  
3.  Ripetere il passaggio 2 per la proprietà `RowSpan`.  
  
## Inserimento dei controlli tramite doppio clic nella Casella degli strumenti  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> può essere compilato facendo doppio clic sui controlli nella **Casella degli strumenti**.  
  
#### Per inserire i controlli facendo doppio clic nella Casella degli strumenti  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
2.  Fare doppio clic sull'icona del controllo <xref:System.Windows.Forms.Button> nella **Casella degli strumenti**.  Viene visualizzato un nuovo controllo pulsante nella prima cella del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
3.  Fare doppio clic su diversi altri controlli nella **Casella degli strumenti**.  I nuovi controlli vengono visualizzati in sequenza nelle celle libere del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Inoltre, il controllo <xref:System.Windows.Forms.TableLayoutPanel> si espande in modo da inserire i nuovi controlli qualora non fossero disponibili celle aperte.  
  
## Gestione automatica degli overflow  
 Quando si inserisce un controllo in <xref:System.Windows.Forms.TableLayoutPanel>, potrebbero esaurirsi le celle vuote per i nuovi controlli.  Il controllo <xref:System.Windows.Forms.TableLayoutPanel> gestisce tale situazione aumentando automaticamente il numero delle celle.  
  
#### Per osservare la gestione automatica degli overflow  
  
1.  Se ancora sono presenti celle vuote nel controllo <xref:System.Windows.Forms.TableLayoutPanel>, continuare a inserire nuovi controlli <xref:System.Windows.Forms.Button> fino a completare il controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
2.  Una volta completato il controllo <xref:System.Windows.Forms.TableLayoutPanel>, fare doppio clic sull'icona <xref:System.Windows.Forms.Button> nella **Casella degli strumenti** per inserire un altro controllo <xref:System.Windows.Forms.Button>.  Si noti che il controllo <xref:System.Windows.Forms.TableLayoutPanel> crea nuove celle per inserire il nuovo controllo.  Inserire qualche altro controllo e osservare il comportamento di ridimensionamento.  
  
3.  Modificare il valore della proprietà <xref:System.Windows.Forms.TableLayoutPanel.GrowStyle%2A> del controllo <xref:System.Windows.Forms.TableLayoutPanel> su <xref:System.Windows.Forms.TableLayoutPanelGrowStyle>.  Fare doppio clic sull'icona <xref:System.Windows.Forms.Button> nella **Casella degli strumenti** per inserire i controlli <xref:System.Windows.Forms.Button> fino a completare il controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Fare di nuovo doppio clic sull'icona <xref:System.Windows.Forms.Button> nella **Casella degli strumenti**.  Viene visualizzato un messaggio di errore di **Progettazione Windows Form** indicante che non è possibile creare altre righe e colonne.  
  
## Inserimento di un controllo tramite il trascinamento della struttura  
 È possibile inserire un controllo in <xref:System.Windows.Forms.TableLayoutPanel> e determinarne la dimensione trascinando la struttura in una cella.  
  
#### Per inserire un controllo tramite il trascinamento della struttura  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
2.  Nella **Casella degli strumenti** fare clic sull'icona del controllo <xref:System.Windows.Forms.Button>.  Non trascinare nel form.  
  
3.  Spostare il puntatore del mouse sul controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Il puntatore assumerà la forma di una croce \(selezione di precisione\) associata all'icona del controllo <xref:System.Windows.Forms.Button>.  
  
4.  Fare clic e tenere premuto il pulsante del mouse.  
  
5.  Trascinare il puntatore del mouse per disegnare la struttura del controllo <xref:System.Windows.Forms.Button>.  Una volta ottenuta la dimensione desiderata, rilasciare il pulsante del mouse.  Il controllo <xref:System.Windows.Forms.Button> viene creato nella cella in cui è stata disegnata la struttura del controllo.  
  
## Inserimento di più controlli all'interno delle celle non consentito  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> può contenere solo un controllo figlio per cella.  
  
#### Per dimostrare che non si possono inserire più controlli nelle celle  
  
-   Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel controllo <xref:System.Windows.Forms.TableLayoutPanel> rilasciandolo in una delle celle occupate.  Il controllo <xref:System.Windows.Forms.TableLayoutPanel> non consente il rilascio del controllo <xref:System.Windows.Forms.Button> nella cella occupata.  
  
## Scambio di controlli  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> consente lo scambio dei controlli tra due differenti celle.  
  
#### Per scambiare i controlli  
  
-   Trascinare uno dei controlli <xref:System.Windows.Forms.Button> da una cella occupata e rilasciarlo in un'altra cella occupata.  Si noti come i due controlli si scambiano le celle.  
  
## Passaggi successivi  
 È possibile ottenere un layout complesso utilizzando i pannelli e i controlli di layout in combinazione.  Per approfondire l'argomento, si consiglia di effettuare le seguenti operazioni:  
  
-   Provare a ridimensionare uno dei controlli <xref:System.Windows.Forms.Button> su una dimensione maggiore e notare l'effetto sul layout.  
  
-   Incollare una selezione di più controlli in <xref:System.Windows.Forms.TableLayoutPanel> e notare come vengono inseriti.  
  
-   I pannelli layout possono contenere altri pannelli layout.  Provare a rilasciare un controllo <xref:System.Windows.Forms.TableLayoutPanel> nel controllo esistente.  
  
-   Ancorare il controllo <xref:System.Windows.Forms.TableLayoutPanel> al form padre.  Ridimensionare il form e notare l'effetto sul layout.  
  
## Vedere anche  
 <xref:System.Windows.Forms.FlowLayoutPanel>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [Microsoft Windows User Experience, Official Guidelines for User Interface Developers and Designers. Redmond, WA: Microsoft Press, 1999. \(USBN: 0\-7356\-0566\-1\)](http://www.microsoft.com/mspress/southpacific/books/book11588.htm)   
 [Walkthrough: Creating a Resizable Windows Form for Data Entry](http://msdn.microsoft.com/it-it/e193b4fc-912a-4917-b036-b76c7a6f58ab)   
 [Walkthrough: Creating a Localizable Windows Form](http://msdn.microsoft.com/it-it/c5240b6e-aaca-4286-9bae-778a416edb9c)   
 [Suggerimenti per il controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/best-practices-for-the-tablelayoutpanel-control.md)   
 [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [Procedura: ancorare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)   
 [Procedura: agganciare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)   
 [Procedura dettagliata: disposizione di controlli Windows Form utilizzando spaziatura, margini e la proprietà AutoSize](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)