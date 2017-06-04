---
title: "Panoramica di Windows Identity Foundation 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5f723345-7270-49e2-b638-b3a34bd40517
caps.latest.revision: 11
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 11
---
# Panoramica di Windows Identity Foundation 4.5
Windows Identity Foundation 4.5 è un set di classi .NET Framework per l'implementazione dell'identità basata sulle attestazioni nelle applicazioni.  Tramite WIF sarà possibile usufruire più facilmente dei vantaggi offerti dai servizi e dalle applicazioni in grado di riconoscere attestazioni.  WIF 4.5 può essere utilizzato in qualsiasi applicazione Web o servizio Web con .NET Framework 4.5 o versione successiva.  WIF rappresenta solo una parte della famiglia software di identità federativa di Microsoft con cui viene implementata la visione condivisa del settore basata su standard aperti.  L'identità federativa include tre componenti: [Active Directory® Federation Services](http://go.microsoft.com/fwlink/?LinkID=247516) \(AD FS\) 2.0, [Servizio di controllo di accesso di Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=247517) \(ACS\) e WIF.  Insieme, questi tre componenti formano la base della nuova piattaforma di accesso e identità cloud basata sulle attestazioni di Microsoft.  
  
 Per ulteriori informazioni su WIF, vedere il [sito Web di Windows Identity Foundation](http://go.microsoft.com/fwlink/?LinkId=149009) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=149009\) in Security Developer Center su MSDN.  Per un'introduzione alla creazione di applicazioni mediante WIF, vedere la pubblicazione relativa alla [programmazione di Windows Identity Foundation](http://go.microsoft.com/fwlink/?LinkId=210158) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=210158\) di Vittorio Bertocci \(pubblicata da Microsoft Press\).  
  
## Funzionalità di WIF 4.5  
 WIF 4.5 è un framework per la compilazione di applicazioni in grado di riconoscere identità.  Tramite il framework vengono estratti i protocolli WS\-Trust e WS\-Federation e vengono presentati sviluppatori con API per la compilazione di applicazioni in grado di riconoscere attestazioni e, se necessario, servizi token di sicurezza.  Tramite le applicazioni è possibile utilizzare WIF per elaborare i token emessi dai servizi token di sicurezza, ad esempio AD FS 2.0 e ACS, e prendere decisioni basate sulle identità nell'applicazione Web o nel servizio Web.  
  
 WIF 4.5 dispone delle seguenti funzionalità principali:  
  
-   Compilazione di applicazioni in grado di riconoscere attestazioni \(applicazioni relying party\).  WIF supporta gli sviluppatori nella compilazione di applicazioni in grado di riconoscere attestazioni.  Oltre a fornire un modello di attestazioni, offre agli sviluppatori di applicazioni un ampio set di API per supportare gli utenti a prendere decisioni di accesso basate sulle attestazioni.  Garantisce inoltre agli sviluppatori un'esperienza di programmazione coerente se scelgono di compilare le applicazioni in ambienti WCF o ASP.NET.  
  
-   Compilazione del supporto della delega di identità in applicazioni in grado di riconoscere attestazioni.  WIF offre la funzionalità per gestire le identità dei richiedenti originali oltre i limiti del servizio.  Questa funzionalità può essere ottenuta utilizzando "OnBehalfOf" o "ActAs" nel framework e offre agli sviluppatori la possibilità di aggiungere il supporto per la delega di identità nelle applicazioni in grado di riconoscere attestazioni.  
  
-   Compilazione di servizi token di sicurezza personalizzati.  Grazie a WIF, la compilazione di un servizio token di sicurezza personalizzato che supporti il protocollo WS\-Trust è molto più semplice.  Un servizio token di sicurezza di questo tipo viene definito anche servizio token di sicurezza attivo.  
  
     Inoltre, il framework fornisce il supporto per la compilazione di un servizio token di sicurezza che supporta WS\-Federation per abilitare i client del Web browser.  Un servizio token di sicurezza di questo tipo viene definito anche servizio token di sicurezza passivo.  
  
-   Nuovo strumento Identity and Access Tool for Visual Studio 11 con cui è possibile proteggere l'applicazione con l'identità basata sulle attestazione e accettare utenti da più provider di identità.  È possibile scaricare questo strumento di WIF dall'URL seguente: [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=245849](http://go.microsoft.com/fwlink/?LinkID=245849) o direttamente da Visual Studio 11 cercando "identità" in Gestione estensioni.  Per ulteriori informazioni, vedere [Identity and Access Tool per Visual Studio 2012](../../../docs/framework/security/identity-and-access-tool-for-vs.md).  
  
 WIF supporta gli scenari principali seguenti:  
  
-   Federazione.  Tramite WIF è possibile abilitare la federazione tra due o più partner.  Il relativo supporto per compilare applicazioni in grado di riconoscere attestazioni \(relying party\) e servizi token di sicurezza personalizzati facilita la creazione di questo scenario da parte degli sviluppatori.  
  
-   Delega di identità.  Tramite WIF viene semplificata la gestione delle identità oltre i limiti del servizio in modo che gli sviluppatori possano ottenere uno scenario di delega di identità.  
  
-   Autenticazione step\-up.  I requisiti di autenticazione delle diverse risorse in un'applicazione possono variare.  WIF offre agli sviluppatori la possibilità di compilare applicazioni che possono richiedere requisiti incrementali di autenticazione, ad esempio l'accesso iniziale con l'autenticazione di nome utente\/password e, successivamente, l'aggiornamento all'autenticazione con smart card.  
  
 Grazie a WIF, sarà possibile usufruire più facilmente dei vantaggi offerti dal modello di identità basato sulle attestazioni.  Per ulteriori informazioni, vedere il [white paper di Windows Identity Foundation per sviluppatori](http://go.microsoft.com/fwlink/?LinkId=122266).