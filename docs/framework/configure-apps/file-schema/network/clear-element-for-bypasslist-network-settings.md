---
title: "Elemento &lt;clear&gt; per bypasslist (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/clear"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bypasslist>, clear (elemento)"
  - "<clear> (elemento), bypasslist"
  - "bypasslist, clear (elemento)"
  - "clear (elemento), bypasslist"
ms.assetid: 301584ca-a914-4100-b180-3b288d3b099e
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;clear&gt; per bypasslist (Impostazioni di rete)
Consente di cancellare l'elenco di esclusione proxy.  
  
## Sintassi  
  
```  
  
<clear/>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|Fornisce un insieme di espressioni regolari che descrivono gli indirizzi che non utilizzano un proxy.|  
  
## Note  
 L'elemento `clear` cancella tutte le voci dell'elenco di esclusione.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene cancellato il contenuto dell'elenco di esclusione, a cui vengono quindi aggiunti due indirizzi.  Il primo consente di ignorare il proxy per tutti i server del dominio contoso.com, il secondo, invece, di ignorare il proxy per tutti i server i cui indirizzi IP iniziano con 192.168.  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
         <clear/>  
        <add address="[a-z]+\.contoso\.com$" />  
        <add address="192\.168\.\d{1,3}\.\d{1,3}" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>   
```  
  
## Vedere anche  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)