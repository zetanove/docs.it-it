---
title: "Elemento &lt;appDomainResourceMonitoring&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<appDomainResourceMonitoring> (elemento)"
  - "appDomainResourceMonitoring (elemento)"
ms.assetid: 02119ab6-1e91-448e-97ad-e7b2e5c4bbbd
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Elemento &lt;appDomainResourceMonitoring&gt;
Indica al runtime di raccogliere statistiche su tutti i domini di applicazione nel processo per la durata del processo.  
  
## Sintassi  
  
```  
<appDomainResourceMonitoring    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se il runtime raccoglie statistiche per il monitoraggio delle risorse dei domini di applicazione.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`true`|Il runtime raccoglie statistiche per il monitoraggio delle risorse dei domini di applicazione.|  
|`false`|Il runtime non raccoglie statistiche per il monitoraggio delle risorse dei domini di applicazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Il monitoraggio delle risorse dei domini di applicazione è disponibile tramite la classe di dominio delle applicazioni gestite, l'interfaccia [ICLRAppDomainResourceMonitor](../../../../../ocs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md) di hosting e Traccia eventi per Windows.  Quando il monitoraggio è abilitato, le statistiche vengono raccolte per tutti i domini di applicazione nel processo per la durata del processo.  
  
 Per attivare il monitoraggio tramite codice gestito, utilizzare la proprietà <xref:System.AppDomain.MonitoringIsEnabled%2A>.  
  
 Questo elemento di configurazione è disponibile solo in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] e versioni successive.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come abilitare il monitoraggio delle risorse dei domini di applicazione.  
  
```  
<configuration>  
   <runtime>  
      <appDomainResourceMonitoring enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=fullName>   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)