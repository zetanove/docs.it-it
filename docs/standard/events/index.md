---
title: "Gestione e generazione di eventi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sviluppo di applicazioni [.NET Framework], eventi"
  - "modello delegato per eventi"
  - "eventi [.NET Framework]"
ms.assetid: b6f65241-e0ad-4590-a99f-200ce741bb1f
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# Gestione e generazione di eventi
Il funzionamento degli eventi in .NET Framework è basato sul modello a delegati.  Il modello di progettazione osservato dal seguente modello delegato, che consente la registrazione e di ricevere informazioni da un provider.  Un evento del mittente inserisce una notifica di un evento verificato e un ricevitore di eventi riceve la notifica e definisce una risposta.  Questo articolo descrive i componenti principali del modello delegato, come utilizzare gli eventi nelle applicazioni e come implementare eventi nel codice.  
  
 Per informazioni sulla gestione di eventi nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], vedere [Cenni preliminari su eventi ed eventi indirizzati \(applicazioni di Windows Store\)](http://go.microsoft.com/fwlink/p/?LinkId=261485).  
  
## Eventi  
 Un evento è un messaggio inviato da un oggetto per segnalare il verificarsi di un'azione.  L'azione può essere causata dall'utente, ad esempio il clic su un pulsante oppure può essere generata da un altro programma logico, ad esempio modificare le proprietà di un valore.  L'oggetto che genera l'evento viene definito *Evento mittente*.  Il mittente dell'evento non sa quale oggetto o metodo riceverà \(dovrà gestire\) gli eventi generati.  L'evento è in genere un membro dell'evento mittente; ad esempio, l'evento <xref:System.Web.UI.WebControls.Button.Click> è un membro della classe <xref:System.Web.UI.WebControls.Button> e l'evento <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> è un membro di una classe che implementa l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
 Per definire un evento, utilizzare `event` \(in C\#\) o la parola chiave `Event` \(in Visual Basic\) nella firma della classe evento e specificare il tipo di delegato per l'evento.  I delegati sono descritti nella successiva sezione.  
  
 In genere, per generare un evento, si aggiunge un metodo contrassegnato come `protected` e `virtual` \(in C\#\) o `Protected` e `Overridable` \(in Visual Basic\).  Denominare il metodo `On`*EventName*; ad esempio `OnDataReceived`.  Il metodo deve accettare un parametro che specifica un oggetto dato.  Fornire questo metodo per consentire alle classi derivate di eseguire la sostituzione logica per generare l'evento.  Perché l'evento sia ricevuto da delegati registrati, occorre che una classe derivata chiami sempre il metodo `On`*EventName* della classe di base.  
  
 Il seguente esempio mostra come dichiarare un evento denominato `ThresholdReached`:  L'evento viene associato al delegato con il <xref:System.EventHandler> e viene generato in un metodo denominato `OnThresholdReached`.  
  
 [!code-csharp[EventsOverview#1](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#1)]
 [!code-vb[EventsOverview#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#1)]  
  
## Delegati  
 Un delegato è un tipo che mantiene le referenze di un metodo.  Un delegato è dichiarato con una firma che mostra il tipo restituito e i parametri per i metodi a cui fa riferimento e può contenere solo riferimenti a i metodi che corrispondono alla firma.  Un delegato è pertanto equivalente a un callback o a un puntatore a funzione indipendente dai tipi.  La dichiarazione di un delegato è sufficiente a definire una classe delegata.  
  
 I delegati sono molti utilizzati in .NET Framework.  Nel contesto degli eventi, un delegato è un intermediario \(o meccanismo di tipo puntatore\) tra l'origine dell'evento e il codice che gestisce l'evento.  Associa un delegato con un evento includendo la dichiarazione del tipo nella dichiarazione dell'evento, come mostrato nell'esempio nella sezione precedente.  Per ulteriori informazioni su i delegati, vedere la classe <xref:System.Delegate>.  
  
 .NET Framework fornisce i delegati <xref:System.EventHandler%601> e <xref:System.EventHandler> per supportare la maggior parte degli scenari di evento.  Utilizzare il delegato <xref:System.EventHandler> per tutti gli eventi che non includono dati.  Utilizzare il delegato <xref:System.EventHandler%601> per gli eventi che includono dati nell'evento.  Questi delegati non hanno un valore del tipo di ritorno e accettano due parametri \(un oggetto per l'evento origine e un oggetto per i dati dell'evento\).  
  
 I delegati sono multicast, il che significa che possono mantenere riferimenti a più metodi di gestione eventi.  Per informazioni dettagliate, vedere la pagina di riferimento <xref:System.Delegate>.  I delegati forniscono flessibilità e un controllo avanzato nella gestione eventi.  Un delegato comunica gli eventi della classe che genera l'evento mantenendo un elenco dei gestori eventi registrati per quell'evento.  
  
 Per gli scenari in cui i delegati <xref:System.EventHandler%601> e <xref:System.EventHandler> non funzionano, è possibile definire un delegato.  Gli scenari che richiedono di definire un delegato sono molto rari, ad esempio quando è necessario utilizzare il codice che non riconosce generics.  Contrassegnare un delegato con `delegate` in \(C\#\) e la parola chiave nella dichiarazione `Delegate` \(in Visual Basic\).  Nell'esempio riportato di seguito, viene illustrato come dichiarare un delegato denominato `ThresholdReachedEventHandler`.  
  
 [!code-csharp[EventsOverview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#4)]
 [!code-vb[EventsOverview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#4)]  
  
## Dati evento  
 I dati associati a un evento possono essere forniti tramite una classe di dati dell'evento.  .NET Framework fornisce molte classi dati dell'evento, che sono possibili da utilizzare nelle applicazioni.  Ad esempio, la classe <xref:System.IO.Ports.SerialDataReceivedEventArgs> è la classe di dati di evento per l'evento <xref:System.IO.Ports.SerialPort.DataReceived?displayProperty=fullName>.  .NET Framework riporta il seguente modello di denominazione per interrompere tutte le classi dati dell'evento con `EventArgs`.  Determina quale classe dati dell'evento è associata con un evento valutando il delegato dell'evento.  Ad esempio, il delegato <xref:System.IO.Ports.SerialDataReceivedEventHandler> include la classe <xref:System.IO.Ports.SerialDataReceivedEventArgs> come uno dei parametri.  
  
 La classe <xref:System.EventArgs> è il tipo di base per tutte le classi di dati dell'evento.  <xref:System.EventArgs> è anche la classe da utilizzare quando un evento non ha dati associati.  Quando si crea un evento che deve solo notificare ad altre classi che qualcosa è accaduto, non necessita di passare tutti i dati, ma include la classe <xref:System.EventArgs> come secondo parametro del delegato.  È possibile passare il valore <xref:System.EventArgs.Empty?displayProperty=fullName> quando non vengono forniti dati.  Il delegato <xref:System.EventHandler> include la classe <xref:System.EventArgs> come parametro.  
  
 Quando si desidera creare una classe di dati di evento personalizzata, creare una classe che deriva da <xref:System.EventArgs>quindi assegnare tutti i membri necessari per passare i dati correlati all'evento.  In genere, è consigliabile utilizzare lo stesso modello di denominazione di .NET Framework e terminare con il nome di classe dati dell'evento con `EventArgs`.  
  
 Nell'esempio seguente, viene illustrata una classe dati dell'evento denominata `ThresholdReachedEventArgs`.  Contiene le proprietà specifiche all'evento appena generato.  
  
 [!code-csharp[EventsOverview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#3)]
 [!code-vb[EventsOverview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#3)]  
  
## Gestori di eventi  
 Per rispondere a un evento, definire un metodo ricevitore nel gestore degli eventi.  Questo metodo deve corrispondere alla firma del delegato per l'evento gestito.  Nel gestore eventi, l'esecuzione delle azioni avviene quando l'evento viene generato, come la raccolta degli input che l'utente ha inserito prima di selezionare il pulsante.  Per ricevere notifiche quando si verifica l'evento, il metodo gestore degli eventi deve sottoscrivere l'evento.  
  
 Nell'esempio seguente viene illustrato un metodo per gestori gli eventi denominato `c_ThresholdReached` che corrisponde alla firma del delegato <xref:System.EventHandler>.  Il metodo sottoscrive l'evento `ThresholdReached`.  
  
 [!code-csharp[EventsOverview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#2)]
 [!code-vb[EventsOverview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#2)]  
  
## Gestori eventi statici e dinamici  
 .NET Framework consente di sottoscrivere la registrazione, per le notifiche degli eventi in modo statico e dinamico.  I gestori eventi statici hanno effetto per l'intera durata della classe di cui possono gestire gli eventi.  I gestori eventi dinamici vengono attivati e disattivati in modo esplicito durante l'esecuzione del programma, in genere in risposta a una logica di programma condizionale.  Ad esempio, possono essere utilizzati se le notifiche di eventi sono necessarie solo in determinate condizioni oppure se l'applicazione fornisce più gestori eventi e le condizioni di runtime definiscono quello appropriato da utilizzare.  L'esempio nella sezione precedente mostra come aggiungere dinamicamente un gestore eventi.  Per ulteriori informazioni, vedere [Events](../Topic/Events%20\(Visual%20Basic\).md) e [Eventi](../Topic/Events%20\(C%23%20Programming%20Guide\).md).  
  
## Generazione di più eventi  
 Se la classe genera più eventi, il compilatore genera un campo per un'istanza di un evento delegato.  In presenza di un gran numero di eventi, il costo della memorizzazione di un campo per ogni delegato può rivelarsi eccessivo.  Per questi casi, .NET Framework fornisce delle proprietà dell'evento rendendo possibile l'utilizzo di altre strutture dati scelte per memorizzare i delegati dell'evento.  
  
 Le proprietà evento sono composte da dichiarazioni di eventi accompagnate dalle funzioni di accesso agli eventi.  I metodi di accesso agli eventi che sono definiti per aggiungere o rimuovere istanze di eventi delegati dalla struttura dati memorizzata.  Si noti che le proprietà dell'evento sono più lente dei campi evento, perché ogni delegato dell'evento deve essere recuperato prima di essere invocato.  Si pone pertanto la necessità di scegliere tra risparmio di memoria e velocità.  Se la propria classe definisce molti eventi che vengono generati di rado, è possibile che si preferisca implementare le proprietà evento.  Per ulteriori informazioni, vedere [Procedura: gestire più eventi mediante le relative proprietà](../../../docs/standard/events/how-to-handle-multiple-events-using-event-properties.md).  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Procedura: generare e utilizzare eventi](../../../docs/standard/events/how-to-raise-and-consume-events.md)|Contiene esempi di eventi generati e utilizzati.|  
|[Procedura: gestire più eventi mediante le relative proprietà](../../../docs/standard/events/how-to-handle-multiple-events-using-event-properties.md)|Viene visualizzata come utilizzare le proprietà di un evento per gestire più eventi.|  
|[Modello di progettazione observer](../../../docs/standard/events/observer-design-pattern.md)|Viene descritto il modello di progettazione che consente all'utente di registrarsi e ricevere notifiche da un provider.|  
|[Procedura: Usare eventi in un'applicazione Web Form](../../../docs/standard/events/how-to-consume-events-in-a-web-forms-application.md)|Viene visualizzata la procedura per gestire un evento generato da un controllo Web Form.|  
  
## Vedere anche  
 <xref:System.EventHandler>   
 <xref:System.EventHandler%601>   
 <xref:System.EventArgs>   
 <xref:System.Delegate>   
 [Cenni preliminari su eventi ed eventi indirizzati \(applicazioni di Windows Store\)](http://go.microsoft.com/fwlink/?LinkId=261485)   
 [Events](../Topic/Events%20\(Visual%20Basic\).md)   
 [Eventi](../Topic/Events%20\(C%23%20Programming%20Guide\).md)