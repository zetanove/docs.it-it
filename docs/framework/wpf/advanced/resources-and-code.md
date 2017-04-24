---
title: "Risorse e codice | Microsoft Docs"
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
  - "chiavi, utilizzo di oggetti come"
  - "codice procedurale, accesso alle risorse"
  - "codice procedurale, creazione delle risorse"
  - "risorse, accesso dal codice procedurale"
  - "risorse, creazione con il codice procedurale"
ms.assetid: c1cfcddb-e39c-41c8-a7f3-60984914dfae
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Risorse e codice
In questi cenni preliminari viene presentata la modalità di accesso alle risorse di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] o di creazione delle risorse stesse tramite codice anziché tramite la sintassi [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Per ulteriori informazioni sull'utilizzo delle risorse in generale e sulle risorse dal punto di vista della sintassi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
   
  
<a name="accessing"></a>   
## Accesso alle risorse dal codice  
 Le chiavi che consentono di identificare le risorse, se definite tramite [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], possono essere utilizzate anche per recuperare risorse specifiche qualora si richieda la risorsa nel codice.  Il modo più semplice per recuperare una risorsa dal codice consiste nel chiamare il metodo <xref:System.Windows.FrameworkElement.FindResource%2A> oppure il metodo <xref:System.Windows.FrameworkElement.TryFindResource%2A> da oggetti a livello framework presenti nell'applicazione.  La differenza di comportamento tra i due metodi consiste nell'azione eseguita quando la chiave richiesta non viene trovata.  <xref:System.Windows.FrameworkElement.FindResource%2A> genera un'eccezione; <xref:System.Windows.FrameworkElement.TryFindResource%2A> non genera un'eccezione ma restituisce `null`.  Ciascun metodo accetta la chiave di risorsa come parametro di input e restituisce un oggetto debolmente tipizzato.  In genere, una chiave di risorsa è costituita da una stringa, ma è possibile che talvolta si verifichino utilizzi non stringa; per informazioni dettagliate, vedere la sezione [Utilizzo di oggetti come chiavi](#objectaskey).  Di regola, il cast dell'oggetto restituito viene eseguito nel tipo richiesto dalla proprietà impostata al momento della richiesta della risorsa.  La logica di ricerca per la risoluzione della risorsa del codice è la stessa del codice [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] del riferimento di risorsa dinamica.  La ricerca della risorsa ha inizio dall'elemento chiamante e continua quindi con gli elementi padre successivi della [struttura ad albero logica](GTMT).  La ricerca prosegue nelle risorse, nei temi e, se necessario, nelle risorse di sistema dell'applicazione.  Una richiesta di codice per una risorsa terrà in considerazione le modifiche di runtime eventualmente apportate ai dizionari di risorse successivamente al caricamento di un determinato dizionario di risorse da [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] nonché le modifiche apportate alle risorse di sistema in tempo reale.  
  
 Di seguito viene riportato un breve esempio di codice che individua una risorsa in base alla chiave e utilizza il valore restituito per impostare una proprietà, implementata come gestore di eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  
  
 [!code-csharp[PropertiesOvwSupport#ResourceProceduralGet](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml.cs#resourceproceduralget)]
 [!code-vb[PropertiesOvwSupport#ResourceProceduralGet](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page3.xaml.vb#resourceproceduralget)]  
  
 Un metodo alternativo per l'assegnazione di un riferimento di risorsa è <xref:System.Windows.FrameworkElement.SetResourceReference%2A>.  Tale metodo accetta due parametri: la chiave della risorsa e l'identificatore di una particolare proprietà di dipendenza presente nell'istanza dell'elemento a cui deve essere assegnato il valore della risorsa.  A livello funzionale, questo metodo è identico al precedente e presenta il vantaggio di non richiedere il cast dei valori restituiti.  
  
 Un ulteriore modo per accedere alle risorse a livello di codice consiste nell'accedere al contenuto della proprietà <xref:System.Windows.FrameworkElement.Resources%2A> come dizionario.  L'accesso al dizionario incluso in questa proprietà consente anche di aggiungere nuove risorse alle raccolte esistenti, di verificare se un determinato nome di chiave è già accettato nella raccolta e di eseguire altre operazioni sul dizionario o sulla raccolta.  Se si sta scrivendo un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] interamente in codice, sarà inoltre possibile creare in codice l'intera raccolta, assegnare chiavi alla raccolta e assegnare infine la raccolta completata alla proprietà <xref:System.Windows.FrameworkElement.Resources%2A> di un elemento prestabilito.  Questa procedura sarà descritta nella sezione successiva.  
  
 Sebbene sia possibile creare un indice all'interno di qualsiasi raccolta <xref:System.Windows.FrameworkElement.Resources%2A> specificata utilizzando come indice una chiave specifica, è opportuno considerare che tale modalità di accesso alla risorsa non segue le regole di runtime standard di risoluzione della risorsa.  Viene effettuato l'accesso solo a quella determinata raccolta.  La ricerca della risorsa non attraversa l'ambito fino alla radice o all'applicazione se non è stato trovato alcun oggetto valido in corrispondenza della chiave richiesta.  Tuttavia, questo approccio in alcuni casi può presentare dei vantaggi in termini di prestazioni, proprio perché l'ambito di ricerca della chiave è più limitato.  Per ulteriori informazioni sull'utilizzo diretto del dizionario di risorse, vedere la classe <xref:System.Windows.ResourceDictionary>.  
  
<a name="creating"></a>   
## Creazione delle risorse tramite codice  
 Per creare un'intera applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nel codice, può anche essere necessario creare eventuali risorse di tale applicazione nel codice.  A tal fine, creare una nuova istanza di <xref:System.Windows.ResourceDictionary> e aggiungere tutte le risorse al dizionario tramite chiamate successive a <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName>.  Utilizzare quindi l'oggetto <xref:System.Windows.ResourceDictionary> così creato per impostare la proprietà <xref:System.Windows.FrameworkElement.Resources%2A> su un elemento presente nell'ambito di una pagina oppure su <xref:System.Windows.Application.Resources%2A?displayProperty=fullName>.  È inoltre possibile utilizzare <xref:System.Windows.ResourceDictionary> come oggetto autonomo, senza aggiungerlo a un elemento.  Tuttavia, in questo caso, è necessario accedere alle risorse in esso contenute tramite la chiave dell'elemento, come se si trattasse di un dizionario generico.  Un oggetto <xref:System.Windows.ResourceDictionary> non associato alla proprietà `Resources` di un elemento non potrà esistere come parte della struttura ad albero di quell'elemento né disporrà di un ambito in una sequenza di ricerca che può essere utilizzata da <xref:System.Windows.FrameworkElement.FindResource%2A> e dagli altri metodi correlati.  
  
<a name="objectaskey"></a>   
## Utilizzo di oggetti come chiavi  
 La chiave di una risorsa sarà impostata come stringa nella maggior parte degli utilizzi di quella risorsa.  Tuttavia, diverse funzionalità di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non utilizzano un tipo stringa per specificare le chiavi; tale parametro sarà piuttosto un oggetto.  La possibilità di disporre di un oggetto come chiave della risorsa viene utilizzata dal supporto degli stili e dei temi di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Gli stili dei temi che funzionano da stili predefiniti per un controllo a cui altrimenti non sarebbe applicato alcuno stile utilizzano come chiave l'oggetto <xref:System.Type> del controllo al quale dovrebbero essere applicati.  L'utilizzo di un tipo come chiave fornisce un meccanismo di ricerca affidabile che funziona sulle istanze predefinite di ciascun tipo di controllo; pertanto, il tipo può essere rilevato mediante reflection e utilizzato per applicare uno stile alle classi derivate, anche se il tipo derivato non disporrebbe altrimenti di uno stile predefinito.  È possibile specificare una chiave <xref:System.Type> per una risorsa definita in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzando l'[Estensione del markup x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md).  Esistono estensioni analoghe per altri utilizzi di chiavi di tipo non stringa che supportano funzionalità di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] quali [Estensione del markup ComponentResourceKey](../../../../docs/framework/wpf/advanced/componentresourcekey-markup-extension.md).  
  
## Vedere anche  
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)