---
title: "Modelli di eventi deboli | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "gestori eventi, modello di eventi deboli"
  - "IWeakEventListener (interfaccia)"
  - "implementazione del modello di eventi deboli"
  - "WeakEventManager (classe)"
ms.assetid: e7c62920-4812-4811-94d8-050a65c856f6
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Modelli di eventi deboli
Nelle applicazioni, è possibile che i gestori associati a origini evento non vengano eliminati insieme all'oggetto listener che ha associato il gestore all'origine.  Tale situazione può causare perdite di memoria.  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] introduce un modello di progettazione che può essere utilizzato per risolvere questo problema, fornendo una classe di gestione dedicata per eventi particolari e implementando un'interfaccia nei listener relativi all'evento in questione.  Questo modello di progettazione è noto come *modello di evento debole*.  
  
## Vantaggi offerti dall'implementazione del modello di evento debole  
 L'utilizzo di listener di eventi può causare perdite di memoria.  La tecnica standard di ascolto di un evento consiste nell'utilizzare la sintassi specifica del linguaggio che associa un gestore a un evento in un'origine.  In [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)], ad esempio, la sintassi è la seguente: `source.SomeEvent += new SomeEventHandler(MyEventHandler)`.  
  
 Questa tecnica crea un riferimento forte dall'origine evento al listener di eventi.  Di norma, l'associazione di un gestore eventi per un listener fa sì che la durata dell'oggetto del listener sia influenzata dalla durata dell'oggetto dell'origine, a meno che il gestore eventi non venga rimosso in modo esplicito.  In determinate circostanze, tuttavia, è possibile che la durata dell'oggetto del listener sia controllata da altri fattori, ad esempio l'eventuale appartenenza del listener alla struttura ad albero visuale dell'applicazione, non dalla durata dell'origine.  Se la durata dell'origine va oltre la durata del listener, il modello di eventi standard causa una perdita di memoria: il listener viene tenuto vivo più a lungo di quanto previsto.  
  
 Il modello di evento debole è progettato per risolvere questo problema di perdita di memoria  e può essere utilizzato ogni qualvolta un listener deve effettuare la registrazione per un evento ma non conosce in modo esplicito il momento in cui annullare la registrazione.  Il modello di evento debole può inoltre essere utilizzato ogni qualvolta la durata dell'oggetto dell'origine supera la durata dell'oggetto utile del listener.  In questo caso, *utile* è determinato dall'utente. Il modello di evento debole consente al listener di registrarsi per l'evento e riceverlo senza influire in alcun modo sulle caratteristiche di durata dell'oggetto del listener.  Di fatto, il riferimento implicito dall'origine non determina l'eventuale idoneità del listener per Garbage Collection.  Si tratta di un riferimento debole, da cui la denominazione del modello di evento debole e delle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] correlate.  Il listener può essere sottoposto a Garbage Collection o altrimenti eliminato e l'origine può continuare senza mantenere riferimenti del gestore non sottoponibili a Garbage Collection relativi a un oggetto ora eliminato.  
  
## Identificazione dei soggetti più indicati per l'implementazione del modello di evento debole  
 L'implementazione del modello di evento debole sarà interessante soprattutto per gli autori dei controlli,  responsabili in larga parte del comportamento e del contenimento del controllo oltre che dell'impatto che questo ha sulle applicazioni nelle quali viene inserito.  Ciò include il comportamento relativo alla durata dell'oggetto del controllo, in particolare la gestione del problema di perdita di memoria descritto.  
  
 Determinati scenari si prestano implicitamente all'applicazione del modello di evento debole.  Uno di questi è l'associazione dati.  Nell'associazione dati accade comunemente che l'oggetto di origine sia completamente indipendente dall'oggetto listener, che è una destinazione di un'associazione.  Il modello di evento debole viene già applicato a molti aspetti dell'associazione dati [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] rispetto al modo in cui vengono implementati gli eventi.  
  
## Modalità di implementazione del modello di evento debole  
 Esistono tre modi per implementare il modello di evento debole.  Nella tabella seguente sono elencati i tre approcci e fornisce alcune linee guida per l'utilizzo di.  
  
