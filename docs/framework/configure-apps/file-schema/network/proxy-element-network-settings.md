---
title: "Elemento &lt;proxy&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/proxy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#proxy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<proxy> (elemento)"
  - "proxy (elemento)"
ms.assetid: 37a548d8-fade-4ac5-82ec-b49b6c6cb22a
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# Elemento &lt;proxy&gt; (Impostazioni di rete)
Consente di definire un server proxy.  
  
## Sintassi  
  
```  
  
      <proxy   
  autoDetect="true|false|unspecified"    
  bypassonlocal="true|false|unspecified"   
  proxyaddress="uriString"  
  scriptLocation="uriString"   
  usesystemdefault="true|false|unspecified "   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`autoDetect`|Specifica se il proxy viene rilevato automaticamente.  Il valore predefinito è `unspecified`.|  
|`bypassonlocal`|Specifica se il proxy viene ignorato per le risorse locali.  Le risorse locali includono il server locale \(http:\/\/hostlocale, http:\/\/loopback o http:\/\/127.0.0.1\) e un URI senza punto \(http:\/\/serverweb\).  Il valore predefinito è `unspecified`.|  
|`proxyaddress`|Specifica l'URI del proxy da utilizzare.|  
|`scriptLocation`|Specifica il percorso dello script di configurazione.|  
|`usesystemdefault`|Specifica se utilizzare le impostazioni proxy di Internet Explorer.  Se impostato su `true`, gli attributi successivi eseguiranno l'override delle impostazioni proxy di Internet Explorer.  Il valore predefinito è `unspecified`.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|Configura il server proxy Hypertext Transfer Protocol \(HTTP\).|  
  
## Valore di testo  
  
## Note  
 L'elemento `proxy` consente di definire un server proxy per un'applicazione.  Se questo elemento non è incluso nel file di configurazione, .NET Framework utilizzerà le impostazioni proxy di Internet Explorer.  
  
 Il valore dell'attributo `proxyaddress` deve essere un URI \(Uniform Resource Indicator\) ben formato.  
  
 L'attributo `scriptLocation` si riferisce al rilevamento automatico degli script di configurazione del proxy.  La classe <xref:System.Net.WebProxy> tenterà di individuare uno script di configurazione, generalmente denominato Wpad.dat, quando viene selezionata l'opzione **Utilizza script di configurazione automatica** di Internet Explorer.  
  
 Utilizzare l'attributo `usesystemdefault` per le applicazioni .NET Framework versione 1.1 che eseguono la migrazione alla versione 2.0.  
  
 Viene generata un'eccezione se l'attributo `proxyaddress` specifica un proxy predefinito non valido.  La proprietà <xref:System.Exception.InnerException%2A> sull'eccezione deve disporre di maggiori informazioni sulla causa principale dell'errore.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono utilizzate le impostazioni predefinite del proxy di Internet Explorer, viene specificato l'indirizzo del proxy e viene ignorato il proxy per l'accesso locale.  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.WebProxy?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)