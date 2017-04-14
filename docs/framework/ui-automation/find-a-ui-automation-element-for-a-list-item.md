---
title: "Find a UI Automation Element for a List Item | Microsoft Docs"
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
  - "list items, finding elements for"
  - "elements, finding for list items"
  - "UI Automation, finding elements for List items"
ms.assetid: c326ad2b-2144-4f64-ae4c-d850c74f95c5
caps.latest.revision: 5
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 5
---
# Find a UI Automation Element for a List Item
> [!NOTE]
>  La presente documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare le classi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gestite definite nello spazio dei nomi <xref:System.Windows.Automation>.  Per informazioni aggiornate sull'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: Automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746) \(la pagina potrebbe essere in inglese\).  
  
 In questo argomento viene illustrato come recuperare un oggetto <xref:System.Windows.Automation.AutomationElement> per un elemento all'interno di un elenco quando l'indice dell'elemento è noto.  
  
## Esempio  
 Nell'esempio seguente vengono illustrate due tecniche per il recupero di un elemento specificato da un elenco. Nel primo caso viene utilizzato l'oggetto <xref:System.Windows.Automation.TreeWalker> e nel secondo l'oggetto <xref:System.Windows.Automation.AutomationElement.FindAll%2A>.  
  
 La prima tecnica è in genere più veloce per i controlli [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)], mentre la seconda è più veloce per i controlli [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)].  
  
 [!code-csharp[UIAClient_snip#184](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#184)]
 [!code-vb[UIAClient_snip#184](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#184)]  
  
## Vedere anche  
 [Obtaining UI Automation Elements](../../../docs/framework/ui-automation/obtaining-ui-automation-elements.md)