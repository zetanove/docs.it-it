---
title: "Operazioni pipe in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pipe [.NET Framework]"
  - "pipe (operazioni) [.NET Framework]"
  - "comunicazione interprocesso [.NET Framework], pipe"
  - "I/O [.NET Framework], pipe"
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Operazioni pipe in .NET Framework
Le pipe forniscono un mezzo per la comunicazione interprocesso.  Esistono due tipi di pipe:  
  
-   Unnamed pipe.  
  
     Le unnamed pipe forniscono la comunicazione interprocesso su un computer locale.  Richiedono meno sovraccarico delle named pipe ma offrono servizi limitati.  Le unnamed pipe sono unidirezionali e non possono essere utilizzate su una rete.  Supportano solo una singola istanza del server.  Sono utili per la comunicazione tra thread o tra processi padre e figlio dove gli handle della pipe possono essere passati facilmente al processo figlio quando viene creato.  
  
     In .NET Framework le unnamed pipe vengono implementate utilizzando le classi <xref:System.IO.Pipes.AnonymousPipeClientStream> e <xref:System.IO.Pipes.AnonymousPipeServerStream>.  
  
     Vedere [Procedura: utilizzare le unnamed pipe per la comunicazione interprocesso locale](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md).  
  
-   Named pipe.  
  
     Le named pipe forniscono la comunicazione interprocesso tra un server pipe e uno o più client pipe.  Le named pipe possono essere unidirezionali o duplex.  Supportano la comunicazione basata su messaggi e consentono a più client di connettersi simultaneamente al processo server utilizzando lo stesso nome di pipe.  Supportano inoltre la rappresentazione, che consente ai processi di connessione di utilizzare le proprie autorizzazioni sui server remoti.  
  
     In .NET Framework, le named pipe vengono implementate utilizzando le classi <xref:System.IO.Pipes.NamedPipeClientStream> e <xref:System.IO.Pipes.NamedPipeServerStream>.  
  
     Vedere [Procedura: utilizzare le named pipe per la comunicazione interprocesso in rete](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md).  
  
## Vedere anche  
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)   
 [Procedura: utilizzare le unnamed pipe per la comunicazione interprocesso locale](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)   
 [Procedura: utilizzare le named pipe per la comunicazione interprocesso in rete](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)