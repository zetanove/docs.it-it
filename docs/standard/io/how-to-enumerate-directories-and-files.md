---
title: "Procedura: enumerare directory e file | Microsoft Docs"
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
  - "I/O [.NET Framework], enumerazione di directory e file"
ms.assetid: 86b69a08-3bfa-4e5f-b4e1-3b7cb8478215
caps.latest.revision: 18
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: enumerare directory e file
E' possibile enumerare directory e file tramite metodi che restituiscono una raccolta enumerabile di stringhe dei relativi nomi.  È inoltre possibile utilizzare metodi che restituiscono una raccolta enumerabile di oggetti <xref:System.IO.DirectoryInfo>, <xref:System.IO.FileInfo> o <xref:System.IO.FileSystemInfo>.  Le raccolte enumerabili offrono prestazioni migliori rispetto alle matrici quando si utilizzano le grandi raccolte di directory e file.  
  
 È anche possibile utilizzare le raccolte enumerabili ottenuti da questi metodi per fornire il parametro <xref:System.Collections.Generic.IEnumerable%601> per i costruttori di classi di raccolte quale la classe <xref:System.Collections.Generic.List%601>.  
  
 Per ottenere solo i nomi delle directory o dei file, utilizzare i metodi di enumerazione della classe <xref:System.IO.Directory>.  Per ottenere altre proprietà delle directory o dei file, utilizzare le classi <xref:System.IO.DirectoryInfo> e <xref:System.IO.FileSystemInfo>.  
  
 Nella tabella seguente viene fornita una guida ai metodi che restituiscono raccolte enumerabili.  
  
|Da enumerare|Raccolta enumerabile da restituire|Metodo da utilizzare|  
|------------------|----------------------------------------|--------------------------|  
|Directory|Nomi di directory.|<xref:System.IO.Directory.EnumerateDirectories%2A?displayProperty=fullName>|  
||Informazioni sulle directory \(<xref:System.IO.DirectoryInfo>\)|<xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=fullName>|  
|File|Nomi di file|<xref:System.IO.Directory.EnumerateFiles%2A?displayProperty=fullName>|  
||Informazioni sui file \(<xref:System.IO.FileInfo>\)|<xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=fullName>|  
|Informazioni sul file system|Voci di file system|<xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=fullName>|  
||Informazioni sul file system \(<xref:System.IO.FileSystemInfo>\)|<xref:System.IO.DirectoryInfo.EnumerateFileSystemInfos%2A?displayProperty=fullName>|  
  
 Sebbene sia possibile enumerare immediatamente tutti i file nelle sottodirectory di una directory padre tramite l'opzione di ricerca <xref:System.IO.SearchOption> fornita dall'enumerazione <xref:System.IO.SearchOption>, le eccezioni di accesso non autorizzato \(<xref:System.UnauthorizedAccessException>\) possono causare un'enumerazione incompleta.  Qualora esista la possibilità di tali eccezioni, è possibile rilevarle e proseguire enumerando prima le directory, quindi i file.  
  
### Per enumerare nomi di directory  
  
-   Utilizzare il metodo <xref:System.IO.Directory.EnumerateDirectories%28System.String%29?displayProperty=fullName> per ottenere un elenco dei nomi delle directory di primo livello in un percorso specificato.  
  
     [!code-csharp[System.IO.EnumDirs1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.enumdirs1/cs/program.cs#1)]
     [!code-vb[System.IO.EnumDirs1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.enumdirs1/vb/program.vb#1)]  
  
### Per enumerare i nomi di file in una directory e nelle sottodirectory  
  
-   Utilizzare il metodo <xref:System.IO.Directory.EnumerateFiles%28System.String%2CSystem.String%2CSystem.IO.SearchOption%29?displayProperty=fullName> per eseguire una ricerca in una directory e \(facoltativamente\) le sue sottodirectory, per ottenere un elenco dei nomi dei file in un percorso specificato corrispondenti a un criterio di ricerca specificato.  
  
     [!code-csharp[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/cs/program.cs#1)]
     [!code-vb[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/vb/program.vb#1)]  
  
### Per enumerare una raccolta di oggetti DirectoryInfo  
  
-   Utilizzare il metodo <xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=fullName> per ottenere una raccolta di directory di primo livello.  
  
     [!code-csharp[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/cs/program.cs#1)]
     [!code-vb[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/vb/module1.vb#1)]  
  
### Per enumerare una raccolta di oggetti FileInfo in tutte le directory  
  
-   Utilizzare il metodo <xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=fullName> per ottenere una raccolta di file corrispondenti a un criterio di ricerca specificato in tutte le directory.  In questo esempio vengono prima enumerate le directory di primo livello per rilevare possibili eccezioni di accesso non autorizzato, quindi vengono enumerati i file.  
  
     [!code-csharp[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/cs/program.cs#1)]
     [!code-vb[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/vb/program.vb#1)]  
  
## Vedere anche  
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)