---
title: "Nomi di peer e ID PNRP | Microsoft Docs"
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
ms.assetid: afa538e8-948f-4a98-aa9f-305134004115
caps.latest.revision: 5
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 5
---
# Nomi di peer e ID PNRP
Un nome peer rappresenta un endpoint di comunicazione, che può essere un computer, un utente, un gruppo, un servizio, o qualsiasi elemento associato a un peer che può essere risolto a un indirizzo IPv6.  Il protocollo peer \(PNRP\) di risoluzione dei nomi accetta il nome peer statisticamente univoci per la creazione di un PNRP ID, utilizzato per identificare i membri cloud.  
  
## Nomi del peer  
 I nomi del peer possono essere registrati come non sicuro o essere protetti.  I nomi non sono garantiti solo stringhe di testo che sono soggetti allo spoofing, poiché chiunque può registrare un nome non sicuro duplicato.  I nomi non sono garantiti utilizzati in modo ottimale in reti private o altrimenti protette.  i nomi protetti sono protetti con un certificato e una firma digitale.  Solo l'editore originale sarà possibile provare la proprietà di un nome protetto.  
  
 La combinazione di cloud e di ambito fornisce un ambiente relativamente protetto per i peer che partecipano all'attività di PNRP.  Tuttavia, l'utilizzo di un nome peer protetto non garantisce la sicurezza globale dell'applicazione di rete.  La sicurezza dell'applicazione dipende dall'implementazione.  
  
 I nomi dei membri protetti sono registrati solo dal proprietario e sono protetti mediante la crittografia a chiave pubblica.  Un nome peer protetto è considerato all'entità peer con la chiave privata corrispondente.  La proprietà può essere tentata tramite l'indirizzo peer certificato \(CPA\), che è firmato utilizzando la chiave privata.  Un utente malintenzionato potrebbe non forgiare la proprietà di un nome peer senza la chiave privata corrispondente.  
  
## PNRP ID  
 ![ID PNRP](../../../docs/framework/network-programming/media/fdc9e8a0-4a1c-488d-a019-bc3a1973220c.png "fdc9e8a0\-4a1c\-488d\-a019\-bc3a1973220c")  
  
 PNRP ID sono composti da quanto segue:  
  
-   I 128 bit più significativi, noti come \(P2P\) l'id peer\-to\-peer, sono un hash di un peer nome assegnato all'endpoint.  Il nome peer presenta il formato seguente: *Authority.Classifier*.  Per i nomi protetti, *Autorità* è Secure Hash Algorithm 1 hash \(SHA1\) della chiave pubblica del nome peer in caratteri esadecimali.  Per i nomi non garantisce, *Autorità* è il carattere "0".  *il classificatore* è una stringa che identifica l'applicazione.  Nessun classificatore peer di nome può essere maggiore di 149 caratteri, inclusi il terminatore `null`.  
  
-   I 128 bit meno significativi vengono utilizzati per la posizione del servizio, un numero generato che identifica le istanze diverse dello stesso P2P ID nello stesso cloud.  
  
 Questa combinazione P2P ID e del percorso del servizio consente a più PNRP ID da registrare da un singolo computer.  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer.PeerName>   
 <xref:System.Net.PeerToPeer>