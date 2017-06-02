---
title: "Metadati delle propriet&#224; del framework | Microsoft Docs"
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
  - "metadati delle proprietà del framework"
  - "metadati, proprietà del framework"
ms.assetid: 9962f380-b885-4b61-a62e-457397083fea
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Metadati delle propriet&#224; del framework
Per le proprietà degli elementi oggetto considerati come situati [a livello di framework WPF](GTMT) nell'architettura [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], vengono segnalate delle opzioni di metadati delle proprietà del framework.  In generale, la designazione [a livello di framework WPF](GTMT) implica che funzionalità quali il rendering, l'associazione dati e i miglioramenti del sistema di proprietà siano gestite dalle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di presentazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e dai file eseguibili.  Questi sistemi eseguono una query sui metadati della proprietà del framework per determinare le caratteristiche specifiche delle funzionalità di particolari proprietà dell'elemento.  
  
   
  
<a name="prerequisites"></a>   
## Prerequisiti  
 Questo argomento presuppone la conoscenza delle [proprietà di dipendenza](GTMT) dal punto di vista di un consumer delle proprietà di dipendenza esistenti nelle classi [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], nonché la lettura della sezione [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  È necessario inoltre aver letto l'argomento [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
<a name="What_Is_Communicated_by_Framework_Property"></a>   
## Contenuto dei metadati delle proprietà del framework  
 I metadati delle proprietà del framework possono essere suddivisi nelle seguenti categorie:  
  
-   Metadati che segnalano le proprietà di layout che influiscono su un elemento \(<xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsRender%2A>\).  È possibile impostare questi flag nei metadati se la proprietà influisce sui rispettivi aspetti e se vengono inoltre implementati i metodi <xref:System.Windows.FrameworkElement.MeasureOverride%2A> \/ <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> nella classe per fornire un comportamento di rendering e informazioni specifiche al sistema di layout.  In genere, tale implementazione verificherebbe le convalide di proprietà nelle proprietà di dipendenza, qualora qualcuna di tali proprietà di layout risultasse impostata su true nei metadati della proprietà; solo tali convalide richiederebbero un nuovo passaggio di layout.  
  
-   Metadati che segnalano le proprietà di layout che influiscono sull'elemento padre di un elemento \(<xref:System.Windows.FrameworkPropertyMetadata.AffectsParentArrange%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsParentMeasure%2A>\).  Alcuni esempi in cui questi flag sono impostati come predefiniti sono <xref:System.Windows.Documents.FixedPage.Left%2A?displayProperty=fullName> e <xref:System.Windows.Documents.Paragraph.KeepWithNext%2A?displayProperty=fullName>.  
  
-   <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>.  Per impostazione predefinita, le proprietà di dipendenza non ereditano valori.  <xref:System.Windows.FrameworkPropertyMetadata.OverridesInheritanceBehavior%2A> consente di trasferire il percorso dell'ereditarietà anche in una struttura ad albero visuale, operazione necessaria per alcuni scenari di composizione dei controlli.  
  
    > [!NOTE]
    >  Il termine "eredita", nel contesto dei valori della proprietà è relativo alle proprietà di dipendenza e indica che gli elementi figlio possono ereditare il valore della proprietà di dipendenza effettivo dagli elementi padre grazie a una funzionalità [a livello di framework WPF](GTMT) del sistema di proprietà di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Non è correlato direttamente al tipo di codice gestito né all'ereditarietà dei membri tramite tipi derivati.  Per informazioni dettagliate, vedere [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
-   Metadati che segnalano le caratteristiche dell'associazione dati \(<xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A>, <xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A>\).  Per impostazione predefinita, le proprietà di dipendenza del framework supportano l'associazione dati, con un comportamento di associazione unidirezionale.  Se non è immaginabile alcuno scenario per l'associazione dati, è possibile disabilitare questa funzionalità \(dal momento che sono progettate per essere flessibili ed estensibili, non sono previsti molti esempi di proprietà di questo tipo nelle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] predefinite\).  È possibile impostare l'associazione in modo che disponga di un'impostazione predefinita bidirezionale per le proprietà che collegano i comportamenti di un controllo fra le parti che lo compongono \(ad esempio <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A>\) oppure un'associazione nella quale lo scenario comune e previsto per gli utenti è l'associazione bidirezionale \(ad esempio <xref:System.Windows.Controls.TextBox.Text%2A>\).  La modifica dei metadati correlati all'associazione dati ha effetto sull'impostazione predefinita. È sempre possibile modificare l'impostazione predefinita per singola associazione.  Per informazioni dettagliate sulle modalità di associazione e sull'associazione in generale, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
-   Metadati che segnalano se le proprietà devono essere inserite nel journal dalle applicazioni o dai servizi che supportano il journaling \(<xref:System.Windows.FrameworkPropertyMetadata.Journal%2A>\).  Per impostazione predefinita, il journaling non è abilitato per gli elementi generali, ma è abilitato in maniera selettiva per determinati controlli di input dell'utente.  Questa proprietà deve essere letta dai servizi di journaling, inclusa l'implementazione del journaling di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ed è impostata in genere nei controlli utente, ad esempio le selezioni dell'utente all'interno di elenchi che devono essere resi persistenti nei vari passaggi di navigazione.  Per informazioni sul journal, vedere [Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md).  
  
<a name="Reading_FrameworkPropertyMetadata"></a>   
## Lettura di FrameworkPropertyMetadata  
 Ognuna delle proprietà per le quali sono stati forniti i collegamenti in precedenza rappresentano le proprietà specifiche aggiunte dall'oggetto <xref:System.Windows.FrameworkPropertyMetadata> alla relativa classe di base immediata <xref:System.Windows.UIPropertyMetadata>.  Per impostazione predefinita, ognuna di queste proprietà sarà `false`.  Una richiesta di metadati per una proprietà, qualora sia importante conoscere il valore di queste proprietà, deve tentare di eseguire il cast dei metadati restituiti all'oggetto <xref:System.Windows.FrameworkPropertyMetadata> e verificare quindi i valori delle singole proprietà se necessario.  
  
<a name="Specifying_Metadata"></a>   
## Specifica dei metadati  
 Quando si crea una nuova istanza di metadati al fine di applicare i metadati alla registrazione di una nuova proprietà di dipendenza, è possibile scegliere la classe di metadati da utilizzare: la classe di base <xref:System.Windows.PropertyMetadata> oppure una classe derivata, ad esempio <xref:System.Windows.FrameworkPropertyMetadata>.  In generale, è opportuno utilizzare la classe <xref:System.Windows.FrameworkPropertyMetadata>, soprattutto se la proprietà interagisce in qualche modo con il sistema di proprietà e con funzioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] quali il layout e l'associazione dati.  Per scenari più sofisticati, un'altra opzione consiste nel far derivare la classe da <xref:System.Windows.FrameworkPropertyMetadata>, in modo da creare una classe di segnalazione dei metadati personalizzata con informazioni aggiuntive contenute nei relativi membri.  In alternativa è possibile utilizzare gli oggetti <xref:System.Windows.PropertyMetadata> o <xref:System.Windows.UIPropertyMetadata> per comunicare il livello di supporto delle funzionalità dell'implementazione.  
  
 Per le proprietà esistenti \(chiamata a <xref:System.Windows.DependencyProperty.AddOwner%2A> o <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>\), è sempre necessario eseguire l'override con il tipo di metadati utilizzato nella registrazione originale.  
  
 Se si crea un'istanza di <xref:System.Windows.FrameworkPropertyMetadata>, sono disponibili due modi per popolare i metadati con i valori previsti per le proprietà specifiche che comunicano le caratteristiche delle proprietà del framework :  
  
