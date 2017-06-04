---
title: "Durata chiamata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4973ec3-3c66-4c0b-b5d0-294b62c83f7d
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Durata chiamata
Nome contatore: durata chiamata  
  
## Descrizione  
 Durata media delle chiamate a questa operazione.  La durata media viene calcolata in base a questa equazione: \(N1\-N0\)\/\(D1\-D0\).  
  
> [!WARNING]
>  Quando viene usato in un servizio WCF asincrono, il contatore della durata della chiamata restituirà sempre \-1.  
  
## Vedere anche  
 [PERF\_AVERAGE\_TIMER](http://go.microsoft.com/fwlink/?LinkId=95015)