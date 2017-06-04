---
title: "Implementazione del pattern di controllo GridItem di automazione interfaccia utente | Microsoft Docs"
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
  - "pattern di controllo, GridItem"
  - "automazione interfaccia utente (pattern di controllo GridItem)"
  - "Grid Item (pattern di controllo)"
ms.assetid: bffbae08-fe2a-42fd-ab84-f37187518916
caps.latest.revision: 15
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 15
---
# Implementazione del pattern di controllo GridItem di automazione interfaccia utente
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare gestita [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classi definite nel <xref:System.Windows.Automation> dello spazio dei nomi. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento vengono presentate linee guida e convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.IGridItemProvider>, incluse le informazioni sulle proprietà. Alla fine della panoramica sono elencati collegamenti a ulteriore materiale di riferimento.  
  
 Il <xref:System.Windows.Automation.GridItemPattern> pattern di controllo viene utilizzato per supportare singoli controlli figlio di contenitori che implementano <xref:System.Windows.Automation.Provider.IGridProvider>. Per esempi di controlli che implementano questo pattern di controllo, vedere [Control Pattern Mapping per i client di automazione interfaccia utente](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Linee guida e convenzioni di implementazione  
 Quando si implementa <xref:System.Windows.Automation.Provider.IGridProvider>, tenere presente le linee guida e le convenzioni seguenti:  
  
-   Le coordinate della griglia sono in base zero. Le coordinate della cella in alto a sinistra sono infatti (0, 0).  
  
-   Celle unite segnaleranno loro <xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A> e <xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A> proprietà in base ai loro cella di aggancio sottostanti come definito dal provider di automazione interfaccia utente. In genere si tratterà della riga o della colonna più in alto e più a sinistra.  
  
-   <xref:System.Windows.Automation.Provider.IGridItemProvider> non consente la modifica attiva della griglia, ad esempio l'unione o divisione delle celle.  
  
-   I controlli che implementano <xref:System.Windows.Automation.Provider.IGridItemProvider> in genere possono essere attraversate (ovvero, un client di automazione interfaccia utente può spostarsi ai controlli adiacenti) utilizzando la tastiera.  
  
<a name="Required_Members_for_IGridItemProvider"></a>   
## <a name="required-members-for-igriditemprovider"></a>Membri obbligatori per IGridItemProvider  
 Le proprietà e i metodi seguenti sono necessari per l'implementazione di <xref:System.Windows.Automation.Provider.IGridItemProvider>.  
  
|Membri obbligatori|Tipo di membro|Note|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.RowSpan%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ColumnSpan%2A>|Proprietà|Nessuno|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A>|Proprietà|None|  
  
 Questo pattern di controllo non è associato a metodi o eventi.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Eccezioni  
 Questo pattern di controllo non è associato a eccezioni.  
  
## <a name="see-also"></a>Vedere anche  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Supportare pattern di controllo in un Provider di automazione interfaccia utente](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [Pattern di controllo di automazione interfaccia utente per i client](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementazione del Pattern di controllo Grid di automazione dell'interfaccia utente](../../../docs/framework/ui-automation/implementing-the-ui-automation-grid-control-pattern.md)   
 [Panoramica di struttura ad albero di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Utilizzare la memorizzazione nella cache di automazione interfaccia utente](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)