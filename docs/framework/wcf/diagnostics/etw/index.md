---
title: "Analytic Tracing with ETW | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "diagnostics [WCF], analytic tracing"
  - "administration [WCF], analytic tracing"
  - "analytic tracing [WCF]"
ms.assetid: 1d518e47-a38d-41e8-93d7-8c3b361f6a56
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Analytic Tracing with ETW
La traccia analitica di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] offre un modo per acquisire informazioni diagnostiche durante l'esecuzione di un servizio di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].Gli eventi di traccia analitica di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] vengono generati in punti chiave dello stack [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] per consentire la risoluzione dei problemi relativi ai servizi di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] in un ambiente di produzione.La traccia analitica per i servizi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] produce un impatto minimo sulle prestazioni di un server di prodotto che ospita servizi [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)][!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], poiché tali eventi vengono generati in modo estremamente efficace a una sessione di Traccia eventi per Windows \(ETW\).  
  
## In questa sezione  
 [Panoramica della traccia analitica](../../../../../docs/framework/wcf/diagnostics/etw/analytic-tracing-overview.md)  
 Viene descritta la modalità in cui la traccia analitica di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] viene utilizzata in [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)].  
  
 [Abilitazione dinamica della traccia analitica](../../../../../docs/framework/wcf/diagnostics/etw/dynamically-enabling-analytic-tracing.md)  
 Descrive la modalità di abilitazione o disabilitazione della traccia in modo dinamico mediante ETW.  
  
 [Configurazione della traccia del flusso di messaggi](../../../../../docs/framework/wcf/diagnostics/etw/configuring-message-flow-tracing.md)  
 Descrive la modalità di configurazione della traccia del flusso di messaggi.  
  
 [Riferimento dell'evento di traccia analitica](../../../../../docs/framework/wcf/diagnostics/etw/analytic-trace-event-reference.md)  
 Mostra una tabella di ID evento con i relativi livelli, parole chiave e messaggi dell'evento.  
  
## Vedere anche  
 [Servizi WCF e traccia eventi per Windows](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)   
 [Eventi di rilevamento in Traccia eventi per Windows](../../../../../docs/framework/windows-workflow-foundation/samples/tracking-events-into-event-tracing-in-windows.md)