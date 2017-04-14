---
title: "Elemento &lt;webProxyScript&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#webProxyScript"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/webProxyScript"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<webProxyScript> (elemento)"
  - "webProxyScript (elemento)"
ms.assetid: a13c26db-6218-4af3-9696-38f24b23bfac
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Elemento &lt;webProxyScript&gt; (Impostazioni di rete)
Configura le caratteristiche dello script utilizzato per individuare i proxy Web.  
  
## Sintassi  
  
```  
  
      <webProxyScript  
  downloadTimeout="hh:mm:ss"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`downloadTimeout`|Specifica il tempo massimo di download dello script in ore, minuti e secondi.  Il valore predefinito è un minuto.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.|  
  
## Note  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Vedere anche  
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)