---
title: "Elemento &lt;webRequestModules&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#webRequestModules"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<webRequestModules> (elemento)"
  - "webRequestModules (elemento)"
ms.assetid: 1263de11-3e0a-4f94-97c9-710b2ae53817
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;webRequestModules&gt; (Impostazioni di rete)
Selezione dei moduli da utilizzare per richiedere informazioni agli host di rete.  
  
## Sintassi  
  
```  
  
      <webRequestModules>   
</webRequestModules>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[aggiunta](../../../../../docs/framework/configure-apps/file-schema/network/add-element-for-webrequestmodules-network-settings.md)|Consente di aggiungere un modulo di richiesta Web personalizzato all'applicazione.|  
|[clear](../../../../../docs/framework/configure-apps/file-schema/network/clear-element-for-webrequestmodules-network-settings.md)|Rimuove dall'applicazione tutti i moduli di richiesta Web registrati.|  
|[remove](../../../../../docs/framework/configure-apps/file-schema/network/remove-element-for-webrequestmodules-network-settings.md)|Consente di rimuovere un modulo di richiesta Web personalizzato dall'applicazione.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[system.net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|Contiene le impostazioni che indicano il modo in cui .NET Framework si connette alla rete.|  
  
## Note  
 L'elemento `webRequestModules` consente di registrare i discendenti della classe <xref:System.Net.WebRequest> per gestire le richieste di informazioni inviate agli host di rete.  I moduli di richiesta Web devono implementare l'interfaccia <xref:System.Net.IWebRequestCreate>.  
  
 .NET Framework include i moduli di richiesta Web per gli URI che iniziano con http:\/\/, https:\/\/ e file:\/\/.  Per eseguire l'override dei moduli predefiniti occorre registrare un modulo personalizzato nel file di configurazione.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene registrato il modulo HTTP predefinito.  È necessario sostituire i valori di Version e PublicKeyToken con i valori corretti per il modulo specificato.  
  
```  
<configuration>  
  <system.net>  
    <webRequestModules>  
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
 <xref:System.Net.IWebRequestCreate>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)