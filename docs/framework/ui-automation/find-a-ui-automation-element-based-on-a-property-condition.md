---
title: "Find a UI Automation Element Based on a Property Condition | Microsoft Docs"
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
  - "elements, finding by property conditions"
  - "UI Automation, finding elements by property conditions"
ms.assetid: 3acaee5a-6ce8-4c3e-81c8-67e59eb74477
caps.latest.revision: 19
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 19
---
# Find a UI Automation Element Based on a Property Condition
> [!NOTE]
>  La presente documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare le classi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gestite definite nello spazio dei nomi <xref:System.Windows.Automation>.  Per informazioni aggiornate sull'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: Automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746) \(la pagina potrebbe essere in inglese\).  
  
 In questo argomento viene presentato codice di esempio che mostra come trovare un elemento all'interno della struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] in base a una o più proprietà specifiche.  
  
## Esempio  
 Nell'esempio riportato di seguito viene specificato un insieme di condizioni di proprietà che identifica un determinato elemento \(o più elementi\) di interesse nella struttura ad albero di <xref:System.Windows.Automation.AutomationElement>.  Viene quindi eseguita una ricerca di tutti gli elementi corrispondenti con il metodo <xref:System.Windows.Automation.AutomationElement.FindAll%2A> che incorpora una serie di operazioni booleane <xref:System.Windows.Automation.AndCondition> per limitare il numero di elementi corrispondenti.  
  
> [!NOTE]
>  Quando si eseguono ricerche dalla proprietà <xref:System.Windows.Automation.AutomationElement.RootElement%2A>, è necessario tentare di ottenere solo figli diretti.  Una ricerca dei discendenti potrebbe ripetersi in centinaia o addirittura migliaia di elementi, con la possibilità di un overflow dello stack.  Se si tenta di ottenere un elemento specifico a un livello inferiore, è necessario avviare la ricerca dalla finestra dell'applicazione o da un contenitore a un livello inferiore.  
  
 [!code-csharp[InvokePatternApp#1100](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1100)]
 [!code-vb[InvokePatternApp#1100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1100)]  
  
## Vedere anche  
 [InvokePattern and ExpandCollapsePattern Menu Item Sample](http://msdn.microsoft.com/it-it/b7fa141c-e2d1-4da2-a27f-81a7d1172210)   
 [Obtaining UI Automation Elements](../../../docs/framework/ui-automation/obtaining-ui-automation-elements.md)   
 [Use the AutomationID Property](../../../docs/framework/ui-automation/use-the-automationid-property.md)