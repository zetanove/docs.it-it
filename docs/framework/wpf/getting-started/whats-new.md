---
title: "Novit&#224; di WPF versione 4.5 | Microsoft Docs"
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
  - "Windows Presentation Foundation, novità"
  - "WPF, novità"
ms.assetid: db086ae4-70bb-4862-95db-2eaca5216bc3
caps.latest.revision: 55
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 55
---
# Novit&#224; di WPF versione 4.5
<a name="introduction"></a> In questo argomento vengono fornite informazioni sulle funzionalità nuove e avanzate disponibili in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] versione 4.5.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Controllo della barra multifunzione](#ribbon_control)  
  
-   [Prestazioni migliori quando visualizzare grandi quantità di dati raggruppati](#grouped_virtualization)  
  
-   [Nuove funzionalità per il VirtualizingPanel](#VirtualizingPanel)  
  
-   [Associazione alle proprietà statiche](#static_properties)  
  
-   [Accesso alle raccolte su thread non di interfaccia utente](#xthread_access)  
  
-   [In modo sincrono e in modo asincrono convalidare i dati](#INotifyDataErrorInfo)  
  
-   [Aggiornare automaticamente l'origine di un'associazione dati](#delay)  
  
-   [Associazione a tipi che implementano ICustomTypeProvider](#ICustomTypeProvider)  
  
-   [Recupero delle informazioni di associazione dati da un'espressione di associazione](#binding_state)  
  
-   [Verifica di un oggetto valido di DataContext](#DisconnectedSource)  
  
-   [Riposizionando i dati come la modifica dei valori dei dati \(formazione attivo\)](#live_shaping)  
  
-   [Supporto migliorato per stabilire un riferimento debole a un evento](#weak_event_pattern)  
  
-   [Nuovi metodi per la classe del dispatcher](#async)  
  
-   [Estensioni di markup per gli eventi](#events_markup_extenions)  
  
<a name="ribbon_control"></a>   
## Controllo della barra multifunzione  
 Viene fornito WPF 4,5 con <xref:System.Windows.Controls.Ribbon.Ribbon> verificare che ospita una barra di accesso rapido, un menu dell'applicazione e nelle schede.  Per ulteriori informazioni, vedere [Cenni preliminari sulla barra multifunzione](../Topic/Ribbon%20Overview.md).  
  
<a name="grouped_virtualization"></a>   
## Prestazioni migliori quando visualizzare grandi quantità di dati raggruppati  
 La virtualizzazione di l si verifica quando un sottoinsieme degli elementi dell'interfaccia utente \(UI\) viene generato da un gran numero di elementi di dati basati su quali elementi sono visibili sullo schermo.  <xref:System.Windows.Controls.VirtualizingPanel> definisce la proprietà associata <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A> che consente la virtualizzazione dell'interfaccia utente per i dati raggruppati.  Per ulteriori informazioni sui dati di raggruppamento, vedere procedura: Ordinare e raggruppare i dati utilizzando una visualizzazione in XAML.  Per ulteriori informazioni sulla virtualizzazione dei dati raggruppati, vedere la proprietà associata <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A>.  
  
<a name="VirtualizingPanel"></a>   
## Nuove funzionalità per il VirtualizingPanel  
  
1.  È possibile specificare se <xref:System.Windows.Controls.VirtualizingPanel>, come <xref:System.Windows.Controls.VirtualizingStackPanel>, visualizzare gli elementi parziali utilizzando la proprietà associata <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>.  Se <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> è impostato su <xref:System.Windows.Controls.ScrollUnit>, <xref:System.Windows.Controls.VirtualizingPanel> visualizzati solo gli elementi che sono completamente visibili.  Se <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> è impostato su <xref:System.Windows.Controls.ScrollUnit>, <xref:System.Windows.Controls.VirtualizingPanel> può visualizzare gli elementi visibili parzialmente.  
  
2.  È possibile specificare la dimensione della cache prima e dopo il riquadro di visualizzazione quando <xref:System.Windows.Controls.VirtualizingPanel> sta utilizzando virtualizzando la proprietà associata <xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A>.  La cache è la quantità di spazio sopra o sotto il riquadro di visualizzazione in cui gli elementi non sono virtualizzate.  Utilizzo di una cache evitare di generare elementi di interfaccia utente quando vengono scorsi nella visualizzazione può migliorare le prestazioni.  La cache viene popolato con una priorità più bassa in modo che l'applicazione non diventa non rispondere durante l'operazione.  La proprietà <xref:System.Windows.Controls.VirtualizingPanel.CacheLengthUnit%2A?displayProperty=fullName> determina l'unità di misura utilizzata da <xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A?displayProperty=fullName>.  
  
<a name="static_properties"></a>   
## Associazione alle proprietà statiche  
 È possibile utilizzare le proprietà statiche come origine di associazione dati.  Il motore di associazione dati riconosce quando cambia il valore della proprietà se un evento statico viene generato.  Ad esempio, se la classe `SomeClass` definisce una proprietà statica denominata `MyProperty`, `SomeClass` può definire un evento statico che viene generato quando il valore `MyProperty` cambia.  L'evento statico può utilizzare una delle firme.  
  
-   `public static event EventHandler MyPropertyChanged;`  
  
-   `public static event EventHandler<PropertyChangedEventArgs> StaticPropertyChanged;`  
  
 Si noti che nel primo caso, la classe espone un evento statico denominato *Nomeproprietà*`Changed` che passa <xref:System.EventArgs> al gestore eventi.  Nel secondo caso, la classe espone un evento statico denominato `StaticPropertyChanged` che passa <xref:System.ComponentModel.PropertyChangedEventArgs> al gestore eventi.  Una classe che implementa la proprietà statica possibile generare notifiche di variazione delle proprietà utilizzando qualsiasi metodo.  
  
<a name="xthread_access"></a>   
## Accesso alle raccolte su thread non di interfaccia utente  
 WPF consente di visualizzare e modificare le raccolte di dati in thread diverso da quello che ha creato la raccolta.  Questo consente di utilizzare un thread in background per ricevere i dati da un'origine esterna, ad esempio un database e visualizzare i dati sul thread UI.  Utilizzando un altro thread per modificare la raccolta, l'interfaccia utente risponderà all'utente.  
  
<a name="INotifyDataErrorInfo"></a>   
## In modo sincrono e in modo asincrono convalidare i dati  
 L'interfaccia <xref:System.ComponentModel.INotifyDataErrorInfo> consente alle classi di entità di dati per implementare le regole di convalida personalizzate e per esporre i risultati di convalida in modo asincrono.  Questa interfaccia supporta inoltre gli oggetti di errore personalizzato, più errori per proprietà, errori di rapporti fra proprietà e degli errori livelli model.  Per ulteriori informazioni, vedere <xref:System.ComponentModel.INotifyDataErrorInfo>.  
  
<a name="delay"></a>   
## Aggiornare automaticamente l'origine di un'associazione dati  
 Se si utilizza l'associazione dati per aggiornare un'origine dati, è possibile utilizzare la proprietà <xref:System.Windows.Data.BindingBase.Delay%2A> per specificare un periodo della sessione dopo aver modificato la proprietà di destinazione prima degli aggiornamenti di origine.  Ad esempio, si supponga di avere <xref:System.Windows.Controls.Slider> con limite bidirezionale di dati della proprietà <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> a una proprietà di un oggetto dati e la proprietà <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> è impostata su <xref:System.Windows.Data.UpdateSourceTrigger>.  In questo esempio, quando l'utente sposta <xref:System.Windows.Controls.Slider>, gli aggiornamenti del database di origine per ogni pixel che <xref:System.Windows.Controls.Slider> sposta.  L'oggetto di origine in genere richiede il valore del dispositivo di scorrimento solo quando <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> slider termine della modifica.  Per impedire aggiornare il database di origine troppo frequente, utilizzare <xref:System.Windows.Data.BindingBase.Delay%2A> per specificare che l'origine non deve essere aggiornato finché una certa quantità di tempo non trascorra dopo che il cursore termine dello spostamento.  
  
<a name="ICustomTypeProvider"></a>   
## Associazione a tipi che implementano ICustomTypeProvider  
 WPF supporta l'associazione dati a oggetti che implementano <xref:System.Reflection.ICustomTypeProvider>, noti anche come tipi personalizzati.  È possibile utilizzare personalizzato nei casi seguenti.  
  
1.  Come <xref:System.Windows.PropertyPath> nell'associazione dati.  Ad esempio, la proprietà <xref:System.Windows.Data.Binding.Path%2A><xref:System.Windows.Data.Binding> può fare riferimento alla proprietà di un tipo personalizzato.  
  
2.  Come valore della proprietà <xref:System.Windows.DataTemplate.DataType%2A>.  
  
3.  Come tipo che determina le colonne generate automaticamente in <xref:System.Windows.Controls.DataGrid>.  
  
<a name="binding_state"></a>   
## Recupero delle informazioni di associazione dati da un'espressione di associazione  
 In alcuni casi, è possibile ottenere <xref:System.Windows.Data.BindingExpression><xref:System.Windows.Data.Binding> ed essere necessarie informazioni sul database di origine e gli oggetti di destinazione di associazione.  I nuovi API sono stati aggiunti per consentire di ottenere l'origine o l'oggetto di destinazione o la proprietà associata.  Quando si <xref:System.Windows.Data.BindingExpression>, utilizzare i seguenti API per ottenere informazioni sull'origine e destinazione.  
  
|Per trovare il valore dell'associazione|Utilizzare questa API|  
|---------------------------------------------|---------------------------|  
|l'oggetto di destinazione|<xref:System.Windows.Data.BindingExpressionBase.Target%2A?displayProperty=fullName>|  
|La proprietà di destinazione|<xref:System.Windows.Data.BindingExpressionBase.TargetProperty%2A?displayProperty=fullName>|  
|l'oggetto di origine|<xref:System.Windows.Data.BindingExpression.ResolvedSource%2A?displayProperty=fullName>|  
|La proprietà di origine|<xref:System.Windows.Data.BindingExpression.ResolvedSourcePropertyName%2A?displayProperty=fullName>|  
|Se <xref:System.Windows.Data.BindingExpression> appartiene a <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingExpressionBase.BindingGroup%2A?displayProperty=fullName>|  
|Il proprietario <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingGroup.Owner%2A>|  
  
<a name="DisconnectedSource"></a>   
## Verifica di un oggetto valido di DataContext  
 Vi sono casi in cui <xref:System.Windows.FrameworkElement.DataContext%2A> di un contenitore di elementi in <xref:System.Windows.Controls.ItemsControl> viene disconnesso.  Un contenitore di elementi è l'interfaccia utente che visualizza un elemento in <xref:System.Windows.Controls.ItemsControl>.  Quando <xref:System.Windows.Controls.ItemsControl> associato a dati a una raccolta, un contenitore di elementi viene generato per ogni elemento.  In alcuni casi, i contenitori di elementi vengono rimossi dalla struttura ad albero visuale.  Due casi comuni in cui un contenitore di elementi viene rimosso da quando un elemento viene rimosso dalla raccolta sottostante e quando la virtualizzazione è attivata per <xref:System.Windows.Controls.ItemsControl>.  In questi casi, la proprietà <xref:System.Windows.FrameworkElement.DataContext%2A> del contenitore di elementi viene impostata sull'oggetto sentinel restituito dalla proprietà statica <xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A?displayProperty=fullName>.  È necessario controllare se <xref:System.Windows.FrameworkElement.DataContext%2A> è uguale all'oggetto <xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A> prima di accedere a <xref:System.Windows.FrameworkElement.DataContext%2A> di un contenitore di elementi.  
  
<a name="live_shaping"></a>   
## Riposizionando i dati come la modifica dei valori dei dati \(formazione attivo\)  
 Una raccolta di dati può essere raggruppati, ordinato, o essere filtrata.  WPF 4,5 abilita i dati da ridisporre quando i dati vengono modificati.  Ad esempio, si supponga che un'applicazione può utilizzare <xref:System.Windows.Controls.DataGrid> per elencare le azioni in un mercato azione e le azioni vengono ordinate in base al valore predefinito.  Se l'ordinamento attivo è abilitata in <xref:System.Windows.Data.CollectionView>di azione, la posizione delle azioni in <xref:System.Windows.Controls.DataGrid> si sposta quando il valore delle azioni diventa maggiore o minore del valore di altre azioni.  Per ulteriori informazioni, vedere l'interfaccia <xref:System.ComponentModel.ICollectionViewLiveShaping>.  
  
<a name="weak_event_pattern"></a>   
## Supporto migliorato per stabilire un riferimento debole a un evento  
 Implementare il modello di evento debole è più semplice perché i sottoscrittori gli eventi possono partecipare senza implementare un'interfaccia aggiuntiva.  La classe generica <xref:System.Windows.WeakEventManager> consente inoltre ai sottoscrittori di partecipare al modello di evento debole dedicato <xref:System.Windows.WeakEventManager> se non esiste per un determinato evento.  Per ulteriori informazioni, vedere [Modelli di eventi deboli](../../../../docs/framework/wpf/advanced/weak-event-patterns.md).  
  
<a name="async"></a>   
## Nuovi metodi per la classe del dispatcher  
 La classe del dispatcher definisce i nuovi metodi per sincrono e le operazioni asincrone.  Il metodo sincrono <xref:System.Windows.Threading.Dispatcher.Invoke%2A> definisce gli overload che accettano un parametro <xref:System.Func%601> o <xref:System.Action>.  Il nuovo metodo asincrono, <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>, accetta <xref:System.Action> o <xref:System.Func%601> come parametro di callback e restituisce <xref:System.Windows.Threading.DispatcherOperation> o <xref:System.Windows.Threading.DispatcherOperation%601>.  Le classi <xref:System.Windows.Threading.DispatcherOperation%601> e <xref:System.Windows.Threading.DispatcherOperation> definisce una proprietà <xref:System.Threading.Tasks.Task>.  Quando si chiama <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>, è possibile utilizzare la parola chiave `await` con <xref:System.Windows.Threading.DispatcherOperation> o <xref:System.Threading.Tasks.Task>collegato.  Se è necessario attendere in modo sincrono <xref:System.Threading.Tasks.Task> restituito da <xref:System.Windows.Threading.DispatcherOperation> o da <xref:System.Windows.Threading.DispatcherOperation%601>, chiamare il metodo di estensione <xref:System.Windows.Threading.TaskExtensions.DispatcherOperationWait%2A>.  Chiamare <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> restituisce un deadlock se l'operazione è in coda in un thread chiamante.  Per ulteriori informazioni su l <xref:System.Threading.Tasks.Task> per eseguire operazioni asincrone, vedere [Parallelismo fra attività \(Task Parallel Library\)](../../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md).  
  
<a name="events_markup_extenions"></a>   
## Estensioni di markup per gli eventi  
 Estensioni di markup supporti WPF 4,5 per gli eventi.  In WPF non definisce un'estensione di markup da utilizzare per gli eventi, le terze parti possono creare un'estensione di markup che può essere utilizzata con gli eventi.  
  
## Vedere anche  
 [Novità di .NET Framework](../../../../docs/framework/whats-new/index.md)