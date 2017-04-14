---
title: "Panoramica sull&#39;integrazione con applicazioni COM+ | Microsoft Docs"
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
helpviewer_keywords: 
  - "WCF, Integrazione COM+"
  - "Windows Communication Foundation, Integrazione COM+"
ms.assetid: e481e48f-7096-40eb-9f20-7f0098412941
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 29
---
# Panoramica sull&#39;integrazione con applicazioni COM+
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce un ambiente completo per la creazione di applicazioni distribuite.  Se si sta già usando la logica dell'applicazione basata su componenti ospitata in COM\+, è possibile usare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per estendere la logica esistente senza doverla riscrivere.  Uno degli scenari più comuni si verifica quando si desidera esporre la regola business COM\+ o Enterprise Services esistente tramite servizi Web.  
  
 Quando un'interfaccia su un componente COM\+ viene esposta come servizio Web, la specifica e il contratto di questi servizi vengono determinati da un mapping automatico eseguito in fase di inizializzazione dell'applicazione.  Nell'elenco seguente viene mostrato il modello concettuale di questo mapping:  
  
-   Viene definito un servizio per ogni classe COM esposta.  
  
-   Il contratto per il servizio viene derivato direttamente dalla definizione dell'interfaccia del componente selezionato, con la possibilità di esclusione del metodo definita nella configurazione.  
  
-   Le operazioni nel contratto vengono derivate direttamente dai metodi sulla definizione dell'interfaccia del componente.  
  
-   I parametri delle operazioni vengono derivati direttamente dal tipo dell'interoperabilità COM corrispondente ai parametri del metodo del componente.  
  
 Gli indirizzi e le associazioni di trasporto predefiniti per il servizio vengono forniti in un file di configurazione del servizio, ma possono essere riconfigurati in base alle necessità.  
  
> [!NOTE]
>  I contratti per i servizi Web esposti restano costanti finché le interfacce COM\+ e la configurazione restano immutate.  Una modifica a diverse interfacce non implica l'aggiornamento automatico dei servizi disponibili e richiede la riesecuzione dello strumento di configurazione del modello di servizi COM\+ \(ComSvcConfig.exe\).  
  
 I requisiti di autenticazione e autorizzazione dell'applicazione COM\+ e dei relativi componenti continuano a essere imposti in caso di uso come servizio Web.  
  
 Se il chiamante avvia una transazione del servizio Web, componenti contrassegnati come transazionali vengono integrati nell'ambito della transazione.  
  
 I passaggi seguenti sono necessari per esporre un'interfaccia del componente COM\+ come servizio Web, senza modificare il componente:  
  
1.  Determinare se l'interfaccia del componente COM\+ può essere esposta come servizio Web.  
  
2.  Selezionare una modalità di host appropriata.  
  
3.  Usare lo strumento di configurazione del modello di servizi COM\+ \(ComSvcConfig.exe\) per aggiungere un servizio Web per l'interfaccia.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come usare ComSvcConfig.exe, vedere [Procedura: utilizzare lo strumento di configurazione del modello di servizi di COM\+](../../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md).  
  
4.  Configurare le impostazioni del servizio aggiuntive nel file di configurazione dell'applicazione.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come configurare un componente, vedere [Procedura: configurare le impostazioni del servizio COM\+](../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md).  
  
## Interfacce supportate  
 Esistono alcune restrizioni sul tipo di interfacce che è possibile esporre come servizio Web.  I tipi di interfacce seguenti non sono supportati:  
  
-   Interfacce che passano riferimenti a oggetti come parametri: l'approccio limitato di riferimento a oggetti seguente viene descritto nella sezione sul supporto limitato dei riferimenti a oggetti.  
  
-   Interfacce che passano tipi non compatibili con le conversioni dell'interoperabilità COM di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
-   Interfacce per applicazioni con il pool di applicazioni attivato se ospitate da COM\+.  
  
-   Interfacce di componenti contrassegnati come privati per l'applicazione.  
  
-   Interfacce dell'infrastruttura COM\+.  
  
-   Interfacce dall'applicazione di sistema.  
  
-   Interfacce da componenti Enterprise Services che non sono stati aggiunti alla Global Assembly Cache.  
  
### Supporto limitato dei riferimenti a oggetti  
 Poiché diversi componenti COM\+ distribuiti usano oggetti in base ai parametri di riferimento, per restituire, ad esempio, un oggetto recordset ADO, l'integrazione COM\+ include un supporto limitato per i parametri di riferimento a oggetti.  Il supporto è limitato a oggetti che implementano l'interfaccia COM `IPersistStream`.  Il supporto include oggetti recordset ADO e può essere implementato per oggetti COM specifici dell'applicazione.  
  
 Per abilitare questo supporto, lo strumento ComSvcConfig.exe prevede l'opzione **allowreferences** che disabilita il parametro della firma del metodo normale e controlla che lo strumento venga eseguito, per assicurare che non vengano usati parametri di riferimento a oggetti.  I tipi di oggetto passati come parametri devono anche essere denominati e identificati all'interno dell'elemento di configurazione \<`persistableTypes`\> figlio dell'elemento \<`comContract`\>.  
  
 Quando questa funzionalità viene usata, il servizio di integrazione COM\+ usa l'interfaccia `IPersistStream` per serializzare o deserializzare l'istanza dell'oggetto.  Se l'istanza dell'oggetto non supporta `IPersistStream`, viene generata un'eccezione.  
  
 All'interno di un'applicazione client, i metodi sull'oggetto <xref:System.ServiceModel.ComIntegration.PersistStreamTypeWrapper> possono essere usati per passare un oggetto a un servizio e, analogamente, per recuperare un oggetto.  
  
