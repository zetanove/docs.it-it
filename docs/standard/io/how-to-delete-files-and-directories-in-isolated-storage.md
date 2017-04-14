---
title: "Procedura: Eliminare file e directory nello spazio di memorizzazione isolato | Microsoft Docs"
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
  - "archiviazione di dati mediante spazio di memorizzazione isolato, eliminazione di file e directory"
  - "directory [.NET Framework], spazio di memorizzazione isolato"
  - "file [.NET Framework], spazio di memorizzazione isolato"
  - "spazio di memorizzazione isolato, eliminazione di file e directory"
  - "archivio dati, eliminazione di file e directory"
  - "archivi, creazione di file e directory"
  - "eliminazione di file all'interno del file di fase isolata"
  - "archiviazione di dati usando spazio di memorizzazione isolato, eliminazione di file e directory"
  - "eliminazione di directory all'interno del file di fase isolata"
ms.assetid: 8fcc0dea-435b-4d40-ba4d-ba056265c202
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: Eliminare file e directory nello spazio di memorizzazione isolato
È possibile eliminare le directory e i file contenuti in un file di archiviazione isolata.  All'interno di un archivio, i nomi di file e directory dipendono dal sistema operativo e sono specificati come relativi alla radice del file system virtuale.  Non viene fatta distinzione tra maiuscole e minuscole nei sistemi operativi Windows.  
  
 La classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=fullName> fornisce due metodi di istanza per l'eliminazione di directory e file: <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> e <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A>.  Se si tenta di eliminare un file o una directory che non esiste, verrà generata un'eccezione <xref:System.IO.IsolatedStorage.IsolatedStorageException>.  Se si include un carattere jolly nel nome, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> genera un'eccezione <xref:System.IO.IsolatedStorage.IsolatedStorageException> e <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> genera un'eccezione <xref:System.ArgumentException>.  
  
 Il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> fallisce se la directory contiene tutti i file o sottodirectory.  È possibile utilizzare i metodi <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> e <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> per recuperare i file esistenti e directory.  Per ulteriori informazioni sulla ricerca del file system virtuale di un archivio, vedere [Procedura: Trovare file e directory esistenti nello spazio di memorizzazione isolato](../../../docs/standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md).  
  
## Esempio  
 Nell'esempio di codice che segue vengono creati e quindi eliminati diversi file e directory.  
  
 [!code-cpp[Conceptual.IsolatedStorage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.IsolatedStorage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source4.cs#4)]
 [!code-vb[Conceptual.IsolatedStorage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source4.vb#4)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=fullName>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)