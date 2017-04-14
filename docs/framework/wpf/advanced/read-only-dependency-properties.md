---
title: "Propriet&#224; di dipendenza di sola lettura | Microsoft Docs"
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
  - "proprietà di dipendenza, sola lettura"
  - "proprietà Dependency di sola lettura"
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Propriet&#224; di dipendenza di sola lettura
In questo argomento vengono descritte le proprietà di dipendenza di sola lettura, incluse proprietà di dipendenza di sola lettura esistenti e gli scenari e le tecniche per la creazione di una proprietà di dipendenza di sola lettura personalizzata.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="prerequisites"></a>   
## Prerequisiti  
 Nell'argomento si presuppone la conoscenza degli scenari di base dell'implementazione di una proprietà di dipendenza e del modo in cui i metadati vengono applicati a una proprietà di dipendenza personalizzata.  Per il contesto, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md) e [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
<a name="existing"></a>   
## Proprietà di dipendenza di sola lettura esistenti  
 Alcune delle proprietà di dipendenza definite nel framework [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] sono di sola lettura.  La ragione più comune per cui specificare una proprietà di dipendenza di sola lettura consiste nel fatto che si tratta di proprietà che devono essere utilizzate per la determinazione dello stato; tuttavia se tale stato è influenzato da una molteplicità di fattori, la semplice impostazione della proprietà su quello stato non rappresenta la soluzione appropriata dalla prospettiva di progettazione di un'interfaccia utente.  Ad esempio, la proprietà <xref:System.Windows.UIElement.IsMouseOver%2A> rappresenta realmente solo lo stato superficiale determinato dall'input del mouse.  Ogni tentativo di impostare questo valore a livello di codice aggirando il vero input del mouse sarebbe imprevedibile e potrebbe causare incongruenza.  
  
 Dal momento che non possono essere impostate, le proprietà di dipendenza di sola lettura non sono appropriate a molti degli scenari per i quali in genere tali proprietà offrono una soluzione \(vale a dire: associazione dati, possibilità di applicare direttamente uno stile a un valore, convalida, animazione, ereditarietà\).  Nonostante l'impossibilità a essere impostate, queste proprietà dispongono in ogni caso di alcune delle funzionalità aggiuntive supportate dalle proprietà dipendenza nel sistema di proprietà.  La funzionalità più importante consiste nel fatto che la proprietà di dipendenza di sola lettura può essere comunque utilizzata come trigger di proprietà in uno stile.  Non è possibile abilitare trigger con una proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] standard; è necessaria una proprietà di dipendenza.  La proprietà <xref:System.Windows.UIElement.IsMouseOver%2A> indicata in precedenza è un esempio perfetto di uno scenario in cui potrebbe essere piuttosto utile definire uno stile per un controllo in cui una proprietà visibile, ad esempio un sfondo, un primo piano o proprietà simili di elementi composti all'interno del controllo vengono modificate quando l'utente posiziona il mouse su un'area definita del controllo.  Le modifiche a una proprietà di dipendenza di sola lettura possono inoltre essere rilevate e segnalate dai processi di invalidazione inerenti del sistema di proprietà, che infatti è dotato del supporto interno della funzionalità del trigger di proprietà.  
  
<a name="new"></a>   
## Creazione di proprietà di dipendenza di sola lettura personalizzate  
 Assicurarsi di leggere la sezione precedente relativa ai motivi per i quali le proprietà di dipendenza di sola lettura non funzionano per molti scenari comuni di proprietà di dipendenza.  Se tuttavia si dispone di uno scenario adatto, è possibile creare una proprietà di dipendenza di sola lettura personalizzata.  
  
 Gran parte del processo di creazione di una proprietà di dipendenza di sola lettura è identica al processo descritto negli argomenti [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md) e [Implementare una proprietà di dipendenza](../../../../docs/framework/wpf/advanced/how-to-implement-a-dependency-property.md).  Esistono tuttavia tre differenze importanti:  
  
-   Al momento della registrazione della proprietà, chiamare il metodo <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A> anziché il metodo <xref:System.Windows.DependencyProperty.Register%2A> normale per la registrazione della proprietà.  
  
-   Quando si implementa la proprietà del "wrapper" [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], assicurarsi che nemmeno il wrapper disponga di un'implementazione impostata, in modo che non esista alcuna incongruenza nello stato di sola lettura per il wrapper pubblico che si espone.  
  
-   L'oggetto restituito dalla registrazione di sola lettura è <xref:System.Windows.DependencyPropertyKey> piuttosto che <xref:System.Windows.DependencyProperty>.  Sebbene sia necessario archiviare il campo come membro, questo in genere non viene reso un membro pubblico del tipo.  
  
 A prescindere dal campo privato o dal valore di cui si dispone, il backup della proprietà di dipendenza di sola lettura può essere scritto utilizzando qualsiasi logica.  Tuttavia, il modo più semplice per impostare la proprietà inizialmente o come parte della logica di runtime consiste nell'utilizzare le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] del sistema di proprietà, piuttosto che aggirare il sistema di proprietà e impostare direttamente il campo di backup.  In particolare, esiste una firma di <xref:System.Windows.DependencyObject.SetValue%2A> che accetta un parametro di tipo <xref:System.Windows.DependencyPropertyKey>.  Il modo e il punto in cui viene impostato questo valore a livello di codice all'interno della logica dell'applicazione influisce sulle opzioni disponibili per impostare l'accesso per l'oggetto <xref:System.Windows.DependencyPropertyKey> creato al momento della prima registrazione della proprietà di dipendenza.  Se questa logica viene gestita tutta all'interno della classe è possibile renderla privata o, se è necessario impostarla da un'altra porzione dell'assembly, è possibile impostarla come interna.  Un approccio consiste nel chiamare <xref:System.Windows.DependencyObject.SetValue%2A> all'interno del gestore eventi di una classe relativa a un evento rilevante che informa l'istanza di una classe che il valore della proprietà archiviato deve essere modificato.  Un altro approccio consiste nel collegare le proprietà di dipendenza utilizzando i callback <xref:System.Windows.PropertyChangedCallback> e <xref:System.Windows.CoerceValueCallback> come parte dei metadati di quelle proprietà durante la registrazione.  
  
 Poiché l'oggetto <xref:System.Windows.DependencyPropertyKey> è privato e non viene propagato al di fuori del codice dal sistema di proprietà, una proprietà di dipendenza di sola lettura dispone di una sicurezza delle impostazioni migliore rispetto a una proprietà di dipendenza di lettura e scrittura.  Per una proprietà di dipendenza di lettura e scrittura, il campo di identificazione è pubblico in modo esplicito oppure implicito, per cui la proprietà può essere impostata senza alcuna limitazione.  Per informazioni più specifiche, vedere [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md).  
  
## Vedere anche  
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)