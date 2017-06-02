---
title: "Autorizzazioni Web e socket | Microsoft Docs"
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
  - "Servizi di rete"
  - "posizioni [.NET Framework], accettazione"
  - "socket, autorizzazioni"
  - "rete, autorizzazioni"
  - "Internet, autorizzazioni"
  - "Risorse di rete"
  - "SocketPermission (classe), informazioni"
  - "posizioni [.NET Framework], connessione"
  - "WebPermission (classe), informazioni"
  - "autorizzazioni [.NET Framework], socket"
  - "sicurezza [.NET Framework], Internet"
  - "posizioni [.NET Framework], concessione"
ms.assetid: d51ad8cb-03ae-4a51-bfcd-cfcf6b98afa9
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Autorizzazioni Web e socket
La sicurezza Internet per le applicazioni tramite lo spazio dei nomi <xref:System.Net> viene fornita dalle classi <xref:System.Net.SocketPermission> e <xref:System.Net.WebPermission>.  La classe **WebPermission** controlla la destra di un'applicazione ai dati della richiesta da un URI o utilizzare un URI a Internet.  La classe **SocketPermission** controlla la destra di un'applicazione utilizzare <xref:System.Net.Sockets.Socket> per accettare i dati su una porta locale oppure contattare i dispositivi remoti utilizzando un protocollo di trasporto a un altro indirizzo, in base all'host, al numero di porta e il protocollo di trasporto di socket.  
  
 La classe di autorizzazioni dipende dal tipo di applicazione.  Le applicazioni che utilizzano <xref:System.Net.WebRequest> e i relativi discendenti devono utilizzare la classe **WebPermission** per gestire le autorizzazioni.  Le applicazioni che utilizzano l'accesso a livello di socket dovrebbero utilizzare la classe **SocketPermission** per gestire le autorizzazioni.  
  
 **WebPermission** e **SocketPermission** definiscono due autorizzazioni: accettare e connettersi.  Accettare le concessioni l'applicazione la destra rispondere a una connessione in ingresso da un'altra parte.  Connettere le autorizza l'applicazione a destra avviare una connessione a un'altra parte.  
  
 Per le istanze **SocketPermission**, accettare significa che un'applicazione possa accettare connessioni in ingresso in un indirizzo di trasporto locale, connettersi indica che un'applicazione può connettersi a un indirizzo di trasporto remoto \(o locale\).  
  
 Per le istanze **WebPermission**, accettare indica che un'applicazione possibile esportare l'uri controllato da **WebPermission** in tutto il mondo, connettersi indica che un'applicazione può accedere a un URI \(se è remota o locale\).  
  
## Vedere anche  
 [Security](../../../docs/standard/security/index.md)   
 [Sicurezza in programmazione di rete](../../../docs/framework/network-programming/security-in-network-programming.md)