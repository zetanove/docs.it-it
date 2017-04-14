---
title: "Implementing the UI Automation SelectionItem Control Pattern | Microsoft Docs"
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
  - "Selection Item control pattern"
  - "UI Automation, Selection Item control pattern"
  - "control patterns, Selection Item"
ms.assetid: 76b0949a-5b23-4cfc-84cc-154f713e2e12
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# Implementing the UI Automation SelectionItem Control Pattern
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.ISelectionItemProvider>, incluse le informazioni relative a proprietà, metodi ed eventi. Alla fine della panoramica sono elencati collegamenti a ulteriore materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.SelectionItemPattern> viene usato per supportare i controlli che fungono da singoli elementi figlio selezionabili dei controlli contenitore che implementano <xref:System.Windows.Automation.Provider.ISelectionProvider>. Per esempi di controlli che implementano il pattern di controllo SelectionItem, vedere [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo SelectionItem, tenere presenti le linee guida e le convenzioni seguenti:  
  
-   I controlli a selezione singola che gestiscono i controlli figlio che implementano <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>, ad esempio il dispositivo di scorrimento **Risoluzione schermo** nella finestra di dialogo **Proprietà di visualizzazione** devono implementare <xref:System.Windows.Automation.Provider.ISelectionProvider> e i relativi elementi figlio devono implementare <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> e <xref:System.Windows.Automation.Provider.ISelectionItemProvider>.  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## Membri obbligatori per ISelectionItemProvider  
 Le proprietà, i metodi e gli eventi seguenti sono obbligatori per l'implementazione di <xref:System.Windows.Automation.Provider.ISelectionItemProvider>.  
  
|Membri obbligatori|Tipo di membro|Note|  
|------------------------|--------------------|----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.GetSelection%2A>|Metodo|Nessuna|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Evento|Generato quando una selezione in un contenitore ha subito modifiche significative e richiede l'invio di un numero di eventi <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> e <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> rispetto a quanto definito mediante la costante <xref:System.Windows.Automation.Provider.AutomationInteropProvider.InvalidateLimit>.|  
  
-   Se il risultato di un <xref:System.Windows.Automation.SelectionItemPattern.Select%2A>, <xref:System.Windows.Automation.SelectionItemPattern.AddToSelection%2A> o un <xref:System.Windows.Automation.SelectionItemPattern.RemoveFromSelection%2A> è un singolo elemento selezionato, è necessario generare <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>. In caso contrario inviare <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>\/<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> a seconda dei casi.  
  
<a name="Exceptions"></a>   
## Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|-----------------------|----------------|  
|<xref:System.InvalidOperationException>|Quando vengono tentate le seguenti operazioni:<br /><br /> -   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> viene chiamato in un contenitore a selezione singola dove <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> \= `true` e un elemento è già selezionato.<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> viene chiamato in un contenitore a selezione multipla dove <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> \= `true` ed è selezionato solo un elemento.<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.AddToSelection%2A> viene chiamato in un contenitore a selezione singola dove <xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty> \= `false` e un altro elemento è già selezionato.|  
  
## Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementing the UI Automation Selection Control Pattern](../../../docs/framework/ui-automation/implementing-the-ui-automation-selection-control-pattern.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)   
 [Fragment Provider Sample](http://msdn.microsoft.com/it-it/778ef1bc-8610-4bc9-886e-aeff94a8a13e)