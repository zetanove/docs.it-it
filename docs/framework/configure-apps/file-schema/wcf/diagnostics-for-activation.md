---
title: "&lt;diagnostics&gt; per Activation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1486e0eb-fe2a-46c3-b584-c924889477dd
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;diagnostics&gt; per Activation
Configura le funzionalità di diagnostica del listener [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Sintassi  
  
```  
  
<configuration>  
   <system.serviceModel.activation>  
       <diagnostics performanceCountersEnabled="Boolean" />  
   </system.serviceModel.activation>  
</configuration>  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`performanceCountersEnabled`|Valore booleano che indica se sono i contatori delle prestazioni stati attivati a fini diagnostici.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.serviceModel.activation\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel-activation.md)|Contiene impostazioni di configurazione per il processo del listener SMSvcHost.exe.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Activation.Configuration.DiagnosticSection>