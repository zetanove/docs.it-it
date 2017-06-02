---
title: "Elemento &lt;startup&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#startup"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<startup> (elemento)"
  - "tag contenitore, <startup> (elemento)"
  - "startup (elemento)"
ms.assetid: 536acfd8-f827-452f-838a-e14fa3b87621
caps.latest.revision: 19
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 19
---
# Elemento &lt;startup&gt;
Specifica informazioni di avvio di Common Language Runtime.  
  
## Sintassi  
  
```  
<startup useLegacyV2RuntimeActivationPolicy="true|false" >   
</startup>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`useLegacyV2RuntimeActivationPolicy`|Attributo facoltativo.<br /><br /> Specifica se abilitare i criteri di attivazione runtime di [!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)] o utilizzare i criteri di attivazione di [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)].|  
  
## Attributo useLegacyV2RuntimeActivationPolicy  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`true`|Abilitare i criteri di attivazione runtime di [!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)] per il runtime scelto, vale a dire associare le tecniche di attivazione runtime legacy \(ad esempio [CorBindToRuntimeEx function](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)\) al runtime scelto dal file di configurazione invece di limitarne l'utilizzo a CLR versione 2.0.  Pertanto, se dal file di configurazione si sceglie CLR versione 4 o successive, gli assembly in modalità mista creati con le versioni precedenti di .NET Framework vengono caricati con la versione di CLR scelta.  Con l'impostazione di questo valore si impedisce il caricamento di CLR versione 1.1 o CLR versione 2.0 nello stesso processo, disabilitando in modo efficace la funzionalità side\-by\-side in\-process.|  
|`false`|Utilizzare i criteri di attivazione predefiniti per [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] e versioni successive, che consistono nel consentire tecniche di attivazione runtime legacy per caricare CLR versione 1.1 o 2.0 nel processo.  Con l'impostazione di questo valore si impedisce il caricamento degli assembly in modalità mista in .NET Framework 4 o versioni successive a meno che non siano stati compilati con .NET Framework 4 o versioni successive.  Questo valore è quello predefinito.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<requiredRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md)|Specifica che l'applicazione supporta solo la versione 1.0 di Common Language Runtime \(CLR\).  Nelle applicazioni compilate con il runtime versione 1.1 o successiva sarà necessario utilizzare l'elemento **\<supportedRuntime\>**.|  
|[\<supportedRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)|Specifica le versioni di Common Language Runtime supportate dall'applicazione.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
  
## Note  
 È necessario utilizzare l'elemento **\<supportedRuntime\>** in tutte le applicazioni compilate con la versione 1.1 o successiva di CLR.  Nelle applicazioni compilate per supportare esclusivamente la versione 1.0 è necessario utilizzare l'elemento **\<requiredRuntime\>**.  
  
 Il codice di avvio per un'applicazione inclusa in Microsoft Internet Explorer ignora l'elemento **\<startup\>** e i relativi elementi figlio.  
  
## Attributo useLegacyV2RuntimeActivationPolicy  
 L'attributo è utile se nell'applicazione vengono utilizzati percorsi di attivazione legacy, quale la [funzione CorBindToRuntimeEx](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) e si desidera attivare la versione 4 di CLR anziché una versione precedente per tali percorsi, oppure se l'applicazione viene compilata con [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] ma dipende da un assembly in modalità mista compilato con una versione precedente di .NET Framework.  In tali scenari impostare l'attributo su `true`.  
  
> [!NOTE]
>  Se si imposta l'attributo su `true` viene impedito il caricamento di CLR versione 1.1 o CLR versione 2.0 nello stesso processo, disabilitando in modo efficace la funzionalità side\-by\-side in\-process \(vedere [Side\-by\-Side Execution for COM Interop](http://msdn.microsoft.com/it-it/4302318c-3586-49bf-8620-b9a39cdf4a32)\).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare la versione dell'ambiente di esecuzione in un file di configurazione.  
  
```  
<!-- When used with version 1.0 of the .NET Framework runtime -->  
<configuration>  
   <startup>  
      <requiredRuntime version="v1.0.3705" safemode="true"/>  
   </startup>  
</configuration>  
<!-- When used with version 1.1 (or later) of the runtime -->  
<configuration>  
   <startup>  
      <supportedRuntime version="v1.1.4322"/>  
      <supportedRuntime version="v1.0.3705"/>  
   </startup>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni di avvio](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> Specifying Which Runtime Version to Use](http://msdn.microsoft.com/it-it/c376208d-980d-42b4-865b-fbe0d9cc97c2)   
 [Side\-by\-Side Execution for COM Interop](http://msdn.microsoft.com/it-it/4302318c-3586-49bf-8620-b9a39cdf4a32)   
 [Esecuzione side\-by\-side in\-process](../../../../../docs/framework/deployment/in-process-side-by-side-execution.md)