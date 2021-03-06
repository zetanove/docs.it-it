---
title: "Chiamate non riuscite al secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4ef3773-f650-4876-99cf-4d0c02aa03d4
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Chiamate non riuscite al secondo
Nome contatore: chiamate non riuscite al secondo  
  
## Descrizione  
 Numero di chiamate al secondo con eccezioni non gestite presenti in questa operazione.  
  
 Si tratta di un contatore di prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato usando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)  
  
 Questo contatore viene incrementato ogni volta che si verifica un'eccezione non gestita in questa operazione.  
  
## Vedere anche  
 [Specifica e gestione di errori in contratti e servizi](../../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)