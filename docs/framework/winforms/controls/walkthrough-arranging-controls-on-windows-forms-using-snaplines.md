---
title: "Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento | Microsoft Docs"
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
  - "controlli [Windows Form], disposizione con SnapLine"
  - "SnapLine (classe), procedure dettagliate"
  - "guide di allineamento, disposizione dei controlli Windows Form"
  - "controlli Windows Form, disposizione"
ms.assetid: d5c9edc7-cf30-4a97-8ebe-201d569340f8
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento
Per molte applicazioni è estremamente importante la sistemazione precisa dei controlli nel form.  A tale scopo, Progettazione Windows Form offre diversi strumenti di layout.  Uno dei più importanti è la funzionalità <xref:System.Windows.Forms.Design.Behavior.SnapLine>.  
  
 La funzionalità visualizza delle guide di allineamento che mostrano precisamente dove allineare i controlli con altri controlli  e visualizzano le distanze consigliate tra i margini dei controlli, in base alle indicazioni dell'interfaccia utente di Windows.  Per informazioni dettagliate, vedere [User Interface Design and Development](http://go.microsoft.com/FWLink/?LinkId=83878).  
  
 Le guide di allineamento semplificano l'allineamento dei controlli per un aspetto e un comportamento professionale e nitido.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione di un progetto Windows Form  
  
-   Spaziatura e allineamento dei controlli utilizzando le guide di allineamento  
  
-   Allineamento ai margini di un form e di un contenitore  
  
-   Allineamento a controlli raggruppati  
  
-   Utilizzo delle guide di allineamento per inserire un controllo definendo la dimensione  
  
-   Utilizzo delle guide di allineamento durante il trascinamento di un controllo dalla Casella degli strumenti  
  
-   Ridimensionamento dei controlli utilizzando le guide di allineamento  
  
-   Allineamento di un'etichetta al testo di un controllo  
  
-   Utilizzo delle guide di allineamento con la navigazione da tastiera  
  
-   Pannelli layout e guide di allineamento  
  
-   Disabilitazione delle guide di allineamento  
  
 Al termine, si saranno acquisite le informazioni circa il ruolo di layout delle guide di allineamento.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare il progetto  
  
1.  Creare un progetto di applicazione basata su Windows chiamato "SnaplineExample".  Per informazioni dettagliate, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Selezionare il form in Progettazione form.  
  
## Spaziatura e allineamento dei controlli utilizzando le guide di allineamento  
 Le guide di allineamento forniscono un metodo accurato e intuitivo per allineare i controlli nel form.  Le guide di allineamento vengono visualizzate quando si sposta uno o più controlli selezionati accanto a un altro controllo o gruppo di controlli per l'allineamento.  La selezione verrà bloccata nella posizione suggerita quando la si sposta oltre gli altri controlli.  
  
#### Per disporre i controlli utilizzando le guide di allineamento  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form.  
  
2.  Spostare il controllo <xref:System.Windows.Forms.Button> nell'angolo inferiore destro del form.  Le guide di allineamento vengono visualizzate quando il controllo <xref:System.Windows.Forms.Button> si avvicina ai bordi inferiore e destro del form.  Le guide di allineamento visualizzano la distanza consigliata tra i bordi del controllo e del form.  
  
3.  Spostare il controllo <xref:System.Windows.Forms.Button> intorno ai bordi del form e notare dove vengono visualizzate le guide di allineamento.  Una volta terminato, spostare il controllo <xref:System.Windows.Forms.Button> al centro del form.  
  
4.  Trascinare un altro controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel form.  
  
5.  Spostare il secondo controllo <xref:System.Windows.Forms.Button> in modo che sia quasi allineato al primo.  Si noti la guida di allineamento che viene visualizzata sulla linea di base del testo di entrambi i pulsanti mentre il controllo che si sta spostando si blocca in una posizione perfettamente allineata con l'altro controllo.  
  
