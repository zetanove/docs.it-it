---
title: "Costrutti di backreference nelle espressioni regolari | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espressioni regolari di .NET Framework, costrutti di backreference"
  - "backreference"
  - "costrutti, backreference"
  - "espressioni regolari, costrutti di backreference"
ms.assetid: 567a4b8d-0e79-49dc-8df9-f4b1aa376a2a
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Costrutti di backreference nelle espressioni regolari
I backreference forniscono un modo pratico per identificare un carattere ripetuto o una sottostringa all'interno di una stringa.  Ad esempio, se nella stringa di input sono contenute più occorrenze di una sottostringa arbitraria, è possibile creare una corrispondenza della prima occorrenza con un gruppo Capture, quindi utilizzare un backreference per individuare le corrispondenze con le occorrenze successive della sottostringa.  
  
> [!NOTE]
>  Una sintassi separata è utilizzata per fare riferimento a gruppi di acquisizione denominati e numerati nelle stringhe di sostituzione.  Per ulteriori informazioni, vedere [Sostituzioni](../../../docs/standard/base-types/substitutions-in-regular-expressions.md).  
  
 .NET Framework definisce elementi di linguaggio separati per fare riferimento a gruppi di acquisizione numerati e denominati.  Per ulteriori informazioni sui gruppi di acquisizione, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