> [!NOTE]
>  A causa della natura personalizzata e specifica della piattaforma dell'approccio alla serializzazione, la serializzazione è più adatta ad essere usata tra i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Selezione della modalità di host  
 COM\+ espone i servizi Web in una delle modalità di host seguenti:  
  
-   Host COM\+  
  
     Il servizio Web viene ospitato all'interno del processo del server COM\+ dedicato \(Dllhost.exe\) dell'applicazione.  Questa modalità richiede che l'applicazione sia avviata in modo esplicito prima di poter ricevere richieste del servizio Web.  Le opzioni COM\+ "Esegui come servizio NT" e "Continua l'esecuzione anche in caso di inattività del sistema" possono essere usate per impedire la chiusura per inattività dell'applicazione e dei relativi servizi.  Questa modalità assicura al servizio Web e a DCOM l'accesso all'applicazione server.  
  
-   Host Web  
  
     Il servizio Web viene ospitato all'interno di un processo di lavoro del server Web.  Questa modalità non richiede che COM\+ sia attivo quando viene ricevuta la richiesta iniziale.  Se l'applicazione non è attiva quando viene ricevuta questa richiesta, viene attivata automaticamente prima dell'elaborazione della richiesta.  Questa modalità assicura al servizio Web e a DCOM l'accesso all'applicazione server, ma provoca un hop del processo per le richieste del servizio Web.  Viene in genere richiesto il client per abilitare la rappresentazione.  In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], questo risultato può essere ottenuto con la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> della classe <xref:System.ServiceModel.Security.WindowsClientCredential>, accessibile come proprietà della classe generica <xref:System.ServiceModel.ChannelFactory%601>, e il valore dell'enumerazione <xref:System.Security.Principal.TokenImpersonationLevel>.  
  
-   Host Web in corso  
  
     Il servizio Web e la logica dell'applicazione COM\+ vengono ospitate all'interno del processo di lavoro del server Web.  Questo assicura l'attivazione automatica della modalità di host Web senza provocare un hop del processo per le richieste del servizio Web.  Lo svantaggio è che non è possibile accedere all'applicazione server tramite DCOM.  
  
### Considerazioni sulla sicurezza  
 Come per gli altri servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], le impostazioni di sicurezza per il servizio esposto vengono amministrate tramite impostazioni di configurazione per il canale [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Le tradizionali impostazioni di sicurezza DCOM, quali le impostazioni delle autorizzazioni DCOM a livello di computer, non vengono applicate.  Per imporre i ruoli dell'applicazione COM\+, è necessario che venga attivata l'autorizzazione ai "controlli di accesso a livello di componente" per il componente.  
  
 L'uso di un'associazione non protetta può lasciare la comunicazione soggetta a manomissioni o divulgazione di informazioni.  Per impedire ciò, è consigliabile usare un'associazione protetta.  
  
 Per le modalità di host COM\+ e Web, le applicazioni client devono permettere al processo server di rappresentare l'utente client.  Per ottenere questo risultato nei client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], impostare il livello di rappresentazione su <xref:System.Security.Principal.TokenImpersonationLevel>.  
  
 Se Internet Information Services \(IIS\) o Windows Process Activation Service \(WAS\) usa il trasporto HTTP, lo strumento Httpcfg.exe può essere usato per riservare un indirizzo dell'endpoint di trasporto.  In altre configurazioni, è importante proteggersi dai servizi non autorizzati che si comportano come il servizio desiderato.  Per impedire l'avvio di un servizio non autorizzato nell'endpoint desiderato, è possibile configurare il servizio legittimo perché venga eseguito come servizio NT.  Questo consente al servizio legittimo di attestare l'indirizzo dell'endpoint prima di qualsiasi servizio non autorizzato.  
  
 Quando si espone un'applicazione COM\+ con i ruoli COM\+ configurati come servizio ospitato sul Web, è necessario aggiungere "Avvia conteggio processi IIS" a uno dei ruoli dell'applicazione.  Questo account, denominato in genere IWAM\_nomecomputer, deve essere aggiunto per abilitare la chiusura normale degli oggetti dopo l'uso.  All'account non dovrebbero essere concesse autorizzazioni aggiuntive.  
  
 Le funzionalità di riciclo dei processi COM\+ non possono essere usate su applicazioni integrate.  Se l'applicazione è configurata per l'uso del riciclo dei processi e i componenti sono in esecuzione in un processo ospitato su COM\+, non sarà possibile avviare il servizio.  Questo requisito non include i servizi che usano la modalità di host Web in corso, poiché non vengono applicate le impostazioni di riciclo dei processi.  
  
## Vedere anche  
 [Panoramica sull'integrazione con applicazioni COM](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications-overview.md)