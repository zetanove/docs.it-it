---
title: "Criteri di cache | Microsoft Docs"
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
  - "criteri di cache basati sulla posizione"
  - "cache [.NET Framework], criteri"
  - "criteri di cache per le richieste"
  - "validità minima delle risorse memorizzate nella cache"
  - "criteri di cache per il contenuto"
  - "contenuto scaduto"
ms.assetid: 1a7e04ec-7872-41c2-96c6-52566dcb412b
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Criteri di cache
Nei criteri della cache sono definite le regole utilizzate per determinare se è possibile soddisfare una richiesta utilizzando una copia della risorsa richiesta memorizzata nella cache.   Le applicazioni specificano i requisiti client della cache di dati, ma i criteri della cache sono determinate dai requisiti client della cache, requisiti del contenuto della scadenza del server e dai requisiti della riconvalida del server.  L'interazione di criteri della cache client e i requisiti server comporta sempre i criteri della cache più conservativi, per assicurarsi che il contenuto più nuovo viene restituito all'applicazione client.  
  
 I criteri della cache sono basati sul percorso o temporizzati.  Criteri della cache basati sul percorso definiscono la validità delle voci memorizzate nella cache in base alla risorsa richiesta può essere utilizzata.  Criteri della cache basati sull'ora definiscono la validità delle voci memorizzate nella cache utilizzando il tempo che la risorsa è stata recuperata, le intestazioni restituite dalla risorsa e l'ora corrente.  La maggior parte delle applicazioni possono utilizzare i criteri della cache basati sull'ora predefiniti, che implementano i criteri di cache definiti nello standard RFC 2616, disponibili in [http:\/\/www.ietf.org](http://www.ietf.org/).  
  
 Le classi riportate nella tabella seguente vengono utilizzate per specificare i criteri della cache.  
  
|Nome di classe|Descrizione|  
|--------------------|-----------------|  
|<xref:System.Net.Cache.HttpRequestCachePolicy>|Rappresenta basato su posizione e criteri della cache basati sull'ora delle risorse richieste utilizzando oggetti <xref:System.Net.HttpWebRequest>.|  
|<xref:System.Net.Cache.RequestCachePolicy>|Rappresenta i criteri della cache basati sul percorso o criteri della cache basati sull'ora <xref:System.Net.Cache.RequestCacheLevel> per le risorse richieste utilizzando <xref:System.Net.WebRequest> oggetto.|  
|<xref:System.Net.Cache.HttpCacheAgeControl>|Specifica i valori utilizzati per creare gli oggetti temporizzati <xref:System.Net.Cache.HttpRequestCachePolicy>.|  
|<xref:System.Net.Cache.HttpRequestCacheLevel>|Specifica i valori utilizzati per creare gli oggetti basati sul percorso e temporizzati <xref:System.Net.Cache.HttpRequestCachePolicy>.|  
|<xref:System.Net.Cache.RequestCacheLevel>|Specifica i valori utilizzati per creare in base al percorso o oggetti temporizzati <xref:System.Net.Cache.RequestCacheLevel><xref:System.Net.Cache.RequestCachePolicy>.|  
  
 È possibile definire i criteri della cache per tutte le richieste effettuate dall'applicazione o alle singole richieste.  Quando si specifica i criteri della cache a livello di applicazione che i criteri della cache a livello di richiesta, i criteri a livello di richiesta utilizzati.  È possibile specificare i criteri della cache a livello di applicazione a livello di codice oppure mediante l'applicazione o i file di configurazione del computer.  Per ulteriori informazioni, vedere [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md).  
  
 Per creare criteri della cache, è necessario creare un oggetto di criteri creando un'istanza della classe <xref:System.Net.Cache.HttpRequestCachePolicy> o <xref:System.Net.Cache.RequestCachePolicy>.  Per specificare i criteri in una richiesta, impostare la proprietà <xref:System.Net.WebRequest.CachePolicy%2A> la richiesta all'oggetto di criteri.  Nell'impostare i criteri a livello di applicazione a livello di codice, impostare la proprietà <xref:System.Net.HttpWebRequest.DefaultCachePolicy%2A> all'oggetto di criteri.  
  
 Per gli esempi di codice che illustrano la creazione e l'utilizzo dei criteri della cache, vedere [Configurazione che memorizza nella cache nelle applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md).  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Configurazione della memorizzazione nella cache per applicazioni di rete](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)