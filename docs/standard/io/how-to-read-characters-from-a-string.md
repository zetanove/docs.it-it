---
title: "Procedura: Leggere caratteri da una stringa | Microsoft Docs"
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
  - "lettura di caratteri da stringhe"
  - "flussi di dati, lettura di caratteri dalle stringhe"
  - "I/O [.NET Framework], lettura di caratteri dalle stringhe"
  - "lettura di dati, stringhe"
  - "flussi, lettura di caratteri dalle stringhe"
ms.assetid: 27ea5e52-6db8-42d8-980a-50bcfc7fd270
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: Leggere caratteri da una stringa
Gli esempi di codice seguenti illustrano come leggere i caratteri in modo sincrono e in modo asincrono da una stringa.  
  
## Esempio  
 In questo esempio vengono letti 13 caratteri in modo sincrono da una stringa, li archivia in un array e visualizza tali caratteri.  Quindi legge i caratteri rimanenti della stringa, li archivia nell'array iniziando dal sesto elemento e visualizza il contenuto dell'array.  
  
 [!code-cpp[Conceptual.StringReader#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.stringreader/cpp/source.cpp#1)]
 [!code-csharp[Conceptual.StringReader#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source.cs#1)]
 [!code-vb[Conceptual.StringReader#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source.vb#1)]  
  
## Esempio  
 L'esempio seguente legge tutti i caratteri in modo asincrono da un controllo <xref:System.Windows.Controls.TextBox> e li archivia in un array.  Quindi in modo asincrono scrive ogni lettera o un carattere di spazio vuoto su una riga separata seguita da un'interruzione di riga ad un controllo <xref:System.Windows.Controls.TextBlock>.  
  
 [!code-csharp[Conceptual.StringReader#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source2.cs#2)]
 [!code-vb[Conceptual.StringReader#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.IO.StringReader>   
 <xref:System.IO.StringReader.Read%2A?displayProperty=fullName>   
 [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md)   
 [NIB: How to: Create a Directory Listing](http://msdn.microsoft.com/it-it/4d2772b1-b991-4532-a8a6-6ef733277e69)   
 [Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [Procedura: Aprire e accodare un file di log](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [Procedura: Scrivere caratteri in una stringa](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)