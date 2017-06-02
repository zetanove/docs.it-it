---
title: "Elemento &lt;add&gt; per bypasslist (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/add"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento), bypasslist"
  - "<bypasslist>, add (elemento)"
  - "add (elemento), bypasslist"
  - "bypasslist, add (elemento)"
ms.assetid: a0b86e28-86b4-4497-abe8-d5fd614c7926
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# Elemento &lt;add&gt; per bypasslist (Impostazioni di rete)
Consente di aggiungere un indirizzo IP o un nome DNS all'elenco di esclusione proxy.  
  
## Sintassi  
  
```  
  
      <add   
   address = "regular expression"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|**address**|Espressione regolare che descrive un indirizzo IP o un nome DNS.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|Fornisce un insieme di espressioni regolari che descrivono gli indirizzi che non utilizzano un proxy.|  
  
## Note  
 L'elemento `add` consente di inserire espressioni regolari che descrivono gli indirizzi IP o i nomi server DNS nell'elenco degli indirizzi per cui viene ignorato un server proxy.  
  
 Il valore dell'attributo `address` deve essere un'espressione regolare che descrive un insieme di indirizzi IP o di nomi host.  
  
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