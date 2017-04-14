---
title: "Elemento &lt;add&gt; per connectionManagement (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento), connectionManagement"
  - "<connectionManagement>, add (elemento)"
  - "add (elemento), connectionManagement"
  - "connectionManagement, add (elemento)"
ms.assetid: 856bf57d-1c63-46c7-a178-03d97b0a4149
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;add&gt; per connectionManagement (Impostazioni di rete)
Aggiunge un indirizzo IP o nome DNS all'elenco di gestione delle connessioni.  
  
## Sintassi  
  
```  
  
        <add   
   address = "address expression"   
   maxconnection = integer   
/>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`address`|Stringa che descrive un indirizzo IP o un nome DNS.|  
|`maxconnection`|Numero massimo di connessioni consentite verso un server.  Se non impostato, il valore predefinito è 2.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[connectionManagement](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|Specifica il numero massimo di connessioni a un host di rete.|  
  
## Note  
 Il valore dell'attributo `address` deve essere un'espressione regolare valida o un asterisco per indicare tutte le connessioni oppure una stringa nel formato `<schema>://<idn_hostname>[:<port>]`.  
  
 Se l'URI passato a qualsiasi API HTTP contiene Unicode, il nome verrà convertito internamente usando <xref:System.Uri.DnsSafeHost%2A>, il che potrebbe restituire una stringa Unicode \(il comportamento dipende dalla configurazione IDN corrente\).  
  
## File di configurazione  
 Questo elemento può essere usato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice seguente un'applicazione viene configurata per l'uso di quattro connessioni al server www.contoso.com e due connessioni a tutti gli altri server.  
  
```  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address = "http://www.contoso.com" maxconnection = "4" />  
      <add address = "*" maxconnection = "2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.ServicePoint>   
 <xref:System.Net.ServicePointManager>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)