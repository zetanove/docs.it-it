---
title: "Overflow (Visual Basic Run-Time Error) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrERRID_Overflow"
dev_langs: 
  - "VB"
ms.assetid: c6a23279-3086-412a-bcff-ff8ed2cb8c6f
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Overflow (Visual Basic Run-Time Error)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un overflow si verifica quando si tenta di effettuare un'assegnazione che supera i limiti della destinazione dell'assegnazione.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che i risultati delle assegnazioni, dei calcoli e delle conversioni di tipo di dati non siano troppo grandi per essere rappresentati all'interno dell'intervallo di variabili consentito per il tipo di valore specificato e assegnare il valore a una variabile di un tipo in grado di contenere, se necessario, un intervallo più grande di valori.  
  
2.  Assicurarsi che le assegnazioni alle proprietà rientrino in un intervallo valido per la proprietà per cui sono effettuate.  
  
3.  Assicurarsi che i numeri utilizzati nei calcoli assegnati forzatamente a valori integer non diano risultati superiori ai valori integer.  
  
## Vedere anche  
 <xref:System.Int32.MaxValue?displayProperty=fullName>   
 <xref:System.Double.MaxValue?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)