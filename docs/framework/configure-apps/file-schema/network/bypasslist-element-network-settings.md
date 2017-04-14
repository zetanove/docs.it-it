---
title: "Elemento &lt;bypasslist&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#bypasslist"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bypasslist> (elemento)"
  - "bypasslist (elemento)"
ms.assetid: 124446b7-abb1-4e5e-a492-b64398f268f1
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# Elemento &lt;bypasslist&gt; (Impostazioni di rete)
Fornisce un insieme di espressioni regolari che descrivono gli indirizzi che non utilizzano un proxy.  
  
## Sintassi  
  
```  
  
      <bypasslist>   
</bypasslist>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[aggiunta](../../../../../docs/framework/configure-apps/file-schema/network/add-element-for-bypasslist-network-settings.md)|Consente di aggiungere un indirizzo IP o un nome DNS all'elenco di esclusione proxy.|  
|[clear](../../../../../docs/framework/configure-apps/file-schema/network/clear-element-for-bypasslist-network-settings.md)|Consente di cancellare l'elenco di esclusione.|  
|[remove](../../../../../docs/framework/configure-apps/file-schema/network/remove-element-for-bypasslist-network-settings.md)|Consente di rimuovere un indirizzo IP o un nome DNS dall'elenco di esclusione proxy.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|Configura il server proxy Hypertext Transfer Protocol \(HTTP\).|  
  
## Note  
 L'elenco di esclusione contiene le espressioni regolari che descrivono gli URI a cui le istanze <xref:System.Net.WebRequest> possono accedere direttamente invece di utilizzare il server proxy.  
  
 È necessario prestare attenzione quando si specifica un'espressione regolare per questo elemento.  L'espressione regolare "\[a\-z\]\+\\.contoso\\.com" corrisponde a qualsiasi host nel dominio contoso.com, ma anche a qualsiasi host nel dominio contoso.com.cpandl.com.  Per creare una corrispondenza univoca con un host nel dominio contoso.com, utilizzare un ancoraggio \("$"\): "\[a\-z\]\+\\.contoso\\.com$".  
  
 Per ulteriori informazioni sulle espressioni regolari, vedere [Espressioni regolari di .NET Framework](../../../../../docs/standard/base-types/regular-expressions.md).  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nel codice di esempio riportato di seguito vengono aggiunti due indirizzi all'elenco di esclusione.  Il primo consente di ignorare il proxy per tutti i server del dominio contoso.com, il secondo, invece, di ignorare il proxy per tutti i server i cui indirizzi IP iniziano con 192.168.  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
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