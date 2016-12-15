---
title: "WithEvents (Visual Basic) | Microsoft Docs"
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
  - "vb.WithEvents"
  - "WithEvents"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "WithEvents keyword"
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# WithEvents (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di specificare che una o più variabili membro dichiarate si riferiscono a un'istanza di una classe in grado di generare eventi.  
  
## Note  
 Quando viene definita una variabile con `WithEvents`, è possibile utilizzare la parola chiave `Handles` per specificare in sede di dichiarazione che un metodo gestisce gli eventi della variabile.  
  
 È possibile utilizzare `WithEvents` solo a livello di classe o di modulo.  In altri termini, il contesto della dichiarazione per una variabile `WithEvents` deve essere una classe o un modulo e non può essere un file di origine, uno spazio dei nomi, una struttura o una routine.  
  
 Non è possibile utilizzare `WithEvents` su un membro della struttura.  
  
 Con `WithEvents` è possibile dichiarare solo variabili singole e non matrici.  
  
## Regole  
  
-   **Tipi degli elementi.** È necessario dichiarare le variabili `WithEvents` come variabili oggetto in modo che accettino le istanze di classe.  Non è tuttavia possibile dichiarare le variabili come `Object`.  È necessario dichiarare le variabili come la classe specifica in grado di generare eventi.  
  
 È possibile utilizzare il modificatore `WithEvents` nel seguente contesto: [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## Vedere anche  
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)