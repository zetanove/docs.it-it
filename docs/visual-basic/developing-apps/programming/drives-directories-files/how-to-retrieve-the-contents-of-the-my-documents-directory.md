---
title: 'Procedura: Recuperare il contenuto della directory Documenti in Visual Basic | Microsoft Docs'
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
- My Documents directory
ms.assetid: 26560d01-7dda-4457-8e95-21db23d71aea
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 39e1d8b4d7e613bf245769816ef24a7787f41e04
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-retrieve-the-contents-of-the-my-documents-directory-in-visual-basic"></a>Procedura: recuperare il contenuto della directory Documenti in Visual Basic
L'oggetto <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories> può essere usato per leggere il contenuto di molte delle directory di **Tutti gli utenti**, ad esempio **Documenti** o **Desktop**.  
  
### <a name="to-read-from-the-my-documents-folder"></a>Per leggere il contenuto dalla cartella Documenti  
  
-   Usare il metodo `ReadAllText` per leggere il testo di ogni file in una directory specifica. Il codice seguente consente di specificare una directory e un file e di usare `ReadAllText` per leggere il contenuto nella stringa denominata `patients`.  
  
     [!code-vb[VbVbcnMyFileSystem#15](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-retrieve-the-contents-of-the-my-documents-directory_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>
