---
title: "Procedura: utilizzare le unnamed pipe per la comunicazione interprocesso locale | Microsoft Docs"
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
  - "pipe anonime [.NET Framework]"
  - "comunicazione con il computer locale [.NET Framework], pipe"
  - "comunicazione unidirezionale [.NET Framework]"
  - "comunicazione padre-figlio [.NET Framework]"
  - "pipe [.NET Framework]"
ms.assetid: e7773c77-c646-4a01-8a96-a003d59fc4c9
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: utilizzare le unnamed pipe per la comunicazione interprocesso locale
Le unnamed pipe forniscono la comunicazione interprocesso su un computer locale.  Esse offrono meno funzionalità rispetto alle named pipe ma richiedono anche meno overhead.  È possibile utilizzarle per agevolare la comunicazione interprocesso su un computer locale.  Non è possibile utilizzare le unnamed pipe per la comunicazione in una rete.  
  
 Per implementare le pipe anonime, utilizzare le classi <xref:System.IO.Pipes.AnonymousPipeClientStream> e <xref:System.IO.Pipes.AnonymousPipeServerStream>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una modalità per inviare una stringa da un processo padre a un processo figlio utilizzando le unnamed pipe.  Viene creato un oggetto <xref:System.IO.Pipes.AnonymousPipeServerStream> in un processo padre con un valore <xref:System.IO.Pipes.PipeDirection> di <xref:System.IO.Pipes.PipeDirection>.  Il processo padre crea quindi un processo figlio utilizzando un handle del client per creare un oggetto <xref:System.IO.Pipes.AnonymousPipeClientStream>.  Il processo figlio ha un valore <xref:System.IO.Pipes.PipeDirection> di <xref:System.IO.Pipes.PipeDirection>.  
  
 Il processo padre invia quindi una stringa fornita dall'utente al processo figlio.  La stringa viene visualizzata nella console del processo figlio.  
  
 Nell'esempio riportato di seguito viene illustrato un processo server.  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/vb/program.vb#01)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato un processo client.  Il processo server avvia il processo client e lo passa all'handle del client.  Il file eseguibile risultante dal codice client deve essere denominato `pipeClient.exe` e copiato alla stessa directory del file eseguibile del server prima di eseguire il processo server.  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/vb/program.vb#01)]  
  
## Vedere anche  
 [Pipe](../../../docs/standard/io/pipe-operations.md)   
 [Procedura: utilizzare le named pipe per la comunicazione interprocesso in rete](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)