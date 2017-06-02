---
title: "UI Automation Control Patterns Overview | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "control patterns"
  - "UI Automation, control patterns"
ms.assetid: cc229b33-234b-469b-ad60-f0254f32d45d
caps.latest.revision: 34
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 33
---
# UI Automation Control Patterns Overview
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questa panoramica vengono presentati i pattern di controllo per [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]. I pattern di controllo rappresentano un metodo di classificazione ed esposizione della funzionalità di un controllo indipendentemente dal tipo o dall'aspetto del controllo stesso.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] usa i pattern di controllo per rappresentare i comportamenti comuni dei controlli. Usare il pattern di controllo Invoke per i controlli che possono essere richiamati \(ad esempio, i pulsanti\) e il pattern di controllo Scroll per i controlli con barre di scorrimento \(ad esempio le caselle di riepilogo, le visualizzazioni elenco o le caselle combinate\). Poiché ogni pattern di controllo rappresenta una funzionalità distinta, possono essere combinati per descrivere il set completo di funzionalità supportate da un determinato controllo.  
  
> [!NOTE]
>  I controlli aggregati, compilati con i controlli figlio che forniscono le funzionalità esposte dai controlli padre all'[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)], devono implementare tutti i pattern di controllo normalmente associati a ogni controllo figlio. Per contro questi stessi modelli di controllo non devono essere implementati dai controlli figlio.  
  
<a name="uiautomation_control_pattern_includes"></a>   
## Componenti del pattern di controllo di automazione interfaccia utente  
 I pattern di controllo supportano i metodi, le proprietà, gli eventi e le relazioni necessari per definire una parte discreta della funzionalità disponibile in un controllo.  
  
-   La relazione tra un elemento di automazione interfaccia utente e i relativi elementi padre, figlio e di pari livello descrive la struttura dell'elemento all'interno dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
-   I metodi consentono ai client di automazione interfaccia utente di modificare il controllo.  
  
-   Le proprietà e gli eventi rendono disponibili informazioni sulla funzionalità del pattern di controllo, nonché informazioni sullo stato del controllo.  
  
 I pattern di controllo si relazionano all'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] allo stesso modo in cui le interfacce si relazionano agli oggetti [!INCLUDE[TLA#tla_com](../../../includes/tlasharptla-com-md.md)]. In [!INCLUDE[TLA2#tla_com](../../../includes/tla2sharptla-com-md.md)] è possibile eseguire query su oggetto per chiedere quali interfacce sono supportate e quindi usare tali interfacce per accedere alla funzionalità. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] i client di automazione interfaccia utente possono chiedere a un controllo quali pattern di controllo supporta e quindi interagire con il controllo tramite le proprietà, i metodi, gli eventi e le strutture esposti dai pattern di controllo supportati. Ad esempio, per una casella di modifica multiriga i provider di automazione interfaccia utente implementano <xref:System.Windows.Automation.Provider.IScrollProvider>. Quando un client riconosce che una classe <xref:System.Windows.Automation.AutomationElement> supporta il pattern di controllo <xref:System.Windows.Automation.ScrollPattern>, è possibile usare la proprietà, i metodi e gli eventi esposti da tale pattern di controllo per modificare il controllo o accedere alle informazioni sul controllo.  
  
