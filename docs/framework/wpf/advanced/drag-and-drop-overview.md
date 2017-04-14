---
title: "Cenni preliminari sul trascinamento della selezione | Microsoft Docs"
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
  - "trasferimento dati [WPF], trascinamento"
  - "origini di trascinamento [WPF], trascinamento"
  - "trascinamento [WPF], informazioni su"
  - "trascinamento [WPF], eventi"
  - "trascinamento [WPF], implementazione"
  - "destinazioni degli oggetti trascinati [WPF], trascinamento"
ms.assetid: 1a5b27b0-0ac5-4cdf-86c0-86ac0271fa64
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# Cenni preliminari sul trascinamento della selezione
Questo argomento fornisce una panoramica del supporto per il trascinamento della selezione nelle applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Per trascinamento della selezione si intende di solito un metodo di trasferimento dei dati, in cui si usa un mouse \(o un altro dispositivo di puntamento\) per selezionare uno o più oggetti, si trascinano questi oggetti su un obiettivo di rilascio desiderato nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] e li si rilascia.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="Drag_and_Drop_Support"></a>   
## Supporto del trascinamento della selezione in WPF  
 Nelle operazioni di trascinamento della selezione in genere sono coinvolte due parti: un'origine di trascinamento da cui ha origine l'oggetto trascinato e un obiettivo di rilascio che riceve l'oggetto rilasciato.  L'origine di trascinamento e l'obiettivo di rilascio possono essere elementi dell'interfaccia utente della stessa applicazione o di un'applicazione diversa.  
  
 Il tipo e il numero di oggetti che possono essere manipolati con un trascinamento della selezione sono del tutto arbitrari.  Ad esempio file, cartelle e selezioni di contenuto sono alcuni degli oggetti più comuni manipolati con operazioni di trascinamento della selezione.  
  
 Le particolari azioni eseguite durante un'operazione di trascinamento della selezione sono specifiche dell'applicazione e spesso dipendono dal contesto.  Ad esempio, per impostazione predefinita, trascinando una selezione di file da una cartella a un'altra sullo stesso dispositivo di archiviazione, i file vengono spostati, mentre, per impostazione predefinita, trascinando dei file da una condivisione [!INCLUDE[TLA#tla_unc](../../../../includes/tlasharptla-unc-md.md)] a una cartella locale, i file vengono copiati.  
  
 Le funzionalità di trascinamento della selezione fornite da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono estremamente flessibili e personalizzabili, per poter supportare svariati scenari di trascinamento.  Il trascinamento della selezione supporta la manipolazione di oggetti in una sola applicazione o tra applicazioni diverse.  È completamente supportato anche il trascinamento della selezione tra applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e altre applicazioni [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)].  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], qualsiasi <xref:System.Windows.UIElement> o <xref:System.Windows.ContentElement> può partecipare al trascinamento della selezione.  Gli eventi e i metodi necessari per le operazioni di trascinamento della selezione vengono definiti nella classe <xref:System.Windows.DragDrop>.  Le classi <xref:System.Windows.UIElement> e <xref:System.Windows.ContentElement> contengono alias per gli eventi associati <xref:System.Windows.DragDrop> in modo che gli eventi appaiano nell'elenco dei membri della classe quando un oggetto <xref:System.Windows.UIElement> o <xref:System.Windows.ContentElement> viene ereditato come elemento di base.  I gestori eventi associati a questi eventi vengono associati all'evento associato <xref:System.Windows.DragDrop> sottostante e ricevono la stessa istanza di dati dell'evento.  Per altre informazioni, vedere l'evento <xref:System.Windows.UIElement.Drop?displayProperty=fullName>.  
  
> [!IMPORTANT]
>  Il trascinamento della selezione OLE non funziona nell'area Internet.  
  
<a name="Data_Transfer"></a>   
## Trasferimento dati  
 Il trascinamento della selezione rientra nell'ambito del trasferimento dei dati.  Il trasferimento dei dati include operazioni di trascinamento della selezione e di copia e incolla.  Un'operazione di trascinamento della selezione è analoga a un'operazione di copia e incolla o taglia e incolla usata per trasferire dati da un oggetto o un'applicazione a un'altra usando gli Appunti di sistema.  Entrambi i tipi di operazioni richiedono:  
  
-   Un oggetto di origine che fornisce i dati.  
  
-   Un modo per archiviare temporaneamente i dati trasferiti.  
  
