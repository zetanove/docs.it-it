---
title: "Supporto .NET Framework per applicazioni Windows Store e Windows Runtime | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "app di Windows Store, supporto per .NET Framework"
  - "Windows Runtime, supporto per .NET Framework"
  - ".NET per app di Windows Store"
  - ".NET Framework e app di Windows Store"
  - ".NET Framework e Windows Runtime"
ms.assetid: 6fa7d044-ae12-4c54-b8ee-50915607a565
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# Supporto .NET Framework per applicazioni Windows Store e Windows Runtime
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] supporta numerosi scenari di sviluppo software con [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Questi scenari sono suddivisi in tre categorie:  
  
-   Lo sviluppo di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] App con controlli XAML, come descritto in [Roadmap per applicazioni Windows Store utilizzando c# o Visual Basic](http://go.microsoft.com/fwlink/p/?LinkID=242212), [di sviluppo Windows Store (VB / c# o C++ e XAML)](http://go.microsoft.com/fwlink/p/?LinkId=238311), e [Panoramica le applicazioni .NET per Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=238312) nel Centro sviluppatori Windows.  
  
-   Sviluppo di librerie di classi da utilizzare nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] create con .NET Framework.  
  
-   Sviluppo di componenti [!INCLUDE[wrt](../../../includes/wrt-md.md)], inclusi in un pacchetto in file con estensione WinMD, che possono essere utilizzati con qualsiasi linguaggio di programmazione che supporti [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Ad esempio, vedere [la creazione di componenti Windows Runtime in c# e Visual Basic](http://go.microsoft.com/fwlink/p/?LinkId=238313) nel Centro sviluppatori Windows.  
  
 In questo argomento viene descritto il supporto fornito da .NET Framework per tutte e tre le categorie e vengono illustrati gli scenari per i componenti [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Nella prima sezione sono incluse informazioni di base sulla relazione tra .NET Framework e [!INCLUDE[wrt](../../../includes/wrt-md.md)] e vengono spiegate alcune singolarità che si possono verificare nel sistema della Guida e nell'IDE. Il [seconda sezione](#WindowsRuntimeComponents) vengono illustrati gli scenari per lo sviluppo di [!INCLUDE[wrt](../../../includes/wrt-md.md)] componenti.  
  
## <a name="the-basics"></a>Nozioni di base  
 .NET Framework supporta i tre scenari di sviluppo elencati in precedenza fornendo [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] e supportando [!INCLUDE[wrt](../../../includes/wrt-md.md)] stesso.  
  
-   [.NET per applicazioni Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=247912) fornisce una visualizzazione semplice delle librerie di classi .NET Framework e includere solo i tipi e membri è possibile utilizzare per creare [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] App e [!INCLUDE[wrt](../../../includes/wrt-md.md)] componenti.  
  
    -   Quando si utilizza Visual Studio ([!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] o versioni successive) per sviluppare un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] o un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)], grazie a un set di assembly di riferimento è possibile visualizzare solo i tipi e i membri appropriati.  
  
    -   Questo set di API efficace viene semplificato ulteriormente con la rimozione di funzionalità che sono duplicate in .NET Framework o tramite cui vengono duplicate funzionalità di [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Ad esempio, sono incluse solo le versioni generiche di tipi di raccolta e il modello a oggetti del documento XML viene eliminato a favore del set di API XML di [!INCLUDE[wrt](../../../includes/wrt-md.md)].  
  
    -   Anche le funzionalità tramite cui viene eseguito semplicemente il wrapping delle API del sistema operativo vengono rimosse, dal momento che [!INCLUDE[wrt](../../../includes/wrt-md.md)] è semplice da chiamare dal codice gestito.  
  
     Per ulteriori informazioni di [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)], vedere il [Panoramica le applicazioni .NET per Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=238312) in Center.To di sviluppo Windows leggere informazioni sul processo di selezione di API, vedere il [.NET per applicazioni Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=251061) voce nel blog di .NET.  
  
