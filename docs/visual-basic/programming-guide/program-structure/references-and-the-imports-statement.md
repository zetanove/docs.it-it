---
title: "References and the Imports Statement (Visual Basic) | Microsoft Docs"
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
  - "assemblies [Visual Basic], namespaces"
  - "references, assembly"
  - "namespaces, assemblies"
  - "referencing assemblies"
  - "Imports statement, referencing assemblies"
  - "assemblies [Visual Basic], references"
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# References and the Imports Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile rendere disponibili per il progetto oggetti esterni scegliendo il comando **Aggiungi riferimento** dal menu **Progetto**.  I riferimenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] possono essere relativi ad assembly, ossia oggetti simili a librerie di tipi ma in grado di contenere una maggiore quantità di informazioni.  
  
## Istruzione Imports  
 Gli assembly comprendono uno o più spazi dei nomi.  Quando si aggiunge un riferimento a un assembly, è anche possibile aggiungere un'istruzione `Imports` a un modulo che controlla la visibilità degli spazi dei nomi dell'assembly all'interno del modulo.  L'istruzione `Imports` fornisce un contesto di ambito che consente di utilizzare solamente la parte dello spazio dei nomi necessaria per fornire un riferimento univoco.  
  
 Di seguito è riportata la sintassi dell'istruzione `Imports`.  
  
 `Imports` \[         `|` `Aliasname` \=\] `Namespace`  
  
 `Aliasname` si riferisce a un nome breve che è possibile utilizzare all'interno del codice per fare riferimento a uno spazio dei nomi importato.  `Namespace` è uno spazio dei nomi disponibile tramite un riferimento al progetto, una definizione all'interno del progetto o un'istruzione `Imports` precedente.  
  
 Un modulo può contenere un numero qualsiasi di istruzioni `Imports`.  Tali istruzioni devono essere visualizzate dopo eventuali istruzioni `Option` ma prima di qualsiasi altro codice.  
  
> [!NOTE]
>  Non confondere i riferimenti al progetto con l'istruzione `Imports` o `Declare`.  I riferimenti al progetto rendono disponibili gli oggetti esterni, ad esempio quelli inclusi negli assembly, per i progetti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  L'istruzione `Imports` viene utilizzata per semplificare l'accesso ai riferimenti al progetto, ma non fornisce alcun accesso a questi oggetti.  L'istruzione `Declare` viene utilizzata per dichiarare un riferimento a una routine esterna in una DLL.  
  
## Utilizzo degli alias con l'istruzione Imports  
 L'istruzione `Imports` semplifica l'accesso ai metodi delle classi, eliminando la necessità di digitare in modo esplicito il nome completo dei riferimenti.  Gli alias consentono di assegnare un nome più descrittivo a una sola parte di uno spazio dei nomi.  Ad esempio, la sequenza di ritorno a capo\/avanzamento riga che determina la visualizzazione di una singola porzione di testo su più righe fa parte del modulo <xref:Microsoft.VisualBasic.ControlChars> nello spazio dei nomi <xref:Microsoft.VisualBasic?displayProperty=fullName>.  Per utilizzare questa costante in un programma, senza un alias, sarebbe necessario digitare il codice che segue:  
  
 [!code-vb[VbVbalrApplication#3](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_1.vb)]  
  
 Le istruzioni `Imports` devono essere sempre contenute nelle prime righe immediatamente successive alle istruzioni `Option` in un modulo.  Nel frammento di codice riportato di seguito viene illustrato come importare e assegnare un alias al modulo <xref:Microsoft.VisualBasic.ControlChars?displayProperty=fullName>:  
  
 [!code-vb[VbVbalrApplication#4](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_2.vb)]  
  
 I riferimenti successivi a questo spazio dei nomi possono essere molto più brevi:  
  
 [!code-vb[VbVbalrApplication#5](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_3.vb)]  
  
 Se un'istruzione `Imports` non include un nome alias, gli elementi definiti all'interno dello spazio dei nomi importato possono essere utilizzati nel modulo senza qualificazione.  Se il nome alias è specificato, deve essere utilizzato come qualificatore per i nomi contenuti all'interno di quello spazio dei nomi.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ControlChars>   
 <xref:Microsoft.VisualBasic>   
 [NIB How to: Add or Remove References By Using the Add Reference Dialog Box](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: Creare e usare assembly dalla riga di comando](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)