-   Un oggetto di destinazione che riceve i dati.  
  
 In un'operazione di copia e incolla, vengono usati gli Appunti di sistema per archiviare temporaneamente i dati trasferiti. In un'operazione di trascinamento della selezione, viene usato un oggetto <xref:System.Windows.DataObject> per archiviare i dati.  Concettualmente, un oggetto dati è costituito da una o più coppie di un <xref:System.Object> contenente i dati effettivi e dal corrispondente identificatore di formato dati.  
  
 L'origine di trascinamento avvia un'operazione di trascinamento della selezione chiamando il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=fullName> statico e passandogli i dati trasferiti.  Il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A> eseguirà il wrapping automatico dei dati in <xref:System.Windows.DataObject>, se necessario.  Per un maggiore controllo sul formato dei dati, è possibile eseguire il wrapping dei dati in un <xref:System.Windows.DataObject> prima di passarli al metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>.  L'obiettivo di rilascio è responsabile dell'estrazione dei dati dal <xref:System.Windows.DataObject>.  Per altre informazioni sull'uso degli oggetti dati, vedere [Dati e oggetti dati](../../../../docs/framework/wpf/advanced/data-and-data-objects.md).  
  
 L'origine e la destinazione di un'operazione di trascinamento della selezione sono elementi dell'interfaccia utente, ma i dati effettivamente trasferiti non hanno di solito una rappresentazione visiva.  È possibile scrivere il codice per fornire una rappresentazione visiva dei dati trascinati, come accade quando si trascinano i file in Esplora risorse.  Per impostazione predefinita, viene fornito un feedback all'utente modificando il cursore per rappresentare l'effetto che l'operazione di trascinamento della selezione avrà sui dati, ad esempio se i dati verranno spostati o copiati.  
  
### Effetti di trascinamento della selezione  
 Le operazioni di trascinamento della selezione possono avere effetti diversi sui dati trasferiti.  Ad esempio, è possibile copiare i dati oppure spostarli.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] definisce un'enumerazione <xref:System.Windows.DragDropEffects> che è possibile usare per specificare l'effetto di un'operazione di trascinamento della selezione.  Nell'origine di trascinamento, è possibile specificare gli effetti che verranno consentiti dall'origine nel metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>.  Nell'obiettivo di rilascio, è possibile specificare l'effetto previsto per la destinazione nella proprietà <xref:System.Windows.DragEventArgs.Effects%2A> della classe <xref:System.Windows.DragEventArgs>.  Quando l'obiettivo di rilascio specifica l'effetto previsto nell'evento <xref:System.Windows.DragDrop.DragOver>, queste informazioni vengono passate nuovamente all'origine di trascinamento nell'evento <xref:System.Windows.DragDrop.GiveFeedback>.  L'origine di trascinamento usa queste informazioni per informare l'utente dell'effetto sui dati previsto per l'obiettivo di rilascio.  Quando i dati vengono rilasciati, l'obiettivo di rilascio specifica il vero e proprio effetto nell'evento <xref:System.Windows.DragDrop.Drop>.  Queste informazioni vengono passate all'origine di trascinamento come valore restituito del metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>.  Se l'obiettivo di trascinamento restituisce un effetto non presente nell'elenco di origini di trascinamento di `allowedEffects`, l'operazione di trascinamento della selezione viene annullata e il trasferimento dati non viene eseguito.  
  
 È importante ricordare che in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)],i valori <xref:System.Windows.DragDropEffects> vengono usati solo per fornire la comunicazione tra l'origine di trascinamento e l'obiettivo di rilascio in relazione agli effetti dell'operazione di trascinamento della selezione.  L'effetto vero e proprio dell'operazione di trascinamento della selezione dipende dal codice scritto nell'applicazione.  
  
 L'obiettivo di rilascio, ad esempio, potrebbe specificare che l'effetto di rilascio dei dati è lo spostamento dei dati.  Tuttavia, per spostare i dati, è necessario sia aggiungerli all'elemento di destinazione che rimuoverli dall'elemento di origine.  L'elemento di origine potrebbe indicare che consente lo spostamento dei dati, ma, se non si specifica il codice per rimuovere i dati dall'elemento di origine, come risultato finale i dati verranno copiati e non spostati.  
  
