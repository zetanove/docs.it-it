---
title: "Indirizzamento IPv6 | Microsoft Docs"
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
helpviewer_keywords: 
  - "protocollo IPv6, indirizzi in"
  - "Individuazione router adiacenti"
  - "IPv6, abilitazione"
  - "IPv6, mobilità e"
  - "protocollo IPv6, indirizzi anycast"
  - "IPv6, individuazione router adiacenti"
  - "protocollo IPv6, configurazione automatica"
  - "protocollo IPv6, abilitazione"
  - "IPv6, indirizzi unicast"
  - "IPv6, configurazione automatica"
  - "protocollo IPv6, routing"
  - "IPv6, documenti RFC"
  - "IPv6, routing"
  - "protocollo IPv6, disabilitazione"
  - "protocollo IPv6, indirizzi unicast"
  - "IPv6, indirizzi multicast"
  - "protocollo IPv6, mobilità e"
  - "protocollo IPv6, documenti RFC"
  - "protocollo IPv6, individuazione router adiacenti"
  - "IPv6, indirizzi anycast"
  - "protocollo IPv6, indirizzi multicast"
  - "IPv6, indirizzi in"
  - "IPv6, disabilitazione"
ms.assetid: 20a104ae-1649-4649-a005-531a5cf74c93
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Indirizzamento IPv6
Nella versione 6 \(IPv6\) del protocollo internet, gli indirizzi sono lunga 128 bit.  Un motivo per così elevato spazio degli indirizzi è di dividere gli indirizzi disponibili in una gerarchia di domini di routing che riflettono la topologia Internet.  Un altro motivo è necessario eseguire il mapping degli indirizzi delle schede di rete \(o un'interfaccia\) che collegano i dispositivi alla rete.  L'oggetto IPv6 è disponibile una funzionalità inerente risolvere gli indirizzi al livello inferiore, che è il livello di rete e dispone anche di funzionalità della configurazione.  
  
## Rappresentazione di testo  
 Di seguito sono riportati i tre forme convenzionali utilizzati per rappresentare gli indirizzi IPv6 come stringhe di testo:  
  
-   **Colon\-hexadecimal form**.  Si tratta del form desiderato n: n: n: n: n: n: n: n.  Ogni n rappresenta il valore esadecimale di uno degli otto elementi a 16 bit degli indirizzi.  Ad esempio: `3FFE:FFFF:7654:FEDA:1245:BA98:3210:4562`.  
  
-   **Compressed form**.  A causa della lunghezza di indirizzo, è normale che indirizzi che contengono una lunga serie di zeri.  Per semplificare la scrittura degli indirizzi, utilizzare la forma appiattito, in cui una sola sequenza contigua di 0 blocchi è rappresentata da un segno di due punti doppi \(::\).  Questo simbolo può apparire solo una volta in un indirizzo.  Ad esempio, l'indirizzo multicast `FFED:0:0:0:0:BA98:3210:4562` in formato appiattito è `FFED::BA98:3210:4562`.  L'indirizzo unicast `3FFE:FFFF:0:0:8:800:20C4:0` in formato appiattito è `3FFE:FFFF::8:800:20C4:0`.  L'indirizzo di loopback `0:0:0:0:0:0:0:1` in formato appiattito è `::`1.  L'indirizzo non specificato `0:0:0:0:0:0:0:0` in formato appiattito è `::`.  
  
-   **Mixed form**.  Questo form combina gli indirizzi IPv6 e di IPv4.  In questo caso, il formato di indirizzo è più livelli: n: n: n: n: n: d.d.d.d, dove ogni n rappresenta i valori esadecimali dei sei elementi più significativi di indirizzi a 16 bit IPv6 e ogni d rappresenta il valore decimale di un indirizzo IPv4.  
  
## Tipi di indirizzo  
 I bit iniziali l'indirizzo definiscono il tipo specifico di indirizzo IPv6.  Il campo di lunghezza variabile contenente questi bit iniziali viene chiamato un prefisso \(FP\) di formato.  
  
 Un indirizzo unicast IPv6 in due parti.  La prima parte contiene il prefisso di indirizzo e la seconda parte contiene l'identificatore dell'interfaccia.  Una modalità concisa esprimere un indirizzo IPv6\/combinazione di prefisso è la seguente: ipv6\-address\/prefisso lunghezza.  
  
 L'esempio seguente è un esempio di un indirizzo con un prefisso a 64 bit.  
  
 `3FFE:FFFF:0:CD30:0:0:0:0/64`.  
  
 Il prefisso in questo esempio viene `3FFE:FFFF:0:CD30`.  L'indirizzo potrebbe anche essere scritto in un form appiattito, come `3FFE:FFFF:0:CD30::/64`.  
  
 L'oggetto IPv6 definisce i seguenti tipi di indirizzo:  
  
-   **Unicast address**.  Un identificatore per una singola interfaccia.  Un pacchetto inviato a questo indirizzo viene recapitato all'interfaccia identificata.  Gli indirizzi unicast sono distinti dagli indirizzi multicast dall'ottetto più significativo.  Il ottetto più significativo degli indirizzi multicast ha il valore esadecimale FF.  Qualsiasi altro valore per questo ottetto identifica un indirizzo unicast.  Di seguito sono tipi diversi degli indirizzi unicast:  
  
    -   **Link\-local addresses**.  Gli indirizzi utilizzati in un singolo collegamento e hanno il seguente formato: FE80::*InterfaceID*.  Gli indirizzi relativi locale vengono utilizzati tra i nodi su un collegamento per la configurazione automatica di indirizzo, l'individuazione adiacenti, o quando non sono presenti router.  Un indirizzo relativi locale viene utilizzato principalmente all'avvio e quando il sistema non ha ancora acquisito gli indirizzi di un ambito più ampio.  
  
    -   **Site\-local addresses**.  Gli indirizzi utilizzati in un singolo sito e hanno il seguente formato: FEC0::*SubnetID*:*InterfaceID*.  Gli indirizzi di directory locale vengono utilizzati per risolvere in un sito senza la necessità di un prefisso globale.  
  
    -   **Global IPv6 unicast addresses**.  Gli indirizzi possono essere utilizzati tramite Internet e avere il formato seguente: 010 \(FP, 3 bit\) il TLA L'ID \(13 bit\) è riservato \(8 bit\) contratto di servizio L'ID \(16 bit\) *InterfaceID* \(64 bit\) di NLA L'ID \(24 bit\).  
  
-   **Multicast address**.  Un identificatore per un set di interfacce \(in genere che appartengono ai nodi diversi\).  Un pacchetto inviato a questo indirizzo viene recapitato a tutte le interfacce identificate dall'indirizzo.  I tipi di indirizzo multicast sostituiscono gli indirizzi broadcast IPv4.  
  
-   **Anycast address**.  Un identificatore per un set di interfacce \(in genere che appartengono ai nodi diversi\).  Un pacchetto inviato a questo indirizzo viene recapitato a una sola interfaccia identificata dall'indirizzo.  Si tratta dell'interfaccia più vicina identificata come destinazione la metrica.  Gli indirizzi di Anycast derivano dallo spazio degli indirizzi unicast e non siano sintatticamente distinguibili.  L'interfaccia indirizzata esegue la distinzione tra unicast e indirizzi del anycast in funzione della configurazione.  
  
 Un nodo generalmente ha sempre un indirizzo relativi locale.  Potrebbe avere un indirizzo di directory locale e uno o più indirizzi globali.  
  
## Vedere anche  
 [Protocollo IPv6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)