---
title: "Elemento &lt;legacyImpersonationPolicy&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#legacyImpersonationPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/legacyImpersonationPolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<legacyImpersonationPolicy> (elemento)"
  - "legacyImpersonationPolicy (elemento)"
ms.assetid: 6e00af10-42f3-4235-8415-1bb2db78394e
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Elemento &lt;legacyImpersonationPolicy&gt;
Specifica che il flusso dell'identità Windows non passa attraverso punti asincroni, indipendentemente dalle impostazioni di flusso per il contesto di esecuzione nel thread corrente.  
  
## Sintassi  
  
```  
<legacyImpersonationPolicy    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica che <xref:System.Security.Principal.WindowsIdentity> non passa attraverso punti asincroni, indipendentemente dalle impostazioni di flusso di <xref:System.Threading.ExecutionContext> nel thread corrente.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|<xref:System.Security.Principal.WindowsIdentity> passa attraverso punti asincroni a seconda delle impostazioni di flusso di <xref:System.Threading.ExecutionContext> per il thread corrente.  Questa è l'impostazione predefinita.|  
|`true`|<xref:System.Security.Principal.WindowsIdentity> non passa attraverso punti asincroni, indipendentemente dalle impostazioni di flusso di <xref:System.Threading.ExecutionContext> nel thread corrente.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 In .NET Framework versione 1.0 e 1.1 <xref:System.Security.Principal.WindowsIdentity> non passa attraverso punti asincroni definiti dall'utente.  In .NET Framework versione 2.0 è disponibile un oggetto <xref:System.Threading.ExecutionContext> contenente informazioni sul thread attualmente in esecuzione e che consente il passaggio del flusso attraverso punti asincroni all'interno di un dominio applicazione.  Anche l'oggetto <xref:System.Security.Principal.WindowsIdentity> è incluso nel flusso delle informazioni che passano attraverso i punti asincroni, pertanto il flusso includerà anche un eventuale contesto di rappresentazione esistente.  Questo elemento viene utilizzato per specificare che l'oggetto <xref:System.Security.Principal.WindowsIdentity> non passa attraverso punti asincroni.  
  
> [!NOTE]
>  Common Language Runtime \(CLR\) supporta le operazioni di rappresentazione eseguite utilizzando solo codice gestito e non quelle eseguite al di fuori del codice gestito, ad esempio le operazioni tramite pInvoke al codice non gestito o tramite chiamate dirette alle funzioni Win32.  Solo gli oggetti <xref:System.Security.Principal.WindowsIdentity> gestiti possono attraversare i punti asincroni, a meno che l'elemento `alwaysFlowImpersonationPolicy` non sia stato impostato su true \(`<alwaysFlowImpersonationPolicy enabled="true"/>`\).  L'impostazione dell'elemento `alwaysFlowImpersonationPolicy` su true specifica che il flusso dell'identità Windows passa sempre attraverso punti asincroni, indipendentemente dal modo in cui è stata ottenuta la rappresentazione.  Per ulteriori informazioni sul flusso della rappresentazione non gestita attraverso punti asincroni, vedere [Elemento \<alwaysFlowImpersonationPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/alwaysflowimpersonationpolicy-element.md).  
  
 L'elemento può essere utilizzato esclusivamente nel file di configurazione dell'applicazione.  
  
 È possibile modificare questo comportamento predefinito in due diversi modi:  
  
1.  Nel codice gestito in base ai singoli thread.  
  
     Per sopprimere il flusso in base al singolo thread, modificare le impostazioni <xref:System.Threading.ExecutionContext> e <xref:System.Security.SecurityContext> utilizzando il metodo <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=fullName>, <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=fullName> o <xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=fullName>.  
  
2.  Nella chiamata all'interfaccia di hosting non gestita per il caricamento di CLR \(Common Language Runtime\).  
  
     Se per il caricamento di CLR viene utilizzata un'interfaccia di hosting non gestita, anziché un semplice eseguibile gestito, è possibile specificare uno speciale flag nella chiamata alla funzione [Funzione CorBindToRuntimeEx](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md).  Per attivare la modalità di compatibilità per l'intero processo, impostare su STARTUP\_LEGACY\_IMPERSONATION il parametro `flags` per [Funzione CorBindToRuntimeEx](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come specificare il comportamento legacy che non consente il passaggio del flusso dell'identità Windows attraverso punti asincroni.  
  
```  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)