---
title: "Procedura: scrivere in un file di testo (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "TextWriter.WriteLine"
  - "StreamWriter.Close"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "file [C#], testo (file)"
  - "testo, scrittura su file [C#]"
ms.assetid: 2e99f184-d88b-4719-a7f1-d9ec482aa809
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# Procedura: scrivere in un file di testo (Guida per programmatori C#)
In questi esempi vengono mostrati vari modi per scrivere testo in un file.  I primi due esempi usano metodi pratici statici nella classe <xref:System.IO.File?displayProperty=fullName> per scrivere ogni elemento di un oggetto IEnumerable\<string\> e di una stringa in un file di testo.  Nell'esempio 3 viene illustrato come aggiungere testo a un file quando è necessario elaborare individualmente ogni riga mentre si scrive nel file.  Gli esempi da 1 a 3 sovrascrivono tutto il contenuto esistente nel file, ma l'esempio 4 mostra come aggiungere il testo a un file esistente.  
  
 In tutti gli esempi vengono scritti valori letterali stringa nei file, ma può essere più opportuno utilizzare il metodo <xref:System.String.Format%2A>, che presenta molti controlli per la scrittura di tipi diversi di valori giustificati a destra o a sinistra in un campo, con o senza riempimento e così via.  È anche possibile usare la funzionalità di [interpolazione di stringhe](../../../csharp/language-reference/keywords/interpolated-strings.md) di C\#.  
  
## Esempio  
 [!code-cs[csFilesandFolders#3](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#3)]  
  
 In tutti gli esempi vengono scritti valori letterali stringa nei file, ma può essere più opportuno utilizzare il metodo <xref:System.String.Format%2A>, che presenta molti controlli per la scrittura di tipi diversi di valori giustificati a destra o a sinistra in un campo, con o senza riempimento e così via.  È anche possibile usare la funzionalità di [interpolazione di stringhe](../../../csharp/language-reference/keywords/interpolated-strings.md) di C\#.  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il file esiste ed è di sola lettura.  
  
-   Il nome del percorso è troppo lungo.  
  
-   Il disco è pieno.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)   
 [Esempio: Salvare una raccolta nell'archiviazione di applicazioni](http://code.msdn.microsoft.com/CSWinStoreAppSaveCollection-bed5d6e6)