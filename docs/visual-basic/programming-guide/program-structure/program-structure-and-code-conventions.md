---
title: "Struttura del programma e convenzioni di scrittura del codice (Visual Basic) | Microsoft Docs"
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
  - "convenzioni per la scrittura di codice"
  - "Visual Basic (codice), convenzioni per la scrittura di codice"
  - "convenzioni per la scrittura di codice, Visual Basic"
  - "programmi, struttura"
  - "struttura dei programmi"
  - "convenzioni di denominazione, Visual Basic"
  - "procedure consigliate, convenzioni per la scrittura di codice"
  - "convenzioni, scrittura di codice Visual Basic"
  - "Visual Basic (codice)"
  - "programmazione, convenzioni per la scrittura di codice Visual Basic"
ms.assetid: dd9be76f-6944-4e78-ad72-0b6084a3fc13
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Struttura del programma e convenzioni di scrittura del codice (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa sezione viene fornita un'introduzione alla struttura tipica di un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], viene fornito un semplice programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], "Hello World", e vengono illustrate le convenzioni di scrittura del codice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Le convenzioni di scrittura del codice sono suggerimenti relativi non tanto alla logica del programma, quanto alla sua struttura fisica e al suo aspetto.  Seguendo queste istruzioni, il codice risultante sarà più semplice da leggere, comprendere e gestire.  Le convenzioni di scrittura del codice comprendono quanto segue:  
  
-   Formati standardizzati per l'inserimento di etichette e commenti nel codice,  
  
-   Istruzioni per la spaziatura, la formattazione e il rientro del codice,  
  
-   Convenzioni di denominazione per oggetti, variabili e routine.  
  
 Negli argomenti seguenti vengono illustrate alcune linee guida sulla programmazione di programmi [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], corredate da esempi di corretto utilizzo.  
  
## In questa sezione  
 [Structure of a Visual Basic Program](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 Viene fornita una panoramica degli elementi che compongono un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 [Main Procedure in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md)  
 Viene descritta la routine che funge da punto di partenza e controllo generale dell'applicazione.  
  
 [References and the Imports Statement](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)  
 Viene illustrato come fare riferimento agli oggetti in altri assembly.  
  
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)  
 Viene illustrato come vengono organizzati gli oggetti all'interno degli assembly da parte degli spazi dei nomi.  
  
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)  
 Vengono fornite indicazioni generali sulla denominazione di routine, costanti, variabili, argomenti e oggetti.  
  
 [Visual Basic Coding Conventions](../../../visual-basic/programming-guide/program-structure/coding-conventions.md)  
 Vengono esaminate le linee guida utilizzate per lo sviluppo degli esempi inclusi nella presente documentazione.  
  
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 Viene illustrato come compilare determinati blocchi di codice in modo selettivo e impostare il compilatore in modo da ignorarne altri.  
  
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)  
 Viene illustrato come suddividere lunghe istruzioni in più righe e combinare istruzioni brevi su una riga sola.  
  
 [How to: Collapse and Hide Sections of Code](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)  
 Viene illustrato come comprimere e nascondere sezioni di codice nell'editor del codice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 [How to: Label Statements](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)  
 Viene illustrato come contrassegnare una riga di codice per identificarla per l'utilizzo con istruzioni quali `On Error Goto`.  
  
 [Special Characters in Code](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)  
 Viene illustrato come e quando utilizzare i caratteri non numerici e non alfabetici.  
  
 [Comments in Code](../../../visual-basic/programming-guide/program-structure/comments-in-code.md)  
 Viene illustrato come aggiungere al codice commenti descrittivi.  
  
 [Keywords as Element Names in Code](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)  
 Viene descritto come utilizzare le parentesi \(`[]`\) per delimitare i nomi di variabile che sono anche parole chiave di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 [Me, My, MyBase, and MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)  
 Vengono descritti i diversi modi in cui è possibile fare riferimento agli elementi di un programma [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 [Visual Basic Limitations](../../../visual-basic/programming-guide/program-structure/limitations.md)  
 Viene illustrata la rimozione dei limiti di codifica noti in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
## Sezioni correlate  
 [Typographic and Code Conventions](../../../visual-basic/language-reference/typographic-and-code-conventions.md)  
 Vengono illustrate le convenzioni standard di scrittura del codice per [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 [Scrittura di codice](/visual-studio/ide/writing-code-in-the-code-and-text-editor)  
 Vengono descritte le funzionalità che semplificano la scrittura e la gestione del codice.