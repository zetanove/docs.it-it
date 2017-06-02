---
title: "System.ServiceModel.Channels.PrematureDatagramEof | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec07be8b-b537-4090-be7e-086679dba78d
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# System.ServiceModel.Channels.PrematureDatagramEof
System.ServiceModel.Channels.PrematureDatagramEof  
  
## Descrizione  
 È stato ricevuto un Message Null \(ad indicare la fine del canale\) da un canale del datagramma, ma il canale è ancora nello stato Opened.  Ciò indica un errore nel canale del datagramma e il ciclo di ricezione de\-multiplexer è stato bloccato prematuramente.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)