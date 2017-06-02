---
title: "Eventi di automazione interfaccia utente per i client | Microsoft Docs"
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
  - "Automazione interfaccia utente, gli eventi per i client"
  - "eventi, i client di automazione interfaccia utente"
ms.assetid: b909e388-3f24-4997-b6d4-bd9c35c2dc27
caps.latest.revision: 32
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 32
---
# Eventi di automazione interfaccia utente per i client
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare gestita [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classi definite nel <xref:System.Windows.Automation> dello spazio dei nomi. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Questo argomento viene descritto come [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] gli eventi vengono utilizzati dai client di automazione interfaccia utente.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]consente ai client di sottoscrivere gli eventi di interesse. Questa funzionalità migliora le prestazioni eliminando la necessità di eseguire continuamente il polling di tutti i [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] elementi nel sistema per vedere se qualsiasi informazione, struttura o lo stato è stato modificato.  
  
 Una maggiore efficienza è ottenuta anche grazie alla possibilità di restare in ascolto di eventi solo in un ambito definito. Ad esempio, un client possa restare in ascolto di eventi di modifica dello stato attivo su tutti [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gli elementi nella struttura o in un solo elemento e dei relativi discendenti.  
  
> [!NOTE]
>  Non presupporre che tutti i possibili eventi vengono generati da un [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] provider. Ad esempio, non tutte le modifiche alle proprietà che gli eventi generati da provider proxy standard per [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] controlli.  
  
 Per ulteriori informazioni sugli [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gli eventi, vedere [Cenni preliminari sugli eventi di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
<a name="Subscribing_to_Events"></a>   
## <a name="subscribing-to-events"></a>Sottoscrizione di eventi  
 Le applicazioni client sottoscrivono eventi di una particolare tipologia registrando un gestore eventi, con uno dei metodi seguenti.  
  
|Metodo|Tipo di evento|Tipo argomenti evento|Tipo di delegato|  
|------------|----------------|--------------------------|-------------------|  
|<xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>|Modifica dello stato attivo|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|<xref:System.Windows.Automation.AutomationFocusChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>|Modifica proprietà|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|<xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddStructureChangedEventHandler%2A>|Modifica struttura|<xref:System.Windows.Automation.StructureChangedEventArgs>|<xref:System.Windows.Automation.StructureChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>|Tutti gli altri eventi, identificati da un <xref:System.Windows.Automation.AutomationEvent>|<xref:System.Windows.Automation.AutomationEventArgs> o <xref:System.Windows.Automation.WindowClosedEventArgs>|<xref:System.Windows.Automation.AutomationEventHandler>|  
  
 Prima di chiamare il metodo, è necessario creare un metodo delegato per gestire l'evento. Se si preferisce, è possibile gestire tipologie diverse di eventi con un solo metodo e passare questo metodo in più chiamate a uno dei metodi della tabella. Ad esempio, un singolo <xref:System.Windows.Automation.AutomationEventHandler> può essere configurato per gestire vari eventi in modo diverso in base al <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A>.  
  
> [!NOTE]
>  Per elaborare gli eventi di chiusura delle finestre, il cast del tipo di argomento passato al gestore eventi come <xref:System.Windows.Automation.WindowClosedEventArgs>. Poiché il [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] (elemento) per la finestra non è più valido, non è possibile utilizzare il `sender` parametro per recuperare informazioni; utilizzare <xref:System.Windows.Automation.WindowClosedEventArgs.GetRuntimeId%2A> invece.  
  
> [!CAUTION]
>  Se l'applicazione potrebbe ricevere eventi dalla propria [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)], non utilizzare l'applicazione [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] thread sottoscrivere gli eventi o per annullare la sottoscrizione. perché potrebbe verificarsi un comportamento imprevisto. Per ulteriori informazioni, vedere [i problemi di Threading di automazione dell'interfaccia utente](../../../docs/framework/ui-automation/ui-automation-threading-issues.md).  
  
 In fase di arresto, o quando [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] eventi non sono più interessanti per l'applicazione, i client di automazione interfaccia utente devono chiamare uno dei metodi seguenti.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>|Annulla la registrazione di un gestore eventi che è stato registrato utilizzando <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>.|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationFocusChangedEventHandler%2A>|Annulla la registrazione di un gestore eventi che è stato registrato utilizzando <xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>.|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationPropertyChangedEventHandler%2A>|Annulla la registrazione di un gestore eventi che è stato registrato utilizzando <xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>.|  
|<xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>|Annulla la registrazione di tutti i gestori eventi registrati.|  
  
 Nell'esempio di codice, vedere [sottoscrivere gli eventi di automazione interfaccia utente](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoscrivere gli eventi di automazione interfaccia utente](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)   
 [Cenni preliminari sugli eventi di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-events-overview.md)   
 [Cenni preliminari sulle proprietà di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)   
 [Esempio di TrackFocus](http://msdn.microsoft.com/it-it/4a91c0af-6bb5-4d38-a743-cf136f268fc9)