---
title: "Procedura: Enumerare gli archivi per lo spazio di memorizzazione isolato | Microsoft Docs"
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
  - "enumerazione di archivi"
  - "archivio dati usando lo spazio di memorizzazione isolato, enumerazione di archivi"
  - "archiviazione di dati usando lo spazio di memorizzazione isolato, enumerazione di archivi"
  - "archivi, enumerazione"
  - "spazio di memorizzazione isolato, enumerazione di archivi"
  - "archivi dati, enumerazione"
ms.assetid: 0fcf279a-f241-48f0-8034-2e3d331f1fcb
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: Enumerare gli archivi per lo spazio di memorizzazione isolato
È possibile enumerare tutti gli archivi isolati dell'utente corrente utilizzando il metodo statico <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=fullName>.  Questo metodo accetta un valore <xref:System.IO.IsolatedStorage.IsolatedStorageScope> e restituisce un enumeratore <xref:System.IO.IsolatedStorage.IsolatedStorageFile>.  Per enumerare gli archivi, è necessaria l'autorizzazione <xref:System.Security.Permissions.IsolatedStorageFilePermission> che specifica il valore <xref:System.Security.Permissions.IsolatedStorageContainment>.  Se si chiama il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> con il valore <xref:System.IO.IsolatedStorage.IsolatedStorageScope>, questo restituisce un array di oggetti <xref:System.IO.IsolatedStorage.IsolatedStorageFile> definiti per l'utente corrente.  
  
## Esempio  
 Nell'esempio di codice seguente viene ottenuto un archivio che è isolato dall'utente e dall'assembly, vengono creati alcuni file e vengono recuperati tali file utilizzando il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A>.  
  
 [!code-csharp[Conceptual.IsolatedStorage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source2.cs#2)]
 [!code-vb[Conceptual.IsolatedStorage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)