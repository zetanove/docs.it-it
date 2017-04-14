---
title: "Servizio: errori di convalida e di autenticazione di sicurezza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 55c98268-b1ad-459d-851b-25ef52248187
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# Servizio: errori di convalida e di autenticazione di sicurezza
Nome contatore: errori di convalida e di autenticazione di sicurezza  
  
## Descrizione  
 Questo contatore avanza ogni volta in cui un messaggio viene rifiutato a causa di un problema di sicurezza non coperto dal contatore "chiamate di sicurezza non autorizzate".Tra tali problemi si contano:  
  
-   Non è stato possibile leggere il token client dal messaggio.  
  
-   Il client token non è stato autenticato \(ad esempio, la password era errata\).  
  
-   La verifica della firma non è riuscita \(ad esempio, il messaggio è stato manomesso\).  
  
-   Il messaggio è un duplicato di un messaggio precedente. Ciò può verificarsi durante un attacco di tipo replay.  
  
-   Si è verificato un errore di decrittografia.  
  
-   Alcuni elementi obbligatori \(ad esempio, timestamp mancante o blocco di dati crittografati\) non sono presenti nel messaggio.  
  
-   Si sono verificati errori durante l'handshake TLSNEGO\/SPNEGO.