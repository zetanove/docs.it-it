---
title: "Errori di convalida e di autenticazione della protezione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0d4e3666-dfc6-421c-baf8-9479c22f7050
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Errori di convalida e di autenticazione della protezione
Nome contatore: errori di convalida e di autenticazione di sicurezza  
  
## Descrizione  
 Questo contatore avanza ogni volta in cui un messaggio viene rifiutato a causa di un problema di sicurezza non coperto dal contatore "chiamate di sicurezza non autorizzate".Tra tali problemi si contano:  
  
-   È stato impossibile leggere il client token dal messaggio.  
  
-   Il client token non è stato autenticato \(ad esempio la password era errata\).  
  
-   La verifica della firma non è riuscita \(ad esempio il messaggio è stato manomesso\).  
  
-   Il messaggio è un duplicato di un messaggio precedente, evenienza possibile durante un attacco di tipo replay.  
  
-   Si è verificato un errore di decrittografia.  
  
-   Alcuni elementi obbligatori \(ad esempio timestamp mancante o blocco di dati crittografati\) non sono presenti nel messaggio.  
  
-   Si sono verificati errori durante l'handshake TLSNEGO\/SPNEGO.