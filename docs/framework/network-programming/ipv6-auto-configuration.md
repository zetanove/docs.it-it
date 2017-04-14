---
title: "Configurazione automatica di IPv6 | Microsoft Docs"
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
ms.assetid: 581c1d21-1013-43a3-bf3e-2d9ead62b79c
caps.latest.revision: 5
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 5
---
# Configurazione automatica di IPv6
Un obiettivo importante di l IPv6 è maggiore del plug e play il nodo.  Ovvero deve essere possibile inserire un nodo una rete IPv6 e farvi configurare automaticamente senza l'intervento umano.  
  
## Tipo di Configurazione automatica  
 L'oggetto IPv6 supporta i seguenti tipi di automatica configurazioni:  
  
-   **Stateful auto\-configuration**.  Questo tipo di configurazione richiede un determinato livello dell'intervento umano perché è necessario un DHCP per il server IPv6 \(DHCPv6\) per l'installazione e l'amministrazione di nodi.  Il server DHCPv6 mantiene un elenco di nodi che fornisce le informazioni di configurazione.  Anche gestisce le informazioni sullo stato in modo che il server è la durata di ogni indirizzo viene utilizzato e quando potrebbe essere disponibile per la nuova assegnazione.  
  
-   **Stateless auto\-configuration**.  Questo tipo di configurazione è appropriato per piccole organizzazioni e gli utenti.  In questo caso, ogni host determina gli indirizzi del contenuto degli annunci router ricevuti.  Mediante il provider standard IEEE EUI\-64 per definire parte della rete dell'indirizzo, infatti assumere l'univocità del computer host sul collegamento.  
  
 Indipendentemente da come indirizzo viene determinato, il nodo deve verificare che il relativo indirizzo potenziale sia univoco al collegamento locale.  Questa operazione viene eseguita inviando un messaggio adiacenti in uno all'indirizzo potenziale.  Se il nodo riceve una risposta, saprà che l'indirizzo è già utilizzato e deve determinare un altro indirizzo.  
  
## Mobilità IPv6  
 La proliferazione di dispositivi mobili è stato introdotto un nuovo requisito: Un dispositivo deve essere in grado di modificare arbitrario le posizioni su Internet IPv6 e di gestire le connessioni esistenti.  Per fornire questa funzionalità, un nodo mobile è assegnato un indirizzo di gestione che può essere raggiunto sempre.  Quando il nodo mobile è da casa, si connette al collegamento della home page e utilizza il relativo indirizzo del cane.  Quando il nodo mobile è esterno a gestione, un agente home, in genere un router, messaggi di inoltro tra il nodo mobile e nodi con cui vengono passate.  
  
## Vedere anche  
 [Protocollo IPv6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)