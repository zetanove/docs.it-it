---
title: "Procedura: Trovare file e directory esistenti nello spazio di memorizzazione isolato | Microsoft Docs"
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
  - "archivi, ricerca di file e directory"
  - "individuazione di file nel file di spazio di memorizzazione isolato"
  - "directory [.NET Framework], spazio di memorizzazione isolato"
  - "spazio di memorizzazione isolato, ricerca di file e directory"
  - "archiviazione di dati mediante spazio di memorizzazione isolato, ricerca di file e directory"
  - "file [.NET Framework], spazio di memorizzazione isolato"
  - "archivio dati, ricerca di file e directory"
  - "individuazione di directory nel file di spazio di memorizzazione isolato"
  - "archiviazione di dati usando spazio di memorizzazione isolato, ricerca di file e directory"
ms.assetid: eb28458a-6161-4e7a-9ada-30ef93761b5c
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: Trovare file e directory esistenti nello spazio di memorizzazione isolato
Per trovare una directory nello spazio di memorizzazione isolato, utilizzare il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A?displayProperty=fullName>.  Questo metodo accetta una stringa che rappresenta un criterio di ricerca.  È possibile utilizzare sia i caratteri jolly carattere singolo \(?\) che caratteri multipli \(\*\) nei criteri di ricerca, ma i caratteri jolly devono essere visualizzati nella parte finale del nome.  Ad esempio, `directory1/*ect*` è una stringa di ricerca valida, mentre `*ect*/directory2` non lo è.  
  
 Per cercare un file, utilizzare il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A?displayProperty=fullName>.  La restrizione per caratteri jolly nelle stringhe di ricercache si applica a <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> vale anche per <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>.  
  
 Nessuno di questi metodi sono ricorsivi, la classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile> non fornisce metodi che consentono di elencare tutte le directory o file dell'archivio.  Tuttavia, i metodi ricorsivi sono riportati nel seguente esempio di codice.  
  
## Esempio  
 Nell'esempio di codice che segue viene illustrato come creare file e directory in un archivio isolato.  In primo luogo viene recuperato e inserito nella variabile `isoStore` un archivio isolato in base all'utente, al dominio e all'assembly.  Il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A> viene usato per settare diverse directory e il costruttore <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream.%23ctor%28System.String%2CSystem.IO.FileMode%2CSystem.IO.IsolatedStorage.IsolatedStorageFile%29> crea alcuni file in queste directory.  Il codice consente quindi di scorrere i risultati del metodo `GetAllDirectories`.  Il metodo utilizza <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> per trovare tutti i nomi delle directory contenute nella directory corrente.  Tali nomi vengono memorizzati in un array, quindi `GetAllDirectories` chiama se stesso passando tutte le directory trovate.  Come risultato, l'array restituisce tutti i nomi delle directory.  A questo punto il codice chiama il metodo `GetAllFiles`.  Tale metodo chiama `GetAllDirectories` per trovare i nomi di tutte le directory, e quindi cerca i file contenuti in ciascuna di queste directory utilizzando il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>.  Il risultato viene restituito in una matrice il cui contenuto verrà successivamente visualizzato.  
  
 [!code-cpp[Conceptual.IsolatedStorage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source8.cpp#9)]
 [!code-csharp[Conceptual.IsolatedStorage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source8.cs#9)]
 [!code-vb[Conceptual.IsolatedStorage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source8.vb#9)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)