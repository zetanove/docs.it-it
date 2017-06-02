---
title: "Elemento &lt;shadowCopyVerifyByTimestamp&gt; | Microsoft Docs"
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
  - "<shadowCopyTimeStampVerification> (elemento)"
  - "shadowCopyTimeStampVerification (elemento)"
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;shadowCopyVerifyByTimestamp&gt;
Specifica se la copia shadow utilizza il comportamento di avvio predefinito introdotto in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] o ripristina il comportamento di avvio di versioni precedenti di .NET Framework.  
  
## Sintassi  
  
```  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Specifica se i domini applicazione che utilizzano la copia shadow confrontano il timestamp dell'assembly in caso di avvio, per stabilire se un assembly è stato aggiornato prima della copia shadow dell'assembly.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|true|All'avvio, copia solo assembly aggiornati dall'ultima volta in cui sono stati copiati nella directory della copia shadow.  L'impostazione predefinita per [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] è "Infinity".|  
|false|Ripristina il comportamento di avvio di versioni precedenti di .NET Framework ovvero copiare tutti i file all'avvio.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Avviandosi con [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], sugli assembly viene creata la copia shadow solo se i timestamp indicano che vengono modificati da quando sono stati copiati l'ultima volta nella directory della copia shadow.  Migliora i tempi di avvio per molte applicazioni che utilizzano copia shadow, come descritto in [Creazione di copie replicate di assembly](../../../../../docs/framework/app-domains/shadow-copy-assemblies.md).  Le applicazioni con una percentuale e una frequenza elevate di aggiornamenti dell'assembly non possono trarre vantaggio da questa modifica nel comportamento.  In tal caso, è possibile utilizzare questo elemento per ripristinare il comportamento delle versioni precedenti di .NET Framework.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come disabilitare il comportamento di avvio predefinito dell'esecuzione della copia shadow in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] e ripristinare il comportamento di avvio delle versioni precedenti di .NET Framework.  
  
```  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Creazione di copie replicate di assembly](../../../../../docs/framework/app-domains/shadow-copy-assemblies.md)