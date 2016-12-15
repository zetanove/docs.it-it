---
title: "How to: Declare an Object Variable and Assign an Object to It in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "object variables, declaring"
  - "declaring object variables"
ms.assetid: 2fa77dde-1fb2-439a-80d4-3e9787649fad
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Declare an Object Variable and Assign an Object to It in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile dichiarare una variabile del [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md) specificando `As Object` in un'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md).  Per assegnare un oggetto a tale variabile, inserirlo dopo il segno uguale \(`=`\) in un'istruzione di assegnazione o in una clausola di inizializzazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarata una variabile `Object` alla quale viene assegnata l'istanza corrente.  
  
```  
  
      Dim thisObject As Object  
thisObject = "This is an Object"  
```  
  
 È possibile combinare la dichiarazione e l'assegnazione mediante l'inizializzazione della variabile come parte della rispettiva dichiarazione.  L'esempio che segue equivale a quello precedente.  
  
```  
Dim thisObject As Object = "This is an Object"  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un riferimento allo spazio dei nomi <xref:System>.  
  
-   Una classe, una struttura o un modulo in cui inserire l'istruzione `Dim`.  
  
-   Una routine in cui inserire l'istruzione di assegnazione.  
  
## Vedere anche  
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Declaration](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)