## Backreference numerati  
 Un backreference numerato utilizza la sintassi seguente:  
  
 `\` *number*  
  
 dove *number* è la posizione ordinale di un gruppo di acquisizione nell'espressione regolare.  Ad esempio, `\4` corrisponde al contenuto del quarto gruppo di acquisizione.  Se il *number* non è definito nel criterio di espressione regolare, si verifica un errore di analisi e il motore delle espressioni regolari genera una <xref:System.ArgumentException>.  Ad esempio, l'espressione regolare `\b(\w+)\s\1` è valida perché `(\w+)` è il primo e l'unico gruppo di acquisizione nell'espressione.  D'altra parte, `\b(\w+)\s\2` non è valido e genera un'eccezione di argomento, perché non esiste alcun gruppo di acquisizione numerato `\2`.  
  
 Si noti l'ambiguità tra i codici di escape ottali \(ad esempio, `\16`\) e backreference `\`*number* che utilizzano la stessa notazione.  L'ambiguità viene risolta nel modo seguente:  
  
-   Le espressioni da `\1` a `\9` sono sempre interpretate come backreference, non come codici ottali.  
  
-   Se la prima cifra di un'espressione composta da più cifre è 8 o 9 \(ad esempio `\80` o `\91`\), l'espressione verrà interpretata come un valore letterale.  
  
-   Le espressioni da `\10` e superiori vengono considerate backreference se sono presenti backreference corrispondenti a quel numero; in caso contrario, vengono interpretate come codici ottali.  
  
-   L'inclusione di un riferimento a un numero di gruppo non definito in un'espressione regolare provoca un errore di analisi e il motore delle espressioni regolari genera un <xref:System.ArgumentException>.  
  
 Se l'ambiguità costituisce un problema, è possibile utilizzare la notazione `\k<`*name*`>` che non è ambigua e non può essere confusa con la notazione peri numeri ottali.  Allo stesso modo, i codici esadecimali quali `\xdd` non sono ambigui e non possono quindi venire confusi con backreference.  
  
 Nel seguente esempio vengono individuati caratteri alfanumerici doppi in una stringa.  Definisce un'espressione regolare, `(\w)\1`, costituita dagli elementi seguenti.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`(\w)`|Corrisponde a un carattere alfanumerico e lo assegna al primo gruppo di acquisizione.|  
|`\1`|Corrisponde al carattere successivo uguale al valore del primo gruppo di acquisizione.|  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference1.cs#1)]
 [!code-vb[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference1.vb#1)]  
  
## Backreference denominati  
 Un backreference denominato viene definito mediante la sintassi seguente:  
  
 `\k<` *name* `>`  
  
 oppure:  
  
 `\k'` *name* `'`  
  
 dove *name* è il nome di un gruppo di acquisizione definito nel modello di espressione regolare.  Se il *name* non è definito nel criterio di espressione regolare, si verifica un errore di analisi e il motore delle espressioni regolari genera una <xref:System.ArgumentException>.  
  
 Nel seguente esempio vengono individuati caratteri alfanumerici doppi in una stringa.  Definisce un'espressione regolare, `(?<char>\w)\k<char>`, costituita dagli elementi seguenti.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`(?<char>\w)`|Corrisponde a un carattere alfanumerico e lo assegna a un gruppo di acquisizione denominato `char`.|  
|`\k<char>`|Corrisponde al carattere successivo uguale al valore del gruppo di acquisizione `char`.|  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference2.cs#2)]
 [!code-vb[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference2.vb#2)]  
  
 Il *name* può anche essere la rappresentazione in forma di stringa di un numero.  Nell'esempio seguente viene utilizzata l'espressione regolare `(?<2>\w)\k<2>` per trovare caratteri alfanumerici doppi in una stringa.  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference3.cs#3)]
 [!code-vb[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference3.vb#3)]  
  
## Corrispondenza dei backreference  
 Un riferimento a una corrispondenza memorizzata si riferisce alla definizione più recente di un gruppo \(quella che si trova subito a sinistra, quando l'analisi procede da sinistra a destra\).  Quando un gruppo genera più acquisizioni, un backreference farà riferimento all'acquisizione più recente.  
  
 Nell'esempio seguente viene incluso un modello di espressione regolare, `(?<1>a)(?<1>\1b)*`, che ridefinisce il gruppo denominato \\1.  Nella tabella riportata di seguito vengono descritti i singoli modelli nell'espressione regolare.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`(?<1>a)`|Corrisponde al carattere "a" e assegna il risultato al gruppo di acquisizione denominato `1`.|  
|`(?<1>\1b)*`|Trova la corrispondenza per 0 o 1 occorrenza del gruppo denominato `1` insieme a una "b" e assegna il risultato al gruppo di acquisizione denominato `1`.|  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference4.cs#4)]
 [!code-vb[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference4.vb#4)]  
  
 Nel confronto dell'espressione regolare con la stringa di input \("aababb"\), il motore delle espressioni regolari esegue le seguenti operazioni:  
  
1.  parte dall'inizio della stringa e trova una corrispondenza riuscita per "a" con l'espressione `(?<1>a)`.  A questo punto il valore del gruppo `1` è "a".  
  
2.  Avanza al secondo carattere e trova una corrispondenza corretta della stringa "ab" con l'espressione `\1b` o "ab".  Assegna quindi il risultato, "ab", a `\1`.  
  
3.  Avanza al quarto carattere.  Per l'espressione `(?<1>\1b)` una corrispondenza deve essere individuata zero o più volte, ai fini di una corrispondenza corretta alla stringa "abb" con l'espressione `\1b`.  Assegna il risultato, "abb", nuovamente a `\1`.  
  
 In questo esempio, `*` è un quantificatore di cicli \-\-viene eseguito ripetutamente finché il motore delle espressioni regolari non trova una corrispondenza con il modello che definisce.  I quantificatori di cicli non cancellano le definizioni di gruppi.  
  
 Se un gruppo non ha acquisito alcuna sottostringa, un backreference a tale gruppo risulterà non definito e non verrà mai soddisfatto.  Ciò è illustrato dal modello di espressione regolare `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b`, definito nel modo seguente:  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`(\p{Lu}{2})`|Corrisponde a due lettere maiuscole.  Primo gruppo di acquisizione.|  
|`(\d{2})?`|Corrisponde a zero o a un'occorrenza di due cifre decimali.  Secondo gruppo di acquisizione.|  
|`(\p{Lu}{2})`|Corrisponde a due lettere maiuscole.  Equivale al terzo gruppo di acquisizione.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 Una stringa di input può corrispondere a questa espressione regolare anche se le due cifre decimali definite dal secondo gruppo di acquisizione non sono presenti.  L'esempio seguente mostra che anche se la corrispondenza viene eseguita correttamente, viene individuato un gruppo di acquisizione vuoto tra due gruppi di acquisizione con corrispondenza corretta.  
  
 [!code-csharp[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference5.cs#5)]
 [!code-vb[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference5.vb#5)]  
  
## Vedere anche  
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)