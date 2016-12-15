---
title: "Declared Element Names (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "declared elements, case sensitivity"
  - "names, Visual Basic rules"
  - "naming conventions"
  - "element names"
  - "declared elements, identifiers"
  - "declarations, elements"
  - "declared elements, valid names"
  - "[] escape characters [Visual Basic]"
  - "names, elements"
  - "declaration statements, declared elements"
  - "declaring elements"
  - "identifiers, declared elements"
  - "case sensitivity, declared element names"
  - "escape characters"
  - "names, declared elements"
  - "declared elements, about declared elements"
  - "escaped names"
  - "declared elements, names"
  - "names, naming conventions"
  - "identifiers, elements"
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Declared Element Names (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Ogni elemento dichiarato ha un nome, detto anche *identificatore*, utilizzato dal codice per riferirsi a esso.  
  
## Regole  
 Il nome di un elemento in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] deve rispettare le regole seguenti:  
  
-   Deve iniziare con un carattere alfabetico o un carattere di sottolineatura \(`_`\).  
  
-   Deve contenere solo caratteri alfabetici, cifre decimali e caratteri di sottolineatura.  
  
-   Se inizia con un carattere di sottolineatura, deve contenere almeno un carattere alfabetico o una cifra decimale.  
  
-   Non deve superare la lunghezza massima di 1023 caratteri.  
  
 Il limite di lunghezza di 1023 caratteri si applica anche all'intera stringa di un nome completo, ad esempio `outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement`.  
  
 Nell'esempio riportato di seguito sono illustrati alcuni nomi di elemento validi.  
  
 `aB123__45`  
  
 `_567`  
  
 Nell'esempio riportato di seguito sono illustrati alcuni nomi di elemento non validi.  Il primo contiene solo un carattere di sottolineatura, il secondo inizia con una cifra decimale e il terzo contiene un carattere non valido \($\).  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
>  I nomi di elemento che iniziano con un carattere di sottolineatura \(`_`\) non fanno parte di [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), pertanto non è possibile utilizzare un componente che definisce tali nomi in codice compatibile con CLS.  Tuttavia, il carattere di sottolineatura è compatibile con CLS in qualsiasi altra posizione all'interno di un nome di elemento.  
  
### Indicazioni sulla lunghezza dei nomi  
 Per una questione pratica, il nome dovrebbe essere il più breve possibile e al tempo stesso identificare chiaramente la tipologia dell'elemento.  Questo consente di migliorare la leggibilità del codice e di ridurre la lunghezza delle righe e la dimensione del file di origine.  
  
 D'altro canto, è necessario che il nome abbia una lunghezza sufficiente per descrivere adeguatamente l'elemento e il modo in cui deve essere utilizzato dal codice.  Questa caratteristica è importante per la leggibilità del codice.  L'utilizzo di nomi appropriati consente infatti un notevole risparmio di tempo sia agli altri utenti che dovranno comprendere la funzione dell'elemento che allo stesso autore che dovrà riutilizzare l'elemento dopo un lungo periodo di tempo.  
  
## Nomi forzati  
 Un nome di elemento, in genere, non deve corrispondere alle parole chiave riservate da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], ad esempio `Case` o `Friend`.  È tuttavia possibile definire un *nome forzato*, racchiuso tra parentesi \(`[ ]`\).  Un nome forzato può corrispondere a qualsiasi parola chiave di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], in quanto le parentesi evitano qualsiasi ambiguità.  Utilizzare le parentesi anche quando si fa riferimento al nome in un punto successivo del codice.  
  
 In generale, l'utilizzo dei nomi forzati è necessario solo nei seguenti casi:  
  
-   È stata eseguita la migrazione del codice da una versione precedente di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] in cui la parola chiave utilizzata come nome non era riservata.  
  
-   Si sta utilizzando codice scritto in un altro linguaggio, in cui la parola chiave specificata non è riservata.  
  
 Negli altri casi, si consiglia di rinominare l'elemento se il nome dell'elemento è in conflitto con una parola chiave.  A questo scopo è possibile utilizzare l'ambiente di sviluppo integrato \(IDE, Integrated Development Environment\).  Per ulteriori informazioni, vedere [Finestra di dialogo Rinomina e refactoring](../../../../visual-basic/developing-apps/using-ide/refactoring-and-rename-dialog-box.md).  
  
## Distinzione tra maiuscole e minuscole nei nomi  
 Per i nomi degli elementi in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non viene fatta distinzione tra maiuscole e minuscole.  Questo significa che, quando il compilatore confronta due nomi che differiscono solo nelle maiuscole e minuscole, li interpreta come se fossero lo stesso nome.  `ABC` e `abc`, ad esempio, sono considerati come riferimenti allo stesso elemento dichiarato.  
  
 Nel Common Language Runtime, tuttavia, viene utilizzata l'associazione con distinzione tra maiuscole e minuscole.  Di conseguenza, quando si genera un assembly o una DLL e li si rende disponibili per altri assembly, per i nomi utilizzati verrà fatta distinzione tra maiuscole e minuscole.  Se ad esempio si definisce una classe con un elemento denominato `ABC` e altri assembly utilizzano tale classe tramite il Common Language Runtime, è necessario che gli assembly facciano riferimento all'elemento come `ABC`.  Se, successivamente, la classe viene ricompilata e il nome dell'elemento viene cambiato in `abc`, gli altri assembly che utilizzano la classe non potranno più accedere all'elemento.  Di conseguenza, quando si rilascia una versione aggiornata di un assembly, è preferibile non modificare le maiuscole e le minuscole degli elementi pubblici.  
  
## Nomi e impostazioni locali  
 Il confronto tra i nomi è indipendente dalle impostazioni locali in uso.  Se due nomi corrispondono in un ambiente con determinate impostazioni locali, tali nomi coincideranno in tutti gli ambienti.  
  
## Vedere anche  
 [Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)   
 [Declared Element Characteristics](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Statements](../../../../visual-basic/language-reference/statements/index.md)