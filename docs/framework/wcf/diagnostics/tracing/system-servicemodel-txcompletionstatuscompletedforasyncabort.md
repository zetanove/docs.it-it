---
title: "System.ServiceModel.TxCompletionStatusCompletedForAsyncAbort | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 155c3203-2e17-4709-b896-2254e22da45e
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# System.ServiceModel.TxCompletionStatusCompletedForAsyncAbort
La transazione specificata per l'operazione indicata è stata completata a causa di un'interruzione asincrona.  
  
## Descrizione  
 La transazione corrente è stata interrotta a causa di un altro partecipante che vota per l'interruzione, al verificarsi di timeout o di un altro errore all'interno del partecipante a una transazione.  
  
## Risoluzione dei problemi  
 Se si tratta di un'interruzione imprevista, esaminare tutti i registri eventi di sistema per determinare il motivo effettivo dell'interruzione.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)