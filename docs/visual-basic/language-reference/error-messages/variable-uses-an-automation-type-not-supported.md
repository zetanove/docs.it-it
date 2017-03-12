---
title: "Variable uses an Automation type not supported in Visual Basic | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID458"
dev_langs: 
  - "VB"
ms.assetid: bde4f4da-493b-452c-b6e4-1d370edba4cd
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Variable uses an Automation type not supported in Visual Basic
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Si è tentato di utilizzare una variabile definita in una libreria di tipi o di oggetti con un tipo di dati non supportato in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
### Per correggere l'errore  
  
-   Utilizzare una variabile di un tipo riconosciuto in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
     In alternativa  
  
-   Se quest'errore si verifica durante l'utilizzo di `FileGet` o `FileGetOBject`, controllare che nel file che si sta tentando di utilizzare si sia scritto tramite `FilePut` o `FilePutObject`.  
  
## Vedere anche  
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)