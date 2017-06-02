---
title: "Procedura: gestire l&#39;evento ContextMenuOpening | Microsoft Docs"
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
  - "ContextMenuOpening (evento)"
ms.assetid: 789652fb-1951-4217-934a-7843e355adf4
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: gestire l&#39;evento ContextMenuOpening
L'evento <xref:System.Windows.FrameworkElement.ContextMenuOpening> può essere gestito in un'applicazione per modificare un menu di scelta rapida esistente prima di visualizzare o eliminare il menu che sarebbe altrimenti visualizzato impostando la proprietà <xref:System.Windows.RoutedEventArgs.Handled%2A> su `true` nei dati dell'evento.  In genere, l'impostazione di <xref:System.Windows.RoutedEventArgs.Handled%2A> su `true` nei dati dell'evento consente di sostituire completamente il menu con un nuovo oggetto <xref:System.Windows.Controls.ContextMenu>, rendendo talvolta necessario l'annullamento dell'operazione e l'avvio di una nuova apertura.  Se si scrivono gestori per l'evento <xref:System.Windows.FrameworkElement.ContextMenuOpening>, è necessario tenere in considerazione eventuali problemi di temporizzazione tra un controllo <xref:System.Windows.Controls.ContextMenu> e il servizio responsabile dell'apertura e del posizionamento dei menu di scelta rapida per i controlli in genere.  In questo argomento vengono descritte alcune delle tecniche del codice per diversi scenari di apertura dei menu di scelta rapida e viene illustrato un caso in cui si verifica il problema della temporizzazione.  
  
 Esistono molti scenari per la gestione dell'evento <xref:System.Windows.FrameworkElement.ContextMenuOpening>:  
  
-   Modifica delle voci di menu prima della visualizzazione.  
  
-   Sostituzione di tutto il menu prima della visualizzazione.  
  
-   Eliminazione completa di qualsiasi menu di scelta rapida esistente e conseguente assenza di visualizzazione di menu di questo tipo.  
  
## Esempio  
  