-   Il [Windows Runtime](http://go.microsoft.com/fwlink/p/?LinkId=238319) fornisce all'utente elementi dell'interfaccia per la creazione di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] applicazioni e fornisce accesso alle funzionalità del sistema operativo. Come per .NET Framework, in [!INCLUDE[wrt](../../../includes/wrt-md.md)] sono disponibili metadati che consentono ai compilatori C# e Visual Basic di utilizzare [!INCLUDE[wrt](../../../includes/wrt-md.md)] nello stesso modo in cui utilizzano le librerie di classi .NET Framework. .NET Framework semplifica l'utilizzo di [!INCLUDE[wrt](../../../includes/wrt-md.md)] nascondendo alcune differenze:  
  
    -   Vengono celate alcune differenze nei modelli di programmazione tra .NET Framework e [!INCLUDE[wrt](../../../includes/wrt-md.md)], ad esempio il modello per aggiungere e rimuovere i gestori di eventi. È sufficiente utilizzare il modello di .NET Framework.  
  
    -   Vengono celate alcune differenze nei tipi comunemente utilizzati, ad esempio i tipi primitivi e le raccolte. È sufficiente utilizzare il tipo di .NET Framework, come descritto in [differenze visibili nell'IDE](#DifferencesVisibleInIDE), più avanti in questo articolo.  
  
 In genere, il supporto di .NET Framework per [!INCLUDE[wrt](../../../includes/wrt-md.md)] è trasparente. Nella sezione successiva vengono illustrate alcune delle differenze evidenti tra il codice gestito e [!INCLUDE[wrt](../../../includes/wrt-md.md)].  
  
<a name="AboutReferenceDocumentation"></a>   
### <a name="the-net-framework-and-the-includewrttokenwrtmdmd-reference-documentation"></a>Documentazione di riferimento di .NET Framework e [!INCLUDE[wrt](../../../includes/wrt-md.md)]  
 I set di documentazione di Windows e .NET Framework sono separati. Se si preme F1 per visualizzare la Guida su un tipo o un membro, viene visualizzata la documentazione di riferimento del set appropriato. Tuttavia, se si scorre il [riferimento di Windows Runtime](http://go.microsoft.com/fwlink/p/?LinkId=238319) è possibile riscontrare esempi dubbi:  
  
-   Gli argomenti, ad esempio il [interfaccia IIterable](http://go.microsoft.com/fwlink/p/?LinkId=238321) non dispongono di sintassi di dichiarazione per Visual Basic o c#. Al contrario, viene visualizzata una nota sopra la sezione sintassi (in questo caso, ".NET: questa interfaccia viene visualizzata come IEnumerable<>\>"). Ciò si verifica perché .NET Framework e [!INCLUDE[wrt](../../../includes/wrt-md.md)] forniscono funzionalità simili con interfacce differenti. Inoltre, esistono differenze di comportamento: `IIterable` ha un `First` metodo anziché un <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> per restituire l'enumeratore. Anziché dover apprendere un modo diverso per eseguire un'attività comune, .NET Framework supporta [!INCLUDE[wrt](../../../includes/wrt-md.md)] visualizzando il codice gestito per utilizzare il tipo noto all'utente. L'interfaccia `IIterable` non verrà visualizzata nell'IDE e, pertanto, l'unico modo per riscontrarla nella documentazione di riferimento di [!INCLUDE[wrt](../../../includes/wrt-md.md)] è scorrere direttamente la documentazione in questione.  
  
-   Il [costruttore SyndicationFeed](http://go.microsoft.com/fwlink/p/?LinkId=238322) documentazione viene illustrato un problema strettamente correlato: I tipi di parametro sembrano essere differenti per le diverse lingue. Per c# e Visual Basic, i tipi di parametro sono <xref:System.String?displayProperty=fullName> e <xref:System.Uri?displayProperty=fullName>. Inoltre, questa situazione si verifica in quanto .NET Framework dispone di propri tipi `String` e `Uri` e, per questi tipi comunemente utilizzati, non ha senso imporre agli utenti di .NET Framework di apprendere un modo diverso per eseguire le operazioni. Nell'IDE .NET Framework nasconde i corrispondenti tipi [!INCLUDE[wrt](../../../includes/wrt-md.md)].  
  
-   In alcuni casi, ad esempio il [Windows.UI.Xaml.GridLength](http://go.microsoft.com/fwlink/p/?LinkId=251059) struttura, .NET Framework fornisce un tipo con lo stesso nome ma con ulteriori funzionalità. Ad esempio, un set di argomenti su costruttori e proprietà è associato a `GridLength`, ma con blocchi di sintassi solo per Visual Basic e C# perché i membri sono disponibili solo nel codice gestito. In [!INCLUDE[wrt](../../../includes/wrt-md.md)] le strutture dispongono solo di campi. Il [!INCLUDE[wrt](../../../includes/wrt-md.md)] struttura richiede una classe helper, [Windows.UI.Xaml.GridLengthHelper](http://go.microsoft.com/fwlink/p/?LinkId=251060), per fornire funzionalità equivalenti. Non verrà visualizzata la classe di supporto nell'IDE quando si scrive il codice gestito.  
  
-   Nell'IDE, [!INCLUDE[wrt](../../../includes/wrt-md.md)] sembrano derivare da tipi <xref:System.Object?displayProperty=fullName>. Sembrano disporre di membri ereditati da <xref:System.Object>, ad esempio <xref:System.Object.ToString%2A?displayProperty=fullName>. Questi membri funzionano come se i tipi ereditassero effettivamente da <xref:System.Object>, e [!INCLUDE[wrt](../../../includes/wrt-md.md)] tipi possono essere convertiti in <xref:System.Object>. Questa funzionalità fa parte del supporto fornito da .NET Framework per [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Tuttavia, se si visualizzano i tipi nella documentazione di riferimento di [!INCLUDE[wrt](../../../includes/wrt-md.md)], non viene visualizzato alcun membro. La documentazione per questi membri apparentemente ereditati viene fornita per il <xref:System.Object?displayProperty=fullName> documentazione di riferimento.  
  
<a name="DifferencesVisibleInIDE"></a>   
### <a name="differences-that-are-visible-in-the-ide"></a>Differenze visibili nell'IDE  
 In scenari di programmazione più avanzati, quali l'utilizzo di un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] scritto in C# per fornire la logica per un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] compilata per Windows utilizzando JavaScript, queste differenze sono evidenti nell'IDE, nonché nella documentazione. Quando il componente restituisce un'interfaccia `IDictionary<int, string>` a JavaScript e l'utente lo esamina nel debugger di JavaScript, visualizzerà i metodi di `IMap<int, string>` poiché viene utilizzato il tipo [!INCLUDE[wrt](../../../includes/wrt-md.md)] da parte di JavaScript. Alcuni tipi di raccolte comunemente utilizzati che vengono visualizzati in modo diverso nei due linguaggi sono riportati nella tabella seguente:  
  
|Tipo [!INCLUDE[wrt](../../../includes/wrt-md.md)]|Tipo .NET Framework corrispondente|  
|--------------------------------------------------------------|---------------------------------------|  
|`IIterable<T>`|`IEnumerable<T>`|  
|`IIterator<T>`|`IEnumerator<T>`|  
|`IVector<T>`|`IList<T>`|  
|`IVectorView<T>`|`IReadOnlyList<T>`|  
|`IMap<K, V>`|`IDictionary<TKey, TValue>`|  
|`IMapView<K, V>`|`IReadOnlyDictionary<TKey, TValue>`|  
|`IBindableIterable`|`IEnumerable`|  
|`IBindableVector`|`IList`|  
|`Windows.UI.Xaml.Data.INotifyPropertyChanged`|`System.ComponentModel.INotifyPropertyChanged`|  
|`Windows.UI.Xaml.Data.PropertyChangedEventHandler`|`System.ComponentModel.PropertyChangedEventHandler`|  
|`Windows.UI.Xaml.Data.PropertyChangedEventArgs`|`System.ComponentModel.PropertyChangedEventArgs`|  
  
 In [!INCLUDE[wrt](../../../includes/wrt-md.md)], `IMap<K, V>` e `IMapView<K, V>` vengono iterate utilizzando `IKeyValuePair`. Quando vengono passate al codice gestito, vengono visualizzate come `IDictionary<TKey, TValue>` e `IReadOnlyDictionary<TKey, TValue>`, ed è quindi naturale utilizzare `System.Collections.Generic.KeyValuePair<TKey, TValue>` per enumerarle.  
  
 Il modo in cui le interfacce vengono visualizzate nel codice gestito influisce sul modo in cui vengono visualizzati i tipi tramite cui vengono implementate queste interfacce. Ad esempio, la classe `PropertySet` implementa `IMap<K, V>`, che compare nel codice gestito come `IDictionary<TKey, TValue>`. `PropertySet` compare come se avesse implementato `IDictionary<TKey, TValue>` anziché `IMap<K, V>`, dunque nel codice gestito risulta avere un metodo `Add` che si comporta come il metodo `Add` nei dizionari di .NET Framework. Non risulta avere un metodo `Insert`.  
  
 Per ulteriori informazioni sull'utilizzo di .NET Framework per creare un [!INCLUDE[wrt](../../../includes/wrt-md.md)] componente e una procedura dettagliata che illustra come utilizzare un componente con JavaScript, vedere [la creazione di componenti Windows Runtime in c# e Visual Basic](http://go.microsoft.com/fwlink/p/?LinkId=238313) nel Centro sviluppatori Windows.  
  
### <a name="primitive-types"></a>Tipi primitivi  
 Per abilitare l'utilizzo naturale di [!INCLUDE[wrt](../../../includes/wrt-md.md)] nel codice gestito, vengono visualizzati i tipi primitivi di .NET Framework anziché quelli di [!INCLUDE[wrt](../../../includes/wrt-md.md)] nel codice. In .NET Framework i tipi primitivi quali la struttura `Int32` presentano numerosi metodi e proprietà utili, ad esempio il metodo `Int32.TryParse`. Al contrario, i tipi primitivi e le strutture di [!INCLUDE[wrt](../../../includes/wrt-md.md)] dispongono solo di campi. Quando si utilizzano le primitive nel codice gestito, sembrano essere tipi .NET Framework e si possono utilizzare le proprietà e i metodi dei tipi .NET Framework normalmente. Nell'elenco seguente viene fornito un riepilogo:  
  
-   Per le primitive [!INCLUDE[wrt](../../../includes/wrt-md.md)] `Int32`, `Int64`, `Single`, `Double`, `Boolean`, `String` (una raccolta non modificabile di caratteri Unicode), `Enum`, `UInt32`, `UInt64` e `Guid`, utilizzare il tipo con lo stesso nome nello spazio dei nomi `System`.  
  
-   Per `UInt8`, utilizzare `System.Byte`.  
  
-   Per `Char16`, utilizzare `System.Char`.  
  
-   Per l'interfaccia `IInspectable`, utilizzare `System.Object`.  
  
-   Per `HRESULT`, utilizzare una struttura con un membro `System.Int32`.  
  
 Analogamente ai tipi di interfaccia, l'unico caso in cui si potrebbe verificare l'evidenza di questa rappresentazione è quando il progetto .NET Framework è un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] utilizzato da un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] compilata tramite JavaScript.  
  
 Altri base utilizzati comunemente [!INCLUDE[wrt](../../../includes/wrt-md.md)] tipi visualizzati nel codice gestito come equivalenti di .NET Framework prevedono la `Windows.Foundation.DateTime` struttura, viene visualizzata nel codice gestito come il <xref:System.DateTimeOffset?displayProperty=fullName> struttura e `Windows.Foundation.TimeSpan` struttura, viene visualizzato come il <xref:System.TimeSpan?displayProperty=fullName> struttura.  
  
### <a name="other-differences"></a>Altre differenze  
 In alcuni casi, poiché nel codice gestito vengono visualizzati i tipi .NET Framework anziché i tipi [!INCLUDE[wrt](../../../includes/wrt-md.md)], sono necessarie azioni aggiuntive. Ad esempio, il [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376) classe viene visualizzata come <xref:System.Uri?displayProperty=fullName> nel codice .NET Framework. <xref:System.Uri?displayProperty=fullName> consente a un URI relativo, ma [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376) richiede un URI assoluto. Pertanto, quando si passa un URI a un metodo di [!INCLUDE[wrt](../../../includes/wrt-md.md)], è necessario assicurarsi che sia assoluto. (Vedere [passaggio di un URI a Windows Runtime](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md).)  
  
<a name="WindowsRuntimeComponents"></a>   
## <a name="scenarios-for-developing-windows-runtime-components"></a>Scenari per lo sviluppo di componenti Windows Runtime  
 Gli scenari supportati per i componenti [!INCLUDE[wrt](../../../includes/wrt-md.md)] gestiti dipendono dai seguenti principi generali:  
  
-   I componenti [!INCLUDE[wrt](../../../includes/wrt-md.md)] compilati tramite .NET Framework non presentano differenze evidenti rispetto ad altre librerie [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Ad esempio, se si implementa di nuovo un componente nativo [!INCLUDE[wrt](../../../includes/wrt-md.md)] tramite codice gestito, i due componenti sono apparentemente indistinguibili. Il fatto che il componente sia scritto in codice gestito non è visibile al codice in cui viene utilizzato, anche se il codice è esso stesso codice gestito. Tuttavia, internamente, il componente è realmente codice gestito e viene eseguito in Common Language Runtime (CLR).  
  
-   Nei componenti possono essere contenuti tipi tramite cui viene implementata la logica dell'applicazione, i controlli dell'interfaccia utente di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] o entrambi.  
  
    > [!NOTE]
    >  È consigliabile separare gli elementi dell'interfaccia utente dalla logica dell'applicazione. Inoltre, non è possibile utilizzare i controlli dell'interfaccia utente di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] in un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] compilata per Windows utilizzando JavaScript e HTML.  
  
-   Un componente può essere un progetto all'interno di una soluzione Visual Studio per un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] oppure un componente riutilizzabile che è possibile aggiungere a più soluzioni.  
  
    > [!NOTE]
    >  Se il componente verrà utilizzato solo con C# o Visual Basic, non vi è alcun motivo di convertirlo in un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Se lo si rende invece una comune libreria di classi .NET Framework, non è necessario limitare la relativa superficie dell'API pubblica a tipi [!INCLUDE[wrt](../../../includes/wrt-md.md)].  
  
-   È possibile rilasciare versioni di componenti riutilizzabili tramite il [!INCLUDE[wrt](../../../includes/wrt-md.md)] [VersionAttribute](http://go.microsoft.com/fwlink/p/?LinkId=238563) attributo per identificare i tipi (e i membri all'interno di un tipo) sono state aggiunte nelle diverse versioni.  
  
-   I tipi nel componente possono derivare da tipi [!INCLUDE[wrt](../../../includes/wrt-md.md)]. I controlli possono derivare da tipi di controllo primitivi nel [Windows.UI.Xaml.Controls.Primitives](http://go.microsoft.com/fwlink/p/?LinkId=238564) dello spazio dei nomi o da controlli più avanzati, ad esempio [pulsante](http://go.microsoft.com/fwlink/p/?LinkId=238565).  
  
    > [!IMPORTANT]
    >  A partire da [!INCLUDE[win8](../../../includes/win8-md.md)] e [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], tutti i tipi pubblici in un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] gestito devono essere sealed. Un tipo in un altro componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] non può derivare da questi. Se si desidera fornire il comportamento polimorfico nel componente, è possibile creare un'interfaccia e implementarla nei tipi polimorfici.  
  
-   Tutti i parametri e i tipi restituiti nei tipi pubblici nel componente devono essere tipi [!INCLUDE[wrt](../../../includes/wrt-md.md)], inclusi i tipi [!INCLUDE[wrt](../../../includes/wrt-md.md)] definiti dal componente in questione.  
  
 Nelle sezioni seguenti vengono forniti esempi di scenari comuni.  
  
### <a name="application-logic-for-a-includewin8appnamelongtokenwin8appnamelongmdmd-app-with-javascript"></a>Logica di un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] con JavaScript  
 Quando si sviluppa un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] per Windows utilizzando JavaScript, è possibile che alcune parti della logica dell'applicazione vengano eseguite in maniera ottimale nel codice gestito o risultino più semplici da sviluppare. Con JavaScript non è possibile utilizzare direttamente le librerie di classi .NET Framework, ma si può rendere la libreria di classi un file con estensione WinMD. In questo scenario, il componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] è parte integrante dell'applicazione, pertanto può non essere opportuno fornire attributi della versione.  
  
### <a name="reusable-includewin8appnamelongtokenwin8appnamelongmdmd-ui-controls"></a>Controlli riutilizzabili dell'interfaccia utente di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]  
 È possibile inserire in un pacchetto un set di controlli correlati dell'interfaccia utente in un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] riutilizzabile. Il componente può essere commercializzato da solo o utilizzato come elemento nelle applicazioni create. In questo scenario, è opportuno utilizzare il [!INCLUDE[wrt](../../../includes/wrt-md.md)] [VersionAttribute](http://go.microsoft.com/fwlink/p/?LinkId=238563) attributi per migliorare la compatibilità.  
  
### <a name="reusable-application-logic-from-existing-net-framework-apps"></a>Logica di un'applicazione riutilizzabile da applicazioni .NET Framework esistenti  
 È possibile inserire in un pacchetto il codice gestito di applicazioni desktop esistenti come componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] autonomo. In questo modo è possibile utilizzare il componente in applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] compilate con C++ o JavaScript, nonché in applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] compilate con C# o Visual Basic. Il controllo delle versioni rappresenta un'opzione in caso di più scenari di riutilizzo del codice.  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Panoramica delle app .NET per Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=238312)|Descrive i tipi e i membri di .NET Framework usabili per creare app [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] e componenti [!INCLUDE[wrt](../../../includes/wrt-md.md)]. In Dev Center di Windows.|  
