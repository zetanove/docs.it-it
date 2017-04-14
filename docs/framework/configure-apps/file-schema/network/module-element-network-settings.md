---
title: "Elemento &lt;module&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#module"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/module"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<module> (elemento)"
  - "module (elemento)"
ms.assetid: 10318725-9666-4d65-ab61-b94c64e59f13
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;module&gt; (Impostazioni di rete)
Consente di aggiungere un nuovo modulo proxy all'applicazione.  
  
## Sintassi  
  
```  
  
      <module   
   type = "name", System, Version="version number", Culture="culture", PublicKeyToken="token" "   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attribute**|**Descrizione**|  
|-------------------|---------------------|  
|`type`|Nome e dettagli del modulo che implementa il proxy.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|Configura il server proxy Hypertext Transfer Protocol \(HTTP\).|  
  
## Note  
 L'elemento `module` consente di registrare le classi proxy che implementano l'interfaccia <xref:System.Net.IWebProxy>.  Dopo la registrazione della classe proxy, `module` può essere utilizzato per richiedere informazioni mediante il proxy supportato.  
  
 Il valore dell'attributo `type` deve essere il nome di una libreria a collegamento dinamico \(DLL\) valida e il nome di classe del modulo.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene registrata una classe proxy personalizzata.  
  
```  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <module  
        type = "Test.CustomWebProxy, System, Version=2.0.3600.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.IWebProxy?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)