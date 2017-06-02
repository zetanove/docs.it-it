---
title: "Elemento &lt;defaultFtpCachePolicy&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultFtpCachePolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching/defaultFtpCachePolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<defaultFtpCachePolicy> (elemento)"
  - "defaultFtpCachePolicy (elemento)"
ms.assetid: 0eb0c5cb-dd97-484d-8614-785e88877abb
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;defaultFtpCachePolicy&gt; (Impostazioni di rete)
Indica se la memorizzazione nella cache FTP è attiva e ne descrive i criteri predefiniti.  
  
## Sintassi  
  
```  
< defaultFtpCachePolicy  
  policyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`policyLevel`|Specifica i criteri di memorizzazione nella cache FTP.  Il valore predefinito è `Default`.|  
  
## Attributo policyLevel  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`Default`|Restituisce la risorsa memorizzata nella cache se la risorsa è nuova, la lunghezza del contenuto è precisa e sono presenti gli attributi di scadenza, modifica e lunghezza del contenuto.|  
|`BypassCache`|Restituisce la risorsa dal server.|  
|`CacheOnly`|Restituisce la risorsa memorizzata nella cache se la lunghezza del contenuto è specificata e corrisponde alla dimensione dell'elemento.|  
|`CacheIfAvailable`|Restituisce la risorsa memorizzata nella cache se la lunghezza del contenuto è presente e corrisponde alle dimensioni della voce; in caso contrario la risorsa viene scaricata dal server e restituita al chiamante.|  
|`Revalidate`|Restituisce la risorsa memorizzata nella cache se il relativo timestamp è identico al timestamp della risorsa sul server. In caso contrario, la risorsa viene scaricata dal server, memorizzata nella cache e restituita al chiamante.|  
|`Reload`|Scarica la risorsa dal server, la memorizza nella cache e la restituisce al chiamante.|  
|`NoCacheNoStore`|Se esiste una risorsa memorizzata nella cache, viene cancellata.  La risorsa viene scaricata dal server e restituita al chiamante.|  
|`Revalidate`|Soddisfa una richiesta utilizzando la copia memorizzata nella cache della risorsa se il timestamp è identico a quello della risorsa sul server. In caso contrario, la risorsa viene scaricata dal server, presentata al chiamante e memorizzata nella cache.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[requestCaching](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|Controlla il meccanismo di memorizzazione nella cache per le richieste di rete.|  
  
## Note  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come specificare dei criteri di memorizzazione nella cache FTP di `NoCacheNoStore`.  
  
```  
<configuration>  
  <system.net>  
    <requestCaching>  
      <defaultFtpCachePolicy  
        Level="NoCacheNoStore">  
      </defaultFtpCachePolicy>  
    </requestCaching>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Cache>   
 <xref:System.Net.WebRequest>   
 <xref:System.Net.Cache.RequestCacheLevel>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)