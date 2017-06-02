---
title: "Cloud PNRP | Microsoft Docs"
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
ms.assetid: a82e2bf1-62ab-4c2d-83f3-3217a6aead2e
caps.latest.revision: 4
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 4
---
# Cloud PNRP
Un PNRP “cloud„ rappresenta un set di nodi che possono comunicare tramite la rete.  Il termine “cloud„ è sinonimo con “mesh peer„ e “il grafico peer\-to\-peer„.  
  
 La comunicazione tra nodi deve essere sempre contenuta in una stessa area.  Un'istanza di <xref:System.Net.PeerToPeer.Cloud> è identificata in modo univoco in base al proprio nome, che rileva la differenza tra maiuscole e minuscole.  Un determinato peer o nodo può essere connesso a più aree.  
  
 Le aree sono fortemente correlate alle interfacce di rete.  Il caso di un computer multi\-homed con due schede di rete collegato a subnet diverse prevede tre aree: una per ognuno degli indirizzi locali rispetto al collegamento per ogni interfaccia e un'unica area di ambito globale.  
  
 Cloud “ambiti„ di utilizzare tre di PNRP, in cui un ambito è un raggruppamento dei computer che possono cercarsi:  
  
-   Il cloud complessivo corrisponde all'ambito globale di indirizzo IPv6 e agli indirizzi globali e rappresenta tutti i computer nell'intero Internet IPv6.  Esiste un solo cloud globale.  
  
-   Il cloud relativi locale corrisponde a livello di indirizzo IPv6 relativi locale e agli indirizzi relativi locale.  Un cloud relativi locale a un collegamento specifico, che in genere è lo stesso della subnet locale associato.  Possono essere presenti più cloud relativi locale.  
  
 Un terzo cloud, il cloud directory specifica, corrisponde a livello di indirizzo IPv6 del sito e indirizzi di directory locale.  Questo cloud è stato deprecato, sebbene sia supportato in PNRP.  
  
## Cloud  
 I cloud di PNRP sono rappresentati da istanze della classe <xref:System.Net.PeerToPeer.Cloud>.  I gruppi di cloud stato utilizzato un peer sono rappresentati da istanze della classe enumerabile <xref:System.Net.PeerToPeer.CloudCollection>.  Le raccolte di cloud di PNRP noti al peer corrente possono essere ottenute chiamando il metodo <xref:System.Net.PeerToPeer.Cloud.GetAvailableClouds%2A>.  
  
 I singoli cloud abbiano nomi univoci, rappresentati come stringa Unicode a 256 caratteri.  Questi nomi, con l'ambito suddetto, vengono utilizzati per creare istanze univoche tramite classe cloud.  Queste istanze possono essere serializzati e si compila nuovamente per l'utilizzo persistente.  
  
 Un'istanza di tipo cloud viene creata una volta o estratto, i nomi del peer possono essere registrati con per creare una mesh dei peer noti.  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer.Cloud>   
 [Protocollo PNRP \(Peer Name Resolution Protocol\)](../../../docs/framework/network-programming/peer-name-resolution-protocol.md)