<a name="Drag_and_Drop_Events"></a>   
## Eventi del trascinamento della selezione  
 Le operazioni di trascinamento della selezione supportano un modello basato sugli eventi.  Sia l'origine di trascinamento che l'obiettivo di rilascio usano un set standard di eventi per gestire le operazioni di trascinamento della selezione.  Le tabelle seguenti riepilogano gli eventi di trascinamento della selezione standard.  Sono eventi associati nella <xref:System.Windows.DragDrop> classe.  Per altre informazioni sugli eventi associati, vedere [Cenni preliminari sugli eventi associati](../../../../docs/framework/wpf/advanced/attached-events-overview.md).  
  
### Eventi di origine di trascinamento  
  
|Evento|Riepilogo|  
|------------|---------------|  
|<xref:System.Windows.DragDrop.GiveFeedback>|Questo evento si verifica continuamente durante un'operazione di trascinamento della selezione e consente all'origine di trascinamento di fornire informazioni all'utente.  Per fornire questo feedback, in genere viene modificato l'aspetto del puntatore del mouse per indicare gli effetti consentiti dall'obiettivo di rilascio.  Si tratta di un evento di [bubbling](GTMT).|  
|<xref:System.Windows.DragDrop.QueryContinueDrag>|Questo evento si verifica quando gli stati della tastiera o dei pulsanti del mouse cambiano durante un'operazione di trascinamento della selezione e consente all'origine di rilascio di annullare l'operazione di trascinamento a seconda degli stati di tastiera\/pulsanti.  Si tratta di un evento di bubbling.|  
|<xref:System.Windows.DragDrop.PreviewGiveFeedback>|Versione [tunneling](GTMT) di <xref:System.Windows.DragDrop.GiveFeedback>.|  
|<xref:System.Windows.DragDrop.PreviewQueryContinueDrag>|Versione tunneling di <xref:System.Windows.DragDrop.QueryContinueDrag>.|  
  
### Eventi dell'obiettivo di rilascio  
  
|Evento|Riepilogo|  
|------------|---------------|  
|<xref:System.Windows.DragDrop.DragEnter>|Questo evento si verifica quando un oggetto viene trascinato entro il limite dell'obiettivo di rilascio.  Si tratta di un evento di bubbling.|  
|<xref:System.Windows.DragDrop.DragLeave>|Questo evento si verifica quando un oggetto viene trascinato al di fuori del limite dell'obiettivo di rilascio.  Si tratta di un evento di bubbling.|  
|<xref:System.Windows.DragDrop.DragOver>|Questo evento si verifica continuamente mentre un oggetto viene trascinato \(spostato\) entro il limite dell'obiettivo di rilascio.  Si tratta di un evento di bubbling.|  
|<xref:System.Windows.DragDrop.Drop>|Questo evento si verifica quando un oggetto viene rilasciato sull'obiettivo di rilascio.  Si tratta di un evento di bubbling.|  
|<xref:System.Windows.DragDrop.PreviewDragEnter>|Versione tunneling di <xref:System.Windows.DragDrop.DragEnter>.|  
|<xref:System.Windows.DragDrop.PreviewDragLeave>|Versione tunneling di <xref:System.Windows.DragDrop.DragLeave>.|  
|<xref:System.Windows.DragDrop.PreviewDragOver>|Versione tunneling di <xref:System.Windows.DragDrop.DragOver>.|  
|<xref:System.Windows.DragDrop.PreviewDrop>|Versione tunneling di <xref:System.Windows.DragDrop.Drop>.|  
  
 Per gestire gli eventi di trascinamento della selezione per le istanze di un oggetto, aggiungere i gestori per gli eventi elencati nelle tabelle precedenti.  Per gestire gli eventi di trascinamento della selezione a livello di classe, eseguire l'override dei corrispondenti metodi On\*Event e On\*PreviewEvent virtuali.  Per altre informazioni, vedere [Gestione a livello di classe di eventi indirizzati con le classi base dei controlli](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md#Class_Handling_of_Routed_Events).  
  
<a name="Implementing_Drag_And_Drop"></a>   
## Implementazione del trascinamento della selezione  
 Un elemento dell'interfaccia utente può essere un'origine di trascinamento, un obiettivo di rilascio o entrambi.  Per implementare il trascinamento della selezione di base, è necessario scrivere il codice per avviare l'operazione di trascinamento e per elaborare i dati rilasciati.  È possibile migliorare l'esperienza di trascinamento della selezione gestendo gli eventi di trascinamento facoltativi.  
  
 Per implementare il trascinamento della selezione di base, completare le seguenti attività:  
  
