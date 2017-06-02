---
title: "Procedura: Anticipare le condizioni di spazio insufficiente con lo spazio di memorizzazione isolato | Microsoft Docs"
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
  - "archivi dati, quote"
  - "spazio di memorizzazione isolato, quote"
  - "quantità di spazio di memorizzazione isolato usata"
  - "limite allo spazio di memorizzazione isolato usato"
  - "archivi, quote"
  - "archivi, condizioni di spazio insufficiente"
  - "archivio dati usando spazio di memorizzazione isolato, quote"
  - "archiviazione di dati usando spazio di memorizzazione isolato, quote"
  - "spazio rimanente nello spazio di memorizzazione isolato"
  - "archivi dati, condizioni di spazio insufficiente"
  - "archiviazione di dati usando spazio di memorizzazione isolato, condizioni di spazio insufficiente"
  - "quote per lo spazio di memorizzazione isolato"
  - "spazio di memorizzazione isolato, condizioni di spazio insufficiente"
  - "archivio dati usando spazio di memorizzazione isolato, condizioni di spazio insufficiente"
ms.assetid: e35d4535-3732-421e-b1a3-37412e036145
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: Anticipare le condizioni di spazio insufficiente con lo spazio di memorizzazione isolato
Il codice in cui viene utilizzata l'archiviazione isolata è vincolato da una [quota](../../../docs/standard/io/isolated-storage.md#quotas) che specifica la dimensione massima del contesto dati in cui sono presenti le directory e i file di archiviazione isolata.  Questa quota è definita dai criteri di sicurezza e può essere configurato dagli amministratori.  Se durante un tentativo di scrittura di dati si supera la dimensione massima consentita, verrà generata un'eccezione <xref:System.IO.IsolatedStorage.IsolatedStorageException> e l'operazione non viene completata.  Le quote contribuiscono ad arginare il rischio di attacchi Denial of Service che potrebbero condurre l'applicazione a rifiutare le richieste per esaurimento dello spazio di archiviazione dati.  
  
 Per permettere di stabilire se è probabile che un determinato tentativo di scrittura non riesca per il motivo suddetto, la classe <xref:System.IO.IsolatedStorage.IsolatedStorage> fornisce tre proprietà in sola lettura: <xref:System.IO.IsolatedStorage.IsolatedStorage.AvailableFreeSpace%2A>, <xref:System.IO.IsolatedStorage.IsolatedStorage.UsedSize%2A> e <xref:System.IO.IsolatedStorage.IsolatedStorage.Quota%2A>.  Queste proprietà possono essere utilizzate per determinare se scrivendo nell'archivio si supererà la dimensione massima consentita dello stesso.  Quando si utilizzano queste proprietà, è importante considerare che l'archiviazione isolata consente più accessi contemporanei, pertanto, anche se si calcola lo spazio di archiviazione rimanente, è possibile che questo non sia più disponibile al momento in cui si tenta di scrivere nell'archivio.  Non viene tuttavia così impedito l'utilizzo della dimensione massima dell'archivio per determinare se si sta per raggiungere il limite massimo di archiviazione disponibile.  
  
 La proprietà <xref:System.IO.IsolatedStorage.IsolatedStorage.Quota%2A> dipende dal funzionamento corretto dell'assembly.  Di conseguenza, questa proprietà deve essere recuperata solo negli oggetti <xref:System.IO.IsolatedStorage.IsolatedStorageFile> che sono stati creati utilizzando il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A> o <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>.  Gli oggetti <xref:System.IO.IsolatedStorage.IsolatedStorageFile> creati in altro modo, ad esempio gli oggetti restituiti dal metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A>, non restituiranno una dimensione massima precisa.  
  
## Esempio  
 Nell'esempio di codice che segue viene ottenuto un archivio isolato, vengono creati alcuni file e viene recuperata la proprietà <xref:System.IO.IsolatedStorage.IsolatedStorage.AvailableFreeSpace%2A>.  Lo spazio rimanente viene indicato in byte.  
  
 [!code-cpp[Conceptual.IsolatedStorage#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source7.cpp#8)]
 [!code-csharp[Conceptual.IsolatedStorage#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source7.cs#8)]
 [!code-vb[Conceptual.IsolatedStorage#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source7.vb#8)]  
  
## Vedere anche  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)   
 [Procedura: Recuperare archivi per lo spazio di memorizzazione isolato](../../../docs/standard/io/how-to-obtain-stores-for-isolated-storage.md)