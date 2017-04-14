---
title: "Cenni preliminari sulle animazioni personalizzate | Microsoft Docs"
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
  - "animazione, classi personalizzate"
  - "personalizzate (classi di animazione)"
  - "classi personalizzate, animazione"
  - "personalizzati (fotogrammi chiave)"
  - "fotogrammi chiave, personalizzati"
ms.assetid: 9be69d50-3384-4938-886f-08ce00e4a7a6
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sulle animazioni personalizzate
Questo argomento descrive come e quando estendere il sistema di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] creando fotogrammi chiave personalizzati, classi di animazione oppure utilizzando il callback per frame per evitare l'operazione.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere i diversi tipi di animazione forniti da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per ulteriori informazioni, vedere [Cenni preliminari sulle animazioni From\/To\/By](../../../../docs/framework/wpf/graphics-multimedia/from-to-by-animations-overview.md), [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md) e [Panoramica sulle animazioni percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md).  
  
 Dato che le classi di animazione ereditano dalla classe <xref:System.Windows.Freezable>, dovrebbero essere noti gli oggetti <xref:System.Windows.Freezable> e come ereditare dalla classe <xref:System.Windows.Freezable>.  Per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
<a name="extendingtheanimationsystem"></a>   
## Estensione del sistema di animazione  
 Esistono molti modi di estende il sistema di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], in base al livello di funzionalità incorporate che si desidera utilizzare.  Sono tre i punti di estendibilità principali nel motore di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   Creare un oggetto fotogramma chiave personalizzato ereditando da una delle classi *\<Tipo\>*KeyFrame, come <xref:System.Windows.Media.Animation.DoubleKeyFrame>.  Questo approccio utilizza la maggior parte delle funzionalità incorporate del motore di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Creare classi di animazione personalizzate ereditando da <xref:System.Windows.Media.Animation.AnimationTimeline> o da una delle classi *\<Tipo\>*AnimationBase.  
  
-   Utilizzare il callback per frame per generare animazioni per ogni frame.  Questo approccio ignora completamente il sistema di animazione e di temporizzazione.  
  
 Nella tabella riportata di seguito vengono descritti alcuni degli scenari per l'estensione del sistema di animazione.  
  
