---
title: "Propagazione di ID attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd1c1ae5-cc8a-4f51-90c9-f7b476bcfe70
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Propagazione di ID attivit&#224;
La propagazione si verifica quando la traccia attività ServiceModel viene attivata \(propagazione di ServiceModel\) o disattivata \(propagazione di attività utente\-utente\).  
  
## Traccia attività ServiceModel attivata  
 Se la traccia attività ServiceModel è attivata, la propagazione si verifica tra le attività ProcessAction.  
  
### Server  
 Quando l'attributo `propagateActivity` è impostato su `true` sia sul client che sul server, l' ID dell'attività `ProcessAction` nel server è identico all'ID nell'intestazione del messaggio `ActivityId` propagata.  
  
 Quando non è presente alcuna intestazione `ActivityId` nel messaggio \(quando cioè `propagateActivity` è uguale a `false` sul client\) o quando `propagateActivity` è uguale a `false` sul server, il server genera un nuovo ID attività.  
  
### Client  
 Se il client è a thread singolo in modalità sincrona, ignora qualsiasi impostazione di `propagateActivity` sul client o sul server.  La risposta viene invece gestita nell'attività di richiesta.  Se il client è di tipo multithreading asincrono o sincrono, `propagateActivity` è uguale a `true` nel client ed è presente un'intestazione ID attività nel messaggio inviato dal server, il client recupera l'ID attività dal messaggio e lo trasferisce all'attività Elaborazione azione che contiene l'ID attività propagato.  In caso contrario, il client esegue il trasferimento dall'attività Elaborazione messaggio a una nuova attività Elaborazione azione.  Questo ulteriore trasferimento a una nuova attività Elaborazione azione viene eseguito per coerenza.  In questa attività, il client recupera l'ID attività dell'attività BeginCall dal contesto del thread locale, quando il thread viene allocato per l'elaborazione del messaggio di risposta.  Trasferisce quindi tale ID all'attività Elaborazione azione.  
  
 Se il client è duplex, agisce da server alla ricezione del messaggio.  
  
### Propagazione nei messaggi di errore  
 Non c'è differenza nello gestire messaggi validi e di errore.  Se `propagateActivity` è uguale a `true`, l'ID attività aggiunto alle intestazioni dei messaggi di errore SOAP è identico all'attività dell'ambiente.  
  
## Traccia attività ServiceModel disattivata  
 Se la traccia attività ServiceModel è disattivata, la propagazione si verifica direttamente tra le attività del codice utente, senza passare per le attività ServiceModel.  Viene inoltre propagato un ID attività definito dall'utente tramite l'intestazione ID attività del messaggio.  
  
 Se `propagateActivity`è uguale a `true` e `ActivityTracing`è uguale a `off` per un listener di traccia ServiceModel \(indipendentemente dal fatto che la traccia sia o meno attivata su ServiceModel\), sul client o sul server si verifica quanto segue:  
  
-   Alla richiesta di un'operazione o all'invio di una risposta, l'ID attività in TLS viene propagato fuori dal codice utente fino a quando non viene formato un messaggio.  Viene inoltre inserita un'intestazione ID attività nel messaggio prima dell'invio.  
  
-   Alla ricezione di una richiesta o una risposta, l'ID attività viene recuperato dall'intestazione del messaggio non appena viene creato l'oggetto messaggio.  L'ID attività in TLS viene propagato non appena il messaggio scompare dall'ambito, fino a quando non viene raggiunto il codice utente.  
  
 Questa garanzia delle azioni che le tracce dell'utente saranno visualizzate nella stessa attività se la propagazione è su.  Tuttavia, non costituisce per le tracce ServiceModel.  Le tracce ServiceModel si verificano in un'attività del codice utente solo se l'elaborazione di tali tracce viene eseguita sullo stesso thread dove l'attività del codice utente è impostata.  
  
 In generale, le traccie ServiceModel possono essere osservate nelle posizioni seguenti:  
  
-   Se la traccia ServiceModel è disattivata, tutte le tracce emesse vengono visualizzate in attività utente.  Se la propagazione è attivata sul server e sul client, queste tracce si troveranno nella stessa attività.  
  
-   Se la traccia ServiceModel è attivata, ma ActivityTracing è disattivata, le tracce utente verranno visualizzate nella stessa attività, se la propagazione è attivata su entrambe le estremità.  Le tracce ServiceModel si trovano nell'attività 0000 predefinita, a meno che non si verifichino nello stesso thread dell'elaborazione del codice utente in cui l'attività è inizialmente impostata.  
  
-   Se entrambe le tracce ServiceModel e ActivityTracing sono attivate, le traccie dell'utente sono visualizzate in attività definite dall'utente e le traccie ServiceModel sono visualizzate in attività definite da ServiceModel.  La propagazione si verificherà a livello di ServiceModel.