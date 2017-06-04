---
title: "Elemento &lt;defaultHttpCachePolicy&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching/defaultHttpCachePolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultHttpCachePolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<defaultHttpCachePolicy> (elemento)"
  - "defaultHttpCachePolicy (elemento)"
ms.assetid: 2c1247d0-39b0-4c12-919a-a925ce075c79
caps.latest.revision: 19
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 19
---
# Elemento &lt;defaultHttpCachePolicy&gt; (Impostazioni di rete)
Indica se la memorizzazione nella cache HTTP è attiva e ne descrive i criteri predefiniti.  
  
## Sintassi  
  
```  
< defaultHttpCachePolicy  
  policyLevel="BypassCache|Default"  
  minimumFresh="d.hh:mm:ss"|"minValue"  
  maximumAge  ="d.hh:mm:ss"|"maxValue"  
  maximumStale="d.hh:mm:ss"|"maxValue"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`maximumAge`|Specifica l'intervallo di tempo massimo prima che un oggetto memorizzato nella cache venga contrassegnato come scaduto.|  
|`maximumStale`|Specifica l'intervallo di tempo massimo successivo al periodo calcolato per lo stato di aggiornamento prima che un oggetto memorizzato nella cache venga contrassegnato come scaduto.|  
|`minimumFresh`|Specifica l'intervallo di tempo minimo durante il quale considerare aggiornato un oggetto memorizzato nella cache.|  
|`policyLevel`|Specifica se i criteri di memorizzazione nella cache sono automatici o se la cache viene ignorata.  Il valore predefinito è `BypassCache`.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[requestCaching](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|Controlla il meccanismo di memorizzazione nella cache per le richieste di rete.|  
  
## Note  
 Il valore per l'attributo `policyLevel` è `BypassCache` o `Default`.  
  
 I valori per gli elementi `maximumAge`, `maximumStale` e `minimumFresh` sono rappresentati da un intervallo di tempo esplicito con il formato *d*.*hh*:*mm*:*ss* \(giorni, ore, minuti e secondi\) o dalle costanti `minValue` o `maxValue`, a seconda dei casi.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come specificare un intervallo minimo di sei ore per lo stato aggiornato, un intervallo di durata massima di due giorni e un intervallo di obsolescenza massima di quattro ore.  
  
```  
<configuration>  
  <system.net>  
    <requestCaching>  
      <defaultHttpCachePolicy>  
        <set minimumFresh="0.06:00:00" />  
        <set maximumAge  ="2.00:00:00" />  
        <set maximumStale="0.04:00:00" />  
      </defaultHttpCachePolicy>  
    </requestCaching>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Cache>   
 <xref:System.Net.WebRequest>   
 <xref:System.Net.Cache.RequestCacheLevel>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)