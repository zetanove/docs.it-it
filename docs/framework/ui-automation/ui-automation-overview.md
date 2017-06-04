---
title: "UI Automation Overview | Microsoft Docs"
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
  - "UI Automation, overview"
  - "user interface, see UI"
  - "accessibility, UI automation"
ms.assetid: 65847654-9994-4a9e-b36d-2dd5d998770b
caps.latest.revision: 35
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 35
---
# UI Automation Overview
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] è il nuovo framework di accessibilità per [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)], disponibile su tutti i sistemi operativi che supportano [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)].  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] fornisce l'accesso a livello di codice alla maggior parte degli elementi dell'[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] sul desktop, consentendo a prodotti di assistive technology, quali le utilità per la lettura dello schermo, di fornire informazioni sull'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] agli utenti finali e di modificare l'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] con mezzi diversi dall'input standard.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] consente inoltre l'interazione degli script di test automatizzati con l'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] non abilita la comunicazione tra processi avviati da utenti diversi tramite il comando **Esegui come**.  
  
 Le applicazioni client di automazione interfaccia utente possono essere scritte con la certezza che funzioneranno su più framework. Le funzionalità di base di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] mascherano le eventuali differenze nei framework sottostanti le varie parti dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Ad esempio, la proprietà `Content` di un pulsante di [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)], la proprietà `Caption` di un pulsante di [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] e la proprietà `ALT` di un'immagine HTML sono tutte mappate a un'unica proprietà, <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A>, nella visualizzazione di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] fornisce tutte le funzionalità in [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)], [!INCLUDE[TLA#tla_winxp](../../../includes/tlasharptla-winxp-md.md)] e [!INCLUDE[TLA2#tla_winnetsvrfam](../../../includes/tla2sharptla-winnetsvrfam-md.md)].  
  
 I provider di automazione interfaccia utente offrono supporto per le applicazioni client di [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)], tramite un servizio di bridging incorporato.  
  
<a name="Providers_and_Clients"></a>   
## Provider e client  
 In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sono presenti quattro componenti principali, come illustrato nella tabella riportata di seguito.  
  
|Componente|Descrizione|  
|----------------|-----------------|  
|[!INCLUDE[TLA#tla_api](../../../includes/tlasharptla-api-md.md)] di provider \(UIAutomationProvider.dll e UIAutomationTypes.dll\)|Un insieme di definizioni dell'interfaccia implementate dai provider di automazione interfaccia utente, oggetti che forniscono informazioni sugli elementi dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] e rispondono a input a livello di codice.|  
|API client \(UIAutomationClient.dll e UIAutomationTypes.dll\)|Un insieme di tipi per il codice gestito che consente alle applicazioni client di automazione interfaccia utente di ottenere informazioni sull'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] e inviare input ai controlli.|  
|UiAutomationCore.dll|Il codice sottostante \(talvolta denominato core di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\) che gestisce la comunicazione tra provider e client.|  
|UIAutomationClientsideProviders.dll|Un insieme di provider di automazione interfaccia utente per i controlli standard legacy \(i controlli [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] dispongono di supporto nativo per [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\). Questo supporto è automaticamente disponibile per le applicazioni client.|  
  
 Per uno sviluppatore software, esistono due modalità d'uso di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]: creare supporto per i controlli personalizzati \(usando l'API del provider\) e creare applicazioni che usano il core di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per comunicare con gli elementi dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] \(usando l'API client\). In base allo stato attivo, è necessario fare riferimento a parti diverse della documentazione. Per altre informazioni sui concetti e per istruzioni pratiche sulle procedure, vedere le sezioni seguenti.  
  
|Sezione|Argomento|Destinatari|  
|-------------|---------------|-----------------|  
|[UI Automation Fundamentals](../../../docs/framework/ui-automation/index.md) \(questa sezione\)|Panoramiche generiche dei concetti.|Tutti.|  
|[UI Automation Providers for Managed Code](../../../docs/framework/ui-automation/ui-automation-providers-for-managed-code.md)|Panoramiche e argomenti sulle procedure per consentire l'uso dell'API del provider.|Sviluppatori dei controlli.|  
|[UI Automation Clients for Managed Code](../../../docs/framework/ui-automation/ui-automation-clients-for-managed-code.md)|Panoramiche  e argomenti sulle procedure per l'uso dell'API client.|Sviluppatori di applicazioni client.|  
|[UI Automation Control Patterns](../../../docs/framework/ui-automation/ui-automation-control-patterns.md)|Informazioni sulla modalità di implementazione dei pattern di controllo da parte dei provider e sulle funzionalità disponibili ai client.|Tutti.|  
|[UI Automation Text Pattern](../../../docs/framework/ui-automation/ui-automation-text-pattern.md)|Informazioni sulla modalità di implementazione del pattern di controllo Text da parte dei provider e sulle funzionalità disponibili ai client.|Tutti.|  
|[UI Automation Control Types](../../../docs/framework/ui-automation/ui-automation-control-types.md)|Informazioni sulle proprietà e sui pattern di controllo supportati da diversi tipi di controllo.|Tutti.|  
  
 Nella tabella riportata di seguito vengono elencati gli spazi dei nomi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], le DLL che li contengono e i destinatari che le usano.  
  
|Spazio dei nomi|DLL a cui si fa riferimento|Destinatari|  
|---------------------|---------------------------------|-----------------|  
|<xref:System.Windows.Automation>|UIAutomationClientUIAutomationTypes|Sviluppatori di client di automazione interfaccia utente; usato per cercare oggetti <xref:System.Windows.Automation.AutomationElement>, registrare eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] e usare i pattern di controllo di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.Provider>|UIAutomationProviderUIAutomationTypes|Sviluppatori di provider di automazione interfaccia utente per i framework diversi da [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)].|  
|<xref:System.Windows.Automation.Text>|UIAutomationClientUIAutomationTypes|Sviluppatori di provider di automazione interfaccia utente per framework diversi da [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]; usato per implementare il pattern di controllo TextPattern.|  
|<xref:System.Windows.Automation.Peers>|PresentationFramework|Sviluppatori di provider di automazione interfaccia utente per [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)].|  
  
