---
title: "Elemento &lt;add&gt; per authenticationModules (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#add"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/authenticationModules/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento), authenticationModules"
  - "<authenticationModules>, add (elemento)"
  - "add (elemento), authenticationModules"
  - "authenticationModules, add (elemento)"
ms.assetid: 333c5fb0-a2ab-4db8-8531-a7fe37bb9b5b
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# Elemento &lt;add&gt; per authenticationModules (Impostazioni di rete)
Consente di aggiungere un modulo di autenticazione all'applicazione.  
  
## Sintassi  
  
```  
  
      <add   
   type = "client type", System, Version="version number", Culture="culture", PublicKeyToken="token"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attribute**|**Descrizione**|  
|-------------------|---------------------|  
|`type`|Nome di classe e dettagli del modulo che implementa l'autenticazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[authenticationModules](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|Specifica i moduli utilizzati per autenticare le richieste di rete.|  
  
## Note  
 L'elemento `add` aggiunge un modulo di autenticazione alla fine dell'elenco dei moduli di autenticazione registrati.  I moduli di autenticazione vengono richiamati nell'ordine in cui sono stati aggiunti all'elenco.  
  
 Il valore dell'attributo `type` deve essere costituito da un nome DLL valido e un nome di classe corrispondente, separati da una virgola.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono attivati i moduli di autenticazione predefiniti.  È necessario sostituire i valori di Version e PublicKeyToken con i valori corretti per il modulo specificato.  
  
```  
<configuration>  
  <system.net>  
        <authenticationModules>  
            <add type="System.Net.DigestClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.NegotiateClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.KerberosClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.NtlmClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
            <add type="System.Net.BasicClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
        </authenticationModules>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.IAuthenticationModule>   
 <xref:System.Net.AuthenticationManager>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)