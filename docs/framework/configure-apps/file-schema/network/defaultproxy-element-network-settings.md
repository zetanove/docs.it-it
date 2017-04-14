---
title: "Elemento &lt;defaultProxy&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultProxy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<defaultProxy> (elemento)"
  - "defaultProxy (elemento)"
ms.assetid: 9d663c4b-07b4-4f6f-9b12-efbd3630354f
caps.latest.revision: 21
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 21
---
# Elemento &lt;defaultProxy&gt; (Impostazioni di rete)
Configura il server proxy Hypertext Transfer Protocol \(HTTP\).  
  
## Sintassi  
  
```  
  
        <defaultProxy  
  enabled="true|false"  
  useDefaultCredentials="true|false"  
  <bypasslist> … </bypasslist>  
  <proxy> … </proxy>  
  <module> … </module>  
/>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|`enabled`|Specifica se viene usato un proxy Web.  Il valore predefinito è `true`.|  
|`useDefaultCredentials`|Specifica se vengono usate le credenziali predefinite per questo host per accedere al proxy Web.  Il valore predefinito è `false`.|  
  
### Elementi figlio  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|Fornisce un set di espressioni regolari che descrivono gli indirizzi che non usano il proxy.|  
|[modulo](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md)|Aggiunge un nuovo modulo proxy all'applicazione.|  
|[proxy](../../../../../docs/framework/configure-apps/file-schema/network/proxy-element-network-settings.md)|Definisce un server proxy.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[system.  net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|Contiene le impostazioni di rete che specificano la modalità di connessione alla rete di .NET Framework.|  
  
## Note  
 Se l'elemento defaultProxy è vuoto, verranno usate le impostazioni proxy di Internet Explorer.  Questo comportamento è diverso da quello di .NET Framework versione 1.1.  
  
 Viene generata un'eccezione se l'elemento [module](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md) specifica un tipo non pubblico, il tipo non deriva dalla classe <xref:System.Net.IWebProxy>, si è verificata un'eccezione dal costruttore predefinito di questo oggetto o si è verificata un'eccezione durante il recupero del proxy predefinito specificato dal sistema.  La proprietà <xref:System.Exception.InnerException%2A> nell'eccezione dovrebbe contenere altre informazioni sulla causa principale dell'errore.  
  
## File di configurazione  
 Questo elemento può essere usato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 L'esempio di codice seguente usa le impostazioni predefinite del proxy di Internet Explorer, specifica l'indirizzo del proxy e ignora il proxy per l'accesso locale e contoso.com.  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
      <bypasslist  
        <add address="[a-z]+\.contoso\.com" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)