---
title: "Collaborazione peer-to-peer | Microsoft Docs"
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
ms.assetid: b6216d88-bccb-4a59-9f1c-9f751708e811
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Collaborazione peer-to-peer
La rete peer\-to\-peer è l'utilizzo dei computer relativamente potenti \(PC\) che esistono al bordo Internet per oltre alle attività di elaborazione basate su client.  \(PC\) Con personale moderno computer è un processore più veloce, molto diverse memoria e di un disco rigido, nessuno dei quali sono completamente utilizzandi durante il comune che calcola attività quali la posta elettronica e esplorazione del web.  Il PC moderno può essere utilizzato come client e server \(un peer\) per molti tipi di applicazioni.  
  
-   L'infrastruttura peer\-to\-peer di collaborazione è un'implementazione semplificata dell'infrastruttura peer\-to\-peer Microsoft Windows utilizzando le persone dall'utente servizio in Windows Vista e piattaforme successive.  Viene utilizzata più appropriato per le applicazioni peer\-interno di un subnet per il quale gli utenti dall'utente che viene eseguito il servizio, anche se può assistere gli endpoint o i contatti Internet anche.  Incorpora l'amministratore del contatto comune utilizzato da Live Messenger e da altre applicazioni attivo con determinare gli endpoint, disponibilità e la presenza contatto.  
  
## Applicazioni di collaborazione  
 Un'applicazione tipica peer\-to\-peer di collaborazione comprende i passaggi seguenti:  
  
-   Il peer determinare l'identità di un peer che è interessati all'hosting di una sessione di collaborazione  
  
-   Una richiesta di ospitare una sessione viene inviata, in qualche modo e il peer host acconsente per gestire l'attività di collaborazione.  
  
-   L'host invita i contatti nel richiedente subnet \(inclusi\) a una sessione.  
  
-   Tutti i peer che desiderano collaborare possono aggiungere l'host agli amministratori del contatto.  
  
-   La maggior parte dei peer invieranno le risposte a invito, se accettato o rifiutato in modo tempestivo, del peer host.  
  
-   Tutti i peer che desiderano collaborare sottoscriveranno al peer host.  
  
-   Mentre i peer eseguono le loro attività iniziale della collaborazione, il peer host può aggiungere i peer remoti all'amministratore del contatto.  Anche tutte le risposte a invito per determinare chi ha accettato, che ha rifiutato e che non ha risposto.  Consente di annullare gli richiedere a chi non ha risposto, o eseguire un'altra attività.  
  
-   In questa fase, il peer host può avviare una sessione di collaborazione con tutti i peer invitati, oppure registrare un'applicazione con l'infrastruttura di collaborazione.  Le applicazioni P2P viene utilizzata l'infrastruttura peer\-to\-peer di collaborazione e lo spazio dei nomi <xref:System.Net.PeerToPeer.Collaboration> per coordinare le comunicazioni per giochi, gli albi, la comunicazione con altre applicazioni serverless presenza di.  
  
## Sicurezza peer\-to\-peer di rete  
 In un dominio Active Directory, i controller di dominio forniscono servizi di autenticazione utilizzando Kerberos.  In un ambiente peer serverless, i peer devono fornire la propria autenticazione.  Per rete peer\-to\-peer, qualsiasi nodo può fungere da CA, rimuovendo il requisito di un certificato radice nell'archivio delle fonti attendibili di ogni peer.  L'autenticazione è fornita mediante certificati autofirmati, formattati come certificati X.509.  Si tratta di certificati creati da ciascun peer, che genera una coppia di chiavi pubblica\/privata di chiave pubblica e il certificato che è firmato utilizzando la chiave privata.  Il certificato autofirmato viene utilizzato per l'autenticazione e fornire informazioni sull'entità peer.  Come autenticazione X.509, l'autenticazione peer di rete conta in una catena di certificati di traccia a una chiave pubblica considerato attendibile.  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer.Collaboration>   
 [Informazioni sullo spazio dei nomi System.Net.PeerToPeer.Collaboration](../../../docs/framework/network-programming/about-the-system-net-peertopeer-collaboration-namespace.md)