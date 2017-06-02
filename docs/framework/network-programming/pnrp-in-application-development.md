---
title: "PNRP nello sviluppo di applicazioni | Microsoft Docs"
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
ms.assetid: 265615d6-4423-4b5d-8626-752e456f4f4e
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# PNRP nello sviluppo di applicazioni
In Windows Vista, le applicazioni di rete possono accedere alle funzioni di pubblicazione e di risoluzione del nome tramite l'api semplificate \(API\) di PNRP.  
  
## Implementare il protocollo peer di risoluzione dei nomi  
 Con il PNRP semplificato API, i cloud non sono specificati in modo esplicito registrare il nome e l'indirizzo, il componente di PNRP determina automaticamente i cloud appropriati per aggiungere e indirizzi per la pubblicazione in di cloud.  
  
 Per la risoluzione dei nomi molto semplificata di PNRP in Windows Vista, i nomi di PNRP sono integrati nella funzione di Windows Sockets di getaddrinfo \(\).  Per utilizzare PNRP per risolvere un nome a un indirizzo IPv6, le applicazioni possono utilizzare la funzione di getaddrinfo \(\) per risolvere il nome di dominio completo \(FQDN\) name.prnp.  rete, in cui nome è il nome che viene risolto.  Il pnrp.  il dominio netto è un dominio riservato in Windows Vista la risoluzione dei nomi di PNRP.  
  
 Il passaggio dei messaggi tra applicazioni peer\-to\-peer viene gestito dalle architetture sottostanti come il canale peer e WCF [grandi dati e flusso](http://go.microsoft.com/fwlink/?LinkID=179652).  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer>