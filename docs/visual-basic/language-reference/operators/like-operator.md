---
title: "Like Operator (Visual Basic) | Microsoft Docs"
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
  - "Like"
  - "vb.Like"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "similar to"
  - "pattern matching"
  - "Like operator [Visual Basic]"
  - "? symbol, wildcard character"
  - "string comparison [Visual Basic], Like operator"
  - "strings [Visual Basic], comparing"
  - "comparison operators"
  - "symbols, wildcard"
  - "wildcards, Like operator"
  - "strings [Visual Basic], matching"
  - "string comparison [Visual Basic], sorting data"
  - "data [Visual Basic], sorting"
  - "text [Visual Basic], comparing"
  - "operators [Visual Basic], pattern-matching"
  - "data [Visual Basic], string comparisons"
  - "string comparison [Visual Basic], Like operators"
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Like Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Confronta una stringa con un modello.  
  
## Sintassi  
  
```  
  
result = string Like pattern  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi variabile `Boolean`.  Il risultato è un valore `Boolean` che indica se `string` soddisfa i criteri di corrispondenza con `pattern`.  
  
 `string`  
 Obbligatorio.  Qualsiasi espressione `String`.  
  
 `pattern`  
 Obbligatorio.  Qualsiasi espressione `String` conforme alle convenzioni di corrispondenza dei modelli descritte nella sezione relativa alle osservazioni.  
  
## Note  
 Se il valore di `string` soddisfa i criteri di corrispondenza con il modello contenuto in `pattern`, `result` sarà `True`.  Se tali criteri non vengono soddisfatti, `result` sarà `False`.  Se `string` e `pattern` sono entrambe stringhe vuote, il risultato sarà `True`.  
  
## Metodo di confronto  
 Il comportamento dell'operatore `Like` dipende dall'[Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md).  Il metodo di confronto delle stringhe predefinito per ciascun file di origine è `Option Compare Binary`.  
  
## Opzioni del modello  
 La corrispondenza tra modelli rappresenta uno strumento versatile per il confronto tra stringhe.  Le funzionalità di corrispondenza tra modelli consentono di associare ciascun carattere incluso in `string` con un carattere specifico, un carattere jolly, un elenco o un intervallo di caratteri.  Nella tabella riportata di seguito vengono illustrati i caratteri consentiti in `pattern` e le relative corrispondenze.  
  
|Caratteri inclusi in `pattern`|Corrispondenza in `string`|  
|------------------------------------|--------------------------------|  
|`?`|Qualsiasi carattere singolo.|  
|`*`|Nessuno o più caratteri.|  
|`#`|Qualsiasi cifra singola \(0\-9\).|  
|`[` `charlist` `]`|Qualsiasi carattere singolo incluso in `charlist`.|  
|`[!` `charlist` `]`|Qualsiasi carattere singolo non incluso in `charlist`.|  
  
## Elenchi di caratteri  
 Per stabilire una corrispondenza con qualsiasi carattere presente in `string`, è possibile utilizzare un gruppo di uno o più caratteri \(`charlist`\) racchiuso tra parentesi quadre \(`[ ]`\) che può contenere quasi tutti i codici carattere, comprese le cifre.  
  
 Se si specifica un punto esclamativo \(`!`\) all'inizio di `charlist`, la corrispondenza verrà stabilita se `string` contiene uno o più caratteri che non sono inclusi in `charlist`.  Se utilizzato fuori dalle parentesi quadre, il punto esclamativo non svolgerà alcuna funzione particolare.  
  
## Caratteri speciali  
 Per verificare la corrispondenza di caratteri speciali quali la parentesi quadra aperta \(`[`\), il punto interrogativo \(`?`\), il segno di numero \(`#`\) e l'asterisco \(`*`\), è necessario racchiuderli tra parentesi quadre.  La parentesi quadra chiusa \(`]`\) può essere utilizzata per stabilire una corrispondenza con un carattere identico all'esterno ma non all'interno di un gruppo.  
  
 La sequenza di caratteri `[]` viene considerata una stringa di lunghezza zero \(`""`\).  Non può tuttavia far parte di un elenco di caratteri racchiusi tra parentesi quadre.  Per verificare se una determinata posizione in `string` contiene un solo carattere di un gruppo o non contiene alcun carattere, è possibile utilizzare `Like` due volte.  Per un esempio, vedere [How to: Match a String against a Pattern](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md).  
  