|Per|Utilizzare il seguente approccio|  
|---------|--------------------------------------|  
|Personalizzare l'interpolazione tra i valori di un tipo che abbia una classe *\<Tipo\>*AnimationUsingKeyFrames corrispondente.|Creare un fotogramma chiave personalizzato.  Per ulteriori informazioni, vedere la sezione [Creare un fotogramma chiave personalizzato](#createacustomkeyframe).|  
|Personalizzare più che la semplice interpolazione tra i valori di un tipo che abbia una classe *\<Tipo\>*Animation corrispondente.|Creare una classe di animazione personalizzata che erediti dalla classe *\<Tipo\>*AnimationBase che corrisponde al tipo che si desidera animare.  Per ulteriori informazioni, vedere la sezione [Creare una classe di animazione personalizzata](#createcustomanimationtype).|  
|Animare un tipo che non abbia un'animazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corrispondente|Utilizzare un oggetto <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> oppure creare una classe che erediti da <xref:System.Windows.Media.Animation.AnimationTimeline>.  Per ulteriori informazioni, vedere la sezione [Creare una classe di animazione personalizzata](#createcustomanimationtype).|  
|Animare più oggetti con valori calcolati per ogni fotogramma e che si basano sull'ultimo insieme di interazioni oggetto.|Utilizzare il callback per frame.  Per ulteriori informazioni, vedere la sezione [Creare un callback per frame](#useperframecallback).|  
  
<a name="createacustomkeyframe"></a>   
## Creare un fotogramma chiave personalizzato  
 La creazione di una classe di fotogrammi chiave personalizzati è il modo più semplice di estendere il sistema di animazione.  Utilizzare questo approccio quando si desidera un metodo di interpolazione diverso per un'animazione con fotogrammi chiave.  Come descritto in [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md), un'animazione con fotogrammi chiave utilizza oggetti fotogrammi chiave per generare i valori di output.  Ogni oggetto fotogramma chiave consente di eseguire tre funzioni:  
  
-   Specifica un valore di destinazione mediante la relativa proprietà <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>.  
  
-   Specifica il momento in cui tale valore deve essere raggiunto utilizzando la proprietà <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> relativa.  
  
-   Crea un'interpolazione tra il valore del fotogramma chiave precedente e quello del proprio valore implementando il metodo InterpolateValueCore.  
  
 **Istruzioni per l'implementazione**  
  
 Effettuare la derivazione dalla classe astratta *\<Tipo\>*KeyFrame e implementare il metodo InterpolateValueCore.  Il metodo InterpolateValueCore restituisce il valore corrente del fotogramma chiave.  Accetta due parametri, vale a dire il valore del fotogramma chiave precedente e un valore di avanzamento che va da 0 a 1.  Un avanzamento pari a 0 indica che il fotogramma chiave è appena iniziato e un valore pari a 1 indica che il fotogramma chiave è appena stato completato e che deve restituire il valore specificato dalla relativa proprietà <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>.  
  
 Dato che la classe *\<Tipo\>*KeyFrame eredita dalla classe <xref:System.Windows.Freezable>, è anche necessario eseguire l'override della classe <xref:System.Windows.Freezable.CreateInstanceCore%2A> per restituire una nuova istanza della classe.  Se la classe non utilizza le [proprietà di dipendenza](GTMT) per archiviare i dati o richiede un'ulteriore inizializzazione dopo la creazione, potrebbe essere necessario eseguire l'override di altri metodi; per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 Dopo avere creato l'animazione *\<Tipo\>*KeyFrame personalizzata, è possibile utilizzarla con *\<Tipo\>*AnimationUsingKeyFrames per tale tipo.  
  
<a name="createacustomanimationtype"></a>   
## Creare una classe di animazione personalizzata  
 La creazione di un tipo di animazione personalizzato consente un maggiore controllo sul modo in cui un oggetto viene animato.  Sono due i modi consigliati per creare un tipo di animazione personalizzata. È possibile effettuare la derivazione dalla classe <xref:System.Windows.Media.Animation.AnimationTimeline> o dalla classe *\<Tipo\>*AnimationBase.  La derivazione dalla classe *\<Tipo\>*Animation o *\<Tipo\>*AnimationUsingKeyFrames non è consigliata.  
  
### Derivazione dalla classe \<Tipo\>AnimationBase  
 La derivazione da una classe *\<Tipo\>*AnimationBase è il modo più semplice di creare un nuovo tipo di animazione.  Utilizzare questo approccio quando si desidera creare una nuova animazione per il tipo che dispone già di una classe *\<Tipo\>*AnimationBase corrispondente.  
  
 **Istruzioni per l'implementazione**  
  
 Effettuare la derivazione da una classe *\<Tipo\>*Animation e implementare il metodo GetCurrentValueCore.  Il metodo GetCurrentValueCore restituisce il valore corrente dell'animazione.  Accetta tre parametri, vale a dire un valore iniziale suggerito, un valore finale suggerito e un oggetto <xref:System.Windows.Media.Animation.AnimationClock>, che viene utilizzato per determinare l'avanzamento dell'animazione.  
  
 Dato che la classe *\<Tipo\>*AnimationBase eredita dalla classe <xref:System.Windows.Freezable>, è anche necessario eseguire l'override della classe <xref:System.Windows.Freezable.CreateInstanceCore%2A> per restituire una nuova istanza della classe.  Se la classe non utilizza le [proprietà di dipendenza](GTMT) per archiviare i dati o richiede un'ulteriore inizializzazione dopo la creazione, potrebbe essere necessario eseguire l'override di altri metodi; per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 Per ulteriori informazioni, vedere la documentazione relativa al metodo GetCurrentValueCore per la classe *\<Tipo\>*AnimationBase per il tipo che si desidera animare.  Per un esempio, vedere [Esempio di animazione personalizzata](http://go.microsoft.com/fwlink/?LinkID=159981) \(la pagina potrebbe essere in inglese\).  
  
 **Approcci alternativi**  
  
 Se si desidera semplicemente modificare il modo in cui i valori dell'animazione vengono interpolati, si prenda in considerazione la derivazione da una delle classi *\<Tipo\>*KeyFrame.  Il fotogramma chiave creato può essere utilizzato con la classe *\<Tipo\>*AnimationUsingKeyFrames corrispondente fornita da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Derivazione dalla classe AnimationTimeline  
 Effettuare la derivazione dalla classe <xref:System.Windows.Media.Animation.AnimationTimeline> quando si desidera creare un'animazione per un tipo che non dispone già di un'animazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corrispondente o se si desidera creare un'animazione che non sia fortemente tipizzata.  
  
 **Istruzioni per l'implementazione**  
  
 Effettuare la derivazione dalla classe <xref:System.Windows.Media.Animation.AnimationTimeline> e l'override dei seguenti membri:  
  
-   <xref:System.Windows.Freezable.CreateInstanceCore%2A>: se la nuova classe è concreta, è necessario eseguire l'override di <xref:System.Windows.Freezable.CreateInstanceCore%2A> per restituire una nuova istanza della classe.  
  
-   <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A>: eseguire l'override di questo metodo per restituire il valore corrente dell'animazione.  Accetta tre parametri: un valore di origine predefinito, un valore di destinazione predefinito e un oggetto <xref:System.Windows.Media.Animation.AnimationClock>.  Utilizzare l'oggetto <xref:System.Windows.Media.Animation.AnimationClock> per ottenere il momento corrente o lo stato di avanzamento dell'animazione.  È possibile scegliere se utilizzare i valori di origine e di destinazione predefiniti.  
  
-   <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A>: eseguire l'override di questa proprietà per indicare se l'animazione utilizza il valore di destinazione predefinito specificato dal metodo <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A>.  
  
-   <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A>: eseguire l'override di questa proprietà per indicare l'oggetto <xref:System.Type> di output prodotto dall'animazione.  
  
 Se la classe non utilizza le [proprietà di dipendenza](GTMT) per archiviare i dati o richiede un'ulteriore inizializzazione dopo la creazione, potrebbe essere necessario eseguire l'override di altri metodi; per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 Il paradigma consigliato \(utilizzato dall'animazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]\) consiste nell'utilizzare due livelli di ereditarietà:  
  
1.  Creare una classe astratta *\<Tipo\>*AnimationBase che deriva da <xref:System.Windows.Media.Animation.AnimationTimeline>.  Questa classe deve eseguire l'override del metodo <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A>.  Deve anche introdurre un nuovo metodo astratto, GetCurrentValueCore, ed eseguire l'override di <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> per consentire la convalida dei tipi dei parametri del valore di origine predefinito e del valore di destinazione predefinito, quindi chiama GetCurrentValueCore.  
  
2.  Creare un'altra classe che erediti dalla nuova classe *\<Tipo\>*AnimationBase ed esegua l'override del metodo <xref:System.Windows.Freezable.CreateInstanceCore%2A>, del metodo GetCurrentValueCore introdotto e della proprietà <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A>.  
  
 **Approcci alternativi**  
  
 Se si desidera animare un tipo che non ha alcuna animazione From\/To\/By o animazione con fotogrammi chiave corrispondente, si prenda in considerazione l'utilizzo di un oggetto <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>.  Poiché ha una tipizzazione debole, un oggetto <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> può animare qualsiasi tipo di valore.  Lo svantaggio di questo approccio consiste nel fatto che l'oggetto <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> supporta solo l'[interpolazione discreta](GTMT).  
  
<a name="useperframecallback"></a>   
## Utilizzare il callback per frame  
 Utilizzare questo approccio quando è necessario ignorare completamente il sistema di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Uno scenario di questo approccio è rappresentato dalle animazioni fisiche, dove a ciascun passaggio dell'animazione è necessario ricalcolare una nuova direzione o posizione degli oggetti animati in base all'ultima serie di interazioni dell'oggetto.  
  
 **Istruzioni per l'implementazione**  
  
 A differenza degli altri approcci descritti in questi cenni preliminari, per utilizzare un callback per frame non è necessario creare un'animazione personalizzata o una classe con fotogrammi chiave.  
  
 Al contrario si esegue la registrazione per l'evento <xref:System.Windows.Media.CompositionTarget.Rendering> dell'oggetto che contiene gli oggetti da animare.  Questo metodo per la gestione eventi viene chiamato una volta per ciascun frame.  Ogni volta che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esegue il marshalling dei dati di rendering permanenti della [struttura ad albero visuale](GTMT) nella struttura ad albero della composizione, viene chiamato il metodo per la gestione eventi.  
  
 Nel gestore eventi eseguire i calcoli necessari per l'effetto di animazione e impostare le proprietà degli oggetti da animare con tali valori.  
  
 Per ottenere l'ora di presentazione del frame corrente, è possibile eseguire il cast dell'oggetto <xref:System.EventArgs> associato a questo evento come <xref:System.Windows.Media.RenderingEventArgs> che fornisce una proprietà <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> utilizzabile per ottenere l'ora di rendering del frame corrente.  
  
 Per ulteriori informazioni, vedere la pagina <xref:System.Windows.Media.CompositionTarget.Rendering>.  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.AnimationTimeline>   
 <xref:System.Windows.Media.Animation.IKeyFrame>   
 [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Cenni preliminari sulle animazioni From\/To\/By](../../../../docs/framework/wpf/graphics-multimedia/from-to-by-animations-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Panoramica sulle animazioni percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [Esempio di animazione personalizzata](http://go.microsoft.com/fwlink/?LinkID=159981)