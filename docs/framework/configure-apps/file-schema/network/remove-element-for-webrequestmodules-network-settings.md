---
title: "Elemento &lt;remove&gt; per webRequestModules (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<remove> (elemento), webRequestModules"
  - "<webRequestModules>, remove (elemento)"
  - "remove (elemento), webRequestModules"
  - "webRequestModules, remove (elemento)"
ms.assetid: dd84d2fe-2f4f-457a-9d3c-441d0d21cc10
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;remove&gt; per webRequestModules (Impostazioni di rete)
Consente di rimuovere un modulo di richiesta Web personalizzato dall'applicazione.  
  
## Sintassi  
  
```  
  
      <remove   
  name = "URI prefix"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`name`|Prefisso URI per le richieste gestite da questo modulo di richiesta Web.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|Selezione dei moduli da utilizzare per richiedere informazioni agli host di rete.|  
  
## Note  
 L'elemento `remove` rimuove il modulo di richiesta Web registrato per il prefisso URI specificato.  
  
 Il valore dell'attributo `prefix` deve corrispondere ai caratteri iniziali di un URI valido, ad esempio "http" o "http:\/\/www.contoso.com".  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene rimosso il modulo di richiesta Web per HTTP esistente e viene registrato un nuovo modulo di richiesta Web personalizzato per le richieste HTTP destinate a www.contoso.com.  
  
```  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <remove prefix = "http">  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.WebRequest>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)