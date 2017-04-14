---
title: "Socket | Microsoft Docs"
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
  - "protocolli applicativi, socket"
  - "invio di dati, socket"
  - "richieste dati, socket"
  - "Windows Sockets"
  - "socket, informazioni sui socket"
  - "Socket (classe), informazioni"
  - "socket"
  - "richiesta di dati da Internet, socket"
  - "rete, socket"
  - "ricezione di dati, socket"
  - "protocolli, socket"
  - "Internet, socket"
ms.assetid: 10d22735-bd37-42c1-a2be-c1932f979a7d
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Socket
Lo spazio dei nomi <xref:System.Net.Sockets> contiene un'implementazione gestita dell'interfaccia Windows Sockets.  Tutte le altre classi di accesso alla rete nello spazio dei nomi <xref:System.Net> vengono compilate questa implementazione di socket.  
  
 La classe di .NET Framework <xref:System.Net.Sockets.Socket> è una versione di codice gestito i servizi di socket forniti da Winsock32 API.  Nella maggior parte dei casi, i metodi della classe **Socket** esegue il marshalling semplicemente i dati nelle rispettive controparti Win32 native e gestire tutti i controlli di sicurezza necessarie.  
  
 La classe **Socket** supporta due modalità di base, sincrono e asincrono.  In modalità sincrona, le chiamate alle funzioni che eseguono operazioni di rete \(ad esempio <xref:System.Net.Sockets.Socket.Send%2A> e <xref:System.Net.Sockets.Socket.Receive%2A>\) attende che l'operazione non termina prima di restituire il controllo al programma chiamante.  In modalità asincrona, queste chiamate restituisce immediatamente.  
  
## Vedere anche  
 [Procedura: Creare un socket](../../../docs/framework/network-programming/how-to-create-a-socket.md)   
 [TCP\/UDP](../../../docs/framework/network-programming/tcp-udp.md)   
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)