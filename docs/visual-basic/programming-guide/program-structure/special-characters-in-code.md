---
title: "Special Characters in Code (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.)"
  - "vb.("
  - "vb.colon"
  - "vb.!"
  - "vb.."
  - "vb.:"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "special characters, in code"
  - "parentheses, using in code"
  - "colons (:)"
  - "period character in code"
  - "dot operator (.)"
  - "dictionary access operator"
  - "concatenation operators, special characters in code"
  - "concatenation operators, vs. addition operator"
  - "! operator"
  - "separators, using in code"
  - "operators [Visual Basic], dictionary access"
  - ": separator character"
  - "member access operator"
  - "addition operator"
  - "operators [Visual Basic], member access"
  - ". operator"
  - "exclamation points"
  - "separators"
  - "exclamation point operator (!)"
  - "Visual Basic code, special characters"
ms.assetid: 310dce0c-45b5-4e0d-83e9-32df258d2a3e
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Special Characters in Code (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Talvolta può risultare necessario utilizzare caratteri speciali nel codice, ovvero caratteri non alfanumerici o numerici.  La punteggiatura e i caratteri speciali presenti nel set di caratteri [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono utilizzati per diversi scopi, dall'organizzazione del testo di programma alla definizione di attività eseguite dal compilatore o dal programma compilato.  Questi caratteri non specificano l'esecuzione di un'operazione.  
  
## Parentesi  
 Utilizzare le parentesi per definire una procedura, quale `Sub` o `Function`.  È necessario racchiudere tra parentesi tutti gli elenchi di argomenti della routine.  È possibile, inoltre, utilizzare le parentesi per inserire variabili o argomenti in gruppi logici, soprattutto per eseguire l'override dell'ordine di precedenza predefinito degli operatori in un'espressione complessa.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbcnConventions#11](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_1.vb)]  
  
 Dopo l'esecuzione del codice precedente, il valore di `d` è 8,225 e il valore di `e` è 3.  Il calcolo per `d` utilizza la precedenza predefinita di `/` rispetto a `+` ed è equivalente a `d = b + (c / a)`.  Le parentesi nel calcolo di `e` sostituiscono la precedenza predefinita.  
  
## Separatori  
 Come suggerito dal nome stesso, il ruolo dei separatori consiste nella separazione delle sezioni del codice.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], il carattere separatore è rappresentato dai due punti \(`:`\).  Utilizzare i separatori per includere più istruzioni su una sola riga anziché su righe separate,   al fine di risparmiare spazio e migliorare la leggibilità del codice.  Nell'esempio seguente vengono mostrate tre istruzioni separate da due punti.  
  
 [!code-vb[VbVbcnConventions#12](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_2.vb)]  
  
 Per ulteriori informazioni, vedere [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md).  
  
 Il carattere due punti \(`:`\) viene inoltre utilizzato per identificare un'etichetta dell'istruzione.  Per ulteriori informazioni, vedere [How to: Label Statements](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md).  
  
## Concatenazione  
 Per la *concatenazione*, ovvero il collegamento di più stringhe, utilizzare l'operatore `&`,  da non confondere con l'operatore `+` che invece somma valori numerici.  L'utilizzo dell'operatore `+` per la concatenazione può generare risultati errati nel caso di operandi numerici.  Nell'esempio che segue viene illustrato quanto descritto.  
  
 [!code-vb[VbVbcnConventions#13](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_3.vb)]  
  
 Dopo l'esecuzione del codice precedente, il valore di `resultA` è 21,01 e il valore di `resultB` è "10,0111".  
  
## Operatori di accesso ai membri  
 Per accedere al membro di un tipo, utilizzare l'operatore punto \(`.`\) o punto esclamativo \(`!`\) inserendolo tra il nome del tipo e il nome del membro.  
  
### Punto \(.\) Operatore  
 Utilizzare l'operatore `.` in una classe, struttura, interfaccia o enumerazione come operatore di accesso al membro.  Il membro può essere un campo, una proprietà, un evento o un metodo.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbcnConventions#14](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_4.vb)]  
  
### Punto esclamativo \(\!\) Operatore  
 Utilizzare l'operatore `!` solo in una classe o in un'interfaccia, come operatore di accesso al dizionario.  È necessario che la classe o l'interfaccia disponga di una proprietà predefinita che accetta un unico argomento `String`.  L'identificatore immediatamente successivo all'operatore `!` diventa il valore dell'argomento passato alla proprietà predefinita come stringa.  Nell'esempio che segue viene illustrato quanto descritto.  
  
 [!code-vb[VbVbcnConventions#15](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_5.vb)]  
  
 In tutte le tre righe di output `MsgBox` viene visualizzato il valore `32856`.  La prima riga utilizza l'accesso tradizionale alla proprietà `index`, la seconda tiene conto del fatto che `index` è la proprietà predefinita della classe `hasDefault` e la terza utilizza l'accesso del dizionario alla classe.  
  
 Il secondo operando dell'operatore `!` deve essere una identificatore Visual Basic valido non racchiuso tra virgolette \(`" "`\).  In altre parole, non è possibile utilizzare una stringa letterale o una variabile di tipo stringa.  La modifica seguente dell'ultima riga della chiamata `MsgBox` genera un errore perché `"X"` è una stringa letterale racchiusa.  
  
 `"Dictionary access returns " & hD!"X")`  
  
> [!NOTE]
>  È necessario che i riferimenti alle raccolte predefinite siano espliciti.  In particolare, non è possibile utilizzare l'operatore `!` su una variabile ad associazione tardiva.  
  
 Il carattere `!` viene utilizzato anche come carattere tipo `Single`.  
  
## Vedere anche  
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Type Characters](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)