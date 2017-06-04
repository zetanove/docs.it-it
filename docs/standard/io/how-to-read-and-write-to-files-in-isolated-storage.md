---
title: "Procedura: leggere e scrivere sui file nello spazio di memorizzazione isolato | Microsoft Docs"
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
  - "archiviazione di dati mediante spazio di memorizzazione isolato, lettura e scrittura in file"
  - "dati (archivi), lettura e scrittura in file"
  - "file, spazio di memorizzazione isolato"
  - "spazio di memorizzazione isolato, lettura e scrittura in file"
  - "lettura di dati"
  - "lettura di file all'interno dell'archivio"
  - "archivi, lettura e scrittura in file"
  - "dati (archiviazione mediante spazio di memorizzazione isolato), lettura e scrittura in file"
  - "scrittura di file all'interno dell'archivio"
ms.assetid: f977ebdc-1b55-475a-bc3d-3376470b08ae
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: leggere e scrivere sui file nello spazio di memorizzazione isolato
Per leggere, scrivere, un file in un archivio isolato, utilizzare un oggetto <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> con un lettore di flusso \(oggetto di<xref:System.IO.StreamReader> \) o uno scrittore di flusso \(oggetto di<xref:System.IO.StreamWriter> \).  
  
## Esempio  
 Il seguente esempio di codice ottiene un archivio isolato e controlla se un file denominato TestStore.txt esista nell'archivio.  Se non esiste, viene creato il file e scriverà "Hello Isolated Storage" nel file.  Se TestStore.txt è già presente, il codice di esempio viene letto dal file.  
  
 [!code-csharp[Conceptual.IsolatedStorage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source5.cs#5)]
 [!code-vb[Conceptual.IsolatedStorage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source5.vb#5)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>   
 <xref:System.IO.FileMode?displayProperty=fullName>   
 <xref:System.IO.FileAccess?displayProperty=fullName>   
 <xref:System.IO.StreamReader?displayProperty=fullName>   
 <xref:System.IO.StreamWriter?displayProperty=fullName>   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)