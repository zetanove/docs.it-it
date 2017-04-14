---
title: "Messaggi in coda rifiutati al secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77ea9aa3-b9e2-4a1d-a65e-5ca115ba0567
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Messaggi in coda rifiutati al secondo
Nome contatore: messaggi in coda rifiutati al secondo  
  
## Descrizione  
 Numero di messaggi rifiutati dal trasporto in coda di questo servizio al secondo.  
  
 Si tratta di un contatore di prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato utilizzando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)