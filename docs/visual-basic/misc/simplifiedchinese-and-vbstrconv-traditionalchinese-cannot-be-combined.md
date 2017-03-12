---
title: "SimplifiedChinese e VbStrConv.TraditionalChinese non possono essere combinati | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrArgument_StrConvSCandTC"
ms.assetid: d8e6a11b-f549-43b5-8337-0594340e1325
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# SimplifiedChinese e VbStrConv.TraditionalChinese non possono essere combinati
L'applicazione sta tentando di combinare i membri `SimplifiedChinese` e `TraditionalChinese` dell'enumerazione `VbStrConv`, che si escludono reciprocamente.  
  
### Per correggere l'errore  
  
-   Rimuovere  `VbStrConv.SimplifiedChinese` o `VbStrConv.TraditionalChinese`.  
  
## Vedere anche  
 <xref:System.Globalization>   
 [NOTINBUILD Enumerazione VbStrConv](http://msdn.microsoft.com/it-it/59f83dd9-6361-47df-a836-02ba9d4cb936)   
 [Introduzione alle applicazioni internazionali basate su .NET Framework](/visual-studio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)