<a name="UI_Automation_Model"></a>   
## Modello di automazione interfaccia utente  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] espone tutte le parti dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] alle applicazioni client come <xref:System.Windows.Automation.AutomationElement>. Gli elementi sono contenuti in una struttura ad albero, con il desktop come elemento radice. I client possono filtrare la visualizzazione non elaborata della struttura ad albero come visualizzazione controlli o visualizzazione contenuto. Le applicazioni possono inoltre creare visualizzazioni personalizzate.  
  
 Gli oggetti <xref:System.Windows.Automation.AutomationElement> espongono proprietà comuni degli elementi di [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] che rappresentano. Una di queste proprietà è il tipo di controllo, che definisce l'aspetto e le funzionalità di base come singola entità riconoscibile, ad esempio un pulsante o una casella di controllo.  
  
 Inoltre, gli elementi espongono pattern di controllo che forniscono proprietà specifiche per i tipi di controllo. I pattern di controllo espongono anche metodi che consentono ai client di ottenere altre informazioni sull'elemento e fornire input.  
  
> [!NOTE]
>  Non esiste una corrispondenza uno\-a\-uno tra tipi di controllo e pattern di controllo. Un pattern di controllo può essere supportato da più tipi di controllo e un controllo può supportare più pattern di controllo, ognuno dei quali espone aspetti diversi del comportamento. Ad esempio, una casella combinata dispone di almeno due pattern di controllo: uno che rappresenta la possibilità di espansione e compressione e un altro che rappresenta il meccanismo di selezione. Per informazioni dettagliate, vedere [UI Automation Control Types](../../../docs/framework/ui-automation/ui-automation-control-types.md).  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] fornisce anche informazioni alle applicazioni client tramite gli eventi. A differenza di [!INCLUDE[TLA2#tla_winevents](../../../includes/tla2sharptla-winevents-md.md)], gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] non sono basati su un meccanismo di trasmissione. I client di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] si registrano per le notifiche di eventi specifici e possono richiedere che nei propri gestori eventi siano passate informazioni sulle proprietà e sui pattern di controllo specifici di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Inoltre, un evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] contiene un riferimento all'elemento che lo ha generato. I provider possono migliorare le prestazioni generando eventi in modo selettivo, a seconda dei client in ascolto.  
  
## Vedere anche  
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)   
 [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md)   
 [UI Automation Security Overview](../../../docs/framework/ui-automation/ui-automation-security-overview.md)