---
title: "Registrazione eventi in WCF | Microsoft Docs"
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
  - "registrazione eventi [WCF]"
ms.assetid: aac0530d-f44c-45a1-bada-e30e0677b41f
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Registrazione eventi in WCF
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] tiene traccia degli eventi interni nel registro eventi di Windows.  
  
## Visualizzazione dei registri eventi  
 La registrazione degli eventi è abilitata automaticamente per impostazione predefinita e non è disponibile un meccanismo per disabilitarlo.Gli eventi registrati da [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] possono essere visualizzati utilizzando il Visualizzatore eventi.Per avviare questo strumento, fare clic su **Start**, selezionare **Pannello di controllo**, fare doppio clic su **Strumenti di amministrazione**, quindi doppio clic su **Visualizzatore eventi**.  
  
### Registro eventi dell'applicazione  
 Nel **registro eventi dell'applicazione** è contenuta la maggior parte degli eventi generati da [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].La maggior parte delle voci riguardano errori nell'avvio di una particolare funzionalità per un'applicazione.Gli esempi includono:  
  
-   Registrazione\/traccia dei messaggi: [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] scrive un evento nel registro eventi quando si verificano errori nella traccia e nella registrazione dei messaggi.Tuttavia, non tutti gli errori di traccia generano un evento.Per impedire che il registro eventi venga riempito completamente da errori di traccia, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] implementa un periodo di blackout di 10 minuti per questo tipo di evento.Pertanto, se [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] scrive un errore di traccia nel registro eventi, non ripeterà questa operazione per almeno 10 minuti.  
  
-   Listener condiviso: il servizio di condivisione porte TCP WCF registra un evento quando non può essere avviato.  
  
-   [!INCLUDE[infocard](../../../../../includes/infocard-md.md)]: registra eventi quando il servizio non può essere avviato.  
  
-   Eventi critici e di errore, quali errori di avvio o arresti anomali del sistema  
  
-   Registrazione messaggi attivata: gli eventi vengono registrati quando la registrazione dei messaggi è attivata.Questa funzionalità consente di notificare all'amministratore che informazioni riservate specifiche dell'applicazione possono essere registrate nelle intestazioni e nel corpo del messaggio.  
  
-   Viene registrato un evento quando è impostato l'attributo `enableLoggingKnownPII` dell'elemento `machineSettings` nel file `machine.config`.Questo attributo specifica se un'applicazione in esecuzione sul computer può registrare informazioni che consentono l'identificazione personale \(PII\).  
  
-   Se l'attributo `logKnownPii` nel file `app.config` o `web.config` è impostato su `true` affinché un'applicazione specifica attivi la registrazione delle informazioni che consentono l'identificazione personale, ma l'attributo `enableLoggingKnownPII` nell'elemento `machineSettings` del file `machine.config` è impostato su `false`, viene registrato un evento.In aggiunta, se `logKnownPii` e `enableLoggingKnownPII` sono impostati su `true` viene registrato un evento.Per ulteriori informazioni su queste impostazioni di configurazione, vedere la sezione Protezione dell'argomento [Configurazione della registrazione dei messaggi](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md).  
  
### Registro eventi di sicurezza  
 Il **registro eventi di sicurezza** contiene gli eventi del controllo di sicurezza registrati da WCF.  
  
### Registro eventi di sistema  
 WCF non registra alcun evento nel **registro eventi di sistema**.  
  
### Voci del registro eventi  
 L'**origine** di un evento è il nome dell'assembly che genera la voce del registro.  
  
 Il tipo di una voce del registro eventi consente di determinare la gravità di una voce.Ogni evento deve appartenere a un solo tipo, che l'applicazione indica quando riferisce l'evento.Il Visualizzatore eventi utilizza tale tipo per scegliere l'icona da visualizzare nella vista elenco del registro.Per i diversi tipi di evento di una voce del registro eventi, vedere <xref:System.Diagnostics.EventLogEntryType>.  
  
 Quando si seleziona "Ulteriori informazioni" durante la visualizzazione di un evento nel Visualizzatore eventi, quest'ultimo può inviare informazioni via Internet.Per ulteriori informazioni, vedere la Guida del Visualizzatore eventi.  
  
## Vedere anche  
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [Riferimenti generali sugli eventi](../../../../../docs/framework/wcf/diagnostics/event-logging/events-general-reference.md)