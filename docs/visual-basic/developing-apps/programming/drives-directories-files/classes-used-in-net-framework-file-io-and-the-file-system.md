---
title: "Classes Used in .NET Framework File I/O and the File System (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "file I/O classes"
ms.assetid: 4a5ca924-eea8-4a95-a5f0-6ac10de276a3
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Classes Used in .NET Framework File I/O and the File System (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nelle seguenti tabelle vengono elencate le classi comunemente utilizzate per la funzionalità di I\/O di file di .NET Framework, categorizzate in classi I\/O, classi utilizzate per la creazione di flussi e classi utilizzate per leggere e scrivere nei flussi.  
  
 Per accedere alla documentazione di [!INCLUDE[dnprdnlong](../../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)] e individuare un elenco più completo, vedere [Cenni preliminari sulla libreria di classi](../Topic/.NET%20Framework%20Class%20Library%20Overview.md).  
  
## Classi I\/O di base per file, unità e directory  
 Nella seguente tabella sono elencate e descritte le classi principali utilizzate per la funzionalità I\/O di file.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.IO.Directory?displayProperty=fullName>|Consente di utilizzare metodi statici per la creazione, lo spostamento e l'enumerazione di directory e sottodirectory.|  
|<xref:System.IO.DirectoryInfo?displayProperty=fullName>|Consente di utilizzare metodi di istanza per la creazione, lo spostamento e l'enumerazione di directory e sottodirectory.|  
|<xref:System.IO.DriveInfo?displayProperty=fullName>|Consente di utilizzare metodi di istanza per la creazione, lo spostamento e l'enumerazione di unità.|  
|<xref:System.IO.File?displayProperty=fullName>|Consente di utilizzare metodi statici per la creazione, la copia, l'eliminazione, lo spostamento e l'apertura di file, nonché di creare `FileStream`.|  
|<xref:System.IO.FileAccess?displayProperty=fullName>|Consente di definire le costanti per l'accesso in lettura, scrittura o lettura\/scrittura a un file.|  
|<xref:System.IO.FileAttributes?displayProperty=fullName>|Consente di utilizzare attributi per file e directory come `Archive`, `Hidden` e `ReadOnly`.|  
|<xref:System.IO.FileInfo?displayProperty=fullName>|Consente di utilizzare metodi statici per la creazione, la copia, l'eliminazione, lo spostamento e l'apertura di file, nonché di creare `FileStream`.|  
|<xref:System.IO.FileMode?displayProperty=fullName>|Consente di controllare il modo in cui viene aperto il file.  Questo parametro è specificato in molti costruttori per `FileStream` e `IsolatedStorageFileStream` e per i metodi `Open` di <xref:System.IO.File> e <xref:System.IO.FileInfo>.|  
|<xref:System.IO.FileShare?displayProperty=fullName>|Consente di definire le costanti per il controllo del tipo di accesso che altri flussi di file possono avere per lo stesso file.|  
|<xref:System.IO.Path?displayProperty=fullName>|Consente di utilizzare dei metodi e delle proprietà per l'elaborazione delle stringhe di directory.|  
|<xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>|Consente di controllare l'accesso di file e cartelle definendo le autorizzazioni <xref:System.Security.Permissions.FileIOPermissionAttribute.Read%2A>, <xref:System.Security.Permissions.FileIOPermissionAttribute.Write%2A>, <xref:System.Security.Permissions.FileIOPermissionAttribute.Append%2A> e <xref:System.Security.Permissions.FileIOPermissionAttribute.PathDiscovery%2A>.|  
  
## Classi utilizzate per creare i flussi  
 Nella seguente tabella sono elencate e descritte le classi principali utilizzate per la creazione di flussi.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.IO.BufferedStream?displayProperty=fullName>|Consente di aggiungere un livello di buffer per leggere e scrivere le operazioni su un altro flusso.|  
|<xref:System.IO.FileStream?displayProperty=fullName>|Supporta l'accesso casuale ai file tramite il metodo <xref:System.IO.FileStream.Seek%2A>.  Per impostazione predefinita, <xref:System.IO.FileStream> apre i file in modo sincrono, ma supporta anche operazioni asincrone.|  
|<xref:System.IO.MemoryStream?displayProperty=fullName>|Consente di creare un flusso il cui archivio di backup è la memoria, anziché un file.|  
|<xref:System.Net.Sockets.NetworkStream?displayProperty=fullName>|Consente di utilizzare un flusso sottostante di dati per l'accesso alla rete.|  
|<xref:System.Security.Cryptography.CryptoStream?displayProperty=fullName>|Consente di definire un flusso che collega i flussi di dati alle trasformazioni crittografiche.|  
  
## Classi utilizzate per la lettura e la scrittura nei flussi  
 Nella seguente tabella vengono mostrate le classi specifiche utilizzate per la lettura e la scrittura nei file con flussi.  
  
|**Classe**|**Descrizione**|  
|----------------|---------------------|  
|<xref:System.IO.BinaryReader?displayProperty=fullName>|Consente di leggere stringhe codificate e tipi di dati primitivi da <xref:System.IO.FileStream>.|  
|<xref:System.IO.BinaryWriter?displayProperty=fullName>|Consente di scrivere stringhe codificate e tipi di dati primitivi in <xref:System.IO.FileStream>.|  
|<xref:System.IO.StreamReader?displayProperty=fullName>|Legge caratteri da <xref:System.IO.FileStream> utilizzando <xref:System.IO.StreamReader.CurrentEncoding%2A> per convertire i caratteri in byte e viceversa.  <xref:System.IO.StreamReader> dispone di un costruttore che tenta di stabilire quale <xref:System.IO.StreamReader.CurrentEncoding%2A> adottare per un determinato flusso, in base alla presenza di un preambolo specifico di <xref:System.IO.StreamReader.CurrentEncoding%2A>, ad esempio un contrassegno dell'ordine dei byte.|  
|<xref:System.IO.StreamWriter?displayProperty=fullName>|Consente di scrivere i caratteri in `FileStream`, utilizzando <xref:System.IO.StreamWriter.Encoding%2A> per convertire i caratteri in byte.|  
|<xref:System.IO.StringReader?displayProperty=fullName>|Consente di leggere i caratteri da `String`.  L'output può essere un flusso codificato o `String`.|  
|<xref:System.IO.StringWriter?displayProperty=fullName>|Consente di scrivere i caratteri in `String`.  L'output può essere un flusso codificato o `String`.|  
  
## Vedere anche  
 [Composizione dei flussi](../Topic/Composing%20Streams.md)   
 [I\/O di file e di flussi](../Topic/File%20and%20Stream%20I-O.md)   
 [I\/O di file asincrono](../Topic/Asynchronous%20File%20I-O.md)   
 [Nozioni fondamentali sul file system e sulla funzionalità di I\/O di file di .NET Framework \(Visual Basic\)](../../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)