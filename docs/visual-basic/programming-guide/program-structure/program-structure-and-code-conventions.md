---
title: Struttura del programma e convenzioni del codice (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- coding conventions
- Visual Basic code, coding conventions
- coding conventions, Visual Basic
- programs, structure
- program structure
- naming conventions, Visual Basic
- best practices, coding conventions
- conventions, Visual Basic coding
- Visual Basic code
- programming, Visual Basic coding conventions
ms.assetid: dd9be76f-6944-4e78-ad72-0b6084a3fc13
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cd25d99d74bf1e4d416c9da63758f6ad04027258
ms.lasthandoff: 03/13/2017

---
# <a name="program-structure-and-code-conventions-visual-basic"></a>Struttura del programma e convenzioni di scrittura del codice (Visual Basic)
Questa sezione viene presentata la tipica [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] struttura del programma, fornisce una semplice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma "Hello, World" e vengono illustrati [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] convenzioni del codice. Convenzioni nel codice vengono forniti suggerimenti che lo stato attivo non logica del programma ma la struttura fisica e l'aspetto. Seguendo le rende più semplice da leggere, comprendere e gestire il codice. Convenzioni nel codice possono includere, tra gli altri:  
  
-   Formati standardizzati per l'assegnazione di etichette e commenti nel codice.  
  
-   Linee guida per la spaziatura, la formattazione e rientri di codice.  
  
-   Convenzioni di denominazione per gli oggetti, variabili e procedure.  
  
 Gli argomenti seguenti presentano una serie di linee guida per la programmazione [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] i programmi, insieme a esempi di corretto utilizzo.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Struttura di un programma Visual Basic](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 Viene fornita una panoramica degli elementi che costituiscono un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma.  
  
 [Routine Main in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md)  
 Descrive la procedura che viene utilizzato come l'avvio di punto e controllo generale per l'applicazione.  
  
 [Riferimenti e istruzione Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)  
 Viene illustrato come fare riferimento agli oggetti in altri assembly.  
  
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)  
 Viene descritto come gli spazi dei nomi organizzare gli oggetti all'interno di assembly.  
  
 [Convenzioni di denominazione di Visual Basic](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)  
 Include linee guida generali per la denominazione delle procedure, costanti, variabili, argomenti e gli oggetti.  
  
 [Convenzioni di codifica di Visual Basic](../../../visual-basic/programming-guide/program-structure/coding-conventions.md)  
 Esamina le linee guida utilizzate nello sviluppo di esempi in questa documentazione.  
  
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 Viene descritto come compilare determinati blocchi di codice in modo selettivo e impostare il compilatore di ignorare gli altri.  
  
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)  
 Viene illustrato come suddividere lunghe istruzioni in più righe e combinare istruzioni brevi su una riga.  
  
 [Procedura: Comprimere e nascondere sezioni di codice](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)  
 Viene illustrato come comprimere e nascondere sezioni di codice il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] editor di codice.  
  
 [Procedura: Etichettare le istruzioni](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)  
 Viene illustrato come contrassegnare una riga di codice per identificarla per l'utilizzo con le istruzioni, ad esempio `On Error Goto`.  
  
 [Caratteri speciali nel codice](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)  
 Viene illustrato come e dove utilizzare caratteri non alfabetici e non numerici.  
  
 [Commenti nel codice](../../../visual-basic/programming-guide/program-structure/comments-in-code.md)  
 Viene descritto come aggiungere commenti descrittivi al codice.  
  
 [Parole chiave come nomi di elementi nel codice](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)  
 Viene descritto come utilizzare le parentesi quadre (`[]`) per delimitare i nomi delle variabili che sono anche [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] parole chiave.  
  
 [Me, My, MyBase e MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)  
 Descrive diversi modi per fare riferimento agli elementi di un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programma.  
  
 [Limitazioni di Visual Basic](../../../visual-basic/programming-guide/program-structure/limitations.md)  
 Viene illustrata la rimozione dei limiti di codifica noti in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Convenzioni tipografiche e di scrittura del codice](../../../visual-basic/language-reference/typographic-and-code-conventions.md)  
 Vengono illustrate le convenzioni standard per [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 [Writing Code](https://docs.microsoft.com/visualstudio/ide/writing-code-in-the-code-and-text-editor) (Scrittura di codice)  
 Vengono descritte le funzionalità che rendono più semplice per scrivere e gestire il codice.