6.  Spostare il secondo controllo <xref:System.Windows.Forms.Button> in modo che si trovi direttamente sopra il primo.  Le guide di allineamento vengono visualizzate lungo i bordi sinistro e destro di entrambi i pulsanti mentre il controllo che si sta spostando si blocca in una posizione perfettamente allineata con l'altro controllo.  
  
7.  Selezionare uno dei controlli <xref:System.Windows.Forms.Button> e spostarlo accanto all'altro fino quasi a farli toccare.  Si noti la guida di allineamento che viene visualizzata tra i controlli  indicante la distanza consigliata tra i bordi dei controlli.  Si noti inoltre che il controllo che si sta spostando si blocca in questa posizione.  
  
8.  Trascinare due controlli <xref:System.Windows.Forms.Panel> dalla **Casella degli strumenti** nel form.  
  
9. Spostare uno dei controlli <xref:System.Windows.Forms.Panel> in modo che sia quasi allineato al primo.  Le guide di allineamento vengono visualizzate lungo i bordi superiore e inferiore di entrambi i controlli mentre il controllo che si sta spostando si blocca in una posizione perfettamente allineata con l'altro controllo.  
  
## Allineamento ai margini di un form e di un contenitore  
 Le guide di allineamento consentono di allineare i controlli ai margini del form e del contenitore in modo coerente.  
  
#### Per allineare i controlli ai margini del form e del contenitore  
  
1.  Selezionare uno dei controlli <xref:System.Windows.Forms.Button> e spostarlo vicino al bordo destro del form fino a visualizzare una guida di allineamento.  La distanza della guida di allineamento dal bordo destro è costituita dalla somma dei valori della proprietà <xref:System.Windows.Forms.Control.Margin%2A> del controllo e della proprietà <xref:System.Windows.Forms.Control.Padding%2A> del form.  
  
> [!NOTE]
>  Se la proprietà <xref:System.Windows.Forms.Control.Padding%2A> del form viene impostata su 0,0,0,0, tramite Progettazione Windows Form viene assegnato al form un valore di <xref:System.Windows.Forms.Control.Padding%2A> nascosto corrispondente a 9,9,9,9.  Per eseguire l'override di questo comportamento, assegnare un valore diverso da 0,0,0,0.  
  
1.  Modificare il valore della proprietà <xref:System.Windows.Forms.Control.Margin%2A> del controllo <xref:System.Windows.Forms.Button> espandendo la voce <xref:System.Windows.Forms.Control.Margin%2A> nella finestra **Proprietà** e impostando la proprietà <xref:System.Windows.Forms.Padding.All%2A> su 0.  Per informazioni dettagliate, vedere [Procedura dettagliata: disposizione di controlli Windows Form utilizzando spaziatura, margini e la proprietà AutoSize](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md).  
  
2.  Spostare il controllo <xref:System.Windows.Forms.Button> vicino al bordo destro del form fino a visualizzare una guida di allineamento.  La distanza è ora stabilita dal valore della proprietà <xref:System.Windows.Forms.Control.Padding%2A> del form.  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.GroupBox> dalla **Casella degli strumenti** al form.  
  
4.  Modificare il valore della proprietà <xref:System.Windows.Forms.Control.Padding%2A> del controllo <xref:System.Windows.Forms.GroupBox> espandendo la voce <xref:System.Windows.Forms.Control.Padding%2A> nella finestra **Proprietà** e impostando la proprietà <xref:System.Windows.Forms.Padding.All%2A> su 10.  
  
5.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel controllo <xref:System.Windows.Forms.GroupBox>.  
  
6.  Spostare il controllo <xref:System.Windows.Forms.Button> vicino al bordo destro del controllo <xref:System.Windows.Forms.GroupBox> fino a visualizzare una guida di allineamento.  Spostare il controllo <xref:System.Windows.Forms.Button> nel controllo <xref:System.Windows.Forms.GroupBox> e osservare dove vengono visualizzate le guide di allineamento.  
  
