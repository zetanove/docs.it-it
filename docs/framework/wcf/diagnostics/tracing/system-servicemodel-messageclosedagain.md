---
title: "System.ServiceModel.MessageClosedAgain | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24c274d4-65cd-4c91-9869-bc6eb34ef979
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.MessageClosedAgain
System.ServiceModel.MessageClosedAgain  
  
## Descrizione  
 Un messaggio è stato nuovamente chiuso.  
  
 Un messaggio deve essere chiuso solo una volta.Se questa traccia viene emessa in codice di estensione utente, indica che tale codice sta chiudendo un messaggio che è già stato chiuso.Se viene emessa tramite codice del prodotto, indica che il codice di estensione utente potrebbe potenzialmente stare per chiudere un messaggio troppo presto.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)