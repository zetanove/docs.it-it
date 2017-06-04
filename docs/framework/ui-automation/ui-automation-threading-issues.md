---
title: "UI Automation Threading Issues | Microsoft Docs"
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
  - "UI Automation, threading issues"
  - "threading issues with UI Automation"
ms.assetid: 0ab8d42c-5b8b-481b-b788-2caecc2f0191
caps.latest.revision: 9
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 9
---
# UI Automation Threading Issues
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 A causa del modo in cui [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] usa i messaggi di Windows, è possibile che si verifichino conflitti quando un'applicazione client tenta di interagire con la propria [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] sul thread dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Tali conflitti possono rallentare in modo significativo le prestazioni o provocare la mancata risposta dell'applicazione.  
  
 Se l'applicazione client deve interagire con tutti gli elementi sul desktop, tra cui la propria [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)], è consigliabile eseguire tutte le chiamate all'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] in un thread separato. Ciò include l'individuazione di elementi \(ad esempio, mediante il metodo <xref:System.Windows.Automation.TreeWalker> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A>\) e l'uso dei pattern di controllo.  
  
 È consigliabile effettuare chiamate dell'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] all'interno di un gestore eventi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] poiché il gestore eventi viene sempre chiamato in un thread non dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Tuttavia, quando si sottoscrive gli eventi che possono avere origine dall'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] dell'applicazione client, è necessario effettuare la chiamata a <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A> o a un metodo correlato su un thread non dell'[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Rimuovere i gestori eventi sullo stesso thread.