## Allineamento a controlli raggruppati  
 È possibile utilizzare le guide di allineamento per allineare controlli raggruppati e non, in un controllo <xref:System.Windows.Forms.GroupBox>.  
  
#### Per allineare controlli raggruppati  
  
1.  Selezionare nel form due controlli.  Spostare la selezione e notare le guide di allineamento che vengono visualizzate tra la selezione e gli altri controlli.  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.GroupBox> dalla **Casella degli strumenti** al form.  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel controllo <xref:System.Windows.Forms.GroupBox>.  
  
4.  Selezionare uno dei controlli <xref:System.Windows.Forms.Button> e spostarlo intorno al controllo <xref:System.Windows.Forms.GroupBox>.  Le guide di allineamento vengono visualizzate ai bordi del controllo <xref:System.Windows.Forms.GroupBox>.  Vengono inoltre visualizzate le guide di allineamento sui bordi del controllo <xref:System.Windows.Forms.Button> contenuto nel controllo <xref:System.Windows.Forms.GroupBox>.  Anche i controlli figlio di un controllo contenitore supportano le guide di allineamento.  
  
## Utilizzo delle guide di allineamento per inserire un controllo definendo la dimensione  
 Le guide di allineamento consentono di allineare i controlli quando vengono inseriti per la prima volta in un form.  
  
#### Per utilizzare le guide di allineamento per inserire un controllo definendone la dimensione  
  
1.  Nella **Casella degli strumenti** fare clic sull'icona del controllo <xref:System.Windows.Forms.Button>.  Non trascinare nel form.  
  
2.  Spostare il puntatore del mouse sull'area di progettazione del form.  Il puntatore assumerà la forma di una croce \(selezione di precisione\) associata all'icona del controllo <xref:System.Windows.Forms.Button>.  Inoltre, vengono visualizzate le guide di allineamento per indicare le posizioni allineate per il controllo <xref:System.Windows.Forms.Button>.  
  
3.  Fare clic e tenere premuto il pulsante del mouse.  
  
4.  Trascinare il puntatore del mouse sul form.  Viene disegnata una struttura indicante la posizione e la dimensione del controllo.  
  
5.  Trascinare il puntatore fino ad allinearlo con un altro controllo del form.  Viene visualizzata una guida per indicare l'allineamento.  
  
6.  Rilasciare il pulsante del mouse.  Il controllo viene creato utilizzando la posizione e la dimensione indicate dalla struttura.  
  
## Utilizzo delle guide di allineamento durante il trascinamento di un controllo dalla Casella degli strumenti  
 Le guide di allineamento consentono di allineare i controlli quando vengono trascinati dalla **Casella degli strumenti** nel form.  
  
#### Per utilizzare le guide di allineamento durante il trascinamento di un controllo dalla Casella degli strumenti  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nel form, senza rilasciare il pulsante del mouse.  
  
2.  Spostare il puntatore del mouse sull'area di progettazione del form.  Il puntatore cambia per indicare la posizione in cui il nuovo controllo<xref:System.Windows.Forms.Button> verrà creato.  
  
3.  Trascinare il puntatore del mouse sul form.  Vengono visualizzate le guide di allineamento per indicare le posizioni allineate per il controllo <xref:System.Windows.Forms.Button>.  Trovare una posizione allineata ad altri controlli.  
  
4.  Rilasciare il pulsante del mouse.  Il controllo viene creato utilizzando la posizione indicata dalle guide di allineamento.  
  
## Ridimensionamento dei controlli utilizzando le guide di allineamento  
 Le guide di allineamento consentono di allineare i controlli durante il ridimensionamento.  
  
#### Per ridimensionare un controllo utilizzando le guide di allineamento  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form.  
  
2.  Ridimensionare il controllo <xref:System.Windows.Forms.Button> agganciando uno dei quadratini di ridimensionamento presenti negli angoli del controllo e trascinandolo.  Per informazioni dettagliate, vedere [Procedura: ridimensionare i controlli di un Windows Form](../../../../docs/framework/winforms/controls/how-to-resize-controls-on-windows-forms.md).  
  
