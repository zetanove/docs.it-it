---
title: "Sub or Function not defined (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID35"
dev_langs: 
  - "VB"
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Sub or Function not defined (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per essere chiamata, `Sub` o `Function` deve essere definita.  Alcune cause possibili di questo errore sono:  
  
-   Nome della routine digitato in modo errato.  
  
-   Tentativo di chiamare una routine da un altro progetto senza aggiungere in modo esplicito un riferimento a esso nella finestra di dialogo **Riferimenti**.  
  
-   Specifica di una routine invisibile alla routine chiamante.  
  
-   Dichiarazione di una routine di libreria a collegamento dinamico \(DLL\) di Windows o di una routine di risorsa di codice Macintosh che non si trova nella libreria o nella risorsa di codice specificata.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che il nome della routine sia digitato correttamente.  
  
2.  Cercare il nome del progetto contenente la routine che si desidera chiamare nella finestra di dialogo **Riferimenti**.  Se il progetto non è presente, fare clic sul pulsante **Sfoglia** per cercarlo.  Selezionare la casella di controllo che si trova alla sinistra del nome del progetto e scegliere **OK**.  
  
3.  Verificare il nome della routine.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)