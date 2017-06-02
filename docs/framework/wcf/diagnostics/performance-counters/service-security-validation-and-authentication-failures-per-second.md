---
title: "Servizio: errori di convalida di sicurezza e di autenticazione al secondo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4af18009-e778-490b-9ba6-e76485285830
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# Servizio: errori di convalida di sicurezza e di autenticazione al secondo
Nome contatore: errori di convalida di sicurezza e di autenticazione al secondo.  
  
## Descrizione  
 Il contatore viene incrementato ogni volta che un messaggio viene rifiutato a causa di un problema di sicurezza non coperto dal contatore "chiamate di sicurezza non autorizzate".Tra tali problemi si contano:  
  
-   È stato impossibile leggere il client token dal messaggio.  
  
-   Il client token non è stato autenticato \(ad esempio la password era errata\).  
  
-   La verifica della firma non è riuscita \(ad esempio il messaggio è stato manomesso\).  
  
-   Il messaggio è un duplicato di un messaggio precedente, evenienza possibile durante un attacco di tipo replay.  
  
-   Si è verificato un errore di decrittografia.  
  
-   Alcuni elementi obbligatori \(ad esempio timestamp mancante o blocco di dati crittografati\) non sono presenti nel messaggio.  
  
-   Gli errori si sono verificati durante l'handshake TLSNEGO\/SPNEGO.  
  
 Si tratta di un contatore delle prestazioni di tipo [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), il cui valore viene calcolato utilizzando la formula seguente.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)