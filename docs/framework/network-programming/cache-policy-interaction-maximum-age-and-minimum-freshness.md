---
title: "Interazione tra criteri di cache: durata massima e validit&#224; minima | Microsoft Docs"
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
  - "criteri di cache basati sull'ora"
  - "Revalidate (criterio)"
  - "cache [.NET Framework], criteri basati sull'ora"
  - "validità minima delle risorse memorizzate nella cache"
  - "durata massima, criteri"
  - "validità minima, criteri"
  - "validità delle risorse memorizzate nella cache"
ms.assetid: 6567d451-ecec-496c-95a3-a415b99ba52a
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Interazione tra criteri di cache: durata massima e validit&#224; minima
Per assicurarsi che il contenuto più nuovo viene restituito all'applicazione client, l'interazione di criteri della cache client e i requisiti della riconvalida del server restituisce sempre i criteri della cache più conservativi.  Tutti gli esempi di questo argomento vengono illustrati i criteri della cache per una risorsa memorizzata nella cache il 1° gennaio e scade il 4 gennaio.  
  
 Negli esempi seguenti vengono illustrati i criteri della cache che risultati dell'interazione di validità massima \(`maxAge`\) e i valori minimi di dati \(`minFresh`\).  
  
-   Se i criteri della cache per `maxAge` \= 2 giorni e `minFresh` non viene specificato, il contenuto verranno riconvalidati il 3 gennaio.  
  
-   Se i criteri della cache per `maxAge` \= 2 giorni e `minFresh` \= il 1 giorni, come `maxAge`, il contenuto è fino al 3 gennaio nuovo.  Come `minFresh`, il contenuto è fino al 3 gennaio nuovo.  Di conseguenza, il contenuto deve essere verranno riconvalidati il 3 gennaio.  
  
-   Se i criteri della cache per `maxAge`\= 2 giorni e `minFresh` \= 2 giorni, come `maxAge`, il contenuto è fino al 3 gennaio nuovo.  Come `minFresh` il contenuto è fino al 2 gennaio nuovo.  Di conseguenza, il contenuto deve essere verranno riconvalidati il 2 gennaio.  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Configurazione della memorizzazione nella cache per applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)   
 [Interazione tra criteri di cache: durata massima e obsolescenza massima](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-maximum-staleness.md)