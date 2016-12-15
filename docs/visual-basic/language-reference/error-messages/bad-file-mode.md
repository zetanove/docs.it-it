---
title: "Bad file mode | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrID54"
dev_langs: 
  - "VB"
ms.assetid: 74891e96-884b-4c8d-872d-cd11ae272372
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Bad file mode
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È necessario che le istruzioni utilizzate nella modifica dei contenuti del file siano appropriate alla modalità in cui il file è stato aperto.  Fra le cause possibili vi sono le seguenti:  
  
-   Un'istruzione `FilePutObject` o `FileGetObject` specifica un file sequenziale.  
  
-   Un'istruzione `Print` specifica un file aperto per una modalità di accesso diversa da `Output` o `Append`.  
  
-   Un'istruzione `Input` specifica un file aperto per una modalità di accesso diversa da `Input`  
  
-   Si è tentato di scrivere in un file in sola lettura.  
  
### Per correggere l'errore  
  
-   Assicurarsi che `FilePutObject` e `FileGetObject` facciano riferimento solo a file aperti per l'accesso `Random` o `Binary`.  
  
-   Assicurarsi che `Print` specifichi un file aperto per la modalità di accesso `Output` o `Append`.  In caso contrario, utilizzare un'istruzione diversa per inserire dati nel file o riaprire il file in una modalità appropriata.  
  
-   Assicurarsi che `Input` specifichi un file aperto per `Input`.  In caso contrario, utilizzare un'istruzione diversa per inserire dati nel file o riaprire il file in una modalità appropriata.  
  
-   Se si sta scrivendo in un file di sola lettura, modificare lo stato di lettura\/scrittura del file o non tentare di scrivere in esso.  
  
-   Utilizzare la funzionalità disponibile nell'oggetto `My.Computer.FileSystem`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem>   
 [Troubleshooting: Reading from and Writing to Text Files](../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)