---
title: "Procedura: leggere testo da un file | Microsoft Docs"
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
  - "flussi di dati, lettura di testo da file"
  - "I/O [.NET Framework], lettura di testo da file"
  - "lettura di dati, testo (file)"
  - "lettura di file di testo"
  - "flussi, lettura di testo da file"
ms.assetid: ed180baa-dfc6-4c69-a725-46e87edafb27
caps.latest.revision: 23
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 23
---
# Procedura: leggere testo da un file
Negli esempi seguenti viene illustrato come leggere il testo in modo sincrono e in modo asincrono da un file di testo usando .NET per le applicazioni desktop.  In entrambi gli esempi, quando si crea l'istanza della classe <xref:System.IO.StreamReader>, si immette il percorso relativo o assoluto del file.  Negli esempi si presuppone che il file denominato TestFile.txt sia nella stessa cartella dell'applicazione.  
  
 Questi esempi di codice non sono applicabili allo sviluppo di applicazioni Windows Store poiché Windows Runtime offre diversi tipi di flussi che leggono e scrivono sui file.  Per un esempio che illustra come leggere il testo da un file nel contesto di un'app Windows Store, vedere [Guida introduttiva: Lettura e scrittura di file](http://msdn.microsoft.com/library/windows/apps/hh758325.aspx).  Per esempi che illustrano come eseguire la conversione tra i flussi di .NET Framework e flussi di Windows Runtime, vedere [Procedura: eseguire la conversione tra flussi di .NET Framework e flussi di Windows Runtime](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md).  
  
## Esempio  
 Il primo esempio illustra un'operazione di lettura sincrona in un'applicazione console.  In questo esempio viene aperto il file di testo usando un lettore del flusso, il contenuto viene copiato in una stringa, che quindi viene data in output alla console.  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source3.cs#3)]
 [!code-vb[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source3.vb#3)]  
  
## Esempio  
 Nel secondo esempio viene illustrata l'operazione di lettura asincrona in un'applicazione Windows Presentation Foundation \(WPF\).  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source6.cs#6)]
 [!code-vb[Conceptual.BasicIO.TextFiles#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source6.vb#6)]  
  
## Vedere anche  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.File.OpenText%2A?displayProperty=fullName>   
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=fullName>   
 [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md)   
 [NIB: How to: Create a Directory Listing](http://msdn.microsoft.com/it-it/4d2772b1-b991-4532-a8a6-6ef733277e69)   
 [Guida rapida: Lettura e scrittura di file](http://msdn.microsoft.com/library/windows/apps/hh758325.aspx)   
 [Procedura: eseguire la conversione tra flussi di .NET Framework e flussi di Windows Runtime](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)   
 [Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [Procedura: Aprire e accodare un file di log](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [Procedura: Leggere caratteri da una stringa](../../../docs/standard/io/how-to-read-characters-from-a-string.md)   
 [Procedura: Scrivere caratteri in una stringa](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)