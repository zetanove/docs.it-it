---
title: "Implementazione del pattern di controllo TableItem di automazione interfaccia utente | Microsoft Docs"
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
  - "pattern di controllo, elemento di tabella"
  - "Automazione interfaccia utente, il pattern di controllo elemento di tabella"
  - "Table Item (pattern di controllo)"
ms.assetid: ac178408-1485-436f-8d3e-eee3bf80cb24
caps.latest.revision: 14
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 14
---
# Implementazione del pattern di controllo TableItem di automazione interfaccia utente
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare gestita [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classi definite nel <xref:System.Windows.Automation> dello spazio dei nomi. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate linee guida e convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.ITableItemProvider>, incluse le informazioni sugli eventi e proprietà. Alla fine della panoramica sono elencati collegamenti a ulteriore materiale di riferimento.  
  
 Il <xref:System.Windows.Automation.TableItemPattern> pattern di controllo viene utilizzato per supportare i controlli figlio di contenitori che implementano <xref:System.Windows.Automation.Provider.ITableProvider>. Accesso alla funzionalità delle singole celle è fornito dall'implementazione simultanea obbligatoria di <xref:System.Windows.Automation.Provider.IGridItemProvider>. Questo modello di controllo è analogo a <xref:System.Windows.Automation.Provider.IGridItemProvider> con la differenza che qualsiasi controllo che implementa <xref:System.Windows.Automation.Provider.ITableItemProvider> a livello di codice deve esporre la relazione tra la cella singola e le relative informazioni di riga e colonna. Per esempi di controlli che implementano questo pattern di controllo, vedere [Control Pattern Mapping per i client di automazione interfaccia utente](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Linee guida e convenzioni di implementazione  
  
-   Per la funzionalità degli elementi della griglia correlata, vedere [implementazione del Pattern di controllo GridItem di automazione interfaccia utente](../../../docs/framework/ui-automation/implementing-the-ui-automation-griditem-control-pattern.md).  
  
<a name="Required_Members_for_ITableItemProvider"></a>   
## <a name="required-members-for-itableitemprovider"></a>Membri obbligatori per ITableItemProvider  
  
|Membro obbligatorio|Tipo di membro|Note|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider.GetColumnHeaderItems%2A>|Metodo|Nessuno|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider.GetRowHeaderItems%2A>|Metodo|None|  
  
 Questo pattern di controllo non è associato a proprietà o eventi.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Eccezioni  
 Questo pattern di controllo non è associato a eccezioni.  
  
## <a name="see-also"></a>Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Supportare pattern di controllo in un Provider di automazione interfaccia utente](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [Pattern di controllo di automazione interfaccia utente per i client](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementazione del Pattern di controllo Table di automazione dell'interfaccia utente](../../../docs/framework/ui-automation/implementing-the-ui-automation-table-control-pattern.md)   
 [Implementazione del Pattern di controllo GridItem di automazione dell'interfaccia utente](../../../docs/framework/ui-automation/implementing-the-ui-automation-griditem-control-pattern.md)   
 [Panoramica di struttura ad albero di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Utilizzare la memorizzazione nella cache di automazione interfaccia utente](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)