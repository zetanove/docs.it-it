---
title: "Procedura: Creare file e directory nello spazio di memorizzazione isolato | Microsoft Docs"
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
  - "directory [.NET Framework], spazio di memorizzazione isolato"
  - "file [.NET Framework], spazio di memorizzazione isolato"
  - "spazio di memorizzazione isolato, creazione di file e directory"
  - "archivio dati, creazione di file e directory"
  - "archiviazione di dati mediante spazio di memorizzazione isolato, creazione di file e directory"
  - "archivi, creazione di file e directory"
  - "archiviazione di dati usando spazio di memorizzazione isolato, creazione di file e directory"
ms.assetid: 2ca4d2a4-809b-4f00-bc08-bf4a64d3a5c3
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: Creare file e directory nello spazio di memorizzazione isolato
Una volta ottenuto un archivio isolato, è possibile creare directory e file per la memorizzazione dei dati.  All'interno di un archivio, i nomi di file e directory vengono specificati in base alla radice del file system virtuale.  
  
 Per creare una directory, utilizzare il metodo di istanza <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=fullName>.  Se si specifica una sottodirectory di una directory che non esiste, entrambe le directory vengono create.  Se si specifica una directory già esistente, il metodo ritorna senza creare una directory e non viene generata alcuna eccezione.  Se invece si specifica un nome di directory contenente caratteri non validi, verrà generata un'eccezione <xref:System.IO.IsolatedStorage.IsolatedStorageException>.  
  
 Per creare un file, utilizzare il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=fullName>.  
  
 Nel sistema operativo Windows, lo spazio di memorizzazione isolato di nomi di file e directory non fa distinzione tra maiuscole e minuscole.  Pertanto se si tenta di creare un file denominato `ThisFile.txt` e un file denominato `THISFILE.TXT`, verrà creato un solo file.  I nomi dei file vengono comunque visualizzati con la combinazione di maiuscole e minuscole originale.  
  
## Esempio  
 Nell'esempio di codice che segue viene illustrato come creare file e directory in un archivio isolato.  
  
 [!code-csharp[Conceptual.IsolatedStorage#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source.cs#1)]
 [!code-vb[Conceptual.IsolatedStorage#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source.vb#1)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)