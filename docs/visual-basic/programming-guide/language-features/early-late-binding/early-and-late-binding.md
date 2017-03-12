---
title: "Early and Late Binding (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "02/25/2017"
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
  - "early binding"
  - "objects [Visual Basic], late-bound"
  - "objects [Visual Basic], early-bound"
  - "objects [Visual Basic], late bound"
  - "early binding, Visual Basic compiler"
  - "binding, late and early"
  - "objects [Visual Basic], early bound"
  - "Visual Basic compiler, early and late binding"
  - "late binding"
  - "late binding, Visual Basic compiler"
ms.assetid: d6ff7f1e-b94f-4205-ab8d-5cfa91758724
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Early and Late Binding (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando un oggetto viene assegnato a una variabile oggetto, il compilatore di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] esegue un processo definito `binding`.  Un oggetto viene *associato anticipatamente* quando viene assegnato a una variabile di un tipo specifico di oggetto.  Gli oggetti ad associazione anticipata consentono al compilatore di allocare memoria ed eseguire altre ottimizzazioni prima dell'esecuzione di un'applicazione.  Nel frammento di codice riportato di seguito, ad esempio, viene dichiarata una variabile di tipo <xref:System.IO.FileStream>.  
  
 [!code-vb[VbVbalrOOP#90](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#90)]  
  
 Poiché <xref:System.IO.FileStream> è un tipo di oggetto specifico, l'istanza assegnata a `FS` presenta un'associazione anticipata.  
  
 Al contrario, un oggetto viene *associato tardivamente* quando viene assegnato a una variabile dichiarata di tipo `Object`.  Gli oggetti di questo tipo possono contenere riferimenti a qualsiasi oggetto, ma non sono in grado di offrire molti dei vantaggi degli oggetti associati anticipatamente.  Nel frammento di codice che segue, ad esempio, viene dichiarata una variabile oggetto contenente un oggetto restituito dalla funzione `CreateObject`.  
  
 [!code-vb[VbVbalrOOP#91](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/LateBinding.vb#91)]  
  
## Vantaggi dell'associazione anticipata  
 Se possibile, si consiglia di utilizzare gli oggetti ad associazione anticipata, che consentono di effettuare ottimizzazioni rilevanti e di migliorare l'efficienza delle applicazioni.  Gli oggetti associati anticipatamente sono significativamente più veloci degli oggetti associati tardivamente e facilitano la lettura e la gestione del codice dichiarando esattamente il tipo di oggetti utilizzati.  L'associazione anticipata consente inoltre di attivare funzionalità utili quali il completamento automatico del codice e la Guida dinamica, poiché l'ambiente di sviluppo integrato \(IDE, Integrated Development Environment\) di [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] è in grado di determinare esattamente quali tipi di oggetto vengono utilizzati durante la modifica del codice.  Grazie all'associazione anticipata è possibile ridurre il numero e la gravità degli errori in fase di esecuzione, in quanto gli errori possono essere segnalati in fase di compilazione del programma.  
  
> [!NOTE]
>  È possibile utilizzare l'associazione tardiva solo per accedere a membri di tipi dichiarati come `Public`.  L'accesso a membri dichiarati come `Friend` o `Protected Friend` determina errori di runtime.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>   
 [Object Lifetime: How Objects Are Created and Destroyed](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)