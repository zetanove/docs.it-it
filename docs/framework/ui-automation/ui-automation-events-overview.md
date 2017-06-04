---
title: "UI Automation Events Overview | Microsoft Docs"
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
  - "UI Automation, providers"
  - "UI Automation, events"
  - "clients, UI Automation"
  - "events, UI Automation"
  - "providers, UI Automation"
  - "UI Automation, clients"
ms.assetid: 69eebd8b-39ed-40e7-93cc-4457c4caf746
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# UI Automation Events Overview
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere l'argomento sull'[API Automazione interfaccia utente di Windows](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 La notifica degli eventi di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] è una funzionalità chiave per dispositivi di assistive technology, quali utilità per la lettura dello schermo e lenti d'ingrandimento. I client di automazione interfaccia utente tengono traccia degli eventi generati dai provider di automazione interfaccia utente quando si verifica un evento nell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] e usano le informazioni per inviare notifiche agli utenti finali.  
  
 Una maggiore efficienza è ottenuta consentendo alle applicazioni provider di generare eventi in modo selettivo, se per tali eventi esistono sottoscrizioni di client, o di non generarne affatto, se nessun client è in attesa di eventi.  
  
<a name="Types_of_Events"></a>   
## Tipi di eventi  
 Gli eventi di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sono suddivisi nelle categorie seguenti.  
  
|Evento|Descrizione|  
|------------|-----------------|  
|Modifica proprietà|Generato quando una proprietà di un elemento o di un pattern di controllo di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] viene modificata. Ad esempio, se un client deve monitorare una casella di controllo di un'applicazione, può registrarsi per l'attesa di un evento di modifica per la proprietà <xref:System.Windows.Automation.TogglePattern.TogglePatternInformation.ToggleState%2A>. Quando il controllo casella di controllo viene selezionato o deselezionato, il provider genera l'evento e il client può agire secondo necessità.|  
|Azione elemento|Generato quando l'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] viene modificata dall'utente finale o da attività a livello di codice, ad esempio quando si fa clic su un pulsante o quest'ultimo viene richiamato tramite <xref:System.Windows.Automation.InvokePattern>.|  
|Modifica struttura|Generato quando la struttura dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] viene modificata. La struttura viene modificata quando nuovi elementi dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] sono resi visibili oppure vengono nascosti o rimossi dal desktop.|  
|Modifica globale desktop|Generato quando si verificano azioni di interesse globale per il client, ad esempio quando lo stato attivo passa da un elemento a un altro o quando si chiude una finestra.|  
  
 Alcuni eventi non indicano necessariamente che lo stato dell'interfaccia utente è cambiato. Ad esempio, se l'utente passa con il tasto TAB a un campo di immissione testo e quindi fa clic su un pulsante per aggiornare il campo, viene generato un evento `TextChangedEvent` anche se in realtà l'utente non ha modificato il testo. Durante l'elaborazione di un evento, prima di eseguire un'azione può essere necessario per un'applicazione client verificare se sia effettivamente avvenuta una modifica.  
  
 I seguenti eventi possono essere generati anche se lo stato dell'interfaccia utente non è cambiato.  
  
-   `AutomationPropertyChangedEvent` \(a seconda della proprietà che è stata modificata\)  
  
-   `ElementSelectedEvent`  
  
-   `InvalidatedEvent`  
  
-   `TextChangedEvent`  
  
<a name="UI_Automation_Event_Identifiers"></a>   
## Identificatori di eventi di automazione interfaccia utente  
 Gli eventi di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] sono identificati da oggetti <xref:System.Windows.Automation.AutomationEvent>. La proprietà <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> contiene un valore che identifica in modo univoco il tipo di evento.  
  
 I valori possibili per <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> sono indicati nella tabella riportata di seguito, insieme al tipo usato per gli argomenti dell'evento. Si noti che gli identificatori usati da client e provider sono campi denominati in modo identico di classi diverse.  
  
|Identificatore client|Identificatore provider|Tipo argomenti evento|  
|---------------------------|-----------------------------|---------------------------|  
|<xref:System.Windows.Automation.AutomationElement.AsyncContentLoadedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|  
|<xref:System.Windows.Automation.SelectionItemPattern.ElementAddedToSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementRemovedFromSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionPattern.InvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.InvokePattern.InvokedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.LayoutInvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPattern.TextChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationPropertyChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationPropertyChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.StructureChangedEventArgs>|  
|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.WindowClosedEventArgs>|  
  
<a name="UI_Automation_Event_Arguments"></a>   
## Argomenti di eventi di automazione interfaccia utente  
 Le classi seguenti incapsulano argomenti di eventi.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|Contiene informazioni sul caricamento asincrono del contenuto, compresa la percentuale di completamento del caricamento.|  
|<xref:System.Windows.Automation.AutomationEventArgs>|Contiene informazioni su un evento semplice che non richiede dati aggiuntivi.|  
|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|Contiene informazioni su una modifica nello stato attivo di input da un elemento a un altro. Eventi di questo tipo sono generati dal sistema di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], non dai provider.|  
|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|Contiene informazioni sulla modifica del valore di una proprietà di un elemento o di un pattern di controllo.|  
|<xref:System.Windows.Automation.StructureChangedEventArgs>|Contiene informazioni su una modifica all'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.WindowClosedEventArgs>|Contiene informazioni sulla chiusura di una finestra.|  
  
 Tutte le classi di argomenti di eventi contengono un membro <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A>. Questo identificatore è incapsulato in un <xref:System.Windows.Automation.AutomationEvent>.  
  
 Gli oggetti <xref:System.Windows.Automation.AutomationEvent> usati per l'identificazione di eventi sono ottenuti dai provider, che li recuperano da campi in <xref:System.Windows.Automation.AutomationElementIdentifiers> e da classi di identificatori di pattern di controllo quale <xref:System.Windows.Automation.DockPatternIdentifiers>. I campi equivalenti vengono ottenuti dalle applicazioni client da campi in <xref:System.Windows.Automation.AutomationElement> e da classi di pattern di controllo quale <xref:System.Windows.Automation.DockPattern>.  
  
 Per un elenco degli identificatori di evento, vedere [UI Automation Events for Clients](../../../docs/framework/ui-automation/ui-automation-events-for-clients.md).  
  
## Vedere anche  
 [UI Automation Events for Clients](../../../docs/framework/ui-automation/ui-automation-events-for-clients.md)   
 [Server\-Side UI Automation Provider Implementation](../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)   
 [Subscribe to UI Automation Events](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)