---
title: "Implementing the UI Automation Transform Control Pattern | Microsoft Docs"
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
  - "control patterns, Transform"
  - "Transform control pattern"
  - "UI Automation, Transform control pattern"
ms.assetid: 5f49d843-5845-4800-9d9c-56ce0d146844
caps.latest.revision: 14
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 14
---
# Implementing the UI Automation Transform Control Pattern
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.ITransformProvider>, incluse le informazioni relative a proprietà, metodi ed eventi. Alla fine della panoramica sono elencati collegamenti ad altro materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.TransformPattern> viene usato per supportare i controlli che possono essere spostati, ridimensionati o ruotati in uno spazio bidimensionale. Per esempi di controlli che implementano questo pattern di controllo, vedere [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo Transform, tenere presenti le linee guida e le convenzioni seguenti:  
  
-   Il supporto per questo pattern di controllo non è limitato agli oggetti sul desktop. Questo pattern di controllo deve essere supportato dagli elementi figlio di un oggetto contenitore se gli elementi figlio possono essere spostati, ridimensionati o ruotati all'interno dei limiti del contenitore.  
  
-   Un oggetto non può essere spostato, ridimensionato o ruotato in modo che la posizione risultante sullo schermo potrebbe essere completamente esterna alle coordinate del relativo contenitore e pertanto inaccessibile per la tastiera o il mouse \(ad esempio, quando una finestra di primo livello viene spostata fuori schermo o un oggetto figlio viene spostato fuori dai limiti del riquadro di visualizzazione del contenitore\). In questi casi, l'oggetto viene posizionato il più vicino possibile alle coordinate richieste dello schermo rispetto alle coordinate in alto e a sinistra entro i limiti del contenitore.  
  
-   Per sistemi con più monitor, se un oggetto viene spostato, ridimensionato o ruotato completamente al di fuori delle coordinate combinate dello schermo desktop, l'oggetto viene posizionato sul monitor principale il più vicino possibile alle coordinate richieste.  
  
-   Tutti i parametri e i valori delle proprietà sono assoluti e indipendenti dalle impostazioni locali.  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## Membri obbligatori per ITransformProvider  
 Le proprietà e i metodi seguenti sono obbligatori per l'implementazione di <xref:System.Windows.Automation.Provider.ITransformProvider>.  
  
|Membri obbligatori|Tipo di membro|Note|  
|------------------------|--------------------|----------|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.CanMove%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.CanResize%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.CanRotate%2A>|Proprietà|Nessuna|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.Move%2A>|Metodo|Nessuna|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.Resize%2A>|Metodo|Nessuna|  
|<xref:System.Windows.Automation.Provider.ITransformProvider.Rotate%2A>|Metodo|Nessuna|  
  
 Questo pattern di controllo non è associato a eventi.  
  
<a name="Exceptions"></a>   
## Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|-----------------------|----------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.ITransformProvider.Move%2A><br /><br /> -   <xref:System.Windows.Automation.TransformPatternIdentifiers.CanMoveProperty> è false.|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.ITransformProvider.Resize%2A><br /><br /> -   <xref:System.Windows.Automation.TransformPatternIdentifiers.CanResizeProperty> è false.|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.ITransformProvider.Rotate%2A><br /><br /> -   <xref:System.Windows.Automation.TransformPatternIdentifiers.CanRotateProperty> è false.|  
  
## Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)