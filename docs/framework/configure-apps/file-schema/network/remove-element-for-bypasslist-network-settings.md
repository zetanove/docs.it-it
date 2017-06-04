---
title: "Elemento &lt;remove&gt; per bypasslist (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bypasslist>, remove (elemento)"
  - "bypasslist, remove (elemento)"
  - "remove (elemento), bypasslist"
  - "remove (elemento), bypasslist"
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
caps.latest.revision: 16
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 16
---
# Elemento &lt;remove&gt; per bypasslist (Impostazioni di rete)
Consente di rimuovere un indirizzo IP o un nome DNS dall'elenco di esclusione proxy.  
  
## Sintassi  
  
```  
  
      <remove   
   name = "regular expression"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`name`|Espressione regolare che descrive un indirizzo IP o un nome DNS.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|Fornisce un insieme di espressioni regolari che descrivono gli indirizzi che non utilizzano un proxy.|  
  
## Note  
 L'elemento `remove` rimuove espressioni regolari che descrivono indirizzi IP o nomi server DNS dall'elenco di indirizzi che ignorano un server proxy.  Gli indirizzi sono stati definiti in precedenza nel file di configurazione o a un livello superiore nella gerarchia di configurazione.  
  
 Il valore dell'attributo `name` deve essere un'espressione regolare che descrive un insieme di indirizzi IP o nomi host.  
  
 Per ulteriori informazioni sulle espressioni regolari, vedere [Espressioni regolari di .NET Framework](../../../../../docs/standard/base-types/regular-expressions.md).  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene rimossa qualsiasi precedente definizione del dominio adventure\-works.com e viene aggiunto il dominio contoso.com all'elenco di esclusione.  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
        <remove name = "[a-z]+\.adventure-works\.com$" />  
        <add address="[a-z]+\.contoso\.com$" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)