---
title: "Panoramica della traccia analitica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "traccia analitica [WCF], panoramica"
ms.assetid: ae55e9cc-0809-442f-921f-d644290ebf15
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Panoramica della traccia analitica
La traccia analitica in [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] è una funzionalità di traccia a prestazioni elevate e verbosità ridotta impostata in base a Traccia eventi per Windows \(ETW\). ETW è in esecuzione al livello del kernel per ridurre notevolmente il sovraccarico delle operazioni di traccia. Memorizza nel buffer gli eventi in modalità kernel e utente in modo efficace e consente l'abilitazione dinamica della registrazione senza richiedere riavvii del servizio. I dati della traccia sono disponibili nei log eventi in seguito alla generazione e alla ricezione.  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] ETW, vedere [Migliorare il debug e l'ottimizzazione delle prestazioni con ETW](http://go.microsoft.com/fwlink/?LinkId=164781).  
  
 Oltre a utilizzare i registri eventi relativi al sistema Windows, alla sicurezza e alle applicazioni per analizzare l'applicazione, [!INCLUDE[wv](../../../../../includes/wv-md.md)] e [!INCLUDE[lserver](../../../../../includes/lserver-md.md)] hanno introdotto altri log nel nodo di livello superiore Registri applicazioni e servizi. Lo scopo di questi nuovi log consiste nell'archiviare eventi per una particolare applicazione o un componente specifico anziché eventi globali con un impatto a livello di sistema \(ad esempio il tipo di eventi che potrebbero essere registrati dal registro eventi relativo alla sicurezza\).[!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] unifica e correla la registrazione di eventi di traccia [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], log dei messaggi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] e record di rilevamento [!INCLUDE[wf1](../../../../../includes/wf1-md.md)] a Registri applicazioni e servizi.  
  
## Concetti e funzionalità  
 I concetti e le funzionalità seguenti si applicano alla traccia analitica di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].  
  
### Abilitazione di impostazioni di diagnostica WCF  
 La diagnostica WCF è abilitata all'interno della sezione di configurazione \<system.serviceModel\>\<diagnostics\>.  
  
```  
  
<system.serviceModel>  
  <diagnostics>  
  
```  
  
 Le impostazioni di diagnostica WCF per un'applicazione virtuale IIS ospitata su Web sono abilitate nel relativo file Web.config. Un'altra opzione consiste nella creazione di un file Web.config in una sottodirectory all'interno dell'applicazione.  Con questa scelta, le impostazioni vengono applicate a tutti i servizi all'interno di una sottodirectory.  Per verificare che le impostazioni di diagnostica siano inizializzate in modo coerente per tutti i servizi all'interno dell'applicazione, le impostazioni devono trovarsi all'interno del file Web.config nella directory dell'applicazione e non in una delle singole sottodirectory all'interno dell'applicazione.  
  
### Canali  
 ETW consente ai componenti software di dirigere eventi della traccia a un particolare gruppo di destinatari in base all'utilizzo di canali. È ad esempio possibile inviare eventi per gli amministratori di sistema a un canale ed eventi di particolare interesse per gli sviluppatori di applicazioni a un altro canale. I canali vengono denominati e registrati con Windows. In questo modo gli utenti possono visualizzare gli eventi di un canale utilizzando il Visualizzatore eventi.  
  
 La funzionalità della traccia analitica per [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] in [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] scrive nel canale Microsoft\-Windows\-Application\-Server\-Applications. Questo canale è stato progettato in maniera specifica per gli utenti che desiderano monitorare l'integrità dei servizi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] in produzione. Definisce un set di eventi di dimensioni ridotte che può essere utilizzato in diversi scenari di monitoraggio dell'integrità e risoluzione di problemi.  
  
 Per abilitare il manifest di Traccia eventi per Windows in modo che i messaggi vengano decodificati correttamente nel registro eventi, utilizzare lo strumento ServiceModelReg nella riga di comando come segue:  
  
 `ServiceModelReg.exe -i -c:etw`  
  
### Configurazione dinamica  
 L'infrastruttura ETW consente l'abilitazione e la configurazione dinamica della traccia mediante strumenti standard di Windows.[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][Abilitazione dinamica della traccia analitica](../../../../../docs/framework/wcf/diagnostics/etw/dynamically-enabling-analytic-tracing.md).  
  
### Traccia del flusso di messaggi  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] come abilitare la traccia del flusso di messaggi, vedere [Configurazione della traccia del flusso di messaggi](../../../../../docs/framework/wcf/diagnostics/etw/configuring-message-flow-tracing.md).  
  
### Parole chiave  
 Le parole chiave vengono utilizzate per filtrare messaggi di traccia e definire il componente di [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] che ha generato l'evento.[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [Abilitazione dinamica della traccia analitica](../../../../../docs/framework/wcf/diagnostics/etw/dynamically-enabling-analytic-tracing.md).