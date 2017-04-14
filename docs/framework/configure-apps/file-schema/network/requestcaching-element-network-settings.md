---
title: "Elemento &lt;requestCaching&gt; (Impostazioni di rete) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#requestCaching"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<requestCaching> (elemento)"
  - "requestCaching (elemento)"
ms.assetid: 9962a2fe-cbda-41a6-9377-571811eaea84
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# Elemento &lt;requestCaching&gt; (Impostazioni di rete)
Controlla il meccanismo di memorizzazione nella cache per le richieste di rete.  
  
## Sintassi  
  
```  
  
      <requestCaching  
  isPrivateCache ="true|false"  
  disableAllCaching="true|false"  
  defaultPolicyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
  unspecifiedMaximumAge= "d.hh.mm.ss""  
  <defaultHttpCachePolicy> … </defaultHttpCachePolicy>  
  <defaultFtpCachePolicy> … </defaultFtpCachePolicy>  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`isPrivateCache`|Specifica se la cache offre isolamento tra le informazioni di utenti diversi.  Il valore predefinito è `true`.  Tale valore dovrebbe essere `false` per le applicazioni di livello intermedio.|  
|`disableAllCaching`|Specifica che la memorizzazione nella cache è disabilitata per tutte le risposte Web e non può essere sottoposta a override a livello di codice.|  
|`defaultPolicyLevel`|Uno dei valori dell'enumerazione <xref:System.Net.Cache.RequestCacheLevel>.  Il valore predefinito è `BypassCache`.|  
|`unspecifiedMaximumAge`|Specifica il periodo di tempo predefinito trascorso il quale il contenuto viene contrassegnato come scaduto.|  
  
## Attributo policyLevel  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`Default`|Restituisce la risorsa memorizzata nella cache se la risorsa è nuova, la lunghezza del contenuto è precisa e sono presenti gli attributi di scadenza, modifica e lunghezza del contenuto.|  
|`BypassCache`|Restituisce la risorsa dal server.|  
|`CacheOnly`|Restituisce la risorsa memorizzata nella cache se la lunghezza del contenuto è specificata e corrisponde alla dimensione dell'elemento.|  
|`CacheIfAvailable`|Restituisce la risorsa memorizzata nella cache se la lunghezza del contenuto è presente e corrisponde alle dimensioni della voce; in caso contrario la risorsa viene scaricata dal server e restituita al chiamante.|  
|`Revalidate`|Restituisce la risorsa memorizzata nella cache se il relativo time stamp è identico al time stamp della risorsa sul server. In caso contrario, la risorsa viene scaricata dal server, memorizzata nella cache e restituita al chiamante.|  
|`Reload`|Scarica la risorsa dal server, la memorizza nella cache e la restituisce al chiamante.|  
|`NoCacheNoStore`|Se esiste una risorsa memorizzata nella cache, viene cancellata.  La risorsa viene scaricata dal server e restituita al chiamante.|  
|`Revalidate`|Soddisfa una richiesta utilizzando la copia memorizzata nella cache della risorsa se il time stamp è identico a quello della risorsa sul server. In caso contrario, la risorsa viene scaricata dal server, presentata al chiamante e memorizzata nella cache.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[defaultHttpCachePolicy](../../../../../docs/framework/configure-apps/file-schema/network/defaulthttpcachepolicy-element-network-settings.md)|Elemento facoltativo.<br /><br /> Indica se la memorizzazione nella cache HTTP è attiva e ne descrive i criteri predefiniti.|  
|[Elemento \<defaultFtpCachePolicy\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/defaultftpcachepolicy-element-network-settings.md)|Elemento facoltativo.<br /><br /> Indica se la memorizzazione nella cache FTP è attiva e ne descrive i criteri predefiniti.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[system.net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|Contiene le impostazioni che indicano il modo in cui .NET Framework si connette alla rete.|  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come disabilitare la cache.  
  
```  
<configuration>  
  <system.net>  
    <requestCaching  
      disableAllCaching="true"  
    />  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Cache?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)