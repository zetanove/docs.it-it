---
title: "Support Control Patterns in a UI Automation Provider | Microsoft Docs"
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
  - "control patterns, supporting in UI Automation provider"
  - "UI Automation, supporting control patterns in provider"
ms.assetid: 0d635c35-ffa8-4dc8-bbc9-12fcd5445776
caps.latest.revision: 13
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 13
---
# Support Control Patterns in a UI Automation Provider
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento viene descritto come implementare uno o più pattern di controllo in un provider di automazione interfaccia utente in modo che le applicazioni client possano modificare i controlli e ottenere dati.  
  
### Supportare i pattern di controllo  
  
1.  Implementare le interfacce appropriate per i pattern di controllo che l'elemento deve supportare, ad esempio <xref:System.Windows.Automation.Provider.IInvokeProvider> per <xref:System.Windows.Automation.InvokePattern>.  
  
2.  Restituire l'oggetto che contiene l'implementazione di ciascuna interfaccia di controllo nell'implementazione di <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A?displayProperty=fullName>  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'implementazione di <xref:System.Windows.Automation.Provider.ISelectionProvider> per una casella di riepilogo personalizzata a selezione singola. Restituisce tre proprietà e ottiene l'elemento attualmente selezionato.  
  
 [!code-csharp[UIAFragmentProvider_snip#119](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListPattern.cs#119)]
 [!code-vb[UIAFragmentProvider_snip#119](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListPattern.vb#119)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'implementazione <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A> che restituisce la classe che implementa <xref:System.Windows.Automation.Provider.ISelectionProvider>. La maggior parte dei controlli casella di riepilogo supporta anche altri pattern, ma in questo esempio viene restituito un riferimento null \(`Nothing` in [!INCLUDE[TLA#tla_visualbnet](../../../includes/tlasharptla-visualbnet-md.md)]\) per tutti gli altri identificatori di pattern.  
  
 [!code-csharp[UIAFragmentProvider_snip#120](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#120)]
 [!code-vb[UIAFragmentProvider_snip#120](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#120)]  
  
## Vedere anche  
 [UI Automation Providers Overview](../../../docs/framework/ui-automation/ui-automation-providers-overview.md)   
 [Server\-Side UI Automation Provider Implementation](../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)