1.  Utilizzare la firma del costruttore di <xref:System.Windows.FrameworkPropertyMetadata> che accetta un parametro `flags`.  Per questo parametro è necessario specificare una combinazione di tutti i valori desiderati dei flag dell'enumerazione <xref:System.Windows.FrameworkPropertyMetadataOptions>.  
  
2.  Utilizzare una delle firme senza parametro `flags` e impostare quindi ciascuna proprietà booleana di generazione report dell'oggetto <xref:System.Windows.FrameworkPropertyMetadata> su `true` per ogni modifica delle caratteristiche desiderata.  In questo caso, sarà necessario impostare queste proprietà prima della costruzione di qualsiasi elemento con tale proprietà di dipendenza. Le proprietà booleane sono configurate per la lettura e la scrittura, in modo da consentire di popolare i metadati evitando l'inserimento del parametro `flags`; tuttavia i metadati devono essere contrassegnati come sealed prima che la proprietà venga utilizzata.  Il tentativo di impostare le proprietà dopo la richiesta dei metadati sarà pertanto considerato un'operazione non valida.  
  
<a name="Framework_Property_Metadata_Merge_Behavior"></a>   
## Comportamento di unione dei metadati delle proprietà del framework  
 Quando si esegue l'override dei metadati delle proprietà del framework, le diverse caratteristiche dei metadati vengono unite o sostituite.  
  
