---
title: "Implementing the UI Automation Window Control Pattern | Microsoft Docs"
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
  - "control patterns, Window"
  - "UI Automation, Window control pattern"
  - "Window control pattern"
ms.assetid: a28cb286-296e-4a62-b4cb-55ad636ebccc
caps.latest.revision: 21
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 20
---
# Implementing the UI Automation Window Control Pattern
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.IWindowProvider>, incluse le informazioni relative a proprietà, metodi ed eventi di <xref:System.Windows.Automation.WindowPattern>. Alla fine della panoramica sono elencati collegamenti ad altro materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.WindowPattern> viene usato per supportare i controlli che forniscono la funzionalità fondamentale basata su finestra in un'[!INCLUDE[TLA#tla_gui](../../../includes/tlasharptla-gui-md.md)] tradizionale. I controlli che devono implementare questo pattern di controllo sono, ad esempio, le finestre dell'applicazione di primo livello, le finestre figlio dell'[!INCLUDE[TLA#tla_mdi](../../../includes/tlasharptla-mdi-md.md)], i controlli riquadro ridimensionabili, le finestre di dialogo modali e le finestre fumetto della Guida.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo Window, tenere presenti le linee guida e le convenzioni seguenti:  
  
-   Per supportare la possibilità di modificare sia le dimensioni della finestra che la posizione sullo schermo con Automazione interfaccia utente, un controllo deve implementare <xref:System.Windows.Automation.Provider.ITransformProvider> oltre a <xref:System.Windows.Automation.Provider.IWindowProvider>.  
  
-   I controlli contenenti barre del titolo ed elementi della barra del titolo che consentono di spostare, ridimensionare, ingrandire, ridurre a icona o chiudere il controllo in genere devono implementare <xref:System.Windows.Automation.Provider.IWindowProvider>.  
  
-   I controlli come i popup di descrizione comando e le caselle combinate o i menu a discesa in genere non implementano <xref:System.Windows.Automation.Provider.IWindowProvider>.  
  
-   Le finestre fumetto della Guida si distinguono dai popup di descrizione comando di base per il provisioning di un pulsante Chiudi simile a quello delle finestre.  
  
-   La modalità schermo intero non è supportata da IWindowProvider perché è una funzionalità specifica delle applicazioni e non è un comportamento tipico delle finestre.  
  
<a name="Required_Members_for_IWindowProvider"></a>   
## Membri obbligatori per IWindowProvider  
 Le proprietà, i metodi e gli eventi seguenti sono obbligatori per l'implementazione dell'interfaccia IWindowProvider.  
  
|Membro obbligatorio|Tipo di membro|Note|  
|-------------------------|--------------------|----------|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.InteractionState%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.IsModal%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.IsTopmost%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.Maximizable%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.Minimizable%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.VisualState%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.Close%2A>|Metodo|Nessuno|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.SetVisualState%2A>|Metodo|Nessuno|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.WaitForInputIdle%2A>|Metodo|Nessuno|  
|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent>|Evento|Nessuna|  
|<xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent>|Evento|None|  
|<xref:System.Windows.Automation.WindowInteractionState>|Evento|Non è garantito che sia <xref:System.Windows.Automation.WindowInteractionState>|  
  
<a name="Exceptions"></a>   
## Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|-----------------------|----------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.IWindowProvider.SetVisualState%2A><br /><br /> -   Quando un controllo non supporta un comportamento richiesto.|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IWindowProvider.WaitForInputIdle%2A><br /><br /> -   Quando il parametro non è un numero valido.|  
  
## Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)