3.  Trascinare il quadratino di ridimensionamento fino ad allineare uno dei bordi del controllo <xref:System.Windows.Forms.Button> a un altro controllo.  Viene visualizzata una guida di allineamento.  Il quadratino di ridimensionamento si blocca nella posizione indicata dalla guida di allineamento.  
  
4.  Ridimensionare il controllo <xref:System.Windows.Forms.Button> in altre direzioni e allineare il quadratino di ridimensionamento ad altri controlli.  Si noti come le guide di allineamento vengano visualizzate in diverse direzioni per indicare l'allineamento.  
  
## Allineamento di un'etichetta al testo di un controllo  
 Alcuni controlli prevedono una guida per l'allineamento di altri controlli al testo visualizzato.  
  
#### Per allineare un'etichetta al testo di un controllo  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TextBox> dalla **Casella degli strumenti** al form.  Quando si rilascia il controllo <xref:System.Windows.Forms.TextBox> nel form, fare clic sull'icona dello smart tag e selezionare l'opzione **Usa textBox1 come testo**.  Per informazioni dettagliate, vedere [Procedura dettagliata: esecuzione di attività comuni utilizzando gli smart tag nei controlli Windows Form](../../../../docs/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls.md).  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.Label> dalla **Casella degli strumenti** al form.  
  
3.  Modificare il valore della proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> del controllo <xref:System.Windows.Forms.Label> su `true`.  I bordi del controllo vengono modificati in base al testo da visualizzare.  
  
4.  Spostare il controllo <xref:System.Windows.Forms.Label> a sinistra del controllo <xref:System.Windows.Forms.TextBox> in modo che sia allineato al bordo inferiore del controllo <xref:System.Windows.Forms.TextBox>.  Si noti la guida di allineamento che viene visualizzata lungo i bordi inferiori dei due controlli.  
  
5.  Spostare il controllo <xref:System.Windows.Forms.Label>leggermente in avanti fino ad allineare il testo di <xref:System.Windows.Forms.Label>e il testo di <xref:System.Windows.Forms.TextBox>.  Viene visualizzata una guida di allineamento in uno stile differente che indica quando i campi testo di entrambi i controlli sono allineati.  
  
## Utilizzo delle guide di allineamento con la navigazione da tastiera  
 Le guide di allineamento consentono di allineare i controlli quando vengono disposti utilizzando i tasti di direzione della tastiera.  
  
#### Per utilizzare le guide di allineamento con la navigazione da tastiera  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form.  Posizionarlo nell'angolo superiore sinistro del form.  
  
2.  Premere CTRL \+ freccia GIÙ.  Il controllo viene spostato nel form verso il basso, nella prima posizione disponibile per l'allineamento orizzontale.  
  
3.  Premere CTRL \+ freccia GIÙ finché il controllo non raggiunge la fine del form.  Si notino le posizioni occupate dal controllo mentre si sposta verso il basso all'interno del form.  
  
4.  Premere CTRL \+ freccia DESTRA.  Il controllo viene spostato nel form, nella prima posizione disponibile per l'allineamento verticale.  
  
5.  Premere CTRL \+ freccia DESTRA finché il controllo non raggiunge il lato destro del form.  Si notino le posizioni occupate dal controllo mentre si sposta all'interno del form.  
  
6.  Spostare il controllo nel form con una combinazione di tasti di direzione.  Si notino le posizioni occupate dal controllo e le relative guide di allineamento.  
  
7.  Premere MAIUSC \+ un tasto di direzione per ridimensionare il controllo <xref:System.Windows.Forms.Button> in incrementi di un pixel.  
  
8.  Premere CTRL \+ MAIUSC \+ un tasto di direzione per ridimensionare il controllo <xref:System.Windows.Forms.Button> in incrementi della guida di allineamento.  
  
