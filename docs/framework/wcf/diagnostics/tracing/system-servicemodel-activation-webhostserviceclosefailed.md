---
title: "System.ServiceModel.Activation.WebHostServiceCloseFailed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3cab9856-a5cf-4f0e-a0cb-89425e368f8e
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# System.ServiceModel.Activation.WebHostServiceCloseFailed
Si verifica quando un servizio non può essere chiuso normalmente e viene interrotto.  
  
## Descrizione  
 Questo codice di errore viene visualizzato nel file di log.In genere, indica un errore di programmazione, ad esempio quando si tenta di chiudere un servizio dopo che è già stato chiamato Abort.  
  
## Risoluzione dei problemi  
 Verificare il codice sorgente dell'applicazione.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)