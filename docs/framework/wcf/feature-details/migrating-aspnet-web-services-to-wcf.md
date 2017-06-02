---
title: "Migrazione di servizi Web ASP.NET a WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1adbb931-f0b1-47f3-9caf-169e4edc9907
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Migrazione di servizi Web ASP.NET a WCF
ASP.NET fornisce strumenti e librerie di classi .NET Framework per creare servizi Web, oltre a funzionalità per servizi di hosting all'interno di Internet Information Services \(IIS\).[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce strumenti, funzionalità di hosting e librerie di classi .NET Framework per consentire a entità software di comunicare utilizzando qualsiasi protocollo, compresi quelli utilizzati dai servizi Web.La migrazione di servizi Web ASP.NET a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente alle applicazioni di sfruttare le nuove funzionalità e i miglioramenti apportati a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ha molti importanti vantaggi rispetto ai servizi Web ASP.NET.Mentre gli strumenti dei servizi Web ASP.NET sono idonei solo per la creazione di servizi Web, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce strumenti che possono essere utilizzati quando le entità software devono comunicare l'una con l'altra.In tal modo, viene ridotto il numero di tecnologie che gli sviluppatori devono conoscere per far fronte a diversi scenari di comunicazione software. Di conseguenza saranno ridotti i costi delle risorse e i tempi di completamento per i progetti di sviluppo del software.  
  
 Anche nel caso di progetti di sviluppo di servizi Web, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta più protocolli di servizio Web rispetto ai servizi Web ASP.NET.I protocolli aggiuntivi sono in grado di gestire soluzioni più sofisticate, tra cui sessioni e transazioni affidabili.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta un maggior numero di protocolli di trasporto dei messaggi, rispetto ai servizi Web ASP.NET.I servizi Web ASP.NET supportano solo l'invio di messaggi utilizzando HTTP \(Hypertext Transfer Protocol\).[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta l'invio di messaggi utilizzando HTTP, oltre a TCP \(Transmission Control Protocol\), named pipe e l'accodamento messaggi Microsoft \(MSMQ\).La cosa più importante è che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere esteso per supportare protocolli di trasporto aggiuntivi.Pertanto, il software sviluppato utilizzando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere adattato per operare assieme a numerosi altri software, aumentando in tal modo il potenziale rendimento dell'investimento.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce funzionalità molto più ricche per la distribuzione e la gestione delle applicazioni, rispetto ai servizi Web ASP.NET.Oltre a un sistema di configurazione, di cui è dotato anche ASP.NET, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] offre un editor di configurazione, traccia delle attività dai mittenti ai destinatari e viceversa attraverso qualsiasi numero di intermediari, un visualizzatore di tracce, la registrazione dei messaggi, numerosissimi contatori delle prestazioni e supporto per Strumenti gestione Windows \(WMI\).  
  
 Alla luce di questi vantaggi potenziali di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rispetto ai servizi Web ASP.NET, se si stanno utilizzando, o si sta pensando di utilizzare i servizi Web ASP.NET, esistono diverse opzioni:  
  
-   Continuare a utilizzare i servizi Web ASP.NET e rinunciare ai vantaggi offerti da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Continuare a utilizzare i servizi Web ASP.NET con l'intenzione di adottare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in futuro.Negli argomenti di questa sezione viene illustrato come aumentare al massimo le possibilità di riuscire a utilizzare le nuove applicazioni del servizio Web ASP.NET con le applicazioni future [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Viene inoltre spiegato come creare nuovi servizi Web ASP.NET mirati a facilitare la loro migrazione a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Se, tuttavia, è importante proteggere i servizi o se sono richieste garanzie di affidabilità o transazione, o se sarà necessario creare funzionalità personalizzate di gestione, è preferibile adottare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è progettato espressamente per questi scenari.  
  
-   Adottare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per lo sviluppo di nuove applicazioni, continuando a mantenere le applicazioni del servizio Web ASP.NET esistenti.Questa è molto probabilmente la scelta ottimale.Produce i vantaggi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], risparmiando al contempo il costo della modifica delle applicazioni esistenti per utilizzarlo.In questo scenario, le nuove applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono coesistere con le applicazioni ASP.NET esistenti.Le nuove applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] saranno in grado di utilizzare i servizi Web ASP.NET esistenti e [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere utilizzato per programmare nuove funzionalità operative in applicazioni ASP.NET esistenti in virtù della compatibilità ASP.NET di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Adottare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ed eseguire la migrazione delle applicazioni del servizio Web ASP.NET esistenti a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].È possibile scegliere questa opzione per migliorare le applicazioni esistenti con le funzionalità fornite da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], oppure per sostituire la funzionalità dei servizi Web ASP.NET esistenti all'interno di nuove applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] più potenti.  
  
> [!NOTE]
>  Fare attenzione nel caso in cui un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia ospitato da IIS 5.x e ASP.NET sia disinstallato.Quando un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ospitato da IIS 5.x, se ASP.NET è disinstallato è possibile che venga richiesto il codice per il servizio.Quando ASP.NET è disinstallato in un sistema operativo in cui è in esecuzione IIS 5.x e [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è disinstallato, un file con estensione svc viene considerato un file di testo e il contenuto, compreso qualsiasi codice sorgente, viene restituito al richiedente.  
  
 In questa sezione vengono illustrate dettagliatamente le opzioni menzionate, vengono confrontati i servizi Web ASP.NET con [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e vengono fornite istruzioni per la migrazione del codice dei Servizi Web ASP.NET a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Vedere anche  
 [Preparazione all'adozione di Windows Communication Foundation: facilitazione dell'integrazione futura](../../../../docs/framework/wcf/feature-details/anticipating-adopting-wcf-migration.md)   
 [Preparazione all'adozione di Windows Communication Foundation: facilitare l'integrazione futura](../../../../docs/framework/wcf/feature-details/anticipating-adopting-the-wcf-easing-future-integration.md)   
 [Utilizzo di Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/adopting-wcf.md)   
 [Confronto tra i servizi Web ASP.NET e WCF basato sullo scopo e gli standard usati](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used.md)   
 [Confronto tra servizi Web ASP.NET e WCF basato sullo sviluppo](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)