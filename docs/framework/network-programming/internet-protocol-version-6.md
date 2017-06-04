---
title: "Protocollo IPv6 | Microsoft Docs"
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
  - "IPv6, miglioramenti"
  - "IPv4"
  - "IPv6"
  - "protocollo IPv6, miglioramenti"
  - "protocollo IPv6"
ms.assetid: e6fa8ebd-010a-4c48-a5ec-a5102c53c06f
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Protocollo IPv6
La versione 6 \(IPv6\) del protocollo internet è una nuova famiglia di prodotti dei protocolli standard per il livello di rete Internet.  L'oggetto IPv6 è progettato per risolvere molti problemi della versione corrente della famiglia di prodotti del protocollo internet \(nota come l'IPv4\) rispetto a rimozione di un indirizzo, sicurezza, la configurazione, estensibilità, e così via.  L'oggetto IPv6 espandere le funzionalità di Internet abilitare nuovi tipi di applicazioni, incluse le applicazioni peer\-to\-peer e mobili.  Di seguito sono riportati i punti chiave del protocollo corrente IPv4:  
  
-   Rimozione rapido dello spazio degli indirizzi.  
  
     Ciò ha portato all'utilizzo dei traduttori \(NATs\) degli indirizzi di rete gli indirizzi più privati del mapping a un singolo indirizzo IP pubblico.  I problemi principali creati da questo meccanismo stanno sviluppando il sovraccarico e la mancanza di connettività.  
  
-   Mancanza di supporto della gerarchia.  
  
     A causa dell'organizzazione predefinita intrinseca della classe, in IPv4 non dispone di vero supporto gerarchico.  È impossibile per strutturare indirizzi IP in modo che effettivamente esegue il mapping della topologia di rete.  L'errore di progettazione cruciale crea la necessità delle tabelle di grandi dimensioni di routing di fornire pacchetti IPv4 in qualsiasi percorso in Internet.  
  
-   Configurazione di rete complessa.  
  
     All'IPv4, gli indirizzi devono essere assegnati in modo statico o tramite un protocollo di configurazione come DHCP.  In una situazione ideale, gli host non basarsi sull'amministrazione di un'infrastruttura di DHCP.  Invece, possono configurarsi in base al segmento di rete in cui si trovano.  
  
-   Mancanza di autenticazione incorporata e di riservatezza.  
  
     Il IPv4 non richiede il supporto per un meccanismo che fornisce l'autenticazione o la crittografia dei dati scambiati.  Questo modifiche all'IPv6.  Internet Protocol Security di Crittografia\) è un requisito di supporto IPv6.  
  
 Una nuova famiglia di prodotti di protocollo deve soddisfare i seguenti requisiti:  
  
-   Routing e indici su larga scala con il sovraccarico ridotto.  
  
-   La configurazione in diverse situazioni connettersi.  
  
-   L'autenticazione incorporata e riservatezza.  
  
 Per ulteriori informazioni, vedere [Indirizzamento IPv6](../../../docs/framework/network-programming/ipv6-addressing.md), [Routing IPv6](../../../docs/framework/network-programming/ipv6-routing.md), [Configurazione automatica di IPv6](../../../docs/framework/network-programming/ipv6-auto-configuration.md), [Abilitazione e disabilitazione di IPv6](../../../docs/framework/network-programming/enabling-and-disabling-ipv6.md) e [Procedura: Modificare il file di configurazione del computer per abilitare il supporto IPv6](../../../docs/framework/network-programming/how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md).  
  
## Riferimenti  
 Di seguito sono documenti selezionati RFC disponibile nel sito Internet Engineering Task Force \([http:\/\/www.ietf.org](http://www.ietf.org/)\):  
  
-   Lo standard RFC 1287, all'architettura futura Internet.  
  
-   Lo standard RFC 1454, confronto di proposte di versione successiva di IP.  
  
-   Lo standard RFC 2373, l'architettura il routing di ASP.NET versione 6 IP.  
  
-   Lo standard RFC 2374, un formato di indirizzo unicast globale aggregabile IPv6.  
  
 È inoltre possibile trovare informazioni su IPv6\-related su [Area IPv6 su Technet](http://go.microsoft.com/fwlink/?LinkID=179658).  
  
## Vedere anche  
 [Esempio di socket IPv6](http://go.microsoft.com/fwlink/?LinkID=179568)   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)