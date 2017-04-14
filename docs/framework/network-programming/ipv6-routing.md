---
title: "Routing IPv6 | Microsoft Docs"
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
ms.assetid: c98731b4-b542-46a2-9947-1cea63c186b2
caps.latest.revision: 4
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 4
---
# Routing IPv6
Un meccanismo flessibile di routing è un vantaggio di IPv6.  A causa della modalità in cui la rete IPv4 ID era e viene allocata, le tabelle di grandi dimensioni di routing devono essere gestite da router che risiedono su dorsali.  Questi router necessario conoscere le route per inoltrare i pacchetti che potenzialmente vengono indirizzati a qualsiasi nodo in Internet.  Con la possibilità di aggregare gli indirizzi, in IPv6 consente l'indicizzazione flessibile e drasticamente riduce la dimensione delle tabelle di routing.  In questa nuova architettura di indicizzazione, deve intermedio di router ne viene tenuta traccia solo la parte locale della rete per inoltrare messaggi in modo appropriato.  
  
## Individuazione adiacenti  
 Alcune delle funzionalità fornite dall'individuazione adiacenti sono:  
  
-   Individuazione di un router.  Ciò consente agli host di identificare i router locali.  
  
-   IP resolution.  Ciò consente ai nodi riconciliazione un indirizzo relativi livello per un indirizzo corrispondente del seguente\- hop \(una sostituzione per ARP \(IP Resolution Protocol\) ARP \[\]\).  
  
-   La configurazione di indirizzo.  In questo modo gli host automaticamente configurare la directory locale e indirizzi globali.  
  
 L'individuazione adiacenti utilizza il protocollo ICMP per i messaggi IPv6 \(ICMPv6\) che includono:  
  
-   Annuncio router.  Inviato da un router in base pseudoperiodica o in risposta a una uno di router.  Annunci router di utilizzo di router IPv6 per annunciare la disponibilità, i prefissi di indirizzo e altri parametri.  
  
-   Uno di router.  Inviato da un host per richiedere che i router sul collegamento di inviare un annuncio router immediatamente.  
  
-   Uno accanto.  Inviato dai nodi per il computer, resolution rilevamento duplicato di un indirizzo, o verificare che un da sia ancora raggiungibile.  
  
-   Annuncio adiacenti.  Inviato dai nodi per rispondere a una uno adiacenti o per notificare gli elementi adiacenti di una modifica nell'indirizzo relativi livello.  
  
-   Reindirizzamento.  Inviato da router per indicare un migliore indirizzo di seguente\- hop a una particolare destinazione per un nodo oggetto mittente.  
  
## Vedere anche  
 [Protocollo IPv6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)