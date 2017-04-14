---
title: "Elemento &lt;applicationPool&gt; (impostazioni Web) | Microsoft Docs"
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
  - "<applicationPool> (elemento)"
  - "applicationPool (elemento)"
ms.assetid: 46d1baaa-e343-4639-b70d-2a43a9f62b2a
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Elemento &lt;applicationPool&gt; (impostazioni Web)
Specifica le impostazioni di configurazione utilizzate da ASP.NET per gestire il comportamento relativo all'intero processo quando un'applicazione ASP.NET è in esecuzione in modalità integrata in [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] o versioni successive.  
  
> [!IMPORTANT]
>  Questo elemento e la funzionalità che supporta funzionano solo se l'applicazione ASP.NET è ospitata in [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] o versioni successive.  
  
## Sintassi  
  
```  
<applicationPool   
    maxConcurrentRequestsPerCPU="5000"   
    maxConcurrentThreadsPerCPU="0"   
    requestQueueLimit="5000" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`maxConcurrentRequestsPerCPU`|Specifica il numero di richieste simultanee che ASP.NET consente per CPU.|  
|`maxConcurrentThreadsPerCPU`|Specifica quanti thread simultanei possono essere in esecuzione per un pool di applicazioni per ogni CPU.  Questa impostazione fornisce un modo alternativo per controllare la concorrenza ASP.NET, poiché è possibile limitare il numero di thread gestiti per CPU utilizzabili per servire le richieste.  L'impostazione predefinita è 0, il che indica che ASP.NET non limita il numero di thread che possono essere creati per CPU. Tuttavia, il numero di thread che è possibile creare è limitato anche dal pool di thread CLR.|  
|`requestQueueLimit`|Specifica il numero massimo di richieste che è possibile mettere in coda per ASP.NET in un singolo processo.  Quando due o più applicazioni ASP.NET vengono eseguite in un singolo pool di applicazioni, il set cumulativo di richieste inoltrate a qualsiasi applicazione nel pool di applicazioni è soggetto a questa impostazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.web\>](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)|Contiene informazioni sul modo in cui ASP.NET interagisce con un'applicazione host.|  
  
## Note  
 Quando si esegue [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] o versioni successive in modalità integrata, questa combinazione di elementi consente di configurare il modo in cui ASP.NET gestisce i thread e mette in coda le richieste quando l'applicazione è ospitata in un pool di applicazioni IIS.  Se si esegue IIS 6 o [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] in modalità classica o ISAPI, queste impostazioni vengono ignorate.  
  
 Le impostazioni di `applicationPool` si applicano a tutti i pool di applicazioni eseguiti in una determinata versione di .NET Framework.  Le impostazioni sono contenute in un file aspnet.config.  Esiste una versione di questo file per le versioni 2.0 e 4 di .NET Framework. Le versioni 3.0 e 3.5 di .NET Framework presentano lo stesso file aspnet.config della versione 2.0.  
  
> [!IMPORTANT]
>  Se si esegue [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] in [!INCLUDE[win7](../../../../../includes/win7-md.md)] è possibile configurare un file aspnet.config a parte per ogni pool di applicazioni.  Ciò consente di adattare le prestazioni dei thread per ogni pool di applicazioni.  
  
 Per l'impostazione `maxConcurrentRequestsPerCPU`, l'impostazione predefinita di "5000" in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] disattiva di fatto la limitazione delle richieste controllata da ASP.NET, a meno che non si verifichino effettivamente 5000 o più richieste per CPU.  L'impostazione predefinita dipende invece dal pool di thread CLR per gestire automaticamente la concorrenza per CPU.  L'aumento del limite predefinito in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] risulterà vantaggioso per le applicazioni che fanno largo uso dell'elaborazione di richieste asincrona o che presentano molte richieste di lunga durata bloccate su I\/O di rete.  Se si imposta `maxConcurrentRequestsPerCPU` su zero si disattiva l'utilizzo di thread gestiti per l'elaborazione di richieste ASP.NET.  Quando un'applicazione viene eseguita in un pool di applicazioni IIS, le richieste restano nel thread di I\/O IIS e pertanto la concorrenza viene limitata dalle impostazioni dei thread di IIS.  
  
 Il funzionamento dell'impostazione `requestQueueLimit` è uguale a quello dell'attributo `requestQueueLimit` dell'elemento [processModel](http://msdn.microsoft.com/it-it/4b8fe20e-74c8-4566-b72c-ce5f83c8e32d), che viene impostato nei file Web.config delle applicazioni ASP.NET.  Tuttavia, se si imposta `requestQueueLimit` in un file aspnet.config si esegue l'override dell'impostazione `requestQueueLimit` in un file Web.config.  In altre parole, se entrambi gli attributi sono impostati \(il che è vero per impostazione predefinita\), l'impostazione `requestQueueLimit` nel file aspnet.config ha la precedenza.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come configurare il comportamento relativo all'intero processo di ASP.NET nel file aspnet.config nelle circostanze seguenti:  
  
-   L'applicazione è ospitata in un pool di applicazioni [!INCLUDE[iisver](../../../../../includes/iisver-md.md)].  
  
-   [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] viene eseguito in modalità integrata.  
  
-   L'applicazione sta utilizzando [!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)] o versioni successive.  
  
 I valori nell'esempio sono i valori predefiniti.  
  
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
 [Elemento \<system.web\> \(impostazioni Web\)](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)