<a name="uiautomation_control_pattern_client_provider"></a>   
## Provider e client di automazione interfaccia utente  
 I provider di automazione interfaccia utente implementano pattern di controllo per esporre il comportamento appropriato per una parte specifica della funzionalità supportata dal controllo.  
  
 I client di automazione interfaccia utente accedono ai metodi e alle proprietà delle classi del pattern di controllo di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e li usano per ottenere informazioni sull'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] o per modificare l'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Queste classi di pattern di controllo sono disponibili nello spazio dei nomi <xref:System.Windows.Automation>, ad esempio <xref:System.Windows.Automation.InvokePattern> e <xref:System.Windows.Automation.SelectionPattern>.  
  
 I client usano i metodi <xref:System.Windows.Automation.AutomationElement>, ad esempio <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=fullName> o <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=fullName>, oppure le funzioni di accesso di [!INCLUDE[TLA#tla_clr](../../../includes/tlasharptla-clr-md.md)] per accedere alle proprietà di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] di un pattern. Ogni classe del pattern di controllo è un membro di campo \(ad esempio, <xref:System.Windows.Automation.InvokePattern.Pattern?displayProperty=fullName>`` o <xref:System.Windows.Automation.SelectionPattern.Pattern?displayProperty=fullName>\) che identifica tale pattern di controllo e può essere passato come parametro a <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> o <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> per recuperare questo pattern per una classe <xref:System.Windows.Automation.AutomationElement>.  
  
<a name="uiautomation_control_patterns_dynamic"></a>   
## Pattern di controllo dinamici  
 Alcuni controlli non supportano sempre lo stesso set di pattern di controllo. I pattern di controllo vengono considerati supportati quando sono disponibili per un client di automazione interfaccia utente. Ad esempio, una casella di modifica multiriga supporta lo scorrimento verticale solo quando contiene più righe di testo che possono essere visualizzate nella relativa area visualizzabile. Lo scorrimento è disabilitato quando viene rimossa una quantità di testo sufficiente da rendere superfluo lo scorrimento. Per questo esempio, il pattern di controllo ScrollPattern è supportato in modo dinamico a seconda dello stato corrente del controllo, ovvero in base alla quantità di testo contenuta nella casella di modifica.  
  
<a name="Control_Pattern_Classes_and_Interfaces"></a>   
## Classi e interfacce dei pattern di controllo  
 Nella tabella seguente vengono descritti i pattern di controllo per [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Sono inoltre elencate le classi usate dai client di automazione interfaccia utente per accedere ai pattern di controllo, nonché le interfacce usate dai provider di automazione interfaccia utente per implementarli.  
  
|Classe del pattern di controllo|Interfaccia del provider|Descrizione|  
|-------------------------------------|------------------------------|-----------------|  
|<xref:System.Windows.Automation.DockPattern>|<xref:System.Windows.Automation.Provider.IDockProvider>|Usata per i controlli che possono essere ancorati in un contenitore di ancoraggio, ad esempio barre degli strumenti o caselle di strumenti.|  
|<xref:System.Windows.Automation.ExpandCollapsePattern>|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Usata per i controlli che possono essere espansi o compressi, ad esempio voci di menu in un'applicazione, come il menu **File**.|  
|<xref:System.Windows.Automation.GridPattern>|<xref:System.Windows.Automation.Provider.IGridProvider>|Usata per i controlli che supportano la funzionalità di griglia, come il ridimensionamento e spostamento in una cella specificata, ad esempio la visualizzazione Icone grandi in Esplora risorse o le tabelle semplici senza intestazioni in [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)].|  
|<xref:System.Windows.Automation.GridItemPattern>|<xref:System.Windows.Automation.Provider.IGridItemProvider>|Usata per i controlli contenenti celle all'interno di griglie. Le singole celle devono supportare il pattern GridItem. Ad esempio, ogni cella nella visualizzazione Dettagli di [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)].|  
|<xref:System.Windows.Automation.InvokePattern>|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Usata per i controlli che possono essere richiamati, ad esempio un pulsante.|  
|<xref:System.Windows.Automation.MultipleViewPattern>|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|Usata per i controlli che possono passare tra più rappresentazioni dello stesso set di informazioni, dati o elementi figlio. Ad esempio, un controllo visualizzazione elenco in cui i dati sono disponibili nelle visualizzazioni anteprima, affiancata, icona, elenco o dettagliata.|  
|<xref:System.Windows.Automation.RangeValuePattern>|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|Usata per i controlli contenenti un intervallo di valori che possono essere applicati al controllo. Ad esempio, un controllo casella di selezione contenente gli anni potrebbe avere un intervallo di valori da 1900 a 2010, mentre un altro controllo casella di selezione contenente i mesi può avere un intervallo di valori da 1 a 12.|  
|<xref:System.Windows.Automation.ScrollPattern>|<xref:System.Windows.Automation.Provider.IScrollProvider>|Usata per i controlli che supportano lo scorrimento, ad esempio un controllo con barre di scorrimento attive quando sono presenti altre informazioni che possono essere visualizzate nell'area visualizzabile del controllo.|  
|<xref:System.Windows.Automation.ScrollItemPattern>|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|Usata per i controlli contenenti elementi in un elenco che supporta lo scorrimento, ad esempio un elenco contenente singoli elementi nell'elenco a scorrimento, ad esempio un controllo casella combinata.|  
|<xref:System.Windows.Automation.SelectionPattern>|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Usata per i controlli contenitore di selezione, ad esempio caselle di riepilogo e caselle combinate.|  
|<xref:System.Windows.Automation.SelectionItemPattern>|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Usata per i singoli elementi nei controlli contenitore di selezione, ad esempio caselle di riepilogo e caselle combinate.|  
|<xref:System.Windows.Automation.TablePattern>|<xref:System.Windows.Automation.Provider.ITableProvider>|Usata per i controlli che dispongono di una griglia e di informazioni di intestazione, ad esempio, i fogli di lavoro di [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)].|  
|<xref:System.Windows.Automation.TableItemPattern>|<xref:System.Windows.Automation.Provider.ITableItemProvider>|Usata per gli elementi in una tabella.|  
|<xref:System.Windows.Automation.TextPattern>|<xref:System.Windows.Automation.Provider.ITextProvider>|Usata per i controlli di modifica e i documenti che espongono informazioni testuali.|  
|<xref:System.Windows.Automation.TogglePattern>|<xref:System.Windows.Automation.Provider.IToggleProvider>|Usata per i controlli in cui è possibile passare alternativamente tra stati, ad esempio caselle di controllo e voci di menu selezionabili.|  
|<xref:System.Windows.Automation.TransformPattern>|<xref:System.Windows.Automation.Provider.ITransformProvider>|Usata per i controlli che è possibile ridimensionare, spostare e ruotare. Il pattern di controllo Transform viene in genere usato in finestre di progettazione, moduli, editor grafici e applicazioni di disegno.|  
|<xref:System.Windows.Automation.ValuePattern>|<xref:System.Windows.Automation.Provider.IValueProvider>|Consente ai client di ottenere o impostare un valore per i controlli che non supportano un intervallo di valori, ad esempio, un controllo di selezione di data e ora.|  
|<xref:System.Windows.Automation.WindowPattern>|<xref:System.Windows.Automation.Provider.IWindowProvider>|Espone informazioni specifiche di Windows, un concetto fondamentale per il sistema operativo [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)]. Esempi di controlli per Windows sono le finestre dell'applicazione di primo livello \([!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)], [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)] e così via\), finestre figlio [!INCLUDE[TLA#tla_mdi](../../../includes/tlasharptla-mdi-md.md)] e le finestre di dialogo.|  
  
## Vedere anche  
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)   
 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)   
 [UI Automation Events for Clients](../../../docs/framework/ui-automation/ui-automation-events-for-clients.md)