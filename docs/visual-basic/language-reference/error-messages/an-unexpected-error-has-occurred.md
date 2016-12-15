---
title: "An unexpected error has occurred because an operating system resource required for single instance startup cannot be acquired | Microsoft Docs"
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
  - "vbrAppModel_CantGetMemoryMappedFile"
dev_langs: 
  - "VB"
ms.assetid: 0d9f2a30-ff72-4355-8060-744f22339359
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# An unexpected error has occurred because an operating system resource required for single instance startup cannot be acquired
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'applicazione non è riuscita ad acquisire una risorsa del sistema operativo necessaria.  Alcune possibili cause di questo problema sono:  
  
-   L'applicazione non dispone di autorizzazioni per la creazione di oggetti del sistema operativo denominati.  
  
-   Common Language Runtime non dispone di autorizzazioni per la creazione di file mappati alla memoria.  
  
-   L'applicazione deve accedere a un oggetto del sistema operativo, ma un altro processo lo sta usando.  
  
### Per correggere l'errore  
  
1.  Verificare che l'applicazione disponga di autorizzazioni sufficienti per la creazione di oggetti del sistema operativo denominati.  
  
2.  Verificare che Common Language Runtime disponga di autorizzazioni sufficienti per la creazione di file mappati alla memoria.  
  
3.  Riavviare il computer per cancellare i processi che stanno usando la risorsa necessaria per la connessione all'istanza originale.  
  
4.  Prendere nota delle circostanze in cui si è verificato l'errore e contattare il Servizio Supporto Tecnico Clienti Microsoft.  
  
## Vedere anche  
 [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [Nozioni di base sul debugger](/visual-studio/debugger/debugger-basics)   
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)