---
title: "Dizionari risorse uniti | Microsoft Docs"
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
  - "dizionari risorse uniti"
  - "dizionari risorse uniti"
ms.assetid: d159531f-05d4-49fd-b951-c332de51e5bc
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Dizionari risorse uniti
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]risorse supportano una funzionalità di dizionari risorse uniti. Questa funzionalità consente di definire la porzione di risorse di un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dell'applicazione all'esterno della compilazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] dell'applicazione. Le risorse possono quindi essere condivise tra le applicazioni e sono inoltre più facilmente isolata per la localizzazione.  
  
## <a name="introducing-a-merged-resource-dictionary"></a>Introduzione a un dizionario risorse uniti  
 Nel markup, utilizzare la sintassi seguente consente di introdurre un dizionario risorse unito a una pagina:  
  
 [!code-xml[ResourceMergeDictionary#MergedXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ResourceMergeDictionary/CS/default.xaml#mergedxaml)]  
  
 Si noti che il <xref:System.Windows.ResourceDictionary> elemento non dispone di un [direttiva X:Key](../../../../docs/framework/xaml-services/x-key-directive.md), che in genere è richiesto per tutti gli elementi in una raccolta di risorse. Ma un altro <xref:System.Windows.ResourceDictionary> fare riferimento all'interno di <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> raccolta è un caso speciale, riservato per questo scenario di dizionari risorse uniti. Il <xref:System.Windows.ResourceDictionary> che introduce un unita dizionario risorse non può avere un [direttiva X:Key](../../../../docs/framework/xaml-services/x-key-directive.md). In genere, ogni <xref:System.Windows.ResourceDictionary> all'interno di <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> raccolta specifica un <xref:System.Windows.ResourceDictionary.Source%2A> attributo. Il valore di <xref:System.Windows.ResourceDictionary.Source%2A> deve essere un [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] che si risolve il percorso del file di risorse da unire. La destinazione di tale [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] deve essere un altro [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file, con <xref:System.Windows.ResourceDictionary> come elemento radice.  
  
> [!NOTE]
>  È consentito definire le risorse all'interno di un <xref:System.Windows.ResourceDictionary> che viene specificato come un dizionario unito o come alternativa alla specifica <xref:System.Windows.ResourceDictionary.Source%2A>, o oltre a risorse che sono incluse dall'origine specificata. Tuttavia, questo non è in uno scenario comune; lo scenario principale per i dizionari uniti è l'unione delle risorse da posizioni di file esterno. Se si desidera specificare le risorse all'interno del markup per una pagina, è necessario in genere definirle principale <xref:System.Windows.ResourceDictionary> e non nei dizionari uniti.  
  
## <a name="merged-dictionary-behavior"></a>Comportamento del dizionario unito  
 Risorse in un dizionario unito occupano nell'ambito di ricerca che si trova immediatamente dopo l'ambito del dizionario risorse principale in che vengono unite un percorso. Anche se una chiave di risorsa deve essere univoca all'interno di ogni singolo dizionario, una chiave può essere presente più volte in un set di dizionari uniti. In questo caso, la risorsa restituita verrà nell'ultimo dizionario rilevato nella sequenza di <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> insieme. Se il <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> raccolta è stata definita in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], quindi l'ordine dei dizionari uniti nella raccolta è l'ordine degli elementi come specificato nel markup. Se viene definita una chiave nel dizionario primario e anche in un dizionario che è stato unito, la risorsa restituita verrà ricavato dalla dizionario primario. Queste regole di ambito sono ugualmente applicabili per riferimenti a risorse statiche e risorse dinamiche riferimenti.  
  
### <a name="merged-dictionaries-and-code"></a>Dizionari uniti e il codice  
 È possibile aggiungere dizionari uniti a un `Resources` dizionario tramite codice. L'impostazione predefinita, inizialmente vuota <xref:System.Windows.ResourceDictionary> che esiste per qualsiasi `Resources` proprietà ha anche un valore predefinito, inizialmente vuoto <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> proprietà della raccolta. Per aggiungere un dizionario unito tramite codice, per ottenere un riferimento all'oggetto principale <xref:System.Windows.ResourceDictionary>, ottenere il relativo <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> valore della proprietà e chiamare `Add` sulla classe generica `Collection` contenuta in <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>. L'oggetto aggiunto deve essere un nuovo <xref:System.Windows.ResourceDictionary>. Nel codice, non si imposta la <xref:System.Windows.ResourceDictionary.Source%2A> proprietà. In alternativa, è necessario ottenere un <xref:System.Windows.ResourceDictionary> oggetto creandolo oppure caricandolo. Un modo per caricare un oggetto esistente <xref:System.Windows.ResourceDictionary> chiamare <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName> su un oggetto esistente [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] flusso di file che ha un <xref:System.Windows.ResourceDictionary> radice, quindi eseguire il cast di <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName> un valore restituito per <xref:System.Windows.ResourceDictionary>.  
  
### <a name="merged-resource-dictionary-uris"></a>URI dei dizionari risorse uniti  
 Esistono diverse tecniche per includere un dizionario risorse unito, indicati dal [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] formato da utilizzare. In generale, queste tecniche possono essere divisi in due categorie: risorse che vengono compilate come parte del progetto e che non vengono compilate come parte del progetto.  
  
 Per le risorse che vengono compilate come parte del progetto, è possibile utilizzare un percorso relativo che fa riferimento al percorso della risorsa. Il percorso relativo viene valutato durante la compilazione. La risorsa deve essere definita come parte del progetto come un'operazione di compilazione di risorse. Se si include un file di risorse XAML nel progetto come risorsa, non è necessario copiare il file di risorse nella directory di output, la risorsa è già inclusa nell'applicazione compilata. È inoltre possibile utilizzare l'azione di compilazione contenuto, ma è necessario quindi copiare i file nella directory di output e distribuire i file di risorse della stessa relazione di percorso del file eseguibile.  
  
> [!NOTE]
>  Non utilizzare l'azione di compilazione risorsa incorporata. Operazione di compilazione stessa è supportata per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applicazioni, ma la risoluzione di <xref:System.Windows.ResourceDictionary.Source%2A> non incorpora <xref:System.Resources.ResourceManager>e pertanto in grado di separare la singola risorsa dal flusso. È tuttavia possibile usare risorsa incorporata per altri scopi, a condizione che anche <xref:System.Resources.ResourceManager> per accedere alle risorse.  
  
 Una tecnica correlata consiste nell'utilizzare un URI di tipo Pack per un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file e farvi riferimento come origine. URI di tipo pack abilita i riferimenti a componenti di assembly di riferimento e altre tecniche. Per ulteriori informazioni sugli URI di tipo Pack, vedere [risorse dell'applicazione WPF, contenuto e i file di dati](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md).  
  
 Per le risorse che non vengono compilate come parte del progetto, l'URI viene valutata in fase di esecuzione. È possibile utilizzare un trasporto URI comune, ad esempio file: o http: per fare riferimento al file di risorse. Lo svantaggio dell'approccio alle risorse di utilizzo è il file: accesso richiede passaggi di distribuzione aggiuntive e http: accesso implica l'area di protezione Internet.  
  
### <a name="reusing-merged-dictionaries"></a>Riutilizzo dei dizionari uniti  
 È possibile riutilizzare o condividere i dizionari risorse uniti tra diverse applicazioni, poiché il dizionario di risorse di tipo merge è possibile fare riferimento tramite qualsiasi valido [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]. La procedura varia in base la strategia di distribuzione di applicazioni e modello di applicazione esattamente seguire. La strategia di URI di tipo Pack citato in precedenza fornisce un modo per un'origine comune di una risorsa unita tra più progetti durante lo sviluppo condividendo un riferimento all'assembly. In questo scenario le risorse vengono ancora distribuite dal client e almeno una delle applicazioni deve distribuire l'assembly di riferimento. È inoltre possibile fare riferimento alle risorse unite tramite un URI distribuito che utilizza il protocollo http.  
  
 Scrittura di dizionari uniti come applicazione locale i file o nell'archivio locale condiviso è un altro dizionario unito possibili / scenario di distribuzione dell'applicazione.  
  
### <a name="localization"></a>Localizzazione  
 Se le risorse da localizzare sono isolate ai dizionari uniti nei dizionari principali e tenuti come separato [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], questi file possono essere localizzati separatamente. Questa tecnica è una semplice alternativa alla localizzazione gli assembly satellite di risorse. Per informazioni dettagliate, vedere [WPF Panoramica della globalizzazione e localizzazione](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.ResourceDictionary>   
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Risorse e codice](../../../../docs/framework/wpf/advanced/resources-and-code.md)   
 [Risorse dell'applicazione WPF, contenuto e i file di dati](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)