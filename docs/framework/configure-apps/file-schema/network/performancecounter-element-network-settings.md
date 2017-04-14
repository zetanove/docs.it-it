---
title: "Elemento &lt;performanceCounter&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<performanceCounter> (elemento)"
  - "performanceCounter (elemento)"
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;performanceCounter&gt; (Impostazioni di rete)
Abilita o disabilita i contatori delle prestazioni per le comunicazioni di rete.  
  
## Sintassi  
  
```  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Specifica se i contatori delle prestazioni per la comunicazione di rete sono abilitati.  Il valore predefinito è `false`.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.|  
  
## Note  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
 I contatori delle prestazioni per la comunicazione di rete devono essere abilitati nel file di configurazione da utilizzare.  Tutti i contatori delle prestazioni per le comunicazioni di rete sono abilitati o disabilitati con una sola impostazione nel file di configurazione.  Non è possibile abilitare o disabilitare singoli contatori delle prestazioni per le comunicazioni di rete.  Per ulteriori informazioni sui contatori delle prestazioni per le comunicazioni di rete specifici, vedere [Networking Performance Counters](http://msdn.microsoft.com/it-it/d1860235-f643-46ae-846c-ff0ed8b0e3cd).  
  
 Il valore predefinito è che i contatori delle prestazioni per la comunicazione di rete sono disabilitati.  
  
 La proprietà <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo **enabled** dai file di configurazione applicabili.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come configurare <xref:System.Net> e gli spazi dei nomi correlati per abilitare contatori delle prestazioni per la comunicazione di rete.  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=fullName>   
 <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [Networking Performance Counters](http://msdn.microsoft.com/it-it/d1860235-f643-46ae-846c-ff0ed8b0e3cd)