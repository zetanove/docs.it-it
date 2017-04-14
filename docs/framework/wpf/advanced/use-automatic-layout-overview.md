---
title: "Cenni preliminari sull&#39;utilizzo del layout automatico | Microsoft Docs"
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
  - "layout automatico"
  - "layout, automatico"
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Cenni preliminari sull&#39;utilizzo del layout automatico
In questo argomento vengono illustrate le linee guida per gli sviluppatori sulla modalità di scrittura di applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] con [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)] localizzabili.  In passato, la localizzazione di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] era un processo che richiedeva molto tempo.  Ogni lingua per la quale l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] veniva adattata richiedeva modifiche pixel per pixel.  Oggi, con la progettazione e gli standard di codifica corretti, è possibile creare le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] in modo da limitare le attività di ridimensionamento e riposizionamento da parte dei localizzatori.  L'approccio alla scrittura di applicazioni che è possibile ridimensionare e riposizionare con maggiore semplicità viene definito layout automatico e può essere ottenuto utilizzando la progettazione delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Di seguito sono elencate le diverse sezioni di questo argomento.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [Vantaggi dell'utilizzo del layout automatico](#advantages_of_autolayout)  
  
-   [Layout automatico e controlli](#autolayout_controls)  
  
-   [Layout automatico e standard di codifica](#autolayout_coding)  
  
-   [Layout automatico e griglie](#autolay_grids)  
  
-   [Layout automatico e griglie basate sull'utilizzo della proprietà IsSharedSizeScope](#autolay_grids_issharedsizescope)  
  
-   [Argomenti correlati](#seeAlsoToggle)  
  
<a name="advantages_of_autolayout"></a>   
## Vantaggi dell'utilizzo del layout automatico  
 Grazie alle caratteristiche di potenza e flessibilità, il sistema di presentazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consente di creare il layout di elementi in un'applicazione che può essere modificata per soddisfare i requisiti di lingue diverse.  Nell'elenco riportato di seguito sono indicati alcuni vantaggi del layout automatico.  
  
-   L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] viene visualizzata correttamente in qualsiasi lingua.  
  
-   È possibile ridurre le esigenze di ulteriori modifiche alla posizione e alle dimensioni dei controlli dopo la traduzione del testo.  
  
-   È possibile ridurre le esigenze di ulteriori modifiche alle dimensioni delle finestre.  
  
-   Il rendering del layout dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] viene eseguito correttamente in qualsiasi lingua.  
  
-   La localizzazione può essere ridotta a semplici attività che vanno poco oltre la traduzione delle stringhe.  
  
<a name="autolayout_controls"></a>   
## Layout automatico e controlli  
 Il layout automatico consente di modificare automaticamente le dimensioni di un controllo in un'applicazione.  Ad esempio, un controllo può essere modificato per regolare la lunghezza di una stringa.  Questa funzionalità consente ai localizzatori di tradurre la stringa, senza dover ridimensionare il controllo per adattare il testo tradotto.  Nell'esempio riportato di seguito viene creato un pulsante con contenuto in lingua inglese.  
  
 [!code-xml[LocalizationBtn_snip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
 Nell'esempio, l'unica operazione da compiere per creare un pulsante in lingua spagnola consiste nella modifica del testo.  Di seguito è riportato un esempio:  
  
 [!code-xml[LocalizationBtn#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 Nell'immagine riportata di seguito viene illustrato l'output degli esempi di codice.  
  
 ![Lo stesso pulsante con testo in lingue diverse](../../../../docs/framework/wpf/advanced/media/globalizationbutton.png "GlobalizationButton")  
Pulsante a ridimensionamento automatico  
  
<a name="autolayout_coding"></a>   
## Layout automatico e standard di codifica  
 L'utilizzo dell'approccio di layout automatico richiede un insieme di standard e regole di codifica e di progettazione per creare un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] completamente localizzabile.  Le linee guida riportate di seguito agevolano la codifica del layout automatico.  
  
|Standard di codifica|Descrizione|  
|--------------------------|-----------------|  
|Non utilizzare posizioni assolute.|-   Non utilizzare <xref:System.Windows.Controls.Canvas> poiché comporta il posizionamento assoluto degli elementi.<br />-   Utilizzare <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.StackPanel> e <xref:System.Windows.Controls.Grid> per posizionare i controlli.<br />-   Per informazioni sui diversi tipi di pannelli, vedere [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md).|  
|Non impostare una dimensione fissa per una finestra.|-   Utilizzare <xref:System.Windows.Window.SizeToContent%2A>.<br />-   Di seguito è riportato un esempio:<br /><br /> [!code-xml[LocalizationGrid#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)]|  
|Aggiunta di una proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A>.|<ul><li>Aggiungere una proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A> all'elemento radice dell'applicazione.</li><li>[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre un modo pratico per supportare layout orizzontali, bidirezionali e verticali.  Nel framework della presentazione è possibile utilizzare la proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A> per definire il layout.  I pattern di direzione di flusso sono:<br /><br /> <ul><li><xref:System.Windows.FlowDirection> \(LrTb\): layout orizzontale per l'alfabeto latino, asiatico e così via.</li><li><xref:System.Windows.FlowDirection> \(RlTb\): bidirezionale per arabo, ebraico e così via.</li></ul></li></ul>|  
|Utilizzare tipi di carattere compositi anziché tipi di carattere fisici.|<ul><li>Con i tipi di carattere compositi, non è necessario localizzare la proprietà <xref:System.Windows.Controls.Control.FontFamily%2A>.</li><li>Gli sviluppatori possono utilizzare uno dei tipi di carattere riportati di seguito oppure crearne uno personalizzato.<br /><br /> <ul><li>Global User Interface</li><li>Global San Serif</li><li>Global Serif</li></ul></li></ul>|  
|Aggiungere xml:lang.|-   Aggiungere l'attributo `xml:lang` all'elemento radice dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], ad esempio `xml:lang="en-US"` per un'applicazione in lingua inglese.<br />-   Poiché i tipi di carattere compositi utilizzano `xml:lang` per determinare il tipo di carattere da utilizzare, impostare questa proprietà per supportare scenari multilingue.|  
  
<a name="autolay_grids"></a>   
## Layout automatico e griglie  
 L'elemento <xref:System.Windows.Controls.Grid> è utile per il layout automatico poiché consente a uno sviluppatore di posizionare gli elementi.  Un controllo <xref:System.Windows.Controls.Grid> è in grado di distribuire lo spazio disponibile tra gli elementi figlio utilizzando una disposizione per colonne e righe.  È possibile estendere gli elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] su più celle e inserire griglie all'interno di altre griglie.  Le griglie sono utili poiché consentono la creazione e il posizionamento di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] complessa.  Nell'esempio riportato di seguito viene illustrato l'utilizzo di una griglia per posizionare alcuni pulsanti e testo.  Poiché l'altezza e la larghezza delle celle sono impostate su <xref:System.Windows.GridUnitType>, la cella che contiene il pulsante con un'immagine viene modificata in modo da adattarsi all'immagine.  
  
 [!code-xml[LocalizationGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 Nell'immagine riportata di seguito viene illustrata la griglia creata dal codice precedente.  
  
 ![Esempio di Grid](../../../../docs/framework/wpf/advanced/media/glob-grid.png "glob\_grid")  
Grid  
  
<a name="autolay_grids_issharedsizescope"></a>   
## Layout automatico e griglie basate sull'utilizzo della proprietà IsSharedSizeScope  
 Un elemento <xref:System.Windows.Controls.Grid> è utile nelle applicazioni localizzabili per creare controlli che vengono modificati per adattarsi al contenuto.  Tuttavia, in alcuni casi potrebbe essere opportuno che i controlli mantengano una determinata dimensione indipendentemente dal contenuto.  Ad esempio, nei casi dei pulsanti "OK", "Annulla" e "Sfoglia", probabilmente non si desidera che le dimensioni di tali pulsanti si adattino al contenuto.  In questo caso, la proprietà associata <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=fullName> dell'elemento è utile per condividere le stesse dimensioni tra più elementi griglia.  Nell'esempio riportato di seguito viene illustrato come condividere dati sulle dimensioni di colonne e righe tra più elementi <xref:System.Windows.Controls.Grid>.  
  
 [!code-xml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 **Nota** Per il codice di esempio completo, vedere [Condividere le proprietà di ridimensionamento tra griglie](../../../../docs/framework/wpf/controls/how-to-share-sizing-properties-between-grids.md)  
  
## Vedere anche  
 [Globalizzazione per WPF](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)   
 [Utilizzare il layout automatico per creare un pulsante](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)   
 [Utilizzare una griglia per il layout automatico](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)