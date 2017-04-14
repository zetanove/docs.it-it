---
title: "Cenni preliminari sugli oggetti Freezable | Microsoft Docs"
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
  - "classi, Freezable"
  - "Freezable (oggetti), description"
  - "sblocco di oggetti Freezable"
ms.assetid: 89c71692-4f43-4057-b611-67c6a8a863a2
caps.latest.revision: 30
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# Cenni preliminari sugli oggetti Freezable
In questo argomento viene descritto come creare e utilizzare in modo efficace gli oggetti <xref:System.Windows.Freezable> che forniscono funzionalità speciali per migliorare le prestazioni dell'applicazione.  Tra gli esempi di oggetti Freezable sono inclusi pennelli, penne, trasformazioni, geometrie e animazioni.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="whatisafreezable"></a>   
## Definizione di oggetto Freezable  
 <xref:System.Windows.Freezable> è un tipo di oggetto speciale con due stati: non bloccato e bloccato.  Quando non è bloccato, <xref:System.Windows.Freezable> si comporta come gli altri oggetti.  Quando è bloccato, <xref:System.Windows.Freezable> non può più essere modificato.  
  
 <xref:System.Windows.Freezable> fornisce un evento <xref:System.Windows.Freezable.Changed> per notificare gli osservatori di qualsiasi modifica all'oggetto.  Il blocco di un oggetto <xref:System.Windows.Freezable> consente di migliorarne le prestazioni poiché non è più necessario impiegare le risorse nelle notifiche di modifica.  Un oggetto <xref:System.Windows.Freezable> bloccato può anche essere condiviso tra thread mentre ciò non è possibile per gli oggetti <xref:System.Windows.Freezable> non bloccati.  
  
 Sebbene la classe <xref:System.Windows.Freezable> disponga di molte applicazioni, la maggior parte degli oggetti <xref:System.Windows.Freezable> in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] si riferisce al sottosistema grafico.  
  
 La classe <xref:System.Windows.Freezable> semplifica l'utilizzo di alcuni oggetti del sistema grafico e può aiutare a migliorare le prestazioni dell'applicazione.  Tra gli esempi di tipi che ereditano da <xref:System.Windows.Freezable> sono incluse le classi <xref:System.Windows.Media.Brush>, <xref:System.Windows.Media.Transform> e <xref:System.Windows.Media.Geometry>.  Poiché questi oggetti contengono risorse non gestite, il sistema deve monitorare le eventuali modifiche e quindi aggiornare le rispettive risorse non gestite quando viene apportata una modifica all'oggetto originale.  Anche se un oggetto del sistema grafico non viene effettivamente modificato, il sistema deve comunque impiegare parte delle proprie risorse per il monitoraggio dell'oggetto per verificare eventuali modifiche.  
  
 Ad esempio, si supponga di creare un pennello <xref:System.Windows.Media.SolidColorBrush> e di utilizzarlo per disegnare lo sfondo di un pulsante.  
  
 [!code-csharp[freezablesample_procedural#FrozenExamplePart1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart1)]
 [!code-vb[freezablesample_procedural#FrozenExamplePart1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart1)]  
  
 Quando viene eseguito il rendering del pulsante, il sottosistema grafico di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza le informazioni fornite per disegnare un gruppo di pixel per definire l'aspetto di un pulsante.  Anche se è stato utilizzato un pennello a tinta unita per descrivere il disegno del pulsante, tale pennello non esegue effettivamente il disegno.  Il sistema grafico genera oggetti veloci e di basso livello per il pulsante e il pennello e sono questi gli oggetti che vengono effettivamente visualizzati sullo schermo.  
  
 Se fosse necessario modificare il pennello, questi oggetti di basso livello dovrebbero essere rigenerati.  La classe Freezable consente al pennello di trovare i corrispondenti oggetti di basso livello generati e di aggiornarli in caso di modifiche.  In questo caso, il pennello è definito "non bloccato".  
  
 Il metodo <xref:System.Windows.Freezable.Freeze%2A> di un oggetto Freezable consente di disabilitare questa funzione di aggiornamento automatico.  È possibile utilizzare questo metodo per "bloccare" il pennello o renderlo non modificabile.  
  
> [!NOTE]
>  Non tutti gli oggetti Freezable possono essere bloccati.  Per evitare di generare <xref:System.InvalidOperationException>, prima di provare a bloccare l'oggetto Freezable, verificare il valore della relativa proprietà <xref:System.Windows.Freezable.CanFreeze%2A> per determinare se può essere bloccato.  
  
 [!code-csharp[freezablesample_procedural#FrozenExamplePart2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart2)]
 [!code-vb[freezablesample_procedural#FrozenExamplePart2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart2)]  
  
 Quando non è più necessario modificare un oggetto Freezable, è possibile bloccarlo per migliorarne le prestazioni.  Se in questo esempio fosse necessario bloccare il pennello, il sistema grafico non lo monitorerebbe più per verificare la presenza di eventuali modifiche.  Il sistema grafico può anche eseguire ulteriori ottimizzazioni perché è evidente il pennello non sarà modificato.  
  
> [!NOTE]
>  Per comodità, gli oggetti Freezable restano non bloccati a meno che non vengano bloccati in modo esplicito.  
  
<a name="frozenfreezables"></a>   
## Utilizzo degli oggetti Freezable  
 L'utilizzo di un oggetto Freezable non bloccato è simile a quello di qualsiasi altro tipo di oggetto.  Nell'esempio riportato di seguito, il colore di <xref:System.Windows.Media.SolidColorBrush> viene modificato da giallo a rosso dopo essere stato utilizzato per disegnare lo sfondo di un pulsante.  Il sistema grafico modifica automaticamente il colore del pulsante da giallo a rosso al successivo aggiornamento dello schermo.  
  
 [!code-csharp[freezablesample_procedural#UnFrozenExampleShort](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#unfrozenexampleshort)]
 [!code-vb[freezablesample_procedural#UnFrozenExampleShort](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#unfrozenexampleshort)]  
  
### Blocco di un oggetto Freezable  
 Per rendere immodificabile <xref:System.Windows.Freezable>, è necessario chiamare il relativo metodo <xref:System.Windows.Freezable.Freeze%2A>.  Quando viene bloccato un oggetto contenente oggetti bloccabili, anche questi oggetti vengono bloccati.  Ad esempio, se si blocca <xref:System.Windows.Media.PathGeometry>, vengono bloccate anche le relative figure e segmenti.  
  
 Un oggetto Freezable **non può** essere bloccato se una delle seguenti condizioni è vera:  
  
-   Include proprietà animate o associate a dati.  
  
-   Include proprietà impostate da una risorsa dinamica.  \(Per ulteriori informazioni sulle risorse dinamiche, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)\).  
  
-   Contiene oggetti secondari <xref:System.Windows.Freezable> che non possono essere bloccati.  
  
 Se queste condizioni sono false e non si intende modificare <xref:System.Windows.Freezable>, è consigliabile bloccarlo per migliorare le prestazioni come descritto in precedenza.  
  
 Dopo aver chiamato il metodo <xref:System.Windows.Freezable.Freeze%2A> di un oggetto Freezable, non è più possibile apportarvi modifiche.  Il tentativo di modifica di un oggetto bloccato genera <xref:System.InvalidOperationException>.  Il codice riportato di seguito genera un'eccezione perché si tenta di modificare il pennello dopo che è stato bloccato.  
  
 [!code-csharp[freezablesample_procedural#ExceptionExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#exceptionexample)]
 [!code-vb[freezablesample_procedural#ExceptionExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#exceptionexample)]  
  
 Per evitare di generare questa eccezione, è possibile utilizzare il metodo <xref:System.Windows.Freezable.IsFrozen%2A> per determinare se un oggetto <xref:System.Windows.Freezable> è bloccato.  
  
 [!code-csharp[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
 [!code-vb[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]  
  
 Nell'esempio di codice precedente era stata eseguita una copia modificabile di un oggetto bloccato utilizzando il metodo <xref:System.Windows.Freezable.Clone%2A>.  La clonazione viene descritta in modo più dettagliato nella sezione seguente.  
  
 **Nota** Poiché un oggetto Freezable bloccato non può essere animato, il sistema di animazione crea automaticamente dei cloni modificabili degli oggetti <xref:System.Windows.Freezable> bloccati quando si tenta di animarli con <xref:System.Windows.Media.Animation.Storyboard>.  Per evitare la riduzione delle prestazioni provocata dalla clonazione, lasciare non bloccato l'oggetto che si intende animare.  Per ulteriori informazioni sull'animazione con gli storyboard, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
### Blocco dal markup  
 Per bloccare un oggetto <xref:System.Windows.Freezable> dichiarato nel markup, è necessario utilizzare l'attributo `PresentationOptions:Freeze`.  Nell'esempio riportato di seguito, <xref:System.Windows.Media.SolidColorBrush> viene dichiarato risorsa della pagina e viene bloccato.  Viene quindi utilizzato per impostare lo sfondo di un pulsante.  
  
 [!code-xml[FreezableSample#FreezeFromMarkupWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FreezableSample/CS/FreezeFromMarkupExample.xaml#freezefrommarkupwholepage)]  
  
 Per utilizzare l'attributo `Freeze`, è necessario eseguire il mapping allo spazio dei nomi delle opzioni di presentazione: `http://schemas.microsoft.com/winfx/2006/xaml/presentation/options`.  `PresentationOptions` è il prefisso consigliato per il mapping di questo spazio dei nomi:  
  
```  
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"   
```  
  
 Poiché non tutti i reader XAML riconoscono questo attributo, si consiglia di utilizzare [Attributo mc:Ignorable](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md) per contrassegnare l'attributo `Presentation:Freeze` come ignorabile:  
  
```  
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
mc:Ignorable="PresentationOptions"  
```  
  
 Per ulteriori informazioni, vedere la pagina [Attributo mc:Ignorable](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md).  
  
### Sblocco di un oggetto Freezable  
 Una volta bloccato, un oggetto <xref:System.Windows.Freezable> non può più essere modificato o sbloccato, tuttavia è possibile crearne un clone non bloccato utilizzando il metodo <xref:System.Windows.Freezable.Clone%2A> o <xref:System.Windows.Freezable.CloneCurrentValue%2A>.  
  
 Nell'esempio riportato di seguito, lo sfondo del pulsante viene impostato con un pennello che poi viene bloccato.  La copia non bloccata del pennello viene effettuata utilizzando il metodo <xref:System.Windows.Freezable.Clone%2A>.  Il clone viene modificato e utilizzato per modificare il colore dello sfondo da giallo a rosso.  
  
 [!code-csharp[freezablesample_procedural#CloneExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
> [!NOTE]
>  Indipendentemente dal metodo di clonazione utilizzato, le animazioni non vengono mai copiate nel nuovo oggetto <xref:System.Windows.Freezable>.  
  
 I metodi <xref:System.Windows.Freezable.Clone%2A> e <xref:System.Windows.Freezable.CloneCurrentValue%2A> eseguono copie complete dell'oggetto Freezable.  Se tale oggetto contiene altri oggetti Freezable bloccati, questi vengono a loro volta clonati e resi modificabili.  Ad esempio, se si clona un oggetto <xref:System.Windows.Media.PathGeometry> bloccato per renderlo modificabile, anche le figure e i segmenti in esso contenuti vengono copiati e resi modificabili.  
  
<a name="createyourownfreezableclass"></a>   
## Creazione di una classe Freezable personalizzata  
 Una classe che deriva da <xref:System.Windows.Freezable> ottiene le funzionalità riportate di seguito.  
  
-   Stati speciali: uno stato di sola lettura \(bloccato\) e uno stato scrivibile.  
  
-   Sicurezza dei thread: un oggetto <xref:System.Windows.Freezable> bloccato può essere condiviso tra thread.  
  
-   Notifica dettagliata delle modifiche: a differenza di altri oggetti <xref:System.Windows.DependencyObject>, gli oggetti Freezable forniscono notifiche di modifica quando vengono modificati i valori della proprietà secondaria.  
  
-   Clonazione facile: la classe Freezable ha già implementato molti metodi che producono cloni completi.  
  
 <xref:System.Windows.Freezable> è un tipo di <xref:System.Windows.DependencyObject> e perciò utilizza il sistema di proprietà di dipendenza.  Le proprietà di classe personalizzate non devono essere proprietà di dipendenza ma l'utilizzo di queste ultime consente di ridurre la quantità di codice da scrivere poiché la classe <xref:System.Windows.Freezable> è stata progettata tenendo presenti le proprietà di dipendenza.  Per ulteriori informazioni sul sistema di proprietà di dipendenza, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
 Ogni sottoclasse di <xref:System.Windows.Freezable> deve eseguire l'override del metodo <xref:System.Windows.Freezable.CreateInstanceCore%2A>.  Se la classe utilizza proprietà di dipendenza per tutti i dati, l'operazione è completa.  
  
 Se la classe contiene membri dati della proprietà di non dipendenza, è anche necessario eseguire l'override dei seguenti metodi:  
  
-   <xref:System.Windows.Freezable.CloneCore%2A>  
  
-   <xref:System.Windows.Freezable.CloneCurrentValueCore%2A>  
  
-   <xref:System.Windows.Freezable.GetAsFrozenCore%2A>  
  
-   <xref:System.Windows.Freezable.GetCurrentValueAsFrozenCore%2A>  
  
-   <xref:System.Windows.Freezable.FreezeCore%2A>  
  
 Per accedere e scrivere su membri dati che non sono proprietà di dipendenza è anche necessario osservare le seguenti regole:  
  
-   All'inizio di ogni [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] che legge i membri dati della proprietà di non dipendenza, è necessario chiamare il metodo <xref:System.Windows.Freezable.ReadPreamble%2A>.  
  
-   All'inizio di ogni API che scrive i membri dati della proprietà di non dipendenza, è necessario chiamare il metodo <xref:System.Windows.Freezable.WritePreamble%2A>.  Dopo aver chiamato <xref:System.Windows.Freezable.WritePreamble%2A> in un'[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)], non è necessario eseguire un'altra chiamata a <xref:System.Windows.Freezable.ReadPreamble%2A> se vengono letti anche i membri dati della proprietà di non dipendenza.  
  
-   È necessario chiamare il metodo <xref:System.Windows.Freezable.WritePostscript%2A> prima di uscire dai metodi che scrivono sui membri dati della proprietà di non dipendenza.  
  
 Se la classe personalizzata contiene membri dati della proprietà di non dipendenza che sono oggetti <xref:System.Windows.DependencyObject>, è necessario chiamare anche il metodo <xref:System.Windows.Freezable.OnFreezablePropertyChanged%2A> ogni volta che viene modificato uno dei relativi valori, anche se il membro viene impostato su `null`.  
  
> [!NOTE]
>  È molto importante iniziare ogni metodo <xref:System.Windows.Freezable> di cui si esegue l'override chiamando l'implementazione di base.  
  
 Per un esempio di classe <xref:System.Windows.Freezable> personalizzata, vedere [Esempio di animazione personalizzata](http://go.microsoft.com/fwlink/?LinkID=159981) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Freezable>   
 [Esempio di animazione personalizzata](http://go.microsoft.com/fwlink/?LinkID=159981)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)