---
title: "Interazione tra criteri di cache: durata massima e obsolescenza massima | Microsoft Docs"
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
  - "obsolescenza massima"
  - "validità minima delle risorse memorizzate nella cache"
  - "ora, risorse memorizzate nella cache"
  - "durata massima, criteri"
  - "obsolescenza delle risorse memorizzate nella cache"
  - "validità delle risorse memorizzate nella cache"
ms.assetid: 7f775925-89a1-4956-ba90-c869c1749a94
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Interazione tra criteri di cache: durata massima e obsolescenza massima
Per assicurarsi che il contenuto più nuovo viene restituito all'applicazione client, l'interazione di criteri della cache client e i requisiti della riconvalida del server restituisce sempre i criteri della cache più conservativi.  Tutti gli esempi di questo argomento vengono illustrati i criteri della cache per una risorsa memorizzata nella cache il 1° gennaio e scade il 4 gennaio.  
  
 Negli esempi seguenti, il valore massimo di rancidità \(`maxStale`\) viene utilizzato insieme alla validità massima \(`maxAge`\):  
  
-   Se i criteri della cache per `maxAge` \= 5 giorni e non specificano un valore `maxStale`, a seconda del valore `maxAge`, il contenuto è fino al 6 gennaio utilizzabile.  Tuttavia, a seconda dei requisiti della riconvalida del server, il contenuto scade il 4 gennaio.  Poiché la data di scadenza contenuto è più conservativo \(precedente\), ha la precedenza sui criteri `maxAge`.  Di conseguenza, il contenuto scade il 4 gennaio e deve essere verranno riconvalidati anche se la validità massima non è stata raggiunta.  
  
-   Se i criteri della cache per `maxAge` \= 5 giorni e `maxStale` \= 3 giorni, a seconda del valore `maxAge`, il contenuto è fino al 6 gennaio utilizzabile.  A seconda del valore `maxStale`, il contenuto è fino al 7 gennaio utilizzabile.  Di conseguenza, il contenuto ottiene verranno riconvalidati il 6 gennaio.  
  
-   Se i criteri della cache per `maxAge` \= 5 giorni e `maxStale` \= il 1 giorni, a seconda del valore `maxAge`, il contenuto è fino al 6 gennaio utilizzabile.  A seconda del valore `maxStale`, il contenuto è fino al 5 gennaio utilizzabile.  Di conseguenza, il contenuto ottiene verranno riconvalidati il 5 gennaio.  
  
 Quando la validità massima è inferiore alla data di scadenza contenuto, il comportamento più conservativo di memorizzazione nella cache prevale sempre e il valore massimo di rancidità non ha effetto.  Negli esempi seguenti viene illustrato l'effetto di impostare un valore massimo di rancidità \(`maxStale`\) quando la validità massima \(`maxAge`\) viene raggiunta prima che il contenuto scadenza:  
  
-   Se i criteri della cache per `maxAge` \= 1 il giorno e non specificano un valore per il valore `maxStale`, il contenuto verranno riconvalidati il 2 gennaio anche se non è scaduto.  
  
-   Se i criteri della cache per`maxAge` \= 1 il giorno e `maxStale` \= 3 giorni, il contenuto verranno riconvalidati il 2 gennaio per applicare le impostazioni criteri più conservatrice.  
  
-   Se i criteri della cache per `maxAge` \= 1 il giorno e `maxStale` \= 1 il giorno, il contenuto verranno riconvalidati il 2 gennaio.  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Configurazione della memorizzazione nella cache per applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)   
 [Interazione tra criteri di cache: durata massima e validità minima](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-minimum-freshness.md)