---
title: "Class does not support Automation or does not support expected interface | Microsoft Docs"
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
  - "vbrID430"
dev_langs: 
  - "VB"
ms.assetid: d985bb7e-e48e-443e-86f2-ddb86758757c
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Class does not support Automation or does not support expected interface
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La classe specificata nella funzione `GetObject` o `CreateObject` non ha esposto un'interfaccia di programmabilità oppure è stato modificato un progetto da .dll a .exe o viceversa.  
  
### Per correggere l'errore  
  
1.  Consultare la documentazione dell'applicazione che ha creato l'oggetto per verificare l'eventuale presenza di limitazioni sull'uso dell'automazione.  
  
2.  Se è stato modificato un progetto da .dll a .exe o viceversa, è necessario annullare manualmente la registrazione del precedente .dll o .exe.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)