|[Guida di orientamento per applicazioni Windows Store utilizzando c# o Visual Basic](http://go.microsoft.com/fwlink/p/?LinkId=242212)|Fornisce risorse chiave per iniziare a sviluppare applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] utilizzando C# o Visual Basic, inclusi molti argomenti della guida rapida, linee guida e procedure consigliate. In Dev Center di Windows.|  
|[Lo sviluppo di applicazioni Windows Store (VB / c# o C++ e XAML)](http://go.microsoft.com/fwlink/p/?LinkId=238311)|Fornisce risorse chiave per iniziare a sviluppare applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] utilizzando C# o Visual Basic, inclusi molti argomenti della guida rapida, linee guida e procedure consigliate. In Dev Center di Windows.|  
|[Creazione di componenti Windows Runtime in c# e Visual Basic](http://go.microsoft.com/fwlink/p/?LinkId=238313)|Viene illustrato come creare un componente [!INCLUDE[wrt](../../../includes/wrt-md.md)] utilizzando .NET Framework, viene spiegato come utilizzarlo come parte di un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] compilata per Windows utilizzando JavaScript e viene descritto come eseguire il debug della combinazione con Visual Studio. In Dev Center di Windows.|  
|[Riferimento di Windows Runtime](http://go.microsoft.com/fwlink/?LinkId=238319)|Documentazione di riferimento per [!INCLUDE[wrt](../../../includes/wrt-md.md)]. In Dev Center di Windows.|  
|[Passaggio di un URI a Windows Runtime](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)|Viene descritto un problema che può verificarsi quando si passa un URI dal codice gestito a [!INCLUDE[wrt](../../../includes/wrt-md.md)] e come evitare questo inconveniente.|