## Pannelli layout e guide di allineamento  
 Le guide di allineamento sono disabilitate nei pannelli layout.  
  
#### Per disabilitare selettivamente le guide di allineamento  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
2.  Fare doppio clic sull'icona del controllo <xref:System.Windows.Forms.Button> nella **Casella degli strumenti**.  Viene visualizzato un nuovo controllo pulsante nella prima cella del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
3.  Fare doppio clic sull'icona del controllo <xref:System.Windows.Forms.Button> nella **Casella degli strumenti** altre due volte.  In tal modo viene lasciata una cella vuota nel controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
4.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nella cella vuota del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Non viene visualizzata alcuna guida di allineamento.  
  
5.  Trascinare il controllo <xref:System.Windows.Forms.Button> fuori dal controllo <xref:System.Windows.Forms.TableLayoutPanel> e spostarlo all'interno del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Vengono di nuovo visualizzate le guide di allineamento.  
  
## Disabilitazione delle guide di allineamento  
 Per impostazione predefinita le guide di allineamento sono attivate.  È possibile disabilitarle selettivamente oppure nell'ambiente di progettazione.  
  
#### Per disabilitare selettivamente le guide di allineamento  
  
-   Premere ALT mentre si sposta un controllo all'interno del form.  
  
     Si noti che non viene visualizzata alcuna guida di allineamento e il controllo non si blocca in alcuna posizione di allineamento potenziale.  
  
#### Per disabilitare le guide di allineamento nell'ambiente di progettazione  
  
1.  Aprire la finestra di dialogo **Opzioni** dal menu **Strumenti**.  Aprire la finestra di dialogo Progettazione Windows Form.  Per informazioni dettagliate, vedere [General, Windows Forms Designer, Options Dialog Box](http://msdn.microsoft.com/it-it/8dd170af-72f0-4212-b04b-034ceee92834).  
  
2.  Scegliere il nodo **Generale**.  Nella sezione **Modalità layout**, cambiare la selezione da **SnapLines** a **SnapToGrid**.  
  
3.  Scegliere OK per applicare le impostazioni.  
  
4.  Selezionare un controllo nel form e spostarlo intorno agli altri controlli.  Le guide di allineamento non vengono visualizzate.  
  
## Passaggi successivi  
 Le guide di allineamento offrono modalità intuitive per l'allineamento dei controlli nel form.  Per approfondire l'argomento, si consiglia di effettuare le seguenti operazioni:  
  
-   Provare a annidare un controllo <xref:System.Windows.Forms.GroupBox> in un altro controllo <xref:System.Windows.Forms.GroupBox>.  Inserire un controllo <xref:System.Windows.Forms.Button> in un controllo figlio <xref:System.Windows.Forms.GroupBox> e un altro all'interno del controllo padre <xref:System.Windows.Forms.GroupBox>.  Spostare i controlli <xref:System.Windows.Forms.Button> per vedere come le guide di allineamento attraversano i limiti del contenitore.  
  
-   Creare una colonna di controlli <xref:System.Windows.Forms.TextBox> e una corrispondente colonna di controlli <xref:System.Windows.Forms.Label>.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> del controllo <xref:System.Windows.Forms.Label> su `true`.  Utilizzare le guide di allineamento per spostare i controlli <xref:System.Windows.Forms.Label>in modo che il testo visualizzato sia allineato al testo dei controlli <xref:System.Windows.Forms.TextBox>.  
  
 Per informazioni sulla progettazione di interfacce utente Windows, fare riferimento al libro *Microsoft Windows User Experience, Official Guidelines for User Interface Developers and Designers* Redmond, WA: Microsoft Press, 1999.  \(USBN: 0\-7356\-0566\-1\).  
  
## Vedere anche  
 <xref:System.Windows.Forms.Design.Behavior.SnapLine>   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [Procedura dettagliata: disposizione di controlli Windows Form utilizzando spaziatura, margini e la proprietà AutoSize](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)