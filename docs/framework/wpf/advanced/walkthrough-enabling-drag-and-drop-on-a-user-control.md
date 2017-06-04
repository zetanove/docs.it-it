---
title: "Procedura dettagliata: abilitare il trascinamento della selezione in un controllo utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "trascinamento [WPF], procedura dettagliata"
  - "procedura dettagliata [WPF], trascinamento"
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura dettagliata: abilitare il trascinamento della selezione in un controllo utente
In questa procedura dettagliata viene illustrato come creare un controllo utente personalizzato in grado di partecipare al trasferimento dei dati tramite trascinamento della selezione in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
 In questa procedura dettagliata si creerà un oggetto<xref:System.Windows.Controls.UserControl> WPF personalizzato che rappresenta una forma circolare.  Si implementeranno funzionalità nel controllo per consentire il trasferimento di dati tramite trascinamento della selezione.  Ad esempio, se si trascina da un controllo Circle a un altro, i dati del colore di riempimento vengono copiati dal cerchio di origine alla destinazione.  Se si trascina da un controllo Circle a un controllo <xref:System.Windows.Controls.TextBox>, la rappresentazione di stringa del colore di riempimento viene copiata in <xref:System.Windows.Controls.TextBox>.  Si creerà inoltre una piccola applicazione che contiene due controlli Panel e un controllo <xref:System.Windows.Controls.TextBox> per verificare la funzionalità di trascinamento della selezione.  Si scriverà il codice che consente l'elaborazione nei pannelli dei dati Circle trascinati, per permettere lo spostamento o la copia dei cerchi dalla raccolta Children di un pannello all'altro.  
  
 In questa procedura dettagliata vengono illustrate le attività seguenti:  
  
-   Creare un controllo utente personalizzato.  
  
-   Consentire di utilizzare il controllo utente come origine di trascinamento.  
  
-   Consentire di utilizzare il controllo utente come destinazione di trascinamento.  
  
-   Consentire a un pannello di ricevere dati trascinati dal controllo utente.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   Visual Studio 2010  
  
## Creazione di un progetto di applicazione  
 In questa sezione verrà creata l'infrastruttura dell'applicazione che include una pagina principale con due pannelli e un oggetto <xref:System.Windows.Controls.TextBox>.  
  
### Per creare il progetto  
  
1.  Creare un nuovo progetto di applicazione WPF in Visual Basic o Visual C\#, denominato `DragDropExample`.  Per ulteriori informazioni, vedere [Procedura: creare un nuovo progetto di applicazione WPF](http://msdn.microsoft.com/it-it/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).  
  
2.  Aprire MainWindow.xaml.  
  
