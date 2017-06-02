---
title: "Elemento &lt;etwEnable&gt; | Microsoft Docs"
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
  - "<etwEnable> (elemento)"
  - "etwEnable (elemento)"
ms.assetid: 29dde982-6d8b-4099-8867-ad0d7733f6dc
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;etwEnable&gt;
Specifica se abilitare la traccia eventi per Windows \(ETW\) per gli eventi Common Language Runtime.  
  
## Sintassi  
  
```  
<etwEnable enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Consente di specificare se deve essere abilitato ETW.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|true|Attiva ETW.  Si tratta dell'impostazione predefinita di versioni di Windows a partire dai sistemi operativi Windows Vista e Windows Server 2008.|  
|false|Disabilitare ETW.  Si tratta dell'impostazione predefinita per versioni precedenti di Windows.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Iniziando con Windows Vista, ETW è abilitato per impostazione predefinita.  Utilizzare tale elemento per disabilitare ETW per un'applicazione.  In versioni precedenti di Windows, utilizzare questo elemento per abilitare ETW per un'applicazione.  
  
> [!NOTE]
>  ETW può essere abilitato o disabilitato globalmente su un server tramite un'impostazione del registro di sistema.  Vedere [Controlling .NET Framework Logging](../../../../../docs/framework/performance/controlling-logging.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come attivare la tracciatura ETW di un'applicazione.  
  
```  
<configuration>  
   <runtime>  
      <etwEnable enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Controlling .NET Framework Logging](../../../../../docs/framework/performance/controlling-logging.md)