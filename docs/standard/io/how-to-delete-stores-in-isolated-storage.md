---
title: "Procedura: Eliminare gli archivi nello spazio di memorizzazione isolato | Microsoft Docs"
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
  - "archivi, eliminazione"
  - "archivi dati, eliminazione"
  - "eliminazione di archivi"
  - "rimozione di archivi"
  - "spazio di memorizzazione isolato, eliminazione di archivi"
  - "archiviazione di dati usando lo spazio di memorizzazione isolato, eliminazione di archivi"
  - "archivio dati usando lo spazio di memorizzazione isolato, eliminazione di archivi"
ms.assetid: 3947e333-5af6-4601-b2f1-24d4d6129cf3
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: Eliminare gli archivi nello spazio di memorizzazione isolato
La classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile> fornisce due metodi per eliminare i file dello spazio di memorizzazione isolato:  
  
-   Il metodo di istanza <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove> non accetta argomenti ed elimina l'archivio che lo chiama. Non sono necessarie autorizzazioni per questa operazione. Il codice che può accedere all'archivio può eliminare alcuni o tutti i dati in esso contenuti.  
  
-   Il metodo statico <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%28System.IO.IsolatedStorage.IsolatedStorageScope%29> accetta il valore di enumerazione <xref:System.IO.IsolatedStorage.IsolatedStorageScope> ed elimina tutti gli archivi per l'utente che esegue il codice. Questa operazione richiede l'autorizzazione <xref:System.Security.Permissions.IsolatedStorageFilePermission> per il valore <xref:System.Security.Permissions.IsolatedStorageContainment>.  
  
## Esempio  
 L'esempio di codice seguente illustra l'uso dei metodi <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%2A> statici e di istanza. La classe ottiene due archivi, uno isolato per utente e assembly e l'altro isolato per utente, dominio e assembly. L'archivio utente, di dominio e di assembly viene quindi eliminato chiamando il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove> del file dello spazio di memorizzazione isolato `isoStore1`. Tutti gli archivi rimanenti per l'utente vengono quindi eliminati chiamando il metodo statico <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%28System.IO.IsolatedStorage.IsolatedStorageScope%29>.  
  
 [!code-cpp[Conceptual.IsolatedStorage#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source3.cpp#3)]
 [!code-csharp[Conceptual.IsolatedStorage#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source3.cs#3)]
 [!code-vb[Conceptual.IsolatedStorage#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source3.vb#3)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)