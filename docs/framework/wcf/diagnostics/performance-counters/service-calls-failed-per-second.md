---
title: "Servizio: chiamate non riuscite al secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5a2c7939-107d-4f0c-b43c-e02e079e8a9d
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Servizio: chiamate non riuscite al secondo
Nome contatore: chiamate non riuscite al secondo  
  
## Descrizione  
 Numero di chiamate al secondo ricevute dal servizio aventi eccezioni non gestite.  
  
 Si tratta di un contatore di prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato utilizzando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)  
  
 Nel codice gestito, le eccezioni vengono generate quando si verificano condizioni di errore.  
  
 Nel codice gestito, vengono generate eccezioni quando si verificano condizioni di errore.  
  
 Questo contatore viene incrementato ogni volta che si verifica un'eccezione non gestita in questo servizio.  
  
## Vedere anche  
 [Specifica e gestione di errori in contratti e servizi](../../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)