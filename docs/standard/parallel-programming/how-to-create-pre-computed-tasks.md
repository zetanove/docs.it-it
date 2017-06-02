---
title: "How to: Create Pre-Computed Tasks | Microsoft Docs"
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
  - "tasks, creating pre-computed"
ms.assetid: a73eafa2-1f49-4106-a19e-997186029b58
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# How to: Create Pre-Computed Tasks
Questo documento descrive come utilizzare il metodo <xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=fullName> per recuperare i risultati delle operazioni di download asincrone contenuti in una cache.  Il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> restituisce un oggetto <xref:System.Threading.Tasks.Task%601> finito che contiene il valore fornito come proprietà <xref:System.Threading.Tasks.Task%601.Result%2A>.  Questo metodo è utile quando si esegue un'operazione asincrona che restituisce un oggetto <xref:System.Threading.Tasks.Task%601> e il risultato di tale oggetto <xref:System.Threading.Tasks.Task%601> è già calcolato.  
  
## Esempio  
 L'esempio seguente scarica le stringhe dal Web.  Definisce il metodo `DownloadStringAsync`.  Questo metodo scarica le stringhe dal Web in modo asincrono.  In questo esempio viene utilizzato un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> per memorizzare nella cache i risultati di operazioni precedenti.  Se l'indirizzo di input viene utilizzato in questa cache, `DownloadStringAsync` utilizza il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> per produrre un oggetto <xref:System.Threading.Tasks.Task%601> che mantiene il contenuto a quell'indirizzo.  In caso contrario, `DownloadStringAsync` scarica il file dal Web e aggiunge il risultato alla cache.  
  
 [!code-csharp[TPL_CachedDownloads#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cacheddownloads/cs/cacheddownloads.cs#1)]
 [!code-vb[TPL_CachedDownloads#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cacheddownloads/vb/cacheddownloads.vb#1)]  
  
 Questo esempio calcola il tempo necessario per scaricare le stringhe multiple due volte.  Il secondo set di operazioni di download deve richiedere meno tempo del primo set poiché i risultati vengono utilizzati nella cache.  Il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> consente al metodo `DownloadStringAsync` di creare oggetti di <xref:System.Threading.Tasks.Task%601> che utilizzano i risultati pre\-calcolati.  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `CachedDownloads.cs` \(`CachedDownloads.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe CachedDownloads.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe CachedDownloads.vb**  
  
## Programmazione efficiente  
  
## Vedere anche  
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)