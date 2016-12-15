---
title: "&#39;Dir&#39; function must first be called with a &#39;PathName&#39; argument | Microsoft Docs"
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
  - "vbrDIR_IllegalCall"
dev_langs: 
  - "VB"
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;Dir&#39; function must first be called with a &#39;PathName&#39; argument
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una chiamata iniziale alla funzione `Dir` non include l'argomento `PathName`.  La prima chiamata a `Dir` deve includere un `PathName`, ma le chiamate successive a `Dir` non hanno bisogno di includere parametri per recuperare l'elemento successivo.  
  
### Per correggere l'errore  
  
1.  Fornire un argomento `PathName` nella chiamata di funzione.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>