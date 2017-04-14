---
title: "Implementing the UI Automation Invoke Control Pattern | Microsoft Docs"
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
  - "UI Automation, Invoke control pattern"
  - "control patterns, Invoke"
  - "Invoke control pattern"
ms.assetid: e5b1e239-49f8-468e-bfec-1fba02ec9ac4
caps.latest.revision: 31
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 30
---
# Implementing the UI Automation Invoke Control Pattern
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.IInvokeProvider>, incluse le informazioni relative a eventi e proprietà. Alla fine della panoramica sono elencati collegamenti ad altro materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.InvokePattern> viene usato per supportare i controlli che non mantengono lo stato quando sono attivati, bensì avviano o eseguono una singola azione non ambigua. I controlli che mantengono lo stato, ad esempio caselle di controllo e pulsanti di opzione, devono invece implementare rispettivamente <xref:System.Windows.Automation.Provider.IToggleProvider> e <xref:System.Windows.Automation.Provider.ISelectionItemProvider>. Per esempi di controlli che implementano il pattern di controllo Invoke, vedere [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo pattern, tenere presenti le linee guida e le convenzioni seguenti:  
  
-   I controlli implementano <xref:System.Windows.Automation.Provider.IInvokeProvider> se lo stesso comportamento non viene esposto mediante un altro provider di pattern di controllo. Ad esempio, se il metodo <xref:System.Windows.Automation.InvokePattern.Invoke%2A> su un controllo esegue la stessa azione del metodo <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> o <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A>, il controllo non deve implementare <xref:System.Windows.Automation.Provider.IInvokeProvider>.  
  
-   La chiamata di un controllo viene in genere eseguita facendo clic o doppio clic oppure premendo INVIO, una scelta rapida predefinita da tastiera o una combinazione alternativa di tasti.  
  
-   Viene generato un evento <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> su un controllo che è stato attivato in risposta a un controllo che esegue l'azione associata. Se possibile, l'evento deve essere generato dopo che il controllo ha completato l'azione ed è stato restituito senza alcun blocco. L'evento Invoked deve essere generato prima che la richiesta Invoke venga gestita negli scenari seguenti:  
  
    -   Non è possibile o conveniente attendere il completamento dell'azione.  
  
    -   L'azione richiede l'intervento dell'utente.  
  
    -   L'azione è dispendiosa a livello di tempo e comporta il blocco del client chiamante un periodo di tempo significativo.  
  
-   Se il richiamo del controllo è caratterizzato da effetti collaterali significativi, tali effetti collaterali devono essere esposte tramite la proprietà <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A>. Ad esempio, anche se il metodo <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> non è associato alla selezione, <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> può causare la selezione di un altro controllo.  
  
-   Gli effetti del passaggio del mouse sopra un elemento in genere non determinano la generazione di un evento Invoke. Tuttavia, i controlli che eseguono un'azione \(a differenza di quelli che generano un effetto visivo\) basata sullo stato del passaggio del mouse devono supportare il pattern di controllo <xref:System.Windows.Automation.InvokePattern>.  
  
> [!NOTE]
>  Questa implementazione viene considerata un problema di accessibilità se il controllo può essere chiamato solo come risultato di un effetto collaterale relativo al mouse.  
  
-   La chiamata di un controllo è diversa dalla selezione di un elemento. Tuttavia, a seconda del controllo, come effetto collaterale la chiamata potrebbe causare la selezione dell'elemento. Ad esempio, la chiamata di un elemento dell'elenco di documenti di [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] nella cartella Documenti comporta sia la selezione dell'elemento che l'apertura del documento.  
  
-   Un elemento può scomparire dall'albero [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] subito dopo essere stato richiamato. Di conseguenza, la richiesta di informazioni dall'elemento fornito dal callback di evento potrebbe avere esito negativo. La prelettura delle informazioni memorizzate nella cache rappresenta la soluzione alternativa consigliata.  
  
-   I controlli possono implementare più pattern di controllo. Ad esempio, il controllo Colore riempimento sulla barra degli strumenti dell'[!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] implementa sia il pattern di controllo <xref:System.Windows.Automation.InvokePattern> che il pattern di controllo <xref:System.Windows.Automation.ExpandCollapsePattern>.<xref:System.Windows.Automation.ExpandCollapsePattern> espone il menu e <xref:System.Windows.Automation.InvokePattern> riempie la selezione attiva con il colore selezionato.  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## Membri obbligatori per IInvokeProvider  
 Le proprietà e i metodi seguenti sono obbligatori per l'implementazione di <xref:System.Windows.Automation.Provider.IInvokeProvider>.  
  
|Membri obbligatori|Tipo di membro|Note|  
|------------------------|--------------------|----------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A>|metodo|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> è una chiamata asincrona e deve restituire immediatamente un valore senza bloccarsi.<br /><br /> Questo comportamento è particolarmente critico per i controlli che direttamente o indirettamente avviano una finestra di dialogo quando vengono chiamati. Qualsiasi client di automazione interfaccia utente che ha generato l'evento rimarrà bloccato fino a quando non viene chiusa la finestra di dialogo modale.|  
  
<a name="Exceptions"></a>   
## Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|-----------------------|----------------|  
|<xref:System.Windows.Automation.ElementNotEnabledException>|Il controllo non è abilitato.|  
  
## Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Invoke a Control Using UI Automation](../../../docs/framework/ui-automation/invoke-a-control-using-ui-automation.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)