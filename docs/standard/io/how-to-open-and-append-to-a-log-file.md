---
title: "Procedura: Aprire e accodare un file di log | Microsoft Docs"
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
  - "file di log, apertura"
  - "flussi, apertura e aggiunta al file di log"
  - "file di log, aggiunta a"
  - "I/O [.NET Framework], file di log"
ms.assetid: 74423362-1721-49cb-aa0a-e04005f72a06
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: Aprire e accodare un file di log
<xref:System.IO.StreamWriter> e <xref:System.IO.StreamReader> scrivono e leggono caratteri dai flussi.  Nell'esempio di codice che segue viene aperto il file `log.txt` e vi vengono accodate informazioni. Nel caso non sia disponibile, il file verrà creato.  Il contenuto del file viene quindi scritto nell'output standard, che ne consente la visualizzazione.  Come alternativa a questo esempio sarebbe possibile archiviare le informazioni come stringa singola o matrice di stringa, e per ottenere la stessa funzionalità sarebbe possibile utilizzare il metodo <xref:System.IO.File.WriteAllText%2A> o <xref:System.IO.File.WriteAllLines%2A>.  
  
> [!NOTE]
>  Per la creazione o la scrittura nei file di log, gli utenti di Visual Basic possono scegliere di utilizzare i metodi e le proprietà forniti dalla classe <xref:Microsoft.VisualBasic.Logging.Log> o dalla classe <xref:Microsoft.VisualBasic.FileIO.FileSystem>.  
  
## Esempio  
 [!code-csharp[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source2.cs#2)]
 [!code-vb[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.IO.StreamWriter>   
 <xref:System.IO.StreamReader>   
 <xref:System.IO.File.AppendText%2A?displayProperty=fullName>   
 <xref:System.IO.File.OpenText%2A?displayProperty=fullName>   
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=fullName>   
 [Procedura: enumerare directory e file](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [Procedura: Leggere caratteri da una stringa](../../../docs/standard/io/how-to-read-characters-from-a-string.md)   
 [Procedura: Scrivere caratteri in una stringa](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)