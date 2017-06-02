---
title: "Elemento &lt;system.Net&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#system.Net"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.Net"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<system.Net> (elemento)"
  - "system.Net (elemento)"
ms.assetid: 52de4d6c-b24d-44aa-ba7d-6b5061f1357e
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;system.Net&gt; (Impostazioni di rete)
Contiene le impostazioni che indicano il modo in cui .NET Framework si connette alla rete.  
  
## Sintassi  
  
```  
  
      <system.net>   
</system.net>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[authenticationModules](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|Consente di specificare i moduli utilizzati per autenticare le richieste Internet.|  
|[connectionManagement](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|Consente di specificare il numero massimo di connessioni a un host Internet.|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|Configura il server proxy Hypertext Transfer Protocol \(HTTP\).|  
|[mailSettings](../../../../../docs/framework/configure-apps/file-schema/network/mailsettings-element-network-settings.md)|Configura le opzioni di invio della posta elettronica per il protocollo SMTP \(Simple Mail Transport Protocol\).|  
|[requestCaching](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|Controlla il meccanismo di memorizzazione nella cache per le richieste di rete.|  
|[impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura le opzioni di rete di base per le classi in <xref:System.Net> e negli spazi dei nomi figlio correlati.|  
|[Elemento \<webRequestModules\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|Consente di specificare i moduli da utilizzare per richiedere informazioni dagli host Internet.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[configurazione](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Contiene impostazioni per tutti gli spazi dei nomi.|  
  
## Note  
 L'elemento [\<system.net\>](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md) contiene impostazioni per le classi nell'oggetto <xref:System.Net> e negli spazi dei nomi figlio correlati.  Tali impostazioni consentono di configurare i moduli di autenticazione, la gestione delle connessioni, le impostazioni di posta elettronica, il server proxy e i moduli di richiesta Internet per la ricezione delle informazioni dagli host Internet.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrata una configurazione tipica utilizzata con le classi <xref:System.Net>.  
  
```  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <add type = "System.Net.DigestClient" />  
      <add type = "System.Net.NegotiateClient" />  
      <add type = "System.Net.KerberosClient" />  
      <add type = "System.Net.NtlmClient" />  
      <add type = "System.Net.BasicClient" />  
    </authenticationModules>  
    <connectionManagement>  
      <add address = "*" maxconnection = "2" />  
    </connectionManagement>  
    <defaultProxy>  
      <proxy  
        usesystemdefault = "true"  
        bypassonlocal = "true"  
      />  
    </defaultProxy>  
    <webRequestModules>  
      <add prefix = "http"  
        type = "System.Net.HttpRequestCreator"  
      />  
      <add prefix = "https"  
        type = "System.Net.HttpRequestCreator"  
      />  
      <add prefix = "file"  
        type = "System.Net.FileWebRequestCreator"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)