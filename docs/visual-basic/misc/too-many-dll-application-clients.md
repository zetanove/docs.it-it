---
title: "Troppe applicazioni client DLL | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID47"
ms.assetid: 4b87780b-67ad-4c96-9253-db954a751dad
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Troppe applicazioni client DLL
La libreria di collegamento dinamico \(DLL\) per [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] supporta solo l'accesso a un numero limitato di applicazioni host. L'applicazione e altre applicazioni che sono host di [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] \(alcune delle quali sono accessibili dall'applicazione\) stanno tentando di accedere contemporaneamente alla DLL [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
### Per correggere l'errore  
  
-   Ridurre il numero di applicazioni aperte che accedono a [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
## Vedere anche  
 [Error Types](../../visual-basic/programming-guide/language-features/error-types.md)