## Modifica delle voci di menu prima della visualizzazione  
 La modifica delle voci di menu esistenti è abbastanza semplice e si tratta probabilmente dello scenario più comune.  Tale operazione in genere viene eseguita per aggiungere o sottrarre opzioni del menu di scelta rapida in risposta alle informazioni sullo stato corrente dell'applicazione o a informazioni particolari sullo stato, disponibili come proprietà per l'oggetto in cui viene richiesto il menu di scelta rapida.  
  
 La tecnica generale consiste nell'ottenere l'origine dell'evento, vale a dire il controllo specifico selezionato con un clic del pulsante destro del mouse, acquisendone la proprietà <xref:System.Windows.FrameworkElement.ContextMenu%2A>.  È possibile verificare la raccolta <xref:System.Windows.Controls.ItemsControl.Items%2A> per vedere quali sono le voci del menu di scelta rapida già presenti nel menu e successivamente aggiungere o rimuovere nuove voci appropriate <xref:System.Windows.Controls.MenuItem> dalla raccolta.  
  
 [!code-csharp[ContextMenuOpeningHandlers#AddItemNoHandle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#additemnohandle)]  
  
## Sostituzione di tutto il menu prima della visualizzazione  
 La sostituzione di tutto il menu di scelta rapida rappresenta uno scenario alternativo.  Naturalmente, per rimuovere tutte le voci di un menu di scelta rapida esistente e aggiungerne di nuove iniziando dall'elemento zero è anche possibile utilizzare una variazione del codice precedente.  Tuttavia, l'approccio più intuitivo per sostituire tutte le voci del menu di scelta rapida consiste nel creare un nuovo oggetto <xref:System.Windows.Controls.ContextMenu>, popolarlo con delle voci, quindi impostare la proprietà <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=fullName> di un controllo come un nuovo oggetto <xref:System.Windows.Controls.ContextMenu>.  
  
 Di seguito viene riportato il semplice codice di gestione per la sostituzione di un oggetto <xref:System.Windows.Controls.ContextMenu>.  Il codice fa riferimento a un metodo `BuildMenu` personalizzato, separato poiché viene chiamato da più di uno dei gestori di esempio.  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceNoReopen](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacenoreopen)]  
  
 [!code-csharp[ContextMenuOpeningHandlers#BuildMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#buildmenu)]  
  
 Tuttavia, se si utilizza questo stile di gestore per <xref:System.Windows.FrameworkElement.ContextMenuOpening>, è possibile che si verifichi un problema di temporizzazione, se l'oggetto per cui si sta impostando <xref:System.Windows.Controls.ContextMenu> non dispone di un menu di scelta rapida preesistente.  Quando un utente fa clic con il pulsante destro del mouse su un controllo, viene generato un oggetto <xref:System.Windows.FrameworkElement.ContextMenuOpening> anche se quello esistente <xref:System.Windows.Controls.ContextMenu> è vuoto o null.  Tuttavia, in questo caso, qualsiasi nuovo oggetto <xref:System.Windows.Controls.ContextMenu> impostato per l'elemento di origine non può più essere visualizzato per motivi di tempo.  Inoltre, se l'utente fa nuovamente clic con il pulsante destro del mouse, questa volta viene visualizzato il nuovo oggetto <xref:System.Windows.Controls.ContextMenu>, il valore risulta diverso da null e il gestore sostituirà e visualizzerà correttamente il menu alla successiva esecuzione.  Ne conseguono due possibili soluzioni alternative:  
  
1.  Assicurarsi che i gestori <xref:System.Windows.FrameworkElement.ContextMenuOpening> vengano sempre eseguiti in controlli che dispongono di almeno un oggetto <xref:System.Windows.Controls.ContextMenu> segnaposto che si desidera sostituire con il codice di gestione.  In questo caso, è ancora possibile utilizzare il gestore riportato nell'esempio precedente, assegnando tuttavia un oggetto <xref:System.Windows.Controls.ContextMenu> segnaposto nel markup iniziale:  
  
     [!code-xml[ContextMenuOpeningHandlers#XAMLWithInitCM](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml#xamlwithinitcm)]  
  
2.  Si presupponga che il valore <xref:System.Windows.Controls.ContextMenu> iniziale sia null, in base a una logica preliminare.  È possibile controllare se l'oggetto <xref:System.Windows.Controls.ContextMenu> è null o utilizzare un flag all'interno del codice per verificare se il gestore è stato eseguito almeno una volta.  Dal momento che si presuppone che l'oggetto <xref:System.Windows.Controls.ContextMenu> stia per essere visualizzato, il gestore utilizzato imposta <xref:System.Windows.RoutedEventArgs.Handled%2A> su `true` nei dati dell'evento.  Per l'oggetto <xref:System.Windows.Controls.ContextMenuService> responsabile della visualizzazione del menu di scelta rapida, un valore `true` per <xref:System.Windows.RoutedEventArgs.Handled%2A> nei dati dell'evento rappresenta una richiesta di annullamento della visualizzazione della combinazione menu di scelta rapida\/controllo che ha generato l'evento.  
  
 Dopo aver eliminato il menu di scelta rapida potenzialmente sospetto, il passaggio successivo consiste nella creazione di un nuovo menu e nella relativa visualizzazione.  L'impostazione di un nuovo menu è fondamentalmente uguale al gestore precedente: viene compilato un nuovo oggetto <xref:System.Windows.Controls.ContextMenu>, che sarà utilizzato per impostare la proprietà <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=fullName> dell'origine del controllo.  Il passaggio aggiuntivo consiste nel forzare a questo punto la visualizzazione del menu di scelta rapida, in quanto il primo tentativo è stato evitato.  Per forzare la visualizzazione, impostare la proprietà <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A?displayProperty=fullName> su `true` all'interno del gestore.  Prestare attenzione all'esecuzione di questa operazione, poiché l'apertura del menu di scelta rapida nel gestore genera nuovamente l'evento <xref:System.Windows.FrameworkElement.ContextMenuOpening>.  Se si accede nuovamente al gestore, l'evento diventa ricorsivo all'infinito.  Pertanto, è necessario sempre verificare la presenza di un valore `null` o utilizzare un flag quando si apre un menu di scelta rapida dall'interno di un gestore eventi <xref:System.Windows.FrameworkElement.ContextMenuOpening>.  
  
## Eliminazione di tutti i menu di scelta rapida esistenti e conseguente assenza di visualizzazione di menu di questo tipo  
 Lo scenario finale, vale a dire la scrittura di un gestore che elimina completamente un menu è insolito.  Se un controllo specifico non è destinato alla visualizzazione di un menu di scelta rapida, esistono altre modalità più appropriate per assicurare che questa situazione non si verifichi, rispetto all'eliminazione del menu nel momento in cui un utente lo richiede.  Se tuttavia si desidera utilizzare il gestore per eliminare un menu di scelta rapida senza visualizzare nulla, il gestore deve semplicemente impostare <xref:System.Windows.RoutedEventArgs.Handled%2A> su `true` nei dati dell'evento.  L'oggetto <xref:System.Windows.Controls.ContextMenuService> responsabile della visualizzazione di un menu di scelta rapida verificherà i dati evento dell'evento generato sul controllo.  Se l'evento è stato contrassegnato come <xref:System.Windows.RoutedEventArgs.Handled%2A> in un punto della route, l'azione di apertura del menu di scelta rapida che ha iniziato l'evento viene eliminata.  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceReopen](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacereopen)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ContextMenu>   
 <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=fullName>   
 [Cenni preliminari sugli elementi di base](../../../../docs/framework/wpf/advanced/base-elements-overview.md)   
 [Cenni preliminari sull'oggetto ContextMenu](../../../../docs/framework/wpf/controls/contextmenu-overview.md)