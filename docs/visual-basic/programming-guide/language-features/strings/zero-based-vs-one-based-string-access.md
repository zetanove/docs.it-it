---
title: "Zero-based vs. One-based String Access in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "strings [Visual Basic], indexing"
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Zero-based vs. One-based String Access in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento Viene confrontato il modo in cui viene fornito l'accesso ai caratteri di una stringa in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] e in [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] consente sempre l'accesso ai caratteri di una stringa in base zero, mentre [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce l'accesso sia in base zero sia in base uno, a seconda della funzione.  
  
## Base uno  
 Per un esempio di funzione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] in base uno, considerare la funzione `Mid`.  Questa accetta un argomento che indica la posizione del carattere in cui inizia la sottostringa, a partire dalla posizione 1.  Il metodo <xref:System.String.Substring%2A?displayProperty=fullName> di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] accetta un indice del carattere nella stringa in cui inizia la sottostringa desiderata, a partire dalla posizione 0.  Se quindi si dispone di una stringa "ABCDE", ai singoli caratteri viene assegnata la numerazione 1,2,3,4,5 per consentirne l'utilizzo con la funzione `Mid`, ma la numerazione 0,1,2,3,4 per l'utilizzo con il metodo <xref:System.String.Substring%2A?displayProperty=fullName>.  
  
## Base zero  
 Per un esempio di funzione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] in base zero, considerare la funzione `Split`.  Questa funzione divide la stringa e restituisce una matrice contenente le sottostringhe.  Anche il metodo <xref:System.String.Split%2A?displayProperty=fullName> di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] divide la stringa e restituisce una matrice contenente le sottostringhe.  Poiché la funzione `Split` e il metodo <xref:System.String.Split%2A> restituiscono matrici [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)], è necessario che siano in base zero.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:System.String.Substring%2A>   
 <xref:System.String.Split%2A>   
 [Introduction to Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)