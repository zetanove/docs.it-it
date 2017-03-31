---
title: "Procedura: Ottenere informazioni relative a file, cartelle e unità (Guida per programmatori C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- files [C#], getting information about
ms.assetid: 22fc2da6-5494-405b-995e-c0b99142a93e
caps.latest.revision: 30
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: 16950f835938846804ade1a8ad23d907aa69b9c3
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-get-information-about-files-folders-and-drives--c-programming-guide"></a>Procedura: ottenere informazioni relative a file, cartelle e unità (Guida per programmatori C#)
In .NET Framework è possibile accedere a informazioni sul file system mediante le classi seguenti:  
  
-   <xref:System.IO.FileInfo?displayProperty=fullName>  
  
-   <xref:System.IO.DirectoryInfo?displayProperty=fullName>  
  
-   <xref:System.IO.DriveInfo?displayProperty=fullName>  
  
-   <xref:System.IO.Directory?displayProperty=fullName>  
  
-   <xref:System.IO.File?displayProperty=fullName>  
  
 Le classi <xref:System.IO.FileInfo> e <xref:System.IO.DirectoryInfo> rappresentano un file o una directory e contengono proprietà che espongono molti degli attributi di file che sono supportati dal file system NTFS. Contengono anche i metodi per l'apertura, la chiusura, lo spostamento e l'eliminazione di file e cartelle. È possibile creare istanze di queste classi passando al costruttore una stringa che rappresenta il nome del file, della cartella o dell'unità:  
  
```csharp  
System.IO.DriveInfo di = new System.IO.DriveInfo(@"C:\");  
```  
  
 È anche possibile ottenere i nomi di file, cartelle o unità tramite le chiamate a <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=fullName>, <xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=fullName>, e <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=fullName>.  
  
 Le classi <xref:System.IO.Directory?displayProperty=fullName> e <xref:System.IO.File?displayProperty=fullName> specificano metodi statici per il recupero di informazioni su file e directory.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra vari modi per accedere alle informazioni su file e cartelle.  
  
 [!code-cs[csFilesandFolders#6](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-get-information-about-files-folders-and-drives_1.cs)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Quando si elaborano stringhe di percorso specificate dall'utente, occorre gestire anche le eccezioni per le condizioni seguenti:  
  
-   Il nome file non è valido. Ad esempio, contiene caratteri non validi o solo spazi vuoti.  
  
-   Il nome del file è Null.  
  
-   La lunghezza del nome del file è maggiore della lunghezza massima definita nel sistema.  
  
-   Il nome del file contiene i due punti (:).  
  
 Se l'applicazione non ha autorizzazioni sufficienti per leggere il file specificato, il metodo `Exists` restituisce `false` indipendentemente dal fatto che il percorso esista. Il metodo non genera un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema (Guida per programmatori C#)](../../../csharp/programming-guide/file-system/index.md)
