---
title: "Typographic and Code Conventions (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "coding conventions, Visual Basic"
  - "best practices, coding conventions"
  - "conventions, Visual Basic coding"
  - "typographic conventions"
  - "document conventions"
  - "conventions, documentation"
  - "Visual Basic code, conventions"
ms.assetid: 1916cd81-ea9d-4faa-81f7-4a0d864b60f4
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Typographic and Code Conventions (Visual Basic)
[!INCLUDE[vs2017banner](../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nella documentazione di Visual Basic sono state adottate le convenzioni tipografiche e di scrittura del codice di seguito descritte.  
  
## Convenzioni tipografiche  
  
|Esempio|Descrizione|  
|-------------|-----------------|  
|`Sub`, `If`, `ChDir`, `Print`, `True`, `Debug`|Le parole chiave specifiche del linguaggio e i membri di runtime hanno le iniziali maiuscole e il formato mostrato in questo esempio.|  
|PiccoloProgetto, InsiemePulsante|Le parole e le frasi da digitare hanno il formato mostrato in questo esempio.|  
|[Module Statement](../../visual-basic/language-reference/statements/module-statement.md)|I collegamenti da selezionare per passare a un'altra pagina della Guida hanno il formato mostrato in questo esempio.|  
|*oggetto*, *nomeVariabile*, `argumentList`|I segnaposti per le informazioni da fornire hanno il formato mostrato in questo esempio.|  
|\[ Shadows \], \[ *elencoEspressioni* \]|Nella sintassi, gli elementi facoltativi sono racchiusi fra parentesi quadre.|  
|{ `Public` &#124; `Friend` &#124; `Private` }|Nella sintassi, quando è necessario effettuare una scelta tra due o più elementi, gli elementi sono racchiusi tra parentesi graffe e separati da barre verticali.<br /><br /> È possibile selezionare esclusivamente un solo elemento.|  
|\[ `Protected` &#124; `Friend` \]|Nella sintassi, quando è necessario effettuare una scelta tra due o più elementi, gli elementi sono racchiusi tra parentesi quadre e separati da barre verticali.<br /><br /> È possibile selezionare qualsiasi combinazione di elementi o nessun elemento.|  
|\[{ `ByVal` &#124; `ByRef` }\]|Nella sintassi, quando si può selezionare un solo elemento, ma si possono anche omettere tutti gli elementi, questi sono racchiusi tra parentesi quadre contenute in parentesi graffe e separati da barre verticali.|  
|*nomeMembro* 1, *nomeMembro*2, *nomeMembro*3|Le istanze multiple dello stesso segnaposto sono rese differenti tramite i pedici, come indicato nell'esempio.|  
|*nomeMembro1*<br /><br /> ...<br /><br /> *nomeMembroN*|Nella sintassi i puntini di sospensione \(...\) vengono utilizzati per indicare un numero indefinito di elementi del tipo specificato immediatamente prima dei puntini di sospensione.<br /><br /> Nel codice, i puntini di sospensione indicano l'omissione di codice per garantire una maggiore chiarezza.|  
|ESC, INVIO|I tasti e le sequenze di tasti sono indicati in lettere maiuscole.|  
|ALT\+F1|Quando tra i tasti è riportato il segno più \(\+\), è necessario tenere premuto un tasto mentre si preme l'altro.  ALT\+F1, ad esempio, prevede la pressione contemporanea dei tasti ALT e F1.|  
  
## Convenzioni nel codice  
  
|Esempio|Descrizione|  
|-------------|-----------------|  
|`sampleString = "Hello, world!"`|Gli esempi di codice sono riportati in un tipo di carattere a passo fisso, come illustrato in questo esempio.|  
|L'istruzione precedente imposta il valore di `sampleString` su "Hello, world\!".|Gli elementi di codice in testo descrittivo sono riportati in un tipo di carattere a passo fisso, come illustrato in questo esempio.|  
|`' This is a comment.`<br /><br /> `REM This is also a comment.`|I commenti del codice sono introdotti da un apostrofo \('\) o dalla parola chiave REM.|  
|`sampleVar = "This is an " _`<br /><br /> `& "example" _`<br /><br /> `& " of how to continue code."`|Uno spazio seguito da un segno di sottolineatura \( \_\) al termine di una riga indica che l'istruzione continua sulla riga successiva.|  
  
## Vedere anche  
 [Visual Basic Language Reference](../../visual-basic/language-reference/index.md)   
 [Parole chiave](../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic Runtime Library Members](../../visual-basic/language-reference/runtime-library-members.md)   
 [Visual Basic Naming Conventions](../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Procedura: Interrompere e combinare istruzioni nel codice](../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)   
 [Comments in Code](../../visual-basic/programming-guide/program-structure/comments-in-code.md)