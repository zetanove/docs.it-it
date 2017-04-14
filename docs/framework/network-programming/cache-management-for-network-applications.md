---
title: "Gestione della cache per le applicazioni di rete | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "cache [.NET Framework], applicazioni di rete"
  - "risorse di rete, memorizzazione nella cache"
  - "Internet, memorizzazione nella cache"
ms.assetid: fc258a40-f370-434f-ae09-4a8cb11ddaeb
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Gestione della cache per le applicazioni di rete
In questo argomento e i relativi gli argomenti correlati descritti memorizzare nella cache per le risorse ottenute mediante <xref:System.Net.WebClient>, <xref:System.Net.WebRequest>, <xref:System.Net.HttpWebRequest>e le classi <xref:System.Net.FtpWebRequest>.  
  
 In una cache sono provvisoriamente archiviate le risorse richieste da un'applicazione.  Se viene richiesta più volte la stessa risorsa, la risorsa può essere restituita dalla cache, evitando il sovraccarico di una richiesta dal server.  La memorizzazione nella cache può migliorare le prestazioni dell'applicazione riducendo il tempo necessario per ottenere una risorsa richiesta.  La memorizzazione nella cache può inoltre possibile ridurre il traffico di rete riducendo il numero di round trip al server.  Come memorizzare nella cache migliora le prestazioni, aumenta il rischio che la risorsa restituita all'applicazione non è aggiornata, pertanto non è identico alla risorsa che sarebbe stata inviata dal server se la memorizzazione nella cache non venisse utilizzato.  
  
 La memorizzazione nella cache può consentire agli utenti non autorizzati o i processi leggere i dati privati.  Una risposta autenticata memorizzata nella cache può essere recuperata dalla cache senza un'autorizzazione.  Se la memorizzazione nella cache è abilitata, modifica a <xref:System.Net.WebRequest.CachePolicy%2A> a <xref:System.Net.Cache.RequestCacheLevel> o a <xref:System.Net.Cache.RequestCacheLevel> per disabilitare la memorizzazione nella cache per la richiesta.  
  
 A causa di problemi di sicurezza, la memorizzazione nella cache è **not** consigliato per scenari di livello intermedio.  
  
## In questa sezione  
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)  
 Viene illustrata i criteri della cache e viene illustrato come definire uno.  
  
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 Definisce ogni tipo di criteri della cache basati su posizione disponibile per le risorse del protocollo HTTP \(HTTP o HTTPS\).  
  
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 Vengono descritti i criteri che possono essere utilizzati per personalizzare criteri della cache basati sull'ora.  
  
 [Configurazione della memorizzazione nella cache per applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 Viene descritto come creare a livello di codice i criteri della cache e richiede la memorizzazione nella cache di utilizzo.  
  
## Riferimenti  
 <xref:System.Net.Cache>  
 Definisce i tipi e le enumerazioni utilizzate per definire i criteri della cache per le risorse ottenute mediante <xref:System.Net.WebRequest>, <xref:System.Net.HttpWebRequest>e le classi <xref:System.Net.FtpWebRequest>.