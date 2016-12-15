---
title: "Permission denied (Visual Basic) | Microsoft Docs"
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
  - "vbrID70"
dev_langs: 
  - "VB"
ms.assetid: 71f46756-f522-4814-aab4-492bf9924245
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Permission denied (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Si è tentato di scrivere su un disco protetto da scrittura o di accedere a un file bloccato.  
  
### Per correggere l'errore  
  
1.  Per aprire un file protetto da scrittura, modificare l'attributo del file relativo alla protezione dalla scrittura.  
  
2.  Assicurarsi che il file non sia bloccato da un altro processo e attendere che tale processo rilasci il file prima di aprirlo.  
  
3.  Per accedere al Registro di sistema, verificare che le autorizzazioni utente includano questo tipo di accesso al Registro di sistema.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)