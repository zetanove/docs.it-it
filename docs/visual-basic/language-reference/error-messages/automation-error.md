---
title: "Automation error | Microsoft Docs"
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
  - "vbrID440"
dev_langs: 
  - "VB"
ms.assetid: 2c4be5c5-2f0d-4a2b-96fe-d1b24f08fc4c
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Automation error
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Si è verificato un errore durante l'esecuzione di un metodo o durante il recupero o l'impostazione di una proprietà di una variabile oggetto.  L'errore è stato segnalato dall'applicazione che ha creato l'oggetto.  
  
### Per correggere l'errore  
  
1.  Verificare le proprietà dell'oggetto `Err` per determinare l'origine e la natura dell'errore.  
  
2.  Usare l'istruzione `On Error Resume Next` immediatamente prima dell'istruzione di accesso e quindi controllare subito la presenza di errori dopo l'istruzione di accesso.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)