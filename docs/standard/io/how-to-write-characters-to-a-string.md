---
title: "Procedura: Scrivere caratteri in una stringa | Microsoft Docs"
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
  - "flussi di dati, scrittura di caratteri nelle stringhe"
  - "scrittura di caratteri in stringhe"
  - "flussi, scrittura di caratteri in stringhe"
  - "I/O [.NET Framework], scrittura di caratteri nelle stringhe"
ms.assetid: 1222cbeb-0760-44bf-9888-914a2a37174b
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: Scrivere caratteri in una stringa
Gli esempi di codice seguenti scrivono i caratteri in modo sincrono e in modo asincrono da una matrice di caratteri in una stringa.  
  
## Esempio  
 Il seguente esempio scrive 5 caratteri in modo sincrono da una matrice a una stringa.  
  
 [!code-csharp[Conceptual.StringBuilder#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/example2.cs#9)]
 [!code-vb[Conceptual.StringBuilder#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/example2.vb#9)]  
  
## Esempio  
 L'esempio seguente legge tutti i caratteri in modo asincrono da un controllo <xref:System.Windows.Controls.TextBox> e li archivia in un array.  Quindi in modo asincrono scrive ogni lettera o un carattere di spazio vuoto su una riga separata seguita da un'interruzione di riga ad un controllo <xref:System.Windows.Controls.TextBlock>.  
  
 [!code-csharp[Conceptual.StringReader#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source2.cs#2)]
 [!code-vb[Conceptual.StringReader#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.IO.StringWriter>   
 <xref:System.IO.StringWriter.Write%2A?displayProperty=fullName>   
 <xref:System.Text.StringBuilder>   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)   
 [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md)   
 [Procedura: enumerare directory e file](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [Procedura: Aprire e accodare un file di log](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [Procedura: Leggere caratteri da una stringa](../../../docs/standard/io/how-to-read-characters-from-a-string.md)