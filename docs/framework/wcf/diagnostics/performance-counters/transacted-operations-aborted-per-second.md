---
title: "Operazioni transazionali interrotte ogni secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19fc993f-2b3d-4898-852e-3b98ec2153a5
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Operazioni transazionali interrotte ogni secondo
Nome contatorte: operazioni transazionali interrotte ogni secondo.  
  
## Descrizione  
 Numero di operazioni transazionali interrotte in questo servizio in un secondo.  
  
 Si tratta di un contatore di prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato utilizzando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)