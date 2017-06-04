---
title: "Messaggi di messaggistica affidabile ignorati al secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a11b0b80-b242-48e1-b0bb-7f756db5486b
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Messaggi di messaggistica affidabile ignorati al secondo
Nome contatore: sessioni di messaggistica affidabile eliminate al secondo.  
  
## Descrizione  
 Numero complessivo di messaggi di messaggistica affidabile ignorati in questo servizio in un secondo.  
  
 Si tratta di un contatore di prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato utilizzando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)