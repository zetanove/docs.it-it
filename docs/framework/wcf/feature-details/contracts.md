---
title: "Contratti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti [WCF]"
  - "WCF [WCF], contratti"
  - "Windows Communication Foundation [WCF], contratti"
ms.assetid: c8364183-4ac1-480b-804a-c5e6c59a5d7d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Contratti
Questa sezione illustra come definire e implementare contratti [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Un contratto di servizio specifica quale endpoint comunica con il mondo esterno.  A un livello più concreto, è un'istruzione su un set di messaggi specifici organizzati in modelli di scambio di messaggi di base \(MEP, Message Exchange Pattern\) quali, ad esempio, request\/reply, unidirezionale e duplex.  Se un contratto di servizio è un set logicamente correlato di scambi di messaggi, un'operazione di servizio è un singolo scambio di messaggi.  Un'operazione `Hello` deve, ad esempio, accettare un messaggio \(quindi il chiamante può annunciare il saluto\) e può o non può restituire un messaggio \(a seconda del livello di cortesia dell'operazione\).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su contratti e altri concetti [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base, vedere [Concetti fondamentali di Windows Communication Foundation](../../../../docs/framework/wcf/fundamental-concepts.md).  Questo argomento si incentra sulla comprensione dei contratti di servizio.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come compilare client che usano contratti di servizio per connettersi ai servizi, vedere [Panoramica dei client WCF](../../../../docs/framework/wcf/wcf-client-overview.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]i canali client, l'architettura client e altri problemi relativi ai client, vedere [Client](../../../../docs/framework/wcf/feature-details/clients.md).  
  
## Panoramica  
 In questo argomento viene fornito un orientamento concettuale di alto livello alla progettazione e all'implementazione di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Negli argomenti correlati vengono fornite informazioni più dettagliate sulle specifiche di progettazione e implementazione.  Prima di progettare e implementare l'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è consigliabile:  
  
-   Comprendere cosa siano i contratti di servizio, come funzionino e come sia possibile crearne uno.  
  
-   Comprendere che i contratti prevedono requisiti minimi che la configurazione di runtime o l'ambiente host potrebbe non supportare.  
  
## Contratti di servizio  
 Un contratto di servizio è un'istruzione che fornisce informazioni sugli argomenti seguenti:  
  
-   Raggruppamento di operazioni in un servizio.  
  
-   Forma delle operazioni in termini di messaggi scambiati.  
  
-   Tipi di dati di questi messaggi.  
  
-   Posizione delle operazioni.  
  
-   Protocolli e formati di serializzazione specifici usati per supportare la corretta comunicazione con il servizio.  
  
 Un contratto di ordine di acquisto può, ad esempio, includere un'operazione `CreateOrder` che accetta un input di tipi di informazioni sull'ordine e restituisce informazioni sull'esito positivo o negativo, incluso un identificatore di ordine.  Può inoltre includere un'operazione `GetOrderStatus` che accetta un identificatore di ordine e restituisce informazioni sullo stato dell'ordine.  Un contratto di servizio di questo tipo specificherebbe:  
  
-   Che il contratto di ordine di acquisto è costituito da operazioni `CreateOrder` e `GetOrderStatus`.  
  
-   Che le operazioni hanno specificato messaggi di input e di output.  
  
-   I dati che questi messaggi possono contenere.  
  
-   Istruzioni categoriali sull'infrastruttura di comunicazione necessaria per elaborare correttamente i messaggi.  Questi dettagli includono, ad esempio, indicazioni sulla necessità della protezione, e sui tipi di sicurezza eventualmente necessari, per stabilire una corretta comunicazione.  
  
 Per comunicare questo tipo di informazioni alle applicazioni su altre piattaforme \(incluse piattaforme non Microsoft\), i contratti di servizio XML vengono pubblicamente espressi in formati XML standard tra cui, ad esempio [Web Services Description Language \(WSDL\)](http://go.microsoft.com/fwlink/?LinkId=87004) e [XML Schema \(XSD\)](http://go.microsoft.com/fwlink/?LinkId=87005).  Gli sviluppatori operanti su molte piattaforme possono usare queste informazioni pubbliche sui contratti per creare applicazioni che possano comunicare con il servizio, perché comprendono il linguaggio della specifica e perché tali linguaggi sono progettati per consentire l'interoperabilità descrivendo i tipi, i formati e i protocolli pubblici supportati dal servizio.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gestisce questo tipo di informazioni, vedere [Metadata](../../../../docs/framework/wcf/feature-details/metadata.md).  
  
 I contratti possono essere però espressi in molti modi e, sebbene WSDL e XSD siano linguaggi eccellenti per descrivere i servizi in maniera accessibile, sono però difficili da usare in modo diretto e sono, in ogni caso, semplici descrizioni di un servizio, che non riguardano le implementazioni del contratto di servizio.  Pertanto, le applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usano interfacce, classi e attributi gestiti sia per definire la struttura di un servizio sia per implementare il servizio in questione.  
  
 Il contratto risultante, definito in tipi gestiti, può essere convertito \(*esportato*\) in metadati, WSDL e XSD, quando ciò sia richiesto dai client o da altri implementatori di servizi, specialmente su altre piattaforme.  Il risultato è un modello di programmazione semplice, che può essere descritto usando metadati pubblici per qualsiasi applicazione client.  I dettagli dei messaggi SOAP sottostanti, quali ad esempio le informazioni sul trasporto e sulla protezione, possono essere gestiti da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], che esegue automaticamente le conversioni necessarie tra il sistema dei tipi di contratto di servizio e il sistema dei tipi XML.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla progettazione dei contratti, vedere [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'implementazione dei contratti, vedere [Implementazione dei contratti di servizio](../../../../docs/framework/wcf/implementing-service-contracts.md).  
  
 Inoltre, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di sviluppare contratti di servizio interamente a livello di messaggio.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]llo sviluppo di contratti di servizio a livello di messaggio, vedere [Utilizzo dei contratti di messaggio](../../../../docs/framework/wcf/feature-details/using-message-contracts.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]llo sviluppo di servizi in linguaggio XML non SOAP, vedere [Interoperabilità con applicazioni POX](../../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md).  
  
### Informazioni sulla gerarchia di requisiti  
 Un contratto di servizio raggruppa le operazioni, specifica il MEP, i tipi di messaggio e i tipi di dati contenuti nei messaggi e indica le categorie di comportamento di runtime che un'implementazione deve avere per supportare il contratto \(se, ad esempio, è necessario che i messaggi siano crittografati e firmati\).  Il contratto di servizio stesso non specifica, tuttavia, con precisione in che modo questi requisiti siano soddisfatti, indica solo che devono essere soddisfatti.  Il tipo di crittografia e la modalità di firma di un messaggio dipendono dall'implementazione e dalla configurazione di un servizio conforme.  
  
 Si noti il modo in cui il contratto richiede certe caratteristiche dell'implementazione del contratto di servizio e della configurazione di runtime per l'aggiunta di un comportamento.  Il set dei requisiti che devono essere soddisfatti per esporre un servizio affinché possa essere usato si basa sul set di requisiti precedente.  Se un contratto prevede requisiti per l'implementazione, un'implementazione può richiedere ancora più caratteristiche di configurazione e associazioni che consentono l'esecuzione del servizio.  Infine, anche l'applicazione host deve supportare tutti i requisiti aggiunti dalla configurazione e dalle associazioni del servizio.  
  
 Questo processo relativo ai requisiti aggiuntivi è importante da tener presente quando si progetta, implementa, configura e ospita l'applicazione del servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Il contratto può, ad esempio, specificare che deve essere supportata una sessione.  In questo caso sarà quindi necessario configurare le associazioni per supportare il requisito contrattuale o l'implementazione del servizio non funzionerà.  Se il servizio richiede invece l'Autenticazione integrata di Windows ed è ospitato in Internet Information Services \(IIS\), nell'applicazione Web in cui risiede il servizio deve essere attivata l'Autenticazione integrata di Windows e disattivato il supporto di utenti anonimi.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle funzionalità e sull'impatto dei diversi tipi di applicazioni host dei servizi, vedere [Hosting](../../../../docs/framework/wcf/feature-details/hosting.md).  
  
## Vedere anche  
 [Endpoint: indirizzi, associazioni e contratti](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)   
 [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md)   
 [Implementazione dei contratti di servizio](../../../../docs/framework/wcf/implementing-service-contracts.md)