---
title: "Variables in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "variables [Visual Basic]"
  - "values [Visual Basic], storing"
ms.assetid: 4cfaa06d-4ae3-4307-897b-cf599dc24caa
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# Variables in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È spesso necessario archiviare valori durante l'esecuzione di calcoli con [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  È possibile, ad esempio, calcolare diversi valori, confrontarli ed eseguire con essi varie operazioni, a seconda del risultato del confronto.  Per confrontare i valori, è necessario mantenerli.  
  
## Utilizzo  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], come nella maggior parte dei linguaggi di programmazione, le variabili vengono utilizzate per archiviare i valori.  Ogni *variabile* ha un nome, ovvero la parola utilizzata per fare riferimento al valore contenuto dalla variabile.  Ogni variabile ha anche un tipo di dati, che determina il tipo di dati che è possibile archiviare nella variabile.  Una variabile può rappresentare una matrice, se è necessario archiviare un insieme indicizzato di elementi dati strettamente correlati.  
  
 L'inferenza di tipi locali consente di dichiarare variabili senza specificare un tipo di dati in modo esplicito.  Tramite l'inferenza, il compilatore deriva il tipo della variabile dal tipo dell'espressione dell'inizializzazione.  Per ulteriori informazioni, vedere [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) e [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## Assegnazione di valori  
 Utilizzare le istruzioni di assegnazione per eseguire calcoli e assegnare il risultato a una variabile, come nell'esempio seguente.  
  
 [!code-vb[VbVbalrVariables#1](../../../../visual-basic/programming-guide/language-features/variables/codesnippet/VisualBasic/index_1.vb)]  
  
> [!NOTE]
>  Il segno uguale \(`=`\) nell'esempio rappresenta un operatore di assegnazione, non di uguaglianza.  Il valore viene assegnato alla variabile `applesSold`.  
  
 Per ulteriori informazioni, vedere [How to: Move Data Into and Out of a Variable](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md).  
  
## Variabili e proprietà  
 Come una variabile, anche una *proprietà* rappresenta un valore al quale è possibile accedere.  Tuttavia, la proprietà è più complessa di una variabile.  La proprietà utilizza blocchi di codice che consentono di controllare l'impostazione e il recupero del relativo valore.  Per ulteriori informazioni, vedere [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md).  
  
## Vedere anche  
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Risoluzione dei problemi relativi alle variabili](../../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)   
 [How to: Move Data Into and Out of a Variable](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)