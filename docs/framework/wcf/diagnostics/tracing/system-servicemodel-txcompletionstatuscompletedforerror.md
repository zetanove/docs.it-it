---
title: "System.ServiceModel.TxCompletionStatusCompletedForError | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ade4722-a6d5-471c-b960-1cfea4ea2aa9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.TxCompletionStatusCompletedForError
La transazione specificata per l'operazione indicata è stata completata a causa di un'eccezione di esecuzione non gestita.  
  
## Descrizione  
 Traccia eseguita quando si verifica un errore durante un tentativo di completare la transazione corrente.Questo si verifica prima che venga inviata una replica o un errore al chiamante.  
  
## Risoluzione dei problemi  
 Cercare nel messaggio tracciato il messaggio dell'eccezione ed eventuali elementi eseguibili.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)