---
title: "Elemento &lt;add&gt; per webRequestModules (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/add"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento), webRequestModules"
  - "<webRequestModules>, add (elemento)"
  - "add (elemento), webRequestModules"
  - "webRequestModules, add (elemento)"
ms.assetid: 47ec4adc-f39f-4bcd-8680-1ec21fd26890
caps.latest.revision: 16
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 16
---
# Elemento &lt;add&gt; per webRequestModules (Impostazioni di rete)
Consente di aggiungere un modulo di richiesta Web personalizzato all'applicazione.  
  
## Sintassi  
  
```  
  
      <add   
  prefix = "URI prefix"   
  type = "module name, Version, Culture, PublicKeyToken"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`prefix`|Prefisso URI per le richieste gestite da questo modulo di richiesta Web.|  
|`type`|Nome di classe e assembly del modulo che implementa questo modulo di richiesta Web.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|Selezione dei moduli da utilizzare per richiedere informazioni agli host di rete.|  
  
## Note  
 L'attributo `prefix` definisce il prefisso URI che utilizza il modulo di richiesta Web specificato.  I moduli di richiesta Web vengono registrati, in genere, per gestire un protocollo specifico, come HTTP o FTP, ma è possibile registrarli per gestire una richiesta inviata a un server o a un percorso su un server specifico.  
  
 Il modulo di richiesta Web viene creato quando al metodo <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName> viene passato un prefisso corrispondente a un URI.  
  
 Il valore dell'attributo `prefix` deve corrispondere ai caratteri iniziali di un URI valido, ad esempio "http" o "http:\/\/www.contoso.com".  
  
 Il valore dell'attributo `type` deve essere costituito da un nome DLL valido e un nome di classe corrispondente, separati da una virgola.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene registrato un modulo di richiesta Web per HTTP personalizzato.  È necessario sostituire i valori di Version e PublicKeyToken con i valori corretti per il modulo specificato.  
  
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
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)