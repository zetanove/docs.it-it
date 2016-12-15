---
title: "Path/File access error | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrID75"
dev_langs: 
  - "VB"
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Path/File access error
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Durante un'operazione di accesso a un file o a un disco, il sistema operativo non è riuscito a creare una connessione tra il percorso e il nome del file.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che la formattazione della specifica del file sia corretta.  Un nome file può contenere un percorso completo \(assoluto\) o relativo.  Il percorso completo inizia con il nome dell'unità \(se il percorso si riferisce a un'altra unità\) e riporta il percorso esplicito dal primo livello al file.  Ogni percorso che non sia completo è relativo all'unità e alla directory corrente.  
  
2.  Assicurarsi di non aver tentato di salvare un file che avrebbe sostituito un file di sola lettura esistente.  Se si è verificato questo problema, cambiare l'attributo di sola lettura del file di destinazione o salvare il file con un altro nome.  
  
3.  Assicurarsi di non aver tentato di aprire un file di sola lettura in una modalità`Output`o `Append` sequenziale.  Se si è verificato questo problema, aprire il file in modalità `Input` o cambiare l'attributo di sola lettura del file.  
  
4.  Assicurarsi di non aver tentato di modificare un progetto [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] in un database o un documento.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)