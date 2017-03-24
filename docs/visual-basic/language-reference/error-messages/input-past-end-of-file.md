---
title: "Input past end of file | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID62"
dev_langs: 
  - "VB"
ms.assetid: 65292704-6e7d-4622-9f50-eb655a59b016
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Input past end of file
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'istruzione `Input` sta leggendo un file vuoto o i cui dati sono tutti utilizzati, oppure la funzione `EOF` è stata utilizzata con un file aperto per l'accesso binario.  
  
### Per correggere l'errore  
  
1.  Utilizzare la funzione `EOF` subito prima dell'istruzione `Input` per individuare la fine del file.  
  
2.  Se il file è aperto per l'accesso binario, utilizzare `Seek` e `Loc`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem.Input%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.EOF%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.Seek%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.Loc%2A>