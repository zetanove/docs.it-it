---
title: "Eventi di anteprima | Microsoft Docs"
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
  - "eventi, Anteprima"
  - "eventi, soppressione"
  - "eventi di anteprima"
  - "soppressione di eventi"
ms.assetid: b5032308-aa9c-4d02-af11-630ecec8df7e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Eventi di anteprima
Gli eventi di anteprima, noti anche come eventi di tunneling, sono eventi indirizzati nei quali la direzione della route parte dalla radice dell'applicazione e procede verso l'elemento che ha generato l'evento, che viene segnalato come origine nei dati evento.  Non tutti gli scenari supportano o richiedono eventi di anteprima. In questo argomento vengono descritte le situazioni in cui sono presenti tali eventi, il modo in cui le applicazioni o i componenti li gestiscono e i casi in cui la creazione di eventi di anteprima all'interno di componenti o di classi personalizzate potrebbe essere appropriata.  
  
## Eventi di anteprima e input  
 In generale, nella gestione di eventi Preview è necessario prestare attenzione a contrassegnare gli eventi come gestiti nei dati dell'evento.  La gestione di un evento Preview su un elemento diverso da quello che lo ha generato \(l'elemento riportato come origine nei dati dell'evento\) ha l'effetto di escludere la possibilità che un elemento gestisca l'evento che ha originato.  Talvolta si tratta del risultato desiderato, in particolare se gli elementi in questione sono presenti nelle relazioni all'interno della composizione di un controllo.  
  
 Per quanto riguarda specificatamente gli eventi di input, gli eventi Preview condividono determinate istanze di dati degli eventi con l'evento di bubbling equivalente.  Se si utilizza un gestore della classe di eventi Preview per contrassegnare l'evento di input come gestito, il gestore della classe di eventi di input di bubbling non sarà richiamato.  Oppure, se si utilizza un gestore delle istanze di eventi Preview per contrassegnare l'evento come gestito, i gestori dell'evento di bubbling di regola non saranno richiamati.  I gestori delle classi o i gestori delle istanze possono essere registrati o associati a un'opzione da richiamare anche se l'evento è contrassegnato come gestito. Tuttavia tale tecnica generalmente non viene utilizzata.  
  
 Per ulteriori informazioni sulla gestione delle classi e sulla rispettiva relazione con gli eventi Preview, vedere [Contrassegno degli eventi indirizzati come gestiti e gestione delle classi](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md).  
  
### Soluzione per l'eliminazione degli eventi da parte dei controlli  
 Uno scenario in cui gli eventi Preview vengono comunemente utilizzati è la gestione di controlli compositi da parte degli eventi di input.  Talvolta l'autore del controllo evita che un determinato evento sia originato dal relativo controllo, probabilmente al fine di generare invece un evento definito dal componente che disponga di più informazioni o implichi un comportamento più specifico.  Ad esempio, un oggetto [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> elimina gli eventi di bubbling <xref:System.Windows.UIElement.MouseLeftButtonDown> e <xref:System.Windows.UIElement.MouseLeftButtonDown> generati dall'oggetto <xref:System.Windows.Controls.Button> o dai relativi elementi composti per attivare invece lo stato mouse capture e originare un evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> che viene generato sempre dall'oggetto <xref:System.Windows.Controls.Button> stesso.  L'evento e i relativi dati proseguono lungo la route, ma poiché <xref:System.Windows.Controls.Button> contrassegna i dati dell'evento come <xref:System.Windows.RoutedEventArgs.Handled%2A>, vengono richiamati solo i gestori per l'evento che ne ha richiesto in modo specifico l'azione in caso di `handledEventsToo`.  Per fare in modo che altri elementi in direzione della radice dell'applicazione gestiscano un evento eliminato dal controllo, un'alternativa consiste nell'associare dei gestori nel codice specificando `handledEventsToo` come `true`.  Una tecnica più semplice prevede la modifica della direzione di routing gestita in modo che sia l'equivalente Preview di un evento di input.  Ad esempio, se un controllo elimina <xref:System.Windows.UIElement.MouseLeftButtonDown>, provare ad associare invece un gestore per <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown>.  Questa tecnica funziona solo per eventi di input degli elementi di base, ad esempio <xref:System.Windows.UIElement.MouseLeftButtonDown>.  Tali eventi di input utilizzano coppie tunneling\/bubbling, generano entrambi gli eventi e ne condividono i dati.  
  
 Ognuna di queste tecniche presenta effetti collaterali o limitazioni.  L'effetto collaterale della gestione dell'evento Preview è dato dal fatto che la gestione dell'evento in quel punto può disabilitare i gestori che dovrebbero gestire l'evento di bubbling e pertanto la limitazione consisterà nel fatto che non è consigliabile contrassegnare l'evento come gestito mentre si trova ancora nella fase Preview della route.  La limitazione della tecnica `handledEventsToo` è determinata dall'impossibilità di specificare un gestore `handledEventsToo` in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] come attributo, per cui è necessario registrare il gestore eventi nel codice dopo avere ottenuto un riferimento a un oggetto all'elemento a cui il gestore deve essere associato.  
  
## Vedere anche  
 [Contrassegno degli eventi indirizzati come gestiti e gestione delle classi](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)