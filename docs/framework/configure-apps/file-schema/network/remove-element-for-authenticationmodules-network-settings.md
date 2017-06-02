---
title: "Elemento &lt;remove&gt; per authenticationModules (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/authenticationModules/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<authenticationModules>, remove (elemento)"
  - "<remove> (elemento), authenticationModules"
  - "authenticationModules, remove (elemento)"
  - "remove (elemento), authenticationModules"
ms.assetid: abf79949-b05c-465a-b51c-bbeda9a74173
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;remove&gt; per authenticationModules (Impostazioni di rete)
Consente di rimuovere un modulo di autenticazione dall'applicazione.  
  
## Sintassi  
  
```  
  
      <remove   
   name = "authentication module name"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attribute**|**Descrizione**|  
|-------------------|---------------------|  
|**name**|Nome del modulo di autenticazione da rimuovere.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[authenticationModules](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|Specifica i moduli utilizzati per autenticare le richieste di rete.|  
  
## Note  
 L'elemento `remove` consente di rimuovere i moduli di autenticazione precedentemente definiti nel file di configurazione o, ad un livello più alto, nella gerarchia di configurazione.  
  
 Il valore per l'attributo `name` deve essere un nome di classe valido.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene rimosso un modulo di autenticazione.  
  
```  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <remove name = "System.Net.NtlmClient" />  
    </authenticationModules>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.IAuthenticationModule>   
 <xref:System.Net.AuthenticationManager>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)