-   Identificare l'elemento che sarà un'origine di trascinamento.  Un'origine di trascinamento può essere un oggetto <xref:System.Windows.UIElement> o <xref:System.Windows.ContentElement>.  
  
-   Creare un gestore eventi nell'origine di trascinamento che avvierà l'operazione di trascinamento della selezione.  L'evento è in genere <xref:System.Windows.UIElement.MouseMove>.  
  
-   Nel gestore eventi dell'origine di trascinamento chiamare il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A> per avviare l'operazione di trascinamento della selezione.  Nella chiamata a <xref:System.Windows.DragDrop.DoDragDrop%2A> specificare l'origine di trascinamento, i dati da trasferire e gli effetti consentiti.  
  
-   Identificare l'elemento che sarà un obiettivo di rilascio.  Un obiettivo di rilascio può essere un oggetto <xref:System.Windows.UIElement> o <xref:System.Windows.ContentElement>.  
  
-   Nell'obiettivo di rilascio impostare la proprietà <xref:System.Windows.UIElement.AllowDrop%2A> su `true`.  
  
-   Nell'obiettivo di rilascio creare un gestore dell'evento <xref:System.Windows.DragDrop.Drop> per elaborare i dati rilasciati.  
  
-   Nel gestore dell'evento <xref:System.Windows.DragDrop.Drop> estrarre i dati da <xref:System.Windows.DragEventArgs> usando i metodi <xref:System.Windows.DataObject.GetDataPresent%2A> e <xref:System.Windows.DataObject.GetData%2A>.  
  
-   Nel gestore dell'evento <xref:System.Windows.DragDrop.Drop> usare i dati per eseguire l'operazione di trascinamento della selezione desiderata.  
  
 È possibile migliorare l'implementazione del trascinamento della selezione creando un <xref:System.Windows.DataObject> personalizzato e gestendo eventi di origine di trascinamento e obiettivo di rilascio facoltativi, come mostrato nelle attività seguenti:  
  
-   Per trasferire dati personalizzati o più elementi di dati, creare un <xref:System.Windows.DataObject> da passare al metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>.  
  
-   Per eseguire azioni aggiuntive durante un trascinamento, gestire gli eventi <xref:System.Windows.DragDrop.DragEnter>, <xref:System.Windows.DragDrop.DragOver> e <xref:System.Windows.DragDrop.DragLeave> nell'obiettivo di rilascio.  
  
-   Per modificare l'aspetto del puntatore del mouse, gestire l'evento <xref:System.Windows.DragDrop.GiveFeedback> nell'origine di trascinamento.  
  
-   Per modificare la modalità con cui annullare l'operazione di trascinamento della selezione, gestire l'evento <xref:System.Windows.DragDrop.QueryContinueDrag> nell'origine di trascinamento.  
  
