---
title: "Classi usate nel file system e nella funzionalità di I/O di file di .Net Framework (Visual Basic) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- file I/O classes
ms.assetid: 4a5ca924-eea8-4a95-a5f0-6ac10de276a3
caps.latest.revision: 15
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6bf3902995531768b8b065aca70790c16d77b0ce
ms.lasthandoff: 03/13/2017

---
# <a name="classes-used-in-net-framework-file-io-and-the-file-system-visual-basic"></a>Classi utilizzate nel file system e nella funzionalità di I/O di file di .Net Framework (Visual Basic)
Le tabelle seguenti elencano le classi comunemente usate per l'I/O di file di .NET Framework, suddivisi in classi I/O di file, classi usate per la creazione di flussi e classi usate per leggere e scrivere nei flussi.  
  
 Per un elenco più completo incluso nella documentazione di [!INCLUDE[dnprdnlong](../../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)], vedere [Class Library Overview](https://msdn.microsoft.com/library/hfa3fa08) (Panoramica della libreria di classi).  
  
## <a name="basic-io-classes-for-files-drives-and-directories"></a>Classi di I/O di base per file, unità e directory  
 La tabella seguente elenca e descrive le principali classi usate nell'I/O di file.  
  
|Classe|Descrizione|  
|-----------|-----------------|  
|<xref:System.IO.Directory?displayProperty=fullName>|Offre metodi statici per creare, spostare ed enumerare directory e sottodirectory.|  
|<xref:System.IO.DirectoryInfo?displayProperty=fullName>|Offre metodi di istanza per creare, spostare ed enumerare directory e sottodirectory.|  
|<xref:System.IO.DriveInfo?displayProperty=fullName>|Offre metodi di istanza per creare, spostare ed enumerare unità.|  
|<xref:System.IO.File?displayProperty=fullName>|Offre metodi statici per creare, copiare, eliminare, spostare e aprire file e supporta la creazione di un `FileStream`.|  
|<xref:System.IO.FileAccess?displayProperty=fullName>|Definisce le costanti per l'accesso in lettura, scrittura o lettura/scrittura a un file.|  
|<xref:System.IO.FileAttributes?displayProperty=fullName>|Offre attributi per file e directory, ad esempio `Archive`, `Hidden` e `ReadOnly`.|  
|<xref:System.IO.FileInfo?displayProperty=fullName>|Offre metodi statici per creare, copiare, eliminare, spostare e aprire file e supporta la creazione di un `FileStream`.|  
|<xref:System.IO.FileMode?displayProperty=fullName>|Controlla la modalità di apertura di un file. Questo parametro è specificato in molti costruttori per `FileStream` e `IsolatedStorageFileStream` e per i metodi `Open` di <xref:System.IO.File> e <xref:System.IO.FileInfo>.|  
|<xref:System.IO.FileShare?displayProperty=fullName>|Definisce le costanti per controllare il tipo di accesso che altri flussi di file possono avere sullo stesso file.|  
|<xref:System.IO.Path?displayProperty=fullName>|Offre metodi e proprietà per elaborare le stringhe di directory.|  
|<xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>|Controlla l'accesso di file e cartelle definendo le autorizzazioni <xref:System.Security.Permissions.FileIOPermissionAttribute.Read%2A>, <xref:System.Security.Permissions.FileIOPermissionAttribute.Write%2A>, <xref:System.Security.Permissions.FileIOPermissionAttribute.Append%2A> e <xref:System.Security.Permissions.FileIOPermissionAttribute.PathDiscovery%2A>.|  
  
## <a name="classes-used-to-create-streams"></a>Classi usate per creare flussi  
 La tabella seguente elenca e descrive le principali classi usate per creare flussi.  
  
|Classe|Descrizione|  
|-----------|-----------------|  
|<xref:System.IO.BufferedStream?displayProperty=fullName>|Aggiunge un livello di buffer per operazioni di lettura e scrittura in un altro flusso.|  
|<xref:System.IO.FileStream?displayProperty=fullName>|Supporta l'accesso casuale a file tramite il suo metodo <xref:System.IO.FileStream.Seek%2A>. <xref:System.IO.FileStream> apre file simultaneamente per impostazione predefinita, ma supporta anche operazioni asincrone.|  
|<xref:System.IO.MemoryStream?displayProperty=fullName>|Crea un flusso il cui archivio di backup è costituito da memoria, anziché da un file.|  
|<xref:System.Net.Sockets.NetworkStream?displayProperty=fullName>|Offre il flusso sottostante di dati per l'accesso alla rete.|  
|<xref:System.Security.Cryptography.CryptoStream?displayProperty=fullName>|Definisce un flusso che collega i flussi di dati alle trasformazioni crittografiche.|  
  
## <a name="classes-used-to-read-from-and-write-to-streams"></a>Classi usate per leggere e scrivere nei flussi  
 La tabella seguente illustra le classi specifiche usate per leggere e scrivere in file con flussi.  
  
|**Classe**|**Descrizione**|  
|---------------|---------------------|  
|<xref:System.IO.BinaryReader?displayProperty=fullName>|Legge stringhe codificate e tipi di dati primitivi da <xref:System.IO.FileStream>.|  
|<xref:System.IO.BinaryWriter?displayProperty=fullName>|Scrive stringhe codificate e tipi di dati primitivi in <xref:System.IO.FileStream>.|  
|<xref:System.IO.StreamReader?displayProperty=fullName>|Legge caratteri da <xref:System.IO.FileStream> usando <xref:System.IO.StreamReader.CurrentEncoding%2A> per convertire i caratteri da e in byte. <xref:System.IO.StreamReader> ha un costruttore che prova a verificare il corretto <xref:System.IO.StreamReader.CurrentEncoding%2A> per un determinato flusso, basato sulla presenza di un preambolo specifico <xref:System.IO.StreamReader.CurrentEncoding%2A>, ad esempio un byte order mark.|  
|<xref:System.IO.StreamWriter?displayProperty=fullName>|Scrive caratteri in un `FileStream`, usando <xref:System.IO.StreamWriter.Encoding%2A> per convertire i caratteri in byte.|  
|<xref:System.IO.StringReader?displayProperty=fullName>|Legge caratteri da un `String`. L'output può essere un flusso in qualsiasi codifica o una `String`.|  
|<xref:System.IO.StringWriter?displayProperty=fullName>|Scrive caratteri in una `String`. L'output può essere un flusso in qualsiasi codifica o una `String`.|  
  
## <a name="see-also"></a>Vedere anche  
 [Composizione dei flussi](https://msdn.microsoft.com/library/e4y2dch9)   
 [I/O di file e di flussi](https://msdn.microsoft.com/library/k3352a4t)   
 [I/O di file asincrono](https://msdn.microsoft.com/library/kztecsys)   
 [Nozioni fondamentali sul file system e sulla funzionalità di I/O di file di .NET Framework (Visual Basic)](../../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)
