---
title: "VbStrConv.Wide e VbStrConv.Narrow non possono essere combinati | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrArgument_IllegalWideNarrow"
ms.assetid: a53b4e6a-36b1-4e36-b2c5-8196313ec599
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# VbStrConv.Wide e VbStrConv.Narrow non possono essere combinati
L'applicazione sta tentando di combinare i membri `Wide` e `Narrow` dell'enumerazione `VbStrConv`, che si escludono reciprocamente.  
  
### Per correggere l'errore  
  
1.  Rimuovere `VbStrConv.Wide` o `VbStrConv.Narrow`.  
  
## Vedere anche  
 <xref:System.Globalization>   
 [NOTINBUILD Enumerazione VbStrConv](http://msdn.microsoft.com/it-it/59f83dd9-6361-47df-a836-02ba9d4cb936)   
 [Introduzione alle applicazioni internazionali basate su .NET Framework](/visual-studio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)