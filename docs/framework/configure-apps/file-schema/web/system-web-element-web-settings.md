---
title: "Elemento &lt;system.web&gt; (impostazioni Web) | Microsoft Docs"
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
  - "<system.Web> (elemento)"
  - "sistema di configurazione ASP.NET"
  - "file di configurazione [ASP.NET]"
  - "system.Web (elemento)"
  - "file di configurazione Web.config [ASP.NET]"
ms.assetid: 24c4cf4f-ad32-42b2-b040-8e4549e2855e
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Elemento &lt;system.web&gt; (impostazioni Web)
Contiene informazioni su come il livello di hosting ASP.NET gestisce il comportamento relativo all'intero processo.  
  
## Sintassi  
  
```  
<system.web>  
</system.web>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<applicationPool\>](../../../../../docs/framework/configure-apps/file-schema/web/applicationpool-element-web-settings.md)|Specifica le impostazioni di configurazione per i pool di applicazioni IIS in un file aspnet.config.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Specifica l'elemento radice in ogni file di configurazione utilizzato in Common Language Runtime e nelle applicazioni [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)].|  
  
## Note  
 L'elemento `system.web` e il relativo elemento figlio `applicationPool` sono stati aggiunti a [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] come in [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)].  Quando si esegue [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] o versioni successive in modalità integrata, questa combinazione di elementi consente di configurare il modo in cui ASP.NET gestisce i thread e mette in coda le richieste quando ASP.NET è ospitato in un pool di applicazioni IIS.  Se si esegue [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] o versioni successive in modalità classica o ISAPI, queste impostazioni vengono ignorate.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come configurare il comportamento relativo all'intero processo di ASP.NET nel file aspnet.config quando ASP.NET è ospitato in un pool di applicazioni IIS.  L'esempio presuppone che IIS sia in esecuzione in modalità integrata e che l'applicazione stia utilizzando [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)] o una versione successiva.  Questo comportamento non si verifica nelle versioni di [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] precedenti a [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)].  I valori nell'esempio sono i valori predefiniti.  
  
```  
<configuration>  
  <system.web>  
    <applicationPool   
        maxConcurrentRequestsPerCPU="5000"   
        maxConcurrentThreadsPerCPU="0"   
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## Informazioni sull'elemento  
  
|||  
|-|-|  
|Spazio dei nomi||  
|Nome di schema||  
|File di convalida||  
|Può essere vuoto||  
  
## Vedere anche  
 [Elemento \<applicationPool\> \(impostazioni Web\)](../../../../../docs/framework/configure-apps/file-schema/web/applicationpool-element-web-settings.md)