---
title: "Implementing the UI Automation MultipleView Control Pattern | Microsoft Docs"
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
  - "UI Automation, MultipleView control pattern"
  - "MultipleView control pattern"
  - "control patterns, MultipleView"
ms.assetid: 5bf1b248-ffee-48c8-9613-0b134bbe9f6a
caps.latest.revision: 15
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 15
---
# Implementing the UI Automation MultipleView Control Pattern
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.IMultipleViewProvider>, incluse le informazioni relative a eventi e proprietà. Alla fine della panoramica sono elencati collegamenti ad altro materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.MultipleViewPattern> viene usato per supportare i controlli che implementano più rappresentazioni dello stesso set di informazioni o controlli figlio e che sono in grado di scorrere tali rappresentazioni.  
  
 Esempi di controlli che possono presentare più visualizzazioni includono la visualizzazione elenco \(che può visualizzare il proprio contenuto sotto forma di anteprime, riquadri, icone o dettagli\), grafici di [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] \(a torta, a linee, a barre, valore di cella con una formula\), documenti di [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] \(normale, layout Web, layout di stampa, layout lettura, struttura\), calendario di [!INCLUDE[TLA#tla_outlook](../../../includes/tlasharptla-outlook-md.md)] \(anno, mese, settimana, giorno\) e interfacce [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)]. Le visualizzazioni supportate sono determinate dallo sviluppatore del controllo e sono specifiche di ogni controllo.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo MultipleView, tenere presenti le linee guida e le convenzioni seguenti:  
  
-   Anche l'interfaccia <xref:System.Windows.Automation.Provider.IMultipleViewProvider> deve essere implementata in un contenitore che gestisce la visualizzazione corrente se è diversa da un controllo che fornisce la visualizzazione corrente. Ad esempio, Esplora risorse contiene un controllo elenco per il contenuto della cartella corrente, mentre la visualizzazione per il controllo viene gestita dall'applicazione Esplora risorse.  
  
-   Un controllo in grado di ordinare il relativo contenuto non supporta più visualizzazioni.  
  
-   La raccolta di visualizzazioni deve essere identica tra istanze.  
  
-   I nomi delle visualizzazioni devono essere adatti all'uso nelle applicazioni di sintesi vocale o nelle altre applicazioni per la lettura in Braille e altri metodi di lettura.  
  
<a name="Required_Members_for_IMultipleViewProvider"></a>   
## Membri obbligatori per IMultipleViewProvider  
 Le proprietà e i metodi seguenti sono obbligatori per l'implementazione di IMultipleViewProvider.  
  
|Membri obbligatori|Tipo di membro|Note|  
|------------------------|--------------------|----------|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.CurrentView%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetSupportedViews%2A>|Metodo|Nessuna|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A>|Metodo|Nessuna|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A>|Metodo|Nessuna|  
  
 Non sono presenti eventi associati a questo pattern di controllo.  
  
<a name="Exceptions"></a>   
## Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|-----------------------|----------------|  
|<xref:System.ArgumentException>|Viene eseguita una chiamata a <xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A> o <xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A> con un parametro che non è un membro della raccolta delle visualizzazioni supportate.|  
  
## Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)