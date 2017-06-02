---
title: "Elemento &lt;remove&gt; per connectionManagement (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/remove"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<connectionManagement>, remove (elemento)"
  - "<remove> (elemento), connectionManagement"
  - "connectionManagement, remove (elemento)"
  - "remove (elemento), connectionManagement"
ms.assetid: 94b81775-5a22-4975-8c47-8620c40c3f35
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Elemento &lt;remove&gt; per connectionManagement (Impostazioni di rete)
Consente di rimuovere un indirizzo IP o un nome DNS dall'elenco di gestione delle connessioni.  
  
## Sintassi  
  
```  
  
      <remove   
   name = "server name or IP address"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`address`|Indirizzo IP o nome DNS.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[connectionManagement](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|Specifica il numero massimo di connessioni a un host di rete.|  
  
## Note  
 L'elemento `remove` rimuove la voce dell'elenco di gestione delle connessioni relativa al server specificato.  
  
 Il valore dell'attributo `address` deve essere un indirizzo IP o un nome host valido.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono rimosse tutte le voci dell'elenco di gestione delle connessioni relative al server www.adventure\-works.com e viene configurata un'applicazione per l'utilizzo di quattro connessioni al server www.contoso.com e due connessioni a tutti gli altri server.  
  
```  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <remove address = "http://www.adventure-works.com"/>  
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