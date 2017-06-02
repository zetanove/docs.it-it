---
title: "Informazioni sullo spazio dei nomi System.Net.PeerToPeer.Collaboration | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b5d8c1c1-6844-4947-9759-c7f1b564bded
caps.latest.revision: 4
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 4
---
# Informazioni sullo spazio dei nomi System.Net.PeerToPeer.Collaboration
Lo spazio dei nomi <xref:System.Net.PeerToPeer.Collaboration> fornisce classi e interfacce API utilizzati per distribuire le attività peer di collaborazione utilizzando l'infrastruttura peer\-to\-peer di collaborazione.  
  
## Classi  
 Le classi principali utilizzate nell'implementazione di un'attività peer\-to\-peer di collaborazione sono:  
  
-   <xref:System.Net.PeerToPeer.Collaboration.ContactManager>, che possono essere utilizzati per archiviare i contatti peer.  
  
-   <xref:System.Net.PeerToPeer.Collaboration.PeerApplication> in cui collaborare, ad esempio un gioco, un client di chat, o una soluzione di comunicazione.  
  
-   I peer che collaboreranno a un'attività.  Questi membri possono essere rappresentati come <xref:System.Net.PeerToPeer.Collaboration.PeerContact>, <xref:System.Net.PeerToPeer.Collaboration.PeerNearMe>, oppure oggetti <xref:System.Net.PeerToPeer.Collaboration.PeerEndPoint>.  
  
-   La classe statica stessa <xref:System.Net.PeerToPeer.Collaboration.PeerCollaboration>, che specifica quali applicazioni sono disponibili e i peer partecipano essi.  
  
 I metodi <xref:System.Net.PeerToPeer.Collaboration.PeerContact.Invite%2A> vengono utilizzati per richiedere i peer in una sessione di collaborazione.  Un peer chiamante può sottoscrivere un altro peer per gli eventi che il segnale aggiornaapplicazione, all'oggetto, o alle informazioni di presenza affiliate con la sessione di collaborazione.  Le classi presenza di specificare se <xref:System.Net.PeerToPeer.Collaboration.Peer> è disponibile per la collaborazione e la classe <xref:System.Net.PeerToPeer.Collaboration.PeerScope> viene utilizzata per specificare quanta partecipazione è consentita per un peer: <xref:System.Net.PeerToPeer.Collaboration.PeerScope> \(globale\), <xref:System.Net.PeerToPeer.Collaboration.PeerScope>subnet, \(\) o <xref:System.Net.PeerToPeer.Collaboration.PeerScope>.  
  
 Una sessione di collaborazione comprende quattro passaggi:  
  
-   Individuazione.  Individuare o pubblicare applicazioni, i peer e le informazioni di presenza.  Ad esempio, individuare altri utenti sulla subnet locale che esegue gli stessi installare giochi.  
  
-   Invito.  Inviare e accettare gli richiedere sicuri per i peer remoti l'avvio o a far parte delle sessioni <xref:System.Net.PeerToPeer.Collaboration.PeerCollaboration>.  
  
-   Contattare la gestione.  Aggiungere ha individuato i peer come contatto a <xref:System.Net.PeerToPeer.Collaboration.ContactManager>.  
  
-   Comunicazione.  Quando la comunicazione viene stabilita, utilizzare <xref:System.Net> API, <xref:System.Net.PeerToPeer> API, o il canale peer di Windows Communication Foundation le classi per le comunicazioni pluripartitiche.  
  
 Ad esempio, il peer host avvia una sessione di collaborazione e utilizza il metodo <xref:System.Net.PeerToPeer.Collaboration.ContactManager.CreateContact%2A> per aggiungere un peer remoti e i peer locali all'amministratore del contatto del peer host.  I tre utenti quindi prenderanno parte alla propria sessione privata di collaborazione.  
  
 Le applicazioni P2P tipiche sono: teleconferenze per la NOTA\- rimozione o whiteboarding di collaborazione, le applicazioni chat serverless, gli annunci interattivi e le sessioni online di gioco.  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer.Collaboration>