<a name="Drag_And_Drop_Example"></a>   
## Esempi di trascinamento della selezione  
 Questa sezione descrive come implementare il trascinamento della selezione per un elemento <xref:System.Windows.Shapes.Ellipse>.  <xref:System.Windows.Shapes.Ellipse> è sia un'origine di trascinamento che un obiettivo di rilascio.  I dati trasferiti sono la rappresentazione di stringa della proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> dell'ellisse.  Il codice XAML seguente mostra l'elemento <xref:System.Windows.Shapes.Ellipse> e gli eventi relativi al trascinamento della selezione gestiti.  Per i passaggi completi per implementare il trascinamento della selezione, vedere [Procedura dettagliata: abilitare il trascinamento della selezione in un controllo utente](../../../../docs/framework/wpf/advanced/walkthrough-enabling-drag-and-drop-on-a-user-control.md).  
  
 [!code-xml[DragDropSnippets#EllipseXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#ellipsexaml)]  
  
### Impostazione di un elemento come origine di trascinamento  
 Un oggetto che è un'origine di trascinamento è responsabile di:  
  
-   Identificare quando si verifica un trascinamento.  
  
-   Avviare l'operazione di trascinamento della selezione.  
  
-   Identificare i dati da trasferire.  
  
-   Specificare gli effetti che l'operazione di trascinamento della selezione può avere sui dati trasferiti.  
  
 L'origine di trascinamento può anche fornire all'utente feedback relativo alle azioni consentite \(spostamento, copia, nessuna\) e può annullare l'operazione di trascinamento della selezione in base a un input utente aggiuntivo, ad esempio la pressione di ESC durante il trascinamento.  
  
 È responsabilità dell'applicazione determinare quando si verifica un trascinamento e quindi avviare l'operazione di trascinamento della selezione chiamando il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>.  Questo di solito avviene quando si verifica un evento <xref:System.Windows.UIElement.MouseMove> sull'elemento da trascinare mentre viene premuto un pulsante del mouse.  Il seguente esempio mostra come avviare un'operazione di trascinamento della selezione dal gestore dell'evento <xref:System.Windows.UIElement.MouseMove> di un elemento <xref:System.Windows.Shapes.Ellipse> per impostarlo come origine di trascinamento.  I dati trasferiti sono la rappresentazione di stringa della proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> dell'ellisse.  
  
 [!code-csharp[DragDropSnippets#DoDragDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dodragdrop)]
 [!code-vb[DragDropSnippets#DoDragDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dodragdrop)]  
  
 Nel gestore dell'evento <xref:System.Windows.UIElement.MouseMove> chiamare il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A> per avviare l'operazione di trascinamento della selezione.  Il metodo <xref:System.Windows.DragDrop.DoDragDrop%2A> accetta tre parametri:  
  
-   `dragSource`: riferimento all'oggetto dipendenza che è l'origine dei dati trasferiti. Di solito è l'origine dell'evento <xref:System.Windows.UIElement.MouseMove>.  
  
-   `data`: oggetto contenente i dati trasferiti, di cui è stato eseguito il wrapping in un <xref:System.Windows.DataObject>.  
  
-   `allowedEffects`: uno dei valori dell'enumerazione <xref:System.Windows.DragDropEffects>, che specifica gli effetti consentiti dell'operazione di trascinamento della selezione.  
  
 Qualsiasi oggetto serializzabile può essere passato nel parametro `data`.  Se il wrapping dei dati non è già stato eseguito in un <xref:System.Windows.DataObject>, verrà eseguito automaticamente in un nuovo <xref:System.Windows.DataObject>.  Per passare più elementi di dati, è necessario creare il <xref:System.Windows.DataObject> manualmente e passarlo al metodo <xref:System.Windows.DragDrop.DoDragDrop%2A>.  Per altre informazioni, vedere [Dati e oggetti dati](../../../../docs/framework/wpf/advanced/data-and-data-objects.md).  
  
 Il parametro `allowedEffects` viene usato per specificare quali azioni l'origine di trascinamento consentirà di eseguire all'obiettivo di rilascio con i dati trasferiti.  I valori comuni per un'origine di trascinamento sono <xref:System.Windows.DragDropEffects>, <xref:System.Windows.DragDropEffects> e <xref:System.Windows.DragDropEffects>.  
  
> [!NOTE]
>  L'obiettivo di rilascio può anche specificare gli effetti previsti in risposta ai dati rilasciati.  Ad esempio, se l'obiettivo di rilascio non riconosce il tipo di dati da rilasciare, può rifiutare i dati impostando gli effetti consentiti su <xref:System.Windows.DragDropEffects>.  In genere esegue questa operazione nel gestore dell'evento <xref:System.Windows.DragDrop.DragOver>.  
  
 Un'origine di trascinamento può facoltativamente gestire gli eventi <xref:System.Windows.DragDrop.GiveFeedback> e <xref:System.Windows.DragDrop.QueryContinueDrag>.  Questi eventi hanno gestori predefiniti che vengono usati solo se non si contrassegnano gli eventi come gestiti.  In genere si ignorano questi eventi a meno che non esista un'esigenza specifica di modificarne il comportamento predefinito.  
  
 L'evento <xref:System.Windows.DragDrop.GiveFeedback> viene generato continuamente mentre l'origine di trascinamento viene trascinata.  Il gestore predefinito per questo evento controlla se l'origine di trascinamento sia su un obiettivo di rilascio valido.  Se lo è, controlla gli effetti consentiti dell'obiettivo di rilascio.  Fornisce quindi feedback all'utente finale sugli effetti di rilascio consentiti.  A questo scopo il cursore del mouse viene in genere sostituito con un cursore di non rilascio, di copia o di spostamento.  Si dovrebbe gestire questo evento solo se è necessario usare cursori personalizzati per fornire feedback all'utente.  Se si gestisce questo evento, assicurarsi di contrassegnarlo come gestito in modo che il gestore predefinito non esegua l'override del gestore.  
  
 L'evento <xref:System.Windows.DragDrop.QueryContinueDrag> viene generato continuamente mentre l'origine di trascinamento viene trascinata.  È possibile gestire questo evento per determinare quale azione termina l'operazione di trascinamento della selezione in base allo stato dei tasti ESC, MAIUSC, CTRL e ALT, oltre che allo stato dei pulsanti del mouse.  Il gestore predefinito per questo evento annulla l'operazione di trascinamento della selezione se viene premuto ESC e rilascia i dati se il pulsante del mouse viene rilasciato.  
  
> [!CAUTION]
>  Questi eventi vengono generati continuamente durante l'operazione di trascinamento della selezione.  È quindi consigliabile evitare attività a elevato utilizzo di risorse nei gestori eventi.  Ad esempio, usare un cursore nella cache invece di creare un nuovo cursore ogni volta che viene generato l'evento <xref:System.Windows.DragDrop.GiveFeedback>.  
  
### Impostazione di un elemento come obiettivo di rilascio  
 Un oggetto che è un obiettivo di rilascio è responsabile di:  
  
-   Specificare che è un obiettivo di rilascio valido.  
  
-   Rispondere all'origine di trascinamento quando viene trascinata sulla destinazione.  
  
-   Controllare che i dati trasferiti siano in un formato che può ricevere.  
  
-   Elaborare i dati rilasciati.  
  
 Per specificare che un elemento è un obiettivo di rilascio, si imposta la proprietà <xref:System.Windows.UIElement.AllowDrop%2A> su `true`.  Gli eventi dell'obiettivo di rilascio verranno quindi generati nell'elemento per poterli gestire.  Durante un'operazione di trascinamento della selezione, nell'obiettivo di rilascio si verifica la sequenza di eventi seguente:  
  
1.  <xref:System.Windows.DragDrop.DragEnter>  
  
2.  <xref:System.Windows.DragDrop.DragOver>  
  
3.  <xref:System.Windows.DragDrop.DragLeave> o <xref:System.Windows.DragDrop.Drop>  
  
 L'evento <xref:System.Windows.DragDrop.DragEnter> si verifica quando i dati vengono trascinati entro il limite dell'obiettivo di rilascio.  In genere si gestisce questo evento per fornire un'anteprima degli effetti dell'operazione di trascinamento della selezione, se appropriato per l'applicazione.  Non impostare la proprietà <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> nell'evento <xref:System.Windows.DragDrop.DragEnter>, perché verrà sovrascritta nell'evento <xref:System.Windows.DragDrop.DragOver>.  
  
 Il seguente esempio mostra il gestore dell'evento <xref:System.Windows.DragDrop.DragEnter> per un elemento <xref:System.Windows.Shapes.Ellipse>.  Questo codice visualizza in anteprima gli effetti dell'operazione di trascinamento della selezione salvando il pennello <xref:System.Windows.Shapes.Shape.Fill%2A> corrente.  Usa quindi il metodo <xref:System.Windows.DataObject.GetDataPresent%2A> per controllare se il <xref:System.Windows.DataObject> che viene trascinato sull'ellisse contiene dati stringa convertibili in un <xref:System.Windows.Media.Brush>.  In tal caso, i dati vengono estratti con il metodo <xref:System.Windows.DataObject.GetData%2A>.  Vengono quindi convertiti in un <xref:System.Windows.Media.Brush> e applicati all'ellisse.  La modifica viene ripristinata nel gestore dell'evento <xref:System.Windows.DragDrop.DragLeave>.  Se i dati non possono essere convertiti in un <xref:System.Windows.Media.Brush>, non viene eseguita alcuna azione.  
  
 [!code-csharp[DragDropSnippets#DragEnter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragenter)]
 [!code-vb[DragDropSnippets#DragEnter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragenter)]  
  
 L'evento <xref:System.Windows.DragDrop.DragOver> si verifica in modo continuo mentre i dati vengono trascinati sull'obiettivo di rilascio.  Questo evento è associato all'evento <xref:System.Windows.DragDrop.GiveFeedback> nell'origine di trascinamento.  Nel gestore dell'evento <xref:System.Windows.DragDrop.DragOver>, si usano di solito i metodi <xref:System.Windows.DataObject.GetDataPresent%2A> e <xref:System.Windows.DataObject.GetData%2A> per controllare se i dati trasferiti sono in un formato che l'obiettivo di rilascio può elaborare.  È anche possibile controllare se vengono premuti tasti di modifica, che in genere indicano se l'utente intende eseguire un'azione di copia o spostamento.  Dopo questi controlli, si imposta la proprietà <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> per notificare all'origine di trascinamento quale effetto avrà il rilascio dei dati.  L'origine di trascinamento riceve queste informazioni negli argomenti dell'evento <xref:System.Windows.DragDrop.GiveFeedback> e può impostare un cursore appropriato per fornire feedback all'utente.  
  
 Il seguente esempio mostra il gestore dell'evento <xref:System.Windows.DragDrop.DragOver> per un elemento <xref:System.Windows.Shapes.Ellipse>.  Questo codice verifica se il <xref:System.Windows.DataObject> che viene trascinato sull'ellisse contiene dati stringa convertibili in un <xref:System.Windows.Media.Brush>.  In tal caso, imposta la proprietà <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> su <xref:System.Windows.DragDropEffects>.  Questo indica all'origine di trascinamento che i dati possono essere copiati nell'ellisse.  Se i dati non possono essere convertiti in un <xref:System.Windows.Media.Brush>, la proprietà <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> viene impostata su <xref:System.Windows.DragDropEffects>.  Questo indica all'origine di trascinamento che l'ellisse non è un obiettivo di rilascio valido per i dati.  
  
 [!code-csharp[DragDropSnippets#DragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragover)]
 [!code-vb[DragDropSnippets#DragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragover)]  
  
 L'evento <xref:System.Windows.DragDrop.DragLeave> si verifica quando i dati vengono trascinati all'esterno del limite della destinazione senza essere rilasciati.  Si gestisce questo evento per annullare qualsiasi operazione eseguita nel gestore dell'evento <xref:System.Windows.DragDrop.DragEnter>.  
  
 Il seguente esempio mostra il gestore dell'evento <xref:System.Windows.DragDrop.DragLeave> per un elemento <xref:System.Windows.Shapes.Ellipse>.  Questo codice annulla l'anteprima eseguita nel gestore dell'evento <xref:System.Windows.DragDrop.DragEnter> applicando l'oggetto <xref:System.Windows.Media.Brush> salvato all'ellisse.  
  
 [!code-csharp[DragDropSnippets#DragLeave](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragleave)]
 [!code-vb[DragDropSnippets#DragLeave](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragleave)]  
  
 L'evento <xref:System.Windows.DragDrop.Drop> si verifica quando i dati vengono rilasciati sull'obiettivo di rilascio. Per impostazione predefinita, questo avviene quando viene rilasciato il pulsante del mouse.  Nel gestore dell'evento <xref:System.Windows.DragDrop.Drop>, si usa il metodo <xref:System.Windows.DataObject.GetData%2A> per estrarre i dati trasferiti dal <xref:System.Windows.DataObject> ed eseguire l'elaborazione dati richiesta dall'applicazione.  L'evento <xref:System.Windows.DragDrop.Drop> termina l'operazione di trascinamento della selezione.  
  
 Il seguente esempio mostra il gestore dell'evento <xref:System.Windows.DragDrop.Drop> per un elemento <xref:System.Windows.Shapes.Ellipse>.  Questo codice applica gli effetti dell'operazione di trascinamento della selezione ed è simile al codice nel gestore dell'evento <xref:System.Windows.DragDrop.DragEnter>.  Verifica se il <xref:System.Windows.DataObject> che viene trascinato sull'ellisse contiene dati stringa convertibili in un <xref:System.Windows.Media.Brush>.  In tal caso, <xref:System.Windows.Media.Brush> viene applicato all'ellisse.  Se i dati non possono essere convertiti in un <xref:System.Windows.Media.Brush>, non viene eseguita alcuna azione.  
  
 [!code-csharp[DragDropSnippets#Drop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#drop)]
 [!code-vb[DragDropSnippets#Drop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#drop)]  
  
## Vedere anche  
 <xref:System.Windows.Clipboard>   
 [Procedura dettagliata: abilitare il trascinamento della selezione in un controllo utente](../../../../docs/framework/wpf/advanced/walkthrough-enabling-drag-and-drop-on-a-user-control.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/drag-and-drop-how-to-topics.md)   
 [Trascinamento della selezione](../../../../docs/framework/wpf/advanced/drag-and-drop.md)