|Approccio|quando implementare|  
|---------------|-------------------------|  
|Utilizzare una classe debole esistente del gestore degli eventi|Se l'evento che si desidera sottoscrivere ha una corrispondenza <xref:System.Windows.WeakEventManager>, utilizzare il gestore di evento debole esistente.  Per un elenco di gestori degli eventi deboli inclusi in WPF, vedere la gerarchia di ereditarietà in <xref:System.Windows.WeakEventManager> classe.  Si noti, tuttavia, che sono relativamente pochi gestori degli eventi deboli inclusi in WPF, pertanto sarà probabilmente necessario selezionare uno degli altri approcci.|  
|Utilizzare una classe debole generica del gestore degli eventi|Utilizzare un oggetto generico <xref:System.Windows.WeakEventManager%602> quando un oggetto esistente  <xref:System.Windows.WeakEventManager> non è disponibile, si desidera che un modo semplice per implementare e non quanto riguarda efficienza.  L'oggetto generico <xref:System.Windows.WeakEventManager%602> è meno efficiente di esistente o un gestore di evento debole personalizzato.  Ad esempio, la classe generica consente più reflection per individuare l'evento specificato il nome dell'evento.  Inoltre, il codice per registrare l'evento utilizzando l'oggetto generico <xref:System.Windows.WeakEventManager%602> è più dettagliato di utilizzo di un oggetto esistente o di un oggetto personalizzato  <xref:System.Windows.WeakEventManager>.|  
|Creare una classe debole personalizzata del gestore degli eventi|Creare un oggetto personalizzato <xref:System.Windows.WeakEventManager> quando si esistente  <xref:System.Windows.WeakEventManager> non è disponibile e si desidera che il migliore efficienza.  Utilizzando un oggetto personalizzato <xref:System.Windows.WeakEventManager> per sottoscrivere un evento sarà più efficiente, ma si incorre il costo di scrittura del codice nella parte superiore.|  
  
 Nelle sezioni seguenti viene descritto come implementare il modello di evento debole.  Ai fini di questa discussione, l'evento da sottoscrivere presenta le caratteristiche descritte di seguito.  
  
-   il nome di evento è `SomeEvent`.  
  
-   L'evento viene generato da `EventSource` classe.  
  
-   Il gestore eventi il tipo: `SomeEventEventHandler` o  `EventHandler<SomeEventEventArgs>`\).  
  
-   l'evento passa un parametro di tipo `SomeEventEventArgs` i gestori eventi.  
  
### Utilizzando una classe debole esistente del gestore degli eventi  
  
1.  Trovare un gestore di evento debole esistente.  
  
     Per un elenco di gestori degli eventi deboli inclusi in WPF, vedere la gerarchia di ereditarietà in <xref:System.Windows.WeakEventManager> classe.  
  
2.  Utilizzare il nuovo gestore di evento debole anziché collegamento normale dell'evento.  
  
     Ad esempio, se il codice utilizza il modello seguente per sottoscrivere un evento:  
  
    ```  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     Modificare il seguente modello:  
  
    ```  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     Analogamente, se il codice utilizza il modello seguente per annullare la sottoscrizione a un evento:  
  
    ```  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     Modificare il seguente modello:  
  
    ```  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
### Utilizzando la classe debole generica del gestore degli eventi  
  
1.  Utilizzare l'oggetto generico <xref:System.Windows.WeakEventManager%602> classe anziché collegamento normale dell'evento.  
  
     Quando si utilizzano <xref:System.Windows.WeakEventManager%602> per registrare listener di eventi, fornire origine eventi e  <xref:System.EventArgs> tipo come parametri di tipo alla classe e alla chiamata  <xref:System.Windows.WeakEventManager%602.AddHandler%2A> come illustrato nel codice seguente:  
  
    ```  
    WeakEventManager<EventSource, SomeEventEventArgs>.AddHandler(source, "SomeEvent", source_SomeEvent);  
    ```  
  
### Creare una classe debole personalizzata del gestore degli eventi  
  
1.  Copiare il seguente modello di classe al progetto.  
  
     Questa classe eredita dalla classe <xref:System.Windows.WeakEventManager>.  
  
     [!code-csharp[WeakEvents#WeakEventManagerTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WeakEvents/CSharp/WeakEventManagerTemplate.cs#weakeventmanagertemplate)]  
  
2.  Sostituire `SomeEventWeakEventManager` nome con un nome.  
  
3.  Sostituire i tre nomi descritti in precedenza con i nomi corrispondenti per l'evento.  \(`SomeEvent`,  `EventSource`e  `SomeEventEventArgs`\)  
  
4.  Per impostare la visibilità \(pubblica\/interna\/privata\) della classe debole del gestore degli eventi alla stessa visibilità di gestisce l'evento.  
  
5.  Utilizzare il nuovo gestore di evento debole anziché collegamento normale dell'evento.  
  
     Ad esempio, se il codice utilizza il modello seguente per sottoscrivere un evento:  
  
    ```  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     Modificare il seguente modello:  
  
    ```  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     Analogamente, se il codice utilizza il modello seguente per annullare la sottoscrizione a un evento:  
  
    ```  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     Modificare il seguente modello:  
  
    ```  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.WeakEventManager>   
 <xref:System.Windows.IWeakEventListener>   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)