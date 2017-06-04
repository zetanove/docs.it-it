---
title: "Get UI Automation Element Properties | Microsoft Docs"
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
  - "properties, retrieving"
  - "UI Automation, retrieving properties of elements"
ms.assetid: 09576b1a-291f-435c-980e-dee32d899ae1
caps.latest.revision: 5
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 5
---
# Get UI Automation Element Properties
> [!NOTE]
>  La presente documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare le classi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gestite definite nello spazio dei nomi <xref:System.Windows.Automation>.  Per informazioni aggiornate sull'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: Automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746) \(la pagina potrebbe essere in inglese\).  
  
 In questo argomento viene illustrato come recuperare proprietà di un elemento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
### Ottenere un valore di proprietà corrente  
  
1.  Ottenere l'oggetto <xref:System.Windows.Automation.AutomationElement> di cui si desidera ottenere la proprietà.  
  
2.  Chiamare il metodo <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A> o recuperare la struttura della proprietà <xref:System.Windows.Automation.AutomationElement.Current%2A> e ottenere il valore da uno dei membri.  
  
### Ottenere un valore di proprietà memorizzato nella cache  
  
1.  Ottenere l'oggetto <xref:System.Windows.Automation.AutomationElement> di cui si desidera ottenere la proprietà.  È necessario che la proprietà sia stata specificata nell'oggetto <xref:System.Windows.Automation.CacheRequest>.  
  
2.  Chiamare il metodo <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A> o recuperare la struttura della proprietà <xref:System.Windows.Automation.AutomationElement.Cached%2A> e ottenere il valore da uno dei membri.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrate varie modalità per recuperare le proprietà correnti di un oggetto <xref:System.Windows.Automation.AutomationElement>.  
  
 [!code-csharp[UIAClient_snip#170](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#170)]
 [!code-vb[UIAClient_snip#170](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#170)]  
  
## Vedere anche  
 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)   
 [Caching in UI Automation Clients](../../../docs/framework/ui-automation/caching-in-ui-automation-clients.md)