-   L'oggetto <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> viene unito.  Se si aggiunge un nuovo oggetto <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>, quel callback viene archiviato nei metadati.  Se non si specifica un oggetto <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> nell'override, il valore dell'oggetto <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> viene promosso come riferimento dal predecessore più vicino che lo aveva specificato nei metadati.  
  
-   Il comportamento effettivo del sistema di proprietà per l'oggetto <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> prevede che le implementazioni di tutti i proprietari di metadati nella gerarchia vengano mantenute e aggiunte in una tabella, con un ordine di esecuzione da parte del sistema di proprietà tale che vengano richiamati per primi i callback della classe derivata di livello inferiore.  I callback ereditati vengono eseguiti solo una volta, essendo considerati come appartenenti alla classe che li posiziona nei metadati.  
  
-   L'oggetto <xref:System.Windows.PropertyMetadata.DefaultValue%2A> viene sostituito.  Se non si specifica un oggetto <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> nell'override, il valore dell'oggetto <xref:System.Windows.PropertyMetadata.DefaultValue%2A> proviene dal predecessore più vicino che lo aveva specificato nei metadati.  
  
-   Le implementazioni di <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> vengono sostituite.  Se si aggiunge un nuovo oggetto <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>, quel callback viene archiviato nei metadati.  Se non si specifica un oggetto <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> nell'override, il valore dell'oggetto <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> viene promosso come riferimento dal predecessore più vicino che lo aveva specificato nei metadati.  
  
-   Il comportamento del sistema di proprietà prevede che venga richiamato solo l'oggetto <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> dei metadati diretti.  Non viene mantenuto alcun riferimento ad altre implementazioni di <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> all'interno della gerarchia.  
  
-   I contrassegni dell'enumerazione <xref:System.Windows.FrameworkPropertyMetadataOptions> sono combinati come operazione OR bit per bit.  Se si specifica <xref:System.Windows.FrameworkPropertyMetadataOptions>, le opzioni originali non vengono sovrascritte.  Per modificare un'opzione, impostare la proprietà corrispondente su <xref:System.Windows.FrameworkPropertyMetadata>.  Se, ad esempio, l'oggetto <xref:System.Windows.FrameworkPropertyMetadata> originale imposta il contrassegno <xref:System.Windows.FrameworkPropertyMetadataOptions?displayProperty=fullName>, è possibile modificarlo impostando <xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A?displayProperty=fullName> su `false`.  
  
 Questo comportamento viene implementato dal metodo <xref:System.Windows.FrameworkPropertyMetadata.Merge%2A> ed è possibile eseguirne l'override nelle classi di metadati derivate.  
  
## Vedere anche  
 <xref:System.Windows.DependencyProperty.GetMetadata%2A>   
 [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)