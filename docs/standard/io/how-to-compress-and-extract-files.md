---
title: "Procedura: comprimere ed estrarre file | Microsoft Docs"
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
  - "I/O [.NET Framework], compressione"
  - "compressione"
  - "comprimere file"
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
caps.latest.revision: 19
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: comprimere ed estrarre file
Lo spazio dei nomi <xref:System.IO.Compression> contiene i seguenti tipi per la compressione e decompressione dei file e flussi.  È inoltre possibile utilizzare questi tipi per leggere e modificare il contenuto di un file compresso:  
  
-   <xref:System.IO.Compression.ZipFile>  
  
-   <xref:System.IO.Compression.ZipArchive>  
  
-   <xref:System.IO.Compression.ZipArchiveEntry>  
  
-   <xref:System.IO.Compression.DeflateStream>  
  
-   <xref:System.IO.Compression.GZipStream>  
  
 Nei seguenti esempi vengono illustrate alcune funzioni che è possibile eseguire quando si utilizzano file compressi.  
  
## Esempio  
 In questo esempio viene illustrato come creare e estrarre un file compresso con estensione .zip utilizzando la classe <xref:System.IO.Compression.ZipFile>.  Esso comprime il contenuto di una cartella in un nuovo file con estensione .zip e successivamente estrae in contenuto in una nuoca cartella.  Per utilizzare la classe <xref:System.IO.Compression.ZipFile>, è necessario fare riferimento all'assembly `System.IO.Compression.FileSystem` nel progetto.  
  
 [!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
 [!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene mostrati come scorrere il contenuto di un file esistente con estensione .zip ed estrarre file che hanno estensione .txt.  Utilizza la classe <xref:System.IO.Compression.ZipArchive> per accedere a un file esistente con estensione .zip e la classe <xref:System.IO.Compression.ZipArchiveEntry> per controllare le singole voci nel file compresso.  Utilizza un metodo di estensione \(<xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A>\) per l'oggetto <xref:System.IO.Compression.ZipArchiveEntry>.  Il metodo di estensione è disponibile nella classe <xref:System.IO.Compression.ZipFileExtensions?displayProperty=fullName>.  Per utilizzare la classe <xref:System.IO.Compression.ZipFileExtensions>, è necessario fare riferimento all'assembly `System.IO.Compression.FileSystem` nel proprio progetto.  
  
 [!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
 [!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.IO.Compression.ZipArchive> per accedere a un file esistente con estensione .zip e viene aggiunto un nuovo file al file compresso.  Il nuovo file viene compresso quando lo si aggiunge al file esistente con estensione zip.  
  
 [!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
 [!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]  
  
## Esempio  
 È inoltre possibile utilizzare le classi <xref:System.IO.Compression.DeflateStream> e <xref:System.IO.Compression.GZipStream> per comprimere e decomprimere dati.  Utilizzano lo stesso algoritmo di compressione.  Gli oggetti compressi <xref:System.IO.Compression.GZipStream> scritti in un file con estensione .gz possono essere decompressi utilizzando numerosi strumenti comuni oltre ai metodi forniti da <xref:System.IO.Compression.GZipStream>.  Nell'esempio viene illustrato come comprimere e decomprimere una directory di file utilizzando la classe <xref:System.IO.Compression.GZipStream>.  
  
 [!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
 [!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]  
  
## Vedere anche  
 <xref:System.IO.Compression.ZipArchive>   
 <xref:System.IO.Compression.ZipFile>   
 <xref:System.IO.Compression.ZipArchiveEntry>   
 <xref:System.IO.Compression.DeflateStream>   
 <xref:System.IO.Compression.GZipStream>   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)