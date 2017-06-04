---
title: "Cenni preliminari sugli eventi di tempo | Microsoft Docs"
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
  - "Clock (classe)"
  - "classi, orologio"
  - "sequenze temporali"
  - "eventi di temporizzazione"
ms.assetid: 597e3280-0867-4359-a97b-5b2f4149e350
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Cenni preliminari sugli eventi di tempo
In questo argomento viene descritto come utilizzare i cinque eventi di temporizzazione disponibile in <xref:System.Windows.Media.Animation.Timeline> e <xref:System.Windows.Media.Animation.Clock> oggetti.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
## <a name="prerequisites"></a>Prerequisiti  
 In questo argomento, è necessario comprendere come creare e utilizzare le animazioni. Per informazioni introduttive sull'animazione, vedere il [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Esistono diversi modi per animare le proprietà in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   **Utilizzo di oggetti storyboard** (markup e codice): È possibile utilizzare <xref:System.Windows.Media.Animation.Storyboard> oggetti di disporre e distribuire animazioni a uno o più oggetti. Per un esempio, vedere [animare una proprietà utilizzando uno Storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md).  
  
-   **Utilizzo di animazioni locali** (solo codice): È possibile applicare <xref:System.Windows.Media.Animation.AnimationTimeline> oggetti direttamente alle proprietà animate. Per un esempio, vedere [animare una proprietà senza utilizzare uno Storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
-   **Utilizzo di orologi** (solo codice): È possibile gestire la creazione di orologi e distribuire direttamente gli orologi di animazione in modo esplicito.  Per un esempio, vedere [animare una proprietà utilizzando un oggetto AnimationClock](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-an-animationclock.md).  
  
 Poiché è possibile utilizzarli nel markup e codice, utilizzano gli esempi in questa panoramica <xref:System.Windows.Media.Animation.Storyboard> oggetti. Tuttavia, i concetti descritti applicabile ad altri metodi di animazione delle proprietà.  
  
### <a name="what-is-a-clock"></a>Che cos'è un orologio?  
 Una sequenza temporale, da sola, in realtà non diverso da descrivere un intervallo di tempo. È la sequenza temporale <xref:System.Windows.Media.Animation.Clock> oggetto che esegue il lavoro effettivo: la gestione dello stato di runtime correlati alla temporizzazione per la sequenza temporale. Nella maggior parte dei casi, ad esempio quando tramite storyboard, viene creato automaticamente un orologio per la sequenza temporale. È inoltre possibile creare un <xref:System.Windows.Media.Animation.Clock> in modo esplicito utilizzando il <xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> metodo. Per ulteriori informazioni su <xref:System.Windows.Media.Animation.Clock> degli oggetti, vedere il [Animation and Timing System Overview](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).  
  
## <a name="why-use-events"></a>Perché utilizzare eventi?  
 Fatta eccezione per uno (ricerca allineata all'ultimo evento tick), tutte le operazioni interattive intervallo sono asincrone. Non è possibile sapere esattamente quando verrà eseguito. Che può essere un problema quando è presente altro codice che dipende dall'operazione di tempo. Si supponga che si desidera interrompere una sequenza temporale che anima un rettangolo. Dopo la sequenza temporale si interrompe, si modifica il colore del rettangolo.  
  
 [!code-csharp[events_procedural#NeedForEventsFragment](../../../../samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#needforeventsfragment)]
 [!code-vb[events_procedural#NeedForEventsFragment](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#needforeventsfragment)]  
  
 Nell'esempio precedente, la seconda riga di codice potrebbe essere eseguita prima dell'interruzione dello storyboard. Ciò avviene perché l'arresto è un'operazione asincrona. Una sequenza temporale o orologio arrestare crea una "richiesta di arresto" di tipi che non viene elaborata fino tick successivo del motore di temporizzazione.  
  
 Per eseguire comandi dopo il completamento di una sequenza temporale, utilizzare gli eventi di temporizzazione. Nell'esempio seguente, un gestore eventi viene usato per modificare il colore di un rettangolo dopo lo storyboard viene interrotta la riproduzione.  
  
 [!code-csharp[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#registerforstoryboardcurrentstateinvalidatedevent)]
 [!code-vb[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#registerforstoryboardcurrentstateinvalidatedevent)]  
[!code-csharp[events_procedural#StoryboardCurrentStateInvalidatedEvent2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#storyboardcurrentstateinvalidatedevent2)]
[!code-vb[events_procedural#StoryboardCurrentStateInvalidatedEvent2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#storyboardcurrentstateinvalidatedevent2)]  
  
 Per un esempio più completo, vedere [modifiche dello stato di ricevere notifica quando un orologio](../../../../docs/framework/wpf/graphics-multimedia/how-to-receive-notification-when-clock-state-changes.md).  
  
## <a name="public-events"></a>Eventi pubblici  
 Il <xref:System.Windows.Media.Animation.Timeline> e <xref:System.Windows.Media.Animation.Clock> classi forniscono entrambe cinque eventi di temporizzazione. Nella tabella seguente sono elencati questi eventi e le condizioni che le attivano.  
  
|Evento|Operazione interattiva di attivazione|Altri trigger|  
|-----------|--------------------------------------|--------------------|  
|**Completato**|Passaggio al riempimento|L'orologio viene completato.|  
|**CurrentGlobalSpeedInvalidated**|Sospendere, riprendere, ricerca, impostazione di frequenza velocità, andare al riempimento, interruzione|L'orologio inverte, accelera, avvia o arresta.|  
|**CurrentStateInvalidated**|Inizio, passaggio al riempimento, interruzione|L'orologio viene avviato, si arresta o si riempie.|  
|**CurrentTimeInvalidated**|Inizio, ricerca, andare al riempimento, interruzione|L'orologio avanza.|  
|**RemoveRequested**|Rimuovi||  
  
## <a name="ticking-and-event-consolidation"></a>Eventi Tick e consolidamento di eventi  
 Quando si animare oggetti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è il motore di temporizzazione che gestisce le animazioni. Il motore di temporizzazione tiene traccia dell'avanzare del tempo e calcola lo stato di ogni animazione. In questo modo numerosi passaggi di valutazione in un secondo. Questi passaggi di valutazione sono note come "tick".  
  
 Segni di graduazione si verificano di frequente, ma è possibile per molte operazioni da eseguire tra segni di graduazione. Ad esempio, una sequenza temporale può essere arrestata, avviata e nuovamente interrotta, nel qual caso lo stato corrente verrà cambiato tre volte. In teoria, l'evento può essere generato in un singolo tick; Tuttavia, il motore di temporizzazione consolida gli eventi, in modo che ogni evento può essere generato più di una volta per tick.  
  
## <a name="registering-for-events"></a>Registrazione per gli eventi  
 Esistono due modi per registrare gli eventi di temporizzazione: è possibile registrare la sequenza temporale o con l'orologio creato dalla sequenza temporale. La registrazione di un evento direttamente con un orologio è piuttosto semplice, anche se può essere eseguita solo dal codice. È possibile registrare gli eventi con una sequenza temporale dal codice o markup. Nella sezione successiva viene descritto come registrare gli eventi di orologio con una sequenza temporale.  
  
<a name="registeringforclockeventswithatimeline"></a>   
## <a name="registering-for-clock-events-with-a-timeline"></a>Registrazione per gli eventi di orologio con una sequenza temporale  
 Anche se una sequenza temporale <xref:System.Windows.Media.Animation.Timeline.Completed>, <xref:System.Windows.Media.Animation.Timeline.CurrentGlobalSpeedInvalidated>, <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated>, <xref:System.Windows.Media.Animation.Timeline.CurrentTimeInvalidated>, e <xref:System.Windows.Media.Animation.Timeline.RemoveRequested> gli eventi vengono visualizzati da associare con la sequenza temporale, la registrazione per questi eventi associa in effetti un gestore eventi con il <xref:System.Windows.Media.Animation.Clock> creato per la sequenza temporale.  
  
 Quando si registra per il <xref:System.Windows.Media.Animation.Timeline.Completed> evento in una sequenza temporale, ad esempio, si indica al sistema di registrazione per il <xref:System.Windows.Media.Animation.Clock.Completed> evento di ogni orologio creato per la sequenza temporale. Nel codice, è necessario registrare questo evento prima di <xref:System.Windows.Media.Animation.Clock> viene creato per questa sequenza temporale; in caso contrario, si riceverà la notifica. Ciò si verifica automaticamente in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; registra automaticamente il parser per l'evento prima di <xref:System.Windows.Media.Animation.Clock> viene creato.  
  
## <a name="see-also"></a>Vedere anche  
 [Animazione e temporizzazione Panoramica sistema](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sui comportamenti di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)