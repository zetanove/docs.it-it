---
title: "Elemento &lt;alwaysFlowImpersonationPolicy&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/alwaysFlowImpersonationPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#alwaysFlowImpersonationPolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<alwaysFlowImpersonationPolicy> (elemento)"
  - "alwaysFlowImpersonationPolicy (elemento)"
ms.assetid: ee622801-9e46-470b-85ab-88c4b1dd2ee1
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;alwaysFlowImpersonationPolicy&gt;
Specifica che il flusso dell'identità Windows passa sempre attraverso punti asincroni, indipendentemente dal modo in cui è stata ottenuta la rappresentazione.  
  
## Sintassi  
  
```  
<alwaysFlowImpersonationPolicy    
  enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Indica se il flusso dell'identità Windows passa attraverso punti asincroni.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il flusso dell'identità Windows non passa attraverso punti asincroni, a meno che la rappresentazione non sia stata ottenuta tramite metodi gestiti quali <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A>.  Questa è l'impostazione predefinita.|  
|`true`|Il flusso dell'identità Windows passa sempre attraverso punti asincroni, indipendentemente dal modo in cui è stata ottenuta la rappresentazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 In .NET Framework versione 1.0 e 1.1 il flusso dell'identità Windows non passa attraverso punti asincroni.  In .NET Framework versione 2.0 è disponibile un oggetto <xref:System.Threading.ExecutionContext> contenente informazioni sul thread attualmente in esecuzione e che consente il passaggio del flusso attraverso punti asincroni all'interno di un dominio applicazione.  L'oggetto <xref:System.Security.Principal.WindowsIdentity> viene incluso anche nel flusso delle informazioni passate attraverso i punti asincroni, purché per la rappresentazione siano stati utilizzati metodi gestiti quali <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> e non, ad esempio, platform invoke a metodi nativi.  Questo elemento viene utilizzato per specificare che il flusso dell'identità Windows non passa attraverso punti asincroni, indipendentemente dal modo in cui è stata ottenuta la rappresentazione.  
  
 È possibile modificare questo comportamento predefinito in due diversi modi:  
  
1.  Nel codice gestito in base ai singoli thread.  
  
     Per sopprimere il flusso in base al singolo thread, modificare le impostazioni <xref:System.Threading.ExecutionContext> e <xref:System.Security.SecurityContext> utilizzando il metodo <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=fullName>, <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=fullName> o <xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=fullName>.  
  
2.  Nella chiamata all'interfaccia di hosting non gestita per il caricamento di CLR \(Common Language Runtime\).  
  
     Se per il caricamento di CLR viene utilizzata un'interfaccia di hosting non gestita, anziché un semplice eseguibile gestito, è possibile specificare uno speciale flag nella chiamata alla funzione [Funzione CorBindToRuntimeEx](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md).  Per attivare la modalità di compatibilità per l'intero processo, impostare su STARTUP\_ALWAYSFLOW\_IMPERSONATION il parametro `flags` per [Funzione CorBindToRuntimeEx](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md).  
  
## File di configurazione  
 L'elemento può essere utilizzato esclusivamente nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come specificare che il flusso dell'identità Windows passi attraverso punti asincroni anche quando la rappresentazione non viene ottenuta tramite metodi gestiti.  
  
```  
<configuration>  
  <runtime>  
    <alwaysFlowImpersonationPolicy enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Elemento \<legacyImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)