3.  Aggiungere il seguente markup tra i tag <xref:System.Windows.Controls.Grid> di apertura e chiusura.  
  
     Tramite questo markup viene creata l'interfaccia utente per l'applicazione di prova.  
  
     [!code-xml[DragDropWalkthrough#PanelsStep1XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]  
  
## Aggiunta di un nuovo controllo utente al progetto  
 In questa sezione verrà aggiunto un nuovo controllo utente al progetto.  
  
### Per aggiungere un nuovo controllo utente  
  
1.  Scegliere **Aggiungi controllo utente** dal menu Progetto.  
  
2.  Nella finestra di dialogo Aggiungi nuovo elemento modificare il nome in `Circle.xaml` e scegliere **Aggiungi**.  
  
     Circle.xaml e il relativo code\-behind verranno aggiunti al progetto.  
  
3.  Aprire il file Circle.xaml.  
  
     Nel file saranno inclusi gli elementi dell'interfaccia utente del controllo utente.  
  
4.  Aggiungere il seguente markup all'oggetto <xref:System.Windows.Controls.Grid> radice per creare un controllo utente semplice con un cerchio blu come interfaccia utente.  
  
     [!code-xml[DragDropWalkthrough#EllipseXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]  
  
5.  Aprire il file Circle.xaml.cs o Circle.xaml.vb.  
  
6.  In C\# aggiungere il codice seguente dopo il costruttore predefinito per creare un costruttore di copia.  In Visual Basic aggiungere il codice seguente per creare sia il costruttore predefinito sia un costruttore di copia.  
  
     Per consentire la copia del controllo utente, aggiungere un metodo del costruttore di copia nel file code\-behind.  Nel controllo utente Circle semplificato, verranno copiati solo il riempimento e la dimensione del controllo utente.  
  
     [!code-csharp[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]  
  
### Per aggiungere il controllo utente alla finestra principale  
  
1.  Aprire MainWindow.xaml.  
  
2.  Aggiungere il codice XAML seguente al tag <xref:System.Windows.Window> di apertura per creare un riferimento allo spazio dei nomi XML nell'applicazione corrente.  
  
    ```  
    xmlns:local="clr-namespace:DragDropExample"  
    ```  
  
3.  Nel primo oggetto <xref:System.Windows.Controls.StackPanel> aggiungere il codice XAML seguente per creare due istanze del controllo utente Circle nel primo pannello.  
  
     [!code-xml[DragDropWalkthrough#CirclesXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]  
  
     Il codice XAML completo per il pannello ha un aspetto simile al seguente.  
  
     [!code-xml[DragDropWalkthrough#PanelsStep2XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]  
  
## Implementazione di eventi dell'origine di trascinamento nel controllo utente  
 In questa sezione, verrà eseguito l'override del metodo <xref:System.Windows.UIElement.OnMouseMove%2A> e verrà avviata l'operazione di trascinamento della selezione.  
  
 Se viene avviato un trascinamento \(viene premuto un pulsante del mouse e viene spostato il mouse\), i dati verranno compressi per il trasferimento in <xref:System.Windows.DataObject>.  In questo caso, il controllo Circle comprimerà tre elementi di dati: una rappresentazione di stringa del colore di riempimento, una doppia rappresentazione dell'altezza e una copia di se stesso.  
  
### Per avviare un'operazione di trascinamento della selezione  
  
1.  Aprire il file Circle.xaml.cs o Circle.xaml.vb.  
  
2.  Aggiungere l'override seguente di <xref:System.Windows.UIElement.OnMouseMove%2A> per fornire la gestione delle classi per l'evento <xref:System.Windows.UIElement.MouseMove>.  
  
     [!code-csharp[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]  
  
     Tramite questo override di <xref:System.Windows.UIElement.OnMouseMove%2A> vengono eseguite le attività seguenti:  
  
    -   Viene verificato se il pulsante sinistro del mouse viene premuto mentre il mouse viene spostato.  
  
    -   Vengono compressi i dati di Circle in un oggetto <xref:System.Windows.DataObject>.  In questo caso, il controllo Circle comprime tre elementi di dati: una rappresentazione di stringa del colore di riempimento, una doppia rappresentazione dell'altezza e una copia di se stesso.  
  
    -   Viene chiamato il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=fullName> statico per avviare l'operazione di trascinamento della selezione.  I tre parametri seguenti vengono passati al metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>:  
  
        -   `dragSource`: riferimento a questo controllo.  
  
        -   `data`: <xref:System.Windows.DataObject> creato nel codice precedente.  
  
        -   `allowedEffects`: operazioni di trascinamento della selezione consentite, ovvero <xref:System.Windows.DragDropEffects> o <xref:System.Windows.DragDropEffects>.  
  
3.  Premere F5 per compilare ed eseguire l'applicazione.  
  
4.  Fare clic su uno dei controlli Circle e trascinarlo sui pannelli, sull'altro controllo Circle e su <xref:System.Windows.Controls.TextBox>.  Quando si trascina su <xref:System.Windows.Controls.TextBox>, il cursore cambia aspetto per indicare uno spostamento.  
  
5.  Mentre si trascina un controllo Circle su <xref:System.Windows.Controls.TextBox>, premere il tasto CTRL.  Si noti il cambiamento di aspetto del cursore per indicare una copia.  
  
6.  Trascinare un controllo Circle su <xref:System.Windows.Controls.TextBox>.  La rappresentazione di stringa del colore di riempimento del controllo Circle viene aggiunta a <xref:System.Windows.Controls.TextBox>.  
  
     ![Rappresentazione del colore di riempimento del cerchio](../../../../docs/framework/wpf/advanced/media/dragdrop-colorstring.png "DragDrop\_ColorString")  
  
 Per impostazione predefinita, il cursore cambia aspetto durante un'operazione di trascinamento della selezione per indicare l'effetto del trascinamento dei dati.  È possibile personalizzare i commenti e i suggerimenti forniti all'utente tramite la gestione dell'evento <xref:System.Windows.UIElement.GiveFeedback> e l'impostazione di un cursore diverso.  
  
### Per fornire commenti e suggerimenti all'utente  
  
1.  Aprire il file Circle.xaml.cs o Circle.xaml.vb.  
  
2.  Aggiungere l'override seguente di <xref:System.Windows.UIElement.OnGiveFeedback%2A> per fornire la gestione delle classi per l'evento <xref:System.Windows.UIElement.GiveFeedback>.  
  
     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]  
  
     Tramite questo override di <xref:System.Windows.UIElement.OnGiveFeedback%2A> vengono eseguite le attività seguenti:  
  
    -   Vengono controllati i valori di <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> impostati nel gestore dell'evento <xref:System.Windows.UIElement.DragOver> della destinazione.  
  
    -   Viene impostato un cursore personalizzato basato sul valore di <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A>.  Il cursore ha lo scopo di fornire commenti e suggerimenti visivi all'utente in merito all'effetto del trascinamento dei dati.  
  
3.  Premere F5 per compilare ed eseguire l'applicazione.  
  
4.  Trascinare uno dei controlli Circle sui pannelli, sull'altro controllo Circle e su <xref:System.Windows.Controls.TextBox>.  Si noti che i cursori sono ora i cursori personalizzati specificati nell'override di <xref:System.Windows.UIElement.OnGiveFeedback%2A>.  
  
     ![Trascina selezione con cursori personalizzati](../../../../docs/framework/wpf/advanced/media/dragdrop-customcursor.png "DragDrop\_CustomCursor")  
  
5.  Selezionare il testo `verde` a partire da <xref:System.Windows.Controls.TextBox>.  
  
6.  Trascinare il testo `verde` su un controllo Circle.  Si noti che i cursori predefiniti sono visualizzati per indicare gli effetti dell'operazione di trascinamento della selezione.  Il cursore dei commenti e suggerimenti è sempre impostato dall'origine di trascinamento.  
  
## Implementazione di eventi della destinazione di trascinamento nel controllo utente  
 In questa sezione, si specificherà che il controllo dell'utente è una destinazione di trascinamento, si eseguirà l'override dei metodi che consentono l'utilizzo del controllo utente come destinazione di trascinamento e si elaboreranno i dati trascinati in esso.  
  
### Per consentire di utilizzare il controllo utente come destinazione di trascinamento  
  
1.  Aprire il file Circle.xaml.  
  
2.  Nel tag di apertura <xref:System.Windows.Controls.UserControl>, aggiungere la proprietà <xref:System.Windows.UIElement.AllowDrop%2A> e impostarla su `true`.  
  
     [!code-xml[DragDropWalkthrough#UCTagXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]  
  
 Il metodo <xref:System.Windows.UIElement.OnDrop%2A> viene chiamato quando la proprietà <xref:System.Windows.UIElement.AllowDrop%2A> è impostata su `true` e i dati dell'origine di trascinamento vengono trascinati nel controllo utente Circle.  In questo metodo i dati trascinati verranno elaborati e applicati al controllo Circle.  
  
### Per elaborare i dati trascinati  
  
1.  Aprire il file Circle.xaml.cs o Circle.xaml.vb.  
  
2.  Aggiungere l'override seguente di <xref:System.Windows.UIElement.OnDrop%2A> per fornire la gestione delle classi per l'evento <xref:System.Windows.UIElement.Drop>.  
  
     [!code-csharp[DragDropWalkthrough#OnDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]  
  
     Tramite questo override di <xref:System.Windows.UIElement.OnDrop%2A> vengono eseguite le attività seguenti:  
  
    -   Viene utilizzato il metodo <xref:System.Windows.DataObject.GetDataPresent%2A> per controllare se i dati trascinati contengono un oggetto di tipo stringa.  
  
    -   Viene utilizzato il metodo <xref:System.Windows.DataObject.GetData%2A> per estrarre i dati di tipo stringa se presenti.  
  
    -   Viene utilizzato un oggetto <xref:System.Windows.Media.BrushConverter> per tentare di convertire la stringa in <xref:System.Windows.Media.Brush>.  
  
    -   Se la conversione ha esito positivo, il pennello viene applicato a <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Ellipse> che fornisce l'interfaccia utente del controllo Circle.  
  
    -   L'evento <xref:System.Windows.UIElement.Drop> viene contrassegnato come gestito.  È necessario contrassegnare l'evento di trascinamento come gestito per segnalare ad altri elementi che lo ricevono che l'evento è stato gestito dal controllo utente Circle.  
  
3.  Premere F5 per compilare ed eseguire l'applicazione.  
  
4.  Selezionare il testo `verde` in <xref:System.Windows.Controls.TextBox>.  
  
5.  Trascinare il testo su un controllo Circle.  Il controllo Circle passa dal blu al verde.  
  
     ![Converti stringa in pennello](../../../../docs/framework/wpf/advanced/media/dragdrop-dropgreentext.png "DragDrop\_DropGreenText")  
  
6.  Digitare il testo `verde` in <xref:System.Windows.Controls.TextBox>.  
  
7.  Selezionare il testo `ver` in <xref:System.Windows.Controls.TextBox>.  
  
8.  Trascinare il testo su un controllo Circle.  Si noti che il cursore cambia per indicare che è consentito il trascinamento ma il colore non cambia perché `ver` non è un colore valido.  
  
9. Trascinare dal controllo Circle verde sul controllo Circle blu.  Il controllo Circle passa dal blu al verde.  Si noti che il cursore visualizzato dipende dal fatto che l'origine di trascinamento sia <xref:System.Windows.Controls.TextBox> o Circle.  
  
 L'impostazione della proprietà <xref:System.Windows.UIElement.AllowDrop%2A> su `true` e l'elaborazione dei dati trascinati sono le uniche condizioni necessarie per consentire l'utilizzo di un elemento come destinazione di trascinamento.  Tuttavia, per fornire una migliore esperienza utente, è necessario gestire gli eventi <xref:System.Windows.UIElement.DragEnter>, <xref:System.Windows.UIElement.DragLeave> e <xref:System.Windows.UIElement.DragOver>.  In tali eventi è possibile eseguire controlli e fornire commenti e suggerimenti aggiuntivi all'utente prima del trascinamento dei dati.  
  
 Quando i dati vengono trascinati sul controllo utente Circle, il controllo dovrebbe notificare all'origine di trascinamento se è possibile elaborare dati trascinati.  Se il controllo non è in grado di elaborare i dati, è necessario rifiutare il trascinamento.  Per eseguire tale operazione, verrà gestito l'evento <xref:System.Windows.UIElement.DragOver> e verrà impostata la proprietà <xref:System.Windows.DragEventArgs.Effects%2A>.  
  
### Per verificare che il trascinamento di dati sia consentito  
  
1.  Aprire il file Circle.xaml.cs o Circle.xaml.vb.  
  
2.  Aggiungere l'override seguente di <xref:System.Windows.UIElement.OnDragOver%2A> per fornire la gestione delle classi per l'evento <xref:System.Windows.UIElement.DragOver>.  
  
     [!code-csharp[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]  
  
     Tramite questo override di <xref:System.Windows.UIElement.OnDragOver%2A> vengono eseguite le attività seguenti:  
  
    -   Imposta la proprietà <xref:System.Windows.DragEventArgs.Effects%2A> su <xref:System.Windows.DragDropEffects>.  
  
    -   Vengono eseguiti gli stessi controlli eseguiti nel metodo <xref:System.Windows.UIElement.OnDrop%2A> per determinare se il controllo utente Circle può elaborare i dati trascinati.  
  
    -   Se il controllo dell'utente può elaborare i dati, impostare la proprietà <xref:System.Windows.DragEventArgs.Effects%2A> su <xref:System.Windows.DragDropEffects> o <xref:System.Windows.DragDropEffects>.  
  
3.  Premere F5 per compilare ed eseguire l'applicazione.  
  
4.  Selezionare il testo `ver` in <xref:System.Windows.Controls.TextBox>.  
  
5.  Trascinare il testo su un controllo Circle.  Si noti che il cursore cambia per indicare che il trascinamento non è consentito perché `ver` non è un colore valido.  
  
 È possibile migliorare ulteriormente l'esperienza utente applicando un'anteprima dell'operazione di trascinamento della selezione.  Per il controllo utente Circle, verrà eseguito l'override dei metodi <xref:System.Windows.UIElement.OnDragEnter%2A> e <xref:System.Windows.UIElement.OnDragLeave%2A>.  Quando i dati vengono trascinati sul controllo, l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di sfondo corrente viene salvato in una variabile segnaposto.  La stringa viene quindi convertita in un pennello e applicata all'oggetto <xref:System.Windows.Shapes.Ellipse> che fornisce l'interfaccia utente del controllo Circle.  Se i dati vengono trascinati all'esterno di Circle senza essere rilasciati, il valore di <xref:System.Windows.Shapes.Shape.Fill%2A> originale viene riapplicato al controllo Circle.  
  
### Per visualizzare l'anteprima degli effetti dell'operazione di trascinamento  
  
1.  Aprire il file Circle.xaml.cs o Circle.xaml.vb.  
  
2.  Nella classe Circle dichiarare una variabile <xref:System.Windows.Media.Brush> privata denominata  `_previousFill` e inizializzarla su `null`.  
  
     [!code-csharp[DragDropWalkthrough#Brush](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]  
  
3.  Aggiungere l'override seguente di <xref:System.Windows.UIElement.OnDragEnter%2A> per fornire la gestione delle classi per l'evento <xref:System.Windows.UIElement.DragEnter>.  
  
     [!code-csharp[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]  
  
     Tramite questo override di <xref:System.Windows.UIElement.OnDragEnter%2A> vengono eseguite le attività seguenti:  
  
    -   Viene salvata la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Ellipse> nella variabile `_previousFill` .  
  
    -   Vengono eseguiti gli stessi controlli eseguiti nel metodo <xref:System.Windows.UIElement.OnDrop%2A> per determinare se è possibile convertire i dati in un oggetto <xref:System.Windows.Media.Brush>.  
  
    -   Se i dati sono convertiti in un oggetto <xref:System.Windows.Media.Brush> valido, vengono applicati a <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Ellipse>.  
  
4.  Aggiungere l'override di <xref:System.Windows.UIElement.OnDragLeave%2A> seguente per fornire la gestione delle classi per l'evento <xref:System.Windows.UIElement.DragLeave>.  
  
     [!code-csharp[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]  
  
     Tramite questo override di <xref:System.Windows.UIElement.OnDragLeave%2A> vengono eseguite le attività seguenti:  
  
    -   Viene applicato l'oggetto <xref:System.Windows.Media.Brush> salvato nella variabile `_previousFill` alla proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> dell'oggetto <xref:System.Windows.Shapes.Ellipse> che fornisce l'interfaccia utente del controllo utente Circle.  
  
5.  Premere F5 per compilare ed eseguire l'applicazione.  
  
6.  Selezionare il testo `verde` in <xref:System.Windows.Controls.TextBox>.  
  
7.  Trascinare il testo su un controllo Circle senza rilasciarlo.  Il controllo Circle passa dal blu al verde.  
  
     ![Visualizzare l'anteprima degli effetti di un'operazione di trascinamento](../../../../docs/framework/wpf/advanced/media/dragdrop-previeweffects.png "DragDrop\_PreviewEffects")  
  
8.  Allontanare il testo dal controllo Circle.  Il controllo Circle passa dal verde al blu.  
  
## Consentire a un pannello di ricevere i dati trascinati  
 In questa sezione si consentirà ai pannelli che ospitano i controlli utente Circle di fungere da destinazioni di trascinamento per i dati di Circle trascinati.  Verrà implementato il codice che consente di spostare un controllo Circle da un pannello a un altro o di creare una copia di un controllo Circle tenendo premuto il tasto CTRL mentre si trascina un controllo Circle.  
  
### Per consentire di utilizzare il pannello come destinazione di trascinamento  
  
1.  Aprire MainWindow.xaml.  
  
2.  Come illustrato nel codice XAML seguente, in ciascun controllo <xref:System.Windows.Controls.StackPanel>, aggiungere i gestori per gli eventi <xref:System.Windows.UIElement.DragOver> e <xref:System.Windows.UIElement.Drop>.  Assegnare al gestore dell'evento <xref:System.Windows.UIElement.DragOver> il nome  `panel_DragOver` e al gestore dell'evento <xref:System.Windows.UIElement.Drop> il nome  `panel_Drop`.  
  
     [!code-xml[DragDropWalkthrough#PanelsXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]  
  
3.  Aprire il file MainWindows.xaml.cs o MainWindow.xaml.vb.  
  
4.  Aggiungere il codice seguente al gestore dell'evento <xref:System.Windows.UIElement.DragOver>.  
  
     [!code-csharp[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]  
  
     Tramite il gestore dell'evento <xref:System.Windows.UIElement.DragOver> vengono eseguite le attività riportate di seguito:  
  
    -   Viene verificato che i dati trascinati contengano i dati "Object" compressi in <xref:system.Windows.DataObject> dal controllo utente Circle e passati nella chiamata a <xref:System.Windows.DragDrop.DoDragDrop%2A>.  
  
    -   Se i dati "Object" sono presenti, viene verificato se è stato premuto il tasto CTRL.  
  
    -   Se il tasto CTRL è stato permuto, la proprietà <xref:System.Windows.DragEventArgs.Effects%2A> viene impostata su <xref:System.Windows.DragDropEffects>.  In caso contrario, la proprietà <xref:System.Windows.DragEventArgs.Effects%2A> viene impostata su <xref:System.Windows.DragDropEffects>.  
  
5.  Aggiungere il codice seguente al gestore dell'evento <xref:System.Windows.UIElement.Drop>.  
  
     [!code-csharp[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]  
  
     Tramite il gestore dell'evento <xref:System.Windows.UIElement.Drop> vengono eseguite le attività riportate di seguito:  
  
    -   Viene verificato se l'evento <xref:System.Windows.UIElement.Drop> è già stato gestito.  Ad esempio, se un controllo Circle viene trascinato in un altro controllo Circle che gestisce l'evento <xref:System.Windows.UIElement.Drop>, si desidera evitare che tale evento sia gestito anche dal pannello che contiene Circle.  
  
    -   Se l'evento <xref:System.Windows.UIElement.Drop> non è gestito, viene verificato se è stato premuto il tasto CTRL.  
  
    -   Se il tasto CTRL viene premuto quando si verifica l'evento <xref:System.Windows.UIElement.Drop>, viene creata una copia del controllo Circle che viene aggiunta alla raccolta <xref:System.Windows.Controls.Panel.Children%2A> di <xref:System.Windows.Controls.StackPanel>.  
  
    -   Se il tasto CTRL non viene premuto, il controllo Circle viene spostato dalla raccolta <xref:System.Windows.Controls.Panel.Children%2A> del pannello padre alla raccolta <xref:System.Windows.Controls.Panel.Children%2A> del pannello in cui è stato trascinato.  
  
    -   Viene impostata la proprietà <xref:System.Windows.DragEventArgs.Effects%2A> per notificare al metodo <xref:System.Windows.DragDrop.DoDragDrop%2A> se è stata eseguita un'operazione di spostamento o copia.  
  
6.  Premere F5 per compilare ed eseguire l'applicazione.  
  
7.  Selezionare il testo `verde` a partire da <xref:System.Windows.Controls.TextBox>.  
  
8.  Trascinare il testo su un controllo Circle.  
  
9. Trascinare un controllo Circle dal pannello sinistro al pannello destro.  Il controllo Circle viene rimosso dalla raccolta <xref:System.Windows.Controls.Panel.Children%2A> del pannello sinistro e aggiunto alla raccolta Children del pannello destro.  
  
10. Trascinare un controllo Circle dal pannello in cui si trova all'altro pannello tenendo premuto il tasto CTRL.  Il controllo Circle viene copiato e la copia viene aggiunta alla raccolta <xref:System.Windows.Controls.Panel.Children%2A> del pannello ricevente.  
  
     ![Trascinamento di un cerchio premendo CTRL](../../../../docs/framework/wpf/advanced/media/dragdrop-paneldrop.png "DragDrop\_PanelDrop")  
  
## Vedere anche  
 [Cenni preliminari sul trascinamento della selezione](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)