## Intervalli di caratteri  
 All'interno di `charlist` è possibile specificare un intervallo di caratteri inserendo un trattino \(`–`\) tra il limite superiore e quello inferiore dell'intervallo.  Ad esempio, `[A–Z]` restituisce una corrispondenza se la posizione corrispondente in `string` contiene un qualsiasi carattere compreso nell'intervallo `A`–`Z`, mentre `[!H–L]` restituisce una corrispondenza se la posizione corrispondente contiene un qualsiasi carattere non compreso nell'intervallo `H`–`L`.  
  
 Quando viene specificato un intervallo di caratteri, questi devono essere indicati in ordine crescente, ossia dal minore al maggiore.  L'intervallo `[A–Z]` risulta quindi valido, al contrario di `[Z–A]`.  
  
### Intervalli multipli di caratteri  
 Per specificare più intervalli per la stessa posizione di carattere, inserirli tra le stesse parentesi quadre senza delimitatori.  Ad esempio, `[A–CX–Z]` restituisce una corrispondenza se la posizione corrispondente in `string` contiene un qualsiasi carattere compreso nell'intervallo `A`–`C` o `X`–`Z`.  
  
### Utilizzo del trattino  
 Per stabilire una corrispondenza con un carattere identico, il trattino \(`–`\) può essere inserito sia all'inizio \(dopo il punto esclamativo, se utilizzato\) che alla fine di `charlist` .  In qualsiasi altra posizione il trattino identifica un intervallo di caratteri delimitato dal carattere precedente e successivo.  
  
## Sequenza di confronto  
 Il significato di un intervallo specificato dipende dall'ordinamento dei caratteri in fase di esecuzione, determinato da `Option` `Compare` e dalle impostazioni locali del sistema in cui viene eseguito il codice.  Con `Option` `Compare` `Binary` l'intervallo `[A–E]` corrisponde ad `A`, `B`, `C`, `D` ed `E`.  Con `Option` `Compare` `Text` `[A–E]` corrisponde ad `A`, `a`, `À`, `à`, `B`, `b`, `C`, `c`, `D`, `d`, `E` ed `e`.  L'intervallo non include `Ê` o `ê` perché i caratteri accentati vengono messi a confronto dopo quelli non accentati nella sequenza di ordinamento.  
  
## Caratteri digraph  
 In alcune lingue sono presenti lettere che rappresentano due caratteri distinti.  In diverse lingue viene ad esempio utilizzato il carattere `æ` per rappresentare il dittongo composto da `a` e `e` quando i due caratteri compaiono insieme.  L'operatore `Like` consente di rilevare l'equivalenza tra il singolo carattere digraph e i due caratteri singoli.  
  
 Se nelle impostazioni locali del sistema viene specificata una lingua che utilizza un carattere digraph, l'occorrenza di tale carattere in `pattern` o `string` verrà considerata corrispondente alla sequenza dei due caratteri nell'altra stringa.  Analogamente, un carattere digraph in `pattern` racchiuso tra parentesi quadre \(da solo, in un elenco o in un intervallo\) verrà considerato corrispondente all'equivalente sequenza di due caratteri presente in `string`.  
  
## Overload  
 L'operatore `Like` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Like` viene utilizzato per confrontare stringhe con diversi modelli.  I risultati vengono inseriti in una variabile `Boolean` che indica se ogni stringa soddisfa i criteri di corrispondenza con il modello.  
  
 [!code-vb[VbVbalrOperators#30](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/like-operator_1.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [Comparison Operators](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [How to: Match a String against a Pattern](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)