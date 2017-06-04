---
title: "Attivit&#224; di I/O comuni | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "I/O, attività comuni"
ms.assetid: bf00c380-706a-4e38-b829-454a480629fc
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
---
# Attivit&#224; di I/O comuni
Lo spazio dei nomi <xref:System.IO> fornisce molte classi che consentono di eseguire diverse operazioni, ad esempio la lettura e la scrittura, su file, directory e flussi.  Per ulteriori informazioni, vedere [I\/O di file e di flussi](../../../docs/standard/io/index.md).  
  
## Attività comuni sui file  
  
|Per eseguire questa operazione...|Vedere l'esempio riportato in questo argomento...|  
|---------------------------------------|-------------------------------------------------------|  
|Creare un file di testo|Metodo <xref:System.IO.File.CreateText%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.FileInfo.CreateText%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.File.Create%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.FileInfo.Create%2A?displayProperty=fullName>|  
|Scrivere in un file di testo|[Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)<br /><br /> [Procedura: scrivere un file di testo](../Topic/How%20to:%20Write%20a%20Text%20File%20\(C++-CLI\).md)|  
|Leggere da un file di testo|[Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md)|  
|Aggiungere testo a un file|[Procedura: Aprire e accodare un file di log](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)<br /><br /> Metodo <xref:System.IO.File.AppendText%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.FileInfo.AppendText%2A?displayProperty=fullName>|  
|Rinominare o spostare un file|Metodo <xref:System.IO.File.Move%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.FileInfo.MoveTo%2A?displayProperty=fullName>|  
|Eliminare un file|Metodo <xref:System.IO.File.Delete%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.FileInfo.Delete%2A?displayProperty=fullName>|  
|Copiare un file|Metodo <xref:System.IO.File.Copy%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.FileInfo.CopyTo%2A?displayProperty=fullName>|  
|Ottenere la dimensione di un file|Proprietà <xref:System.IO.FileInfo.Length%2A?displayProperty=fullName>|  
|Ottenere gli attributi di un file|Metodo <xref:System.IO.File.GetAttributes%2A?displayProperty=fullName>|  
|Impostare gli attributi di un file|Metodo <xref:System.IO.File.SetAttributes%2A?displayProperty=fullName>|  
|Verificare se un file esiste|Metodo <xref:System.IO.File.Exists%2A?displayProperty=fullName>|  
|Leggere da un file binario|[Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|  
|Scrivere in un file binario|[Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|  
|Recuperare un'estensione di file|Metodo <xref:System.IO.Path.GetExtension%2A?displayProperty=fullName>|  
|Recuperare il percorso completo di un file|Metodo <xref:System.IO.Path.GetFullPath%2A?displayProperty=fullName>|  
|Recuperare il nome e l'estensione di un file da un percorso|Metodo <xref:System.IO.Path.GetFileName%2A?displayProperty=fullName>|  
|Cambiare l'estensione di un file|Metodo <xref:System.IO.Path.ChangeExtension%2A?displayProperty=fullName>|  
  
## Attività comuni sulle directory  
  
|Per eseguire questa operazione...|Vedere l'esempio riportato in questo argomento...|  
|---------------------------------------|-------------------------------------------------------|  
|Accedere a un file in una cartella speciale, ad esempio Documenti|[Procedura: Scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md)|  
|Creare una directory|Metodo <xref:System.IO.Directory.CreateDirectory%2A?displayProperty=fullName><br /><br /> Proprietà <xref:System.IO.FileInfo.Directory%2A?displayProperty=fullName>|  
|Creare una sottodirectory|Metodo <xref:System.IO.DirectoryInfo.CreateSubdirectory%2A?displayProperty=fullName>|  
|Rinominare o spostare una directory|Metodo <xref:System.IO.Directory.Move%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.DirectoryInfo.MoveTo%2A?displayProperty=fullName>|  
|Copiare una directory|[Procedura: copiare le directory](../../../docs/standard/io/how-to-copy-directories.md)|  
|Eliminare una directory|Metodo <xref:System.IO.Directory.Delete%2A?displayProperty=fullName><br /><br /> Metodo <xref:System.IO.DirectoryInfo.Delete%2A?displayProperty=fullName>|  
|Visualizzare i file e le sottodirectory in una directory|[Procedura: enumerare directory e file](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)|  
|Ottenere la dimensione di una directory|Classe <xref:System.IO.Directory?displayProperty=fullName>|  
|Verificare se una directory esiste|Metodo <xref:System.IO.Directory.Exists%2A?displayProperty=fullName>|  
  
## Vedere anche  
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)   
 [Composizione dei flussi](../../../docs/standard/io/composing-streams.md)   
 [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md)