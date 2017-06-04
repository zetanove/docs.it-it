---
title: "Criteri di cache basati sulla posizione | Microsoft Docs"
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
  - "CacheIfAvailable (criterio)"
  - "reload (criterio)"
  - "criteri di cache basati sulla posizione"
  - "CacheOnly (criterio)"
  - "cache locale"
  - "cache intermedia"
  - "NoCacheNoStore (criterio)"
  - "cache [.NET Framework], criteri basati sulla posizione"
  - "Revalidate (criterio)"
  - "validità minima delle risorse memorizzate nella cache"
  - "CacheOrNextCacheOnly (criterio)"
  - "Refresh (criterio)"
ms.assetid: e41d7f1a-0a6a-4dee-97d1-c6a8b6a07fc2
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Criteri di cache basati sulla posizione
Criteri della cache basati sul percorso definiscono la validità delle voci memorizzate nella cache valide in base alla risorsa richiesta può essere utilizzata.  Una risorsa memorizzata nella cache è valida in uso non fa non viola i requisiti server specificati nella.  Criteri della cache basati sul percorso vengono creati a livello di codice utilizzando un costruttore di classe <xref:System.Net.Cache.HttpRequestCachePolicy> o <xref:System.Net.Cache.RequestCachePolicy>.  Il tipo di criteri basati sul percorso viene passato al costruttore con un valore di enumerazione <xref:System.Net.Cache.HttpRequestCacheLevel> o <xref:System.Net.Cache.RequestCacheLevel>.  Per esempi di codice che creano i criteri della cache basati sul percorso, vedere [Procedura: Impostare criteri della cache Basati sul percorso per un'applicazione](../../../docs/framework/network-programming/how-to-set-a-location-based-cache-policy-for-an-application.md).  Nelle sezioni seguenti viene illustrato ogni tipo di criteri della cache basati sul percorso per le risorse del protocollo HTTP \(HTTP o HTTPS\).  
  
## Se la cache criteri disponibili  
 Se una risorsa richiesta è valida nella cache locale, la risorsa memorizzata nella cache viene utilizzata; in caso contrario, la richiesta per la risorsa viene inviata al server.  Se la risorsa è disponibile in qualsiasi cache tra client e server, tale richiesta può essere soddisfatta dalla cache intermedio.  
  
## Criteri della cache solo  
 Se una risorsa richiesta è valida nella cache locale, la risorsa memorizzata nella cache viene utilizzata.  Quando il livello dei criteri della cache è specificato, viene generata un'eccezione <xref:System.Net.WebException> viene generata se l'elemento non è presente nella cache locale.  
  
## La cache o criteri seguenti della cache solo  
 Se una risorsa richiesta è valida nella cache locale o in una cache intermedio nella rete locale, la risorsa memorizzata nella cache viene utilizzata.  In caso contrario, viene generata un'eccezione <xref:System.Net.WebException>.  Il protocollo di memorizzazione nella cache HTTP, questo viene raggiunto utilizzando la direttiva soltanto\-se\- memorizzata nella cache di controllo della cache.  
  
## Nessun cache non criteri di archiviazione  
 Una risorsa richiesta non viene mai utilizzata da alcun cache e non viene mai alcun inserita nella cache.  Se una risorsa richiesta è presente nella cache locale, viene rimossa.  Questo livello di criteri indica alla cache intermedi che devono essere rimosse anche la risorsa.  Il protocollo di memorizzazione nella cache HTTP, questo viene raggiunto utilizzando la direttiva del controllo della cache no\-pia archivio.  
  
## Aggiornare i criteri  
 Una risorsa può essere utilizzata se viene ottenuta dal server o si trova in una cache diverse della cache locale.  Prima che la richiesta possa essere soddisfatta da una cache intermedia, è necessario che tale cache riconvalidi la voce nella cache con il server.  Il protocollo di memorizzazione nella cache HTTP, questo viene raggiunto utilizzando massimo\- età \= 0 direttive del controllo della cache e l'intestazione del pragma privi cache.  
  
## Criteri di ricaricamento  
 Le risorse richieste devono essere ottenute dal server.  La risposta potrebbe essere salvata nella cache locale.  Il protocollo di memorizzazione nella cache HTTP, questo viene raggiunto utilizzando la direttiva del controllo della cache di privi cache e l'intestazione del pragma privi cache.  
  
## Criteri di Riconvalidare  
 Confronta la copia della risorsa nella cache con la copia sul server.  Se la copia sul server è più recente, viene utilizzata per soddisfare la richiesta e sostituisce la copia nella cache.  Se la copia nella cache è identica alla copia del server, viene utilizzata la copia nella cache.  Nel protocollo della cache HTTP, questa operazione viene eseguita mediante una richiesta condizionale.  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Configurazione della memorizzazione nella cache per applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)   
 [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)