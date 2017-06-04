---
title: "Procedura: leggere e scrivere su un file di dati appena creato | Microsoft Docs"
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
  - "BinaryReader (classe), esempi"
  - "BinaryWriter (classe), esempi"
  - "I/O [.NET Framework], lettura di dati"
  - "I/O [.NET Framework], scrittura di dati"
  - "flussi, lettura e scrittura di dati"
ms.assetid: e209d949-31e8-44ea-8e38-87f9093f3093
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: leggere e scrivere su un file di dati appena creato
Le classi <xref:System.IO.BinaryWriter> e <xref:System.IO.BinaryReader?displayProperty=fullName> vengono utilizzate per scrivere e leggere dati, anziché stringhe di caratteri.  Nell'esempio di codice che segue vengono illustrate la lettura e la scrittura di dati in un nuovo flusso di file vuoto chiamato `Test.data`.  Una volta creato il file di dati nella directory corrente, vengono creati gli oggetti <xref:System.IO.BinaryWriter> e <xref:System.IO.BinaryReader> e l'oggetto <xref:System.IO.BinaryWriter> viene utilizzato per scrivere interi compresi tra 0 e 10 in `Test.data`, il quale lascia il puntatore del file alla fine del file.  Una volta riportato il puntatore del file sull'origine, l'oggetto <xref:System.IO.BinaryReader> legge il contenuto specificato.  
  
## Esempio  
 [!code-cpp[System.IO.BinaryReaderWriter#7](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/CPP/source6.cpp#7)]
 [!code-csharp[System.IO.BinaryReaderWriter#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/CS/source6.cs#7)]
 [!code-vb[System.IO.BinaryReaderWriter#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/VB/source6.vb#7)]  
  
## Programmazione efficiente  
 Se `Test.data` esiste già nella directory corrente, verrà generata un'eccezione <xref:System.IO.IOException>.  Utilizzare l'opzione <xref:System.IO.FileMode?displayProperty=fullName> quando si inizializza il flusso per creare un nuovo file senza generare un'eccezione.  
  
## Vedere anche  
 <xref:System.IO.BinaryReader>   
 <xref:System.IO.BinaryWriter>   
 <xref:System.IO.FileStream>   
 <xref:System.IO.FileStream.Seek%2A?displayProperty=fullName>   
 <xref:System.IO.SeekOrigin>   
 [Procedura: enumerare directory e file](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [Procedura: Aprire e accodare un file di log](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [Procedura: Leggere caratteri da una stringa](../../../docs/standard/io/how-to-read-characters-from-a-string.md)   
 [Procedura: Scrivere caratteri in una stringa](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)