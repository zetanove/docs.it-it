---
title: "Composizione dei flussi | Microsoft Docs"
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
  - "flussi, flussi di base"
  - "I/O [.NET Framework], composizione di flussi"
  - "Stream (classe), composizione di flussi"
  - "flussi di base"
  - "flussi, archivi di backup"
ms.assetid: da761658-a535-4f26-a452-b30df47f73d5
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# Composizione dei flussi
Un archivio di backup è un supporto di archiviazione, quale un disco o una memoria.  Il flusso di ciascun archivio di backup è costituito da un'implementazione della classe <xref:System.IO.Stream>.  Ogni tipo di flusso legge e scrive byte nel proprio archivio di backup.  I flussi connessi ad archivi di backup vengono definiti flussi di base.  I flussi di base presentano costruttori che accettano i parametri che consentono di connettere il flusso all'archivio di backup.  <xref:System.IO.FileStream> prevede, ad esempio, costruttori che specificano un parametro di percorso che indica il modo in cui il file verrà condiviso dai processi e così via.  
  
 Il principio di funzionamento delle classi <xref:System.IO> consente di comporre i flussi in modo ancora più semplice.  I flussi di base possono essere connessi a uno o più flussi intermedi da cui viene fornita la funzionalità desiderata.  La connessione di un visualizzatore o di un writer alla fine della catena consente di leggere o scrivere facilmente i tipi desiderati.  
  
 Nell'esempio di codice riportato di seguito viene creato un **FileStream** per inserire nel buffer il file `MyFile.txt` esistente. Si noti che i **FileStreams** vengono sottoposti a buffering per impostazione predefinita. Viene quindi creato un <xref:System.IO.StreamReader> per leggere caratteri dal **FileStream**, che viene passato allo **StreamReader** come argomento del costruttore.  <xref:System.IO.StreamReader.ReadLine%2A> legge fino a quando <xref:System.IO.StreamReader.Peek%2A> non trova più caratteri.  
  
 [!code-cpp[System.IO.StreamReader#20](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source2.cpp#20)]
 [!code-csharp[System.IO.StreamReader#20](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source2.cs#20)]
 [!code-vb[System.IO.StreamReader#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source2.vb#20)]  
  
 Nell'esempio di codice riportato di seguito viene creato un **FileStream** per inserire nel buffer il file `MyFile.txt` esistente. Si noti che i **FileStreams** vengono sottoposti a buffering per impostazione predefinita. Viene quindi creato un **BinaryReader** per leggere byte dal **FileStream**, che viene passato allo **StreamReader** come argomento del costruttore.  <xref:System.IO.BinaryReader.ReadByte%2A> legge fino a quando <xref:System.IO.BinaryReader.PeekChar%2A> non trova più byte.  
  
 [!code-cpp[System.IO.StreamReader#21](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source3.cpp#21)]
 [!code-csharp[System.IO.StreamReader#21](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source3.cs#21)]
 [!code-vb[System.IO.StreamReader#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source3.vb#21)]  
  
## Vedere anche  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=fullName>   
 <xref:System.IO.StreamReader.Peek%2A?displayProperty=fullName>   
 <xref:System.IO.FileStream>   
 <xref:System.IO.BinaryReader>   
 <xref:System.IO.BinaryReader.ReadByte%2A?displayProperty=fullName>   
 <xref:System.IO.BinaryReader.PeekChar%2A?displayProperty=fullName>