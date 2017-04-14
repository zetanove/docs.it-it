---
title: "Invoke a Control Using UI Automation | Microsoft Docs"
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
  - "invoking controls"
  - "UI Automation, invoking controls"
  - "controls, invoking"
ms.assetid: 5ee2de3f-256c-43ec-b64c-62ace91f9983
caps.latest.revision: 15
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 15
---
# Invoke a Control Using UI Automation
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento viene illustrato come eseguire le attività seguenti:  
  
-   Trovare un controllo che corrisponda a condizioni di proprietà specifiche scorrendo la visualizzazione controlli dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per l'applicazione di destinazione.  
  
-   Creare un <xref:System.Windows.Automation.AutomationElement> per ogni controllo.  
  
-   Ottenere un oggetto <xref:System.Windows.Automation.InvokePattern> da qualsiasi elemento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] trovato che supporta il pattern di controllo <xref:System.Windows.Automation.InvokePattern>.  
  
-   Usare <xref:System.Windows.Automation.InvokePattern.Invoke%2A> per richiamare il controllo da un gestore eventi client.  
  
## Esempio  
 Questo esempio usa il metodo <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> della classe <xref:System.Windows.Automation.AutomationElement> per generare un oggetto <xref:System.Windows.Automation.InvokePattern> e richiamare un controllo mediante il metodo <xref:System.Windows.Automation.InvokePattern.Invoke%2A>.  
  
 [!code-csharp[InvokePatternApp#1100](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1100)]
 [!code-vb[InvokePatternApp#1100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1100)]  
[!code-csharp[InvokePatternApp#1102](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1102)]
[!code-vb[InvokePatternApp#1102](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1102)]  
  
## Vedere anche  
 [InvokePattern and ExpandCollapsePattern Menu Item Sample](http://msdn.microsoft.com/it-it/b7fa141c-e2d1-4da2-a27f-81a7d1172210)