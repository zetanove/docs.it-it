---
title: "TCP/UDP | Microsoft Docs"
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
  - "protocolli, TCP/UDP"
  - "risorse di rete, TCP/UDP"
  - "invio di dati, TCP/UDP"
  - "TCP/UDP"
  - "TcpClient (classe), informazioni"
  - "protocolli applicativi, TCP/UDP"
  - "ricezione di dati, TCP/UDP"
  - "TcpListener (classe), informazioni"
  - "Socket (classe), informazioni"
  - "UDP"
  - "richieste di dati, TCP/UDP"
  - "richiesta di dati da Internet, TCP/UDP"
  - "Internet, TCP/UDP"
ms.assetid: df29b4b0-49e8-4923-82b9-13150dfc40f5
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# TCP/UDP
Le applicazioni possono utilizzare servizi \(UDP\) di protocollo TCP \(TCP\) e di User Datagram Protocol\) con <xref:System.Net.Sockets.TcpClient>, <xref:System.Net.Sockets.TcpListener>e le classi <xref:System.Net.Sockets.UdpClient>.  Queste classi di protocollo si basano sulla classe <xref:System.Net.Sockets.Socket?displayProperty=fullName> e accettano la visualizzazione dei dettagli del trasferimento di dati.  
  
 Le classi di protocollo utilizzano i metodi sincroni della classe **Socket** per fornire l'accesso semplice e chiaro servizi di rete senza il sovraccarico di gestione delle informazioni sullo stato o di conoscere i dettagli di installazione sockets protocollo specifici.  Per utilizzare metodi asincroni di **Socket**, è possibile utilizzare i metodi asincroni forniti dalla classe <xref:System.Net.Sockets.NetworkStream>.  Per accedere alle funzionalità **Socket** classe non esposta dalle classi di protocollo, è necessario utilizzare la classe **Socket**.  
  
 **TcpClient** e **TcpListener** rappresentano la rete utilizzando la classe **NetworkStream**.  Utilizzare il metodo <xref:System.Net.Sockets.TcpClient.GetStream%2A> per restituire il flusso di rete e quindi chiamare i metodi <xref:System.Net.Sockets.NetworkStream.Read%2A> e <xref:System.Net.Sockets.NetworkStream.Write%2A> del flusso.  **NetworkStream** non possiede un socket sottostante di classi del protocollo, quindi chiudere lo non influisce su socket.  
  
 La classe **UdpClient** utilizza una matrice di byte per utilizzare il datagram di UDP.  Utilizzare il metodo <xref:System.Net.Sockets.UdpClient.Send%2A> per inviare i dati alla rete e il metodo <xref:System.Net.Sockets.UdpClient.Receive%2A> per ricevere un datagram in ingresso.  
  
## Vedere anche  
 [Uso dei servizi TCP](../../../docs/framework/network-programming/using-tcp-services.md)   
 [Uso dei servizi UDP](../../../docs/framework/network-programming/using-udp-services.md)   
 [Uso di flussi nella rete](../../../docs/framework/network-programming/using-streams-on-the-network.md)   
 [Uso di un socket server asincrono](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)   
 [Uso di un socket client asincrono](../../../docs/framework/network-programming/using-an-asynchronous-client-socket.md)   
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)