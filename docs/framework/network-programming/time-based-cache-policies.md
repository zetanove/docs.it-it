---
title: "Criteri di cache basati sull&#39;ora | Microsoft Docs"
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
  - "data di sincronizzazione della cache, criteri"
  - "cache [.NET Framework], criteri basati sull'ora"
  - "validità minima delle risorse memorizzate nella cache"
  - "ora, risorse memorizzate nella cache"
  - "durata massima, criteri"
  - "sincronizzazione, cache"
  - "obsolescenza delle risorse memorizzate nella cache"
  - "criteri di cache basati sull'ora predefiniti"
  - "obsolescenza massima, criteri"
  - "criteri di cache per il contenuto"
  - "contenuto scaduto"
  - "validità minima, criteri"
  - "validità delle risorse memorizzate nella cache"
ms.assetid: 74f0bcaf-5c95-40c1-9967-f3bbf1d2360a
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Criteri di cache basati sull&#39;ora
Criteri della cache basati sull'ora definiscono la validità delle voci memorizzate nella cache utilizzando il tempo che la risorsa è stata recuperata, le intestazioni restituito alla risorsa e l'ora corrente.  Nell'impostare criteri della cache basati sull'ora, è possibile utilizzare criteri temporizzati <xref:System.Net.Cache.HttpRequestCacheLevel> o creare criteri temporizzati personalizzati.  Quando si utilizza i criteri temporizzati predefiniti per le risorse ottenuto utilizzando il protocollo HTTP \(HTTP\), il comportamento esatto della cache è determinato dalle intestazioni associate alla risposta memorizzata nella cache e dai comportamenti specificati in parti 13 e 14 dello standard RFC 2616, disponibile su [http:\/\/www.ietf.org](http://www.ietf.org/).  Per un esempio di codice che illustri impostare i criteri temporizzati predefiniti per le risorse HTTP, vedere [Procedura: Impostare criteri della cache basati sull'ora predefiniti per un'applicazione](../../../docs/framework/network-programming/how-to-set-the-default-time-based-cache-policy-for-an-application.md).  Per gli esempi di codice che illustrano la creazione e l'utilizzo dei criteri della cache, vedere [Configurazione che memorizza nella cache nelle applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md).  
  
## Criteri per determinare validità delle voci memorizzate nella cache  
 Per personalizzare criteri della cache basati sull'ora, è possibile specificare che uno o più dei seguenti criteri vengono utilizzati per determinare la validità delle voci memorizzate nella cache:  
  
-   Validità massima  
  
-   Rancidità massima  
  
-   Validità minima  
  
-   Data di sincronizzazione della cache  
  
> [!NOTE]
>  Mediante i criteri della cache basati sull'ora di impostazione predefinita non deve essere confuso con impostare i criteri della cache predefiniti per l'applicazione.  I criteri temporizzati predefiniti sono i criteri specifici che possono essere utilizzati su richiesta o livello di applicazione.  I criteri della cache predefiniti dell'applicazione sono i criteri \(basati sul percorso o temporizzati\) che hanno effetto quando nessun modello viene impostato su una richiesta.  Per informazioni dettagliate sull'impostazione dei criteri della cache predefiniti per l'applicazione, vedere <xref:System.Net.WebRequest.DefaultCachePolicy%2A>.  
  
### Validità massima  
 Il modello massimo di criteri di età specifica la quantità di tempo necessaria una copia memorizzata nella cache di risorsa può essere utilizzato.  Se la copia memorizzata nella cache della risorsa è più recente di tempo specificato, la risorsa deve essere verranno riconvalidati controllandolo sul contenuto nel server.  Se l'età massima consentisse la risorsa da utilizzare dopo la scadenza, questo i criteri non viene rispettato a meno che un valore massimo di rancidità anche sia specificato.  
  
### Rancidità massima  
 Il modello massimo di criteri di rancidità specifica la durata dopo la scadenza contenuto che la copia memorizzata nella cache della risorsa può essere utilizzata.  Questo è l'unico modello dei criteri della cache che consente alle risorse di essere utilizzato dopo che è scaduto.  
  
### Validità minima  
 Il modello minimo di criteri di validità specifica la durata prima di scadenza contenuto che la copia memorizzata nella cache della risorsa può essere utilizzata.  Questi criteri sono l'effetto di forzare una voce della cache di scadere prima della scadenza, pertanto, la validità minima e il massimo le impostazioni di rancidità si escludono reciprocamente.  
  
## Data di sincronizzazione della cache  
 Il modello dei criteri di sincronizzazione della cache determina quando una copia memorizzata nella cache di una risorsa deve essere verranno riconvalidati controllandola sul contenuto nel server.  Se il contenuto è stato modificato da quando l'elemento è stato memorizzato nella cache, viene recuperato il server, viene memorizzato nella cache e viene restituito all'applicazione.  Se il contenuto non è cambiato, il timestamp aggiornato e l'applicazione ottiene il contenuto memorizzato nella cache.  
  
 La data di sincronizzazione della cache consente di specificare una data assoluta in cui è necessario riconvalidare il contenuto nella cache.  Se una voce della cache aggiornata verranno riconvalidati l'ultima volta prima della data di sincronizzazione della cache, la riconvalida con il server viene nuovamente generato.  Se la voce della cache verranno riconvalidati dopo che la data di sincronizzazione della cache e non esistono requisiti aggiuntivi della riconvalida del server o di dati che invalidino la voce memorizzata nella cache, la voce della cache viene utilizzata.  Se la data di sincronizzazione della cache è impostata su una data futura, la voce viene riconvalidata a ogni richiesta, finché non è trascorsa la data di sincronizzazione della cache.  
  
 Negli argomenti seguenti vengono fornite informazioni sugli effetti di combinazione dei criteri dei criteri della cache basati sull'ora:  
  
-   [Interazione tra criteri di cache: durata massima e obsolescenza massima](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-maximum-staleness.md)  
  
-   [Interazione tra criteri di cache: durata massima e validità minima](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-minimum-freshness.md)  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Configurazione della memorizzazione nella cache per applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)   
 [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)