---
title: "Procedura: utilizzare le named pipe per la comunicazione interprocesso in rete | Microsoft Docs"
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
  - "full duplex (comunicazione) [.NET Framework], named pipe"
  - "rappresentazione [.NET Framework], named pipe"
  - "comunicazione basata su messaggi [.NET Compact Framework], named pipe"
  - "più connessioni tramite named pipe"
  - "named pipe [.NET Framework]"
  - "comunicazioni di rete [.NET Framework], named pipe"
  - "pipe [.NET Framework]"
ms.assetid: 4e4d7e64-9f1b-4026-98f7-20488ac7b42b
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: utilizzare le named pipe per la comunicazione interprocesso in rete
Le named pipe forniscono la comunicazione interprocesso tra un server pipe e uno o più client pipe.  Offrono maggiori funzionalità rispetto alle unnamed pipe, che forniscono la comunicazione interprocesso su un computer locale.  Le named pipe supportano la comunicazione full duplex su rete e più istanze server, la comunicazione basata su messaggi e la rappresentazione client, che consente ai processi di connessione di utilizzare il proprio set di autorizzazioni sui server remoti.  
  
 Per implementare le named pipe, utilizzare le classi <xref:System.IO.Pipes.NamedPipeClientStream> e <xref:System.IO.Pipes.NamedPipeServerStream>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come creare una named pipe utilizzando la classe <xref:System.IO.Pipes.NamedPipeServerStream>.  In questo esempio, il processo server crea quattro thread.  Ogni thread può accettare una connessione client.  Il processo client connesso fornisce quindi un nome file al server.  Se il client ha autorizzazioni sufficienti, il processo server apre il file e ne invia il contenuto nuovamente al client.  
  
 [!code-cpp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/vb/program.vb#01)]  
  
## Esempio  
 Nell'esempio che segue viene illustrato il processo client, che utilizza la classe <xref:System.IO.Pipes.NamedPipeClientStream>.  Il client si connette al processo server e invia un nome file al server.  Nell'esempio viene utilizzata la rappresentazione, pertanto l'identità che sta eseguendo l'applicazione client deve disporre dell'autorizzazione per accedere al file.  Il server invia il contenuto del file nuovamente al client.  Il contenuto del file viene quindi visualizzato sulla console.  
  
 [!code-csharp[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/vb/program.vb#01)]  
  
## Programmazione efficiente  
 Si presuppone che i processi client e server in questo esempio siano in esecuzione sullo stesso computer, pertanto il nome del server fornito all'oggetto <xref:System.IO.Pipes.NamedPipeClientStream> è `"."`.  Se i processi client e server fossero su computer separati, `"."` verrebbe sostituito dal nome di rete del computer che esegue il processo server.  
  
## Vedere anche  
 <xref:System.Security.Principal.TokenImpersonationLevel>   
 <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName%2A>   
 [Pipe](../../../docs/standard/io/pipe-operations.md)   
 [Procedura: utilizzare le unnamed pipe per la comunicazione interprocesso locale](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)