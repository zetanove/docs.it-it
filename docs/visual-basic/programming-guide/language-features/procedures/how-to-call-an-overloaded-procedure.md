---
title: "How to: Call an Overloaded Procedure (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, procedures"
  - "procedures, overloading"
  - "procedures, calling"
  - "procedures, multiple versions"
  - "procedure calls, overloaded"
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# How to: Call an Overloaded Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il vantaggio dell'esecuzione dell'overload di una routine è rappresentato dalla flessibilità della chiamata.  Il codice chiamante può ottenere le informazioni necessarie da passare alla routine, quindi chiamare un singolo nome di routine indipendentemente dagli argomenti che sta passando.  
  
### Per chiamare una routine per cui sono definite più versioni  
  
1.  Nel codice chiamante stabilire i dati da passare alla routine.  
  
2.  Scrivere normalmente la chiamata di routine presentando i dati nell'elenco degli argomenti.  Accertarsi che gli argomenti corrispondano all'elenco di parametri in una delle versioni definite per la routine.  
  
3.  Non è necessario stabilire quale versione della routine chiamare.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] il controllo viene passato alla versione che corrisponde all'elenco di argomenti.  
  
     Nell'esempio riportato di seguito viene chiamata la routine `post` dichiarata in [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md).  Tale chiamata ottiene l'identificazione del cliente, determina se si tratta di un valore `String` o di un `Integer` e, in entrambi i casi, chiama la stessa routine.  
  
     [!code-vb[VbVbcnProcedures#56](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-call-an-overloade_1.vb)]  
  
     [!code-vb[VbVbcnProcedures#57](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-call-an-overloade_2.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [How to: Overload a Procedure that Takes Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [How to: Overload a Procedure that Takes an Indefinite Number of Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)