---
title: "Troubleshooting Data Types (Visual Basic) | Microsoft Docs"
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
  - "Char data type, converting"
  - "Decimal data type, conversions"
  - "data types [Visual Basic], troubleshooting"
  - "literals, default types"
  - "type characters, literal"
  - "Mod operator [Visual Basic], in floating-point operations"
  - "troubleshooting Visual Basic, data types"
  - "troubleshooting data types"
  - "floating-point numbers, precision"
  - "Boolean data type, converting"
  - "literal types"
  - "literal type characters"
  - "floating-point numbers, imprecision"
  - "String data type, converting"
  - "floating-point numbers, comparison"
  - "floating-point numbers"
ms.assetid: 90040d67-b630-4125-a6ae-37195b079042
caps.latest.revision: 29
caps.handback.revision: 28
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Troubleshooting Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questa pagina vengono elencati alcuni problemi comuni che possono verificarsi durante l'esecuzione di operazioni sui tipi di dati intrinsechi.  
  
## Le espressioni a virgola mobile non vengono considerate uguali  
 Quando si utilizzano numeri a virgola mobile, quali [Single Data Type](../../../../visual-basic/language-reference/data-types/single-data-type.md) e [Double Data Type](../../../../visual-basic/language-reference/data-types/double-data-type.md), tenere presente che sono archiviati come frazioni binarie.  In altre parole, non possono contenere una rappresentazione esatta di qualsiasi quantità che non sia una frazione binaria \(del formato k \/ \(2 ^ n\), dove k e n sono numeri interi\).  Ad esempio 0,5 \(\= 1\/2\) e 0,3125 \(\= 5\/16\) possono essere mantenuti come valori precisi, mentre 0,2 \(\= 1\/5\) e 0,3 \(\= 3\/10\) possono essere solo approssimazioni.  
  
 A causa di questa imprecisione, quando si utilizzano i valori a virgola mobile non è possibile ottenere risultati esatti.  In particolare, due valori teoricamente identici potrebbero avere rappresentazioni leggermente diverse.  
  
||  
|-|  
|Per confrontare le quantità a virgola mobile|  
|1.  Calcolare il valore assoluto della loro differenza utilizzando il metodo <xref:System.Math.Abs%2A> della classe <xref:System.Math> nello spazio dei nomi <xref:System>.<br />2.  Determinare una differenza massima accettabile, in modo che si possano considerare uguali le due quantità a scopo pratico se la loro differenza non è maggiore.<br />3.  Confrontare il valore assoluto della differenza con la differenza accettabile.|  
  
 Nell''esempio riportato di seguito viene illustrato il confronto corretto e non corretto di due valori `Double`.  
  
 [!code-vb[VbVbalrDataTypes#10](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_1.vb)]  
  
 Nell''esempio precedente viene utilizzato il metodo <xref:System.Double.ToString%2A> della struttura <xref:System.Double> che consente di specificare una maggiore precisione rispetto a `CStr` utilizzata dalla parola chiave.  Il valore predefinito è di 15 cifre, ma il formato "G17" lo estende a 17 cifre.  
  
## L'operatore Mod non restituisce risultati accurati  
 A causa dell'imprecisione dell'archiviazione della virgola mobile, l'[Operatore Mod](../../../../visual-basic/language-reference/operators/mod-operator.md) potrebbe restituire un risultato imprevisto nel caso in cui almeno uno degli operandi sia a virgola mobile.  
  
 Il [Decimal Data Type](../../../../visual-basic/language-reference/data-types/decimal-data-type.md) non utilizza il formato a virgola mobile.  Molti numeri inesatti in `Single` e `Double` sono esatti in `Decimal`, come ad esempio 0,2 e 0,3.  Sebbene il calcolo aritmetico sia più lento nel formato `Decimal` che nel formato a virgola mobile, la perdita di prestazioni potrebbe consentire di ottenere una maggiore precisione.  
  
||  
|-|  
|Per trovare il resto integer delle quantità a virgola mobile|  
|1.  Dichiarare le variabili come `Decimal`.<br />2.  Utilizzare il carattere di tipo letterale `D` per definire il tipo di valore dei letterali come `Decimal`, nel caso i loro valori siano troppo grandi per il tipo di dati `Long`.|  
  
 Nell''esempio riportato di seguito viene illustrata la potenziale imprecisione degli operandi a virgola mobile.  
  
 [!code-vb[VbVbalrDataTypes#11](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_2.vb)]  
  
 Nel precedente esempio, si utilizza il metodo <xref:System.Double.ToString%2A> della struttura <xref:System.Double> in modo che possa specificare una maggiore precisione rispetto a quella utilizzata dalla parola chiave `CStr`.  Il valore predefinito è di 15 cifre, ma il formato "G17" lo estende a 17 cifre.  
  
 Poiché `zeroPointTwo` è `Double`, il suo valore per 0,2 è una frazione binaria ripetuta all'infinito con un valore archiviato di 0,20000000000000001.  Dividendo 2,0 per questa quantità il risultato è 9,9999999999999995 con il resto di 0,19999999999999991.  
  
 Nell''espressione di `decimalRemainder`, il carattere di tipo letterale `D` impone che entrambi gli operandi siano `Decimal` e la rappresentazione di 0,2 è precisa.  Di conseguenza, l'operatore `Mod` restituisce un resto previsto di 0,0.  
  
 Si noti che non è sufficiente dichiarare `decimalRemainder` come `Decimal`,  ma è necessario anche imporre ai valori letterali di essere `Decimal` o di assumere come valore predefinito `Double` e `decimalRemainder` riceve lo stesso valore impreciso di `doubleRemainder`.  
  
## La conversione del tipo booleano in tipo numerico non viene effettuata accuratamente  
 I valori [Boolean Data Type](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) non sono archiviati come numeri e i valori archiviati non vengono considerati equivalenti ai numeri.  Per garantire la compatibilità con le versioni precedenti, con [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono fornite parole chiave di conversione, quali [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md), `CBool`, `CInt` e così via, per la conversione tra tipi `Boolean` e numerici.  Tuttavia a volte altri linguaggi effettuano queste conversioni in maniera diversa, come nel caso dei metodi [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 Non è consentito scrivere codice basato su valori numerici equivalenti di `True` e `False`.  Se possibile, è opportuno utilizzare le variabili `Boolean` soltanto per i valori logici per cui sono progettate.  Per combinare valori `Boolean` e numerici, è importante conoscere bene il metodo di conversione da selezionare.  
  
### Conversione in Visual Basic  
 Quando si utilizzano le parole chiave di conversione `CType` o `CBool` per convertire tipi di dati numerici in `Boolean`, 0 diventa `False` e tutti gli altri valori diventano `True`.  Quando si convertono i valori `Boolean` in tipi di dati numerici utilizzando le parole chiave di conversione, `False` diventa 0 e `True` diventa \-1.  
  
### Conversione nel framework  
 Il metodo <xref:System.Convert.ToInt32%2A> della classe <xref:System.Convert> nello spazio dei nomi <xref:System> consente di convertire `True` a \+1.  
  
 Se occorre convertire un valore `Boolean` in un tipo di dati numerici, scegliere con attenzione il metodo di conversione da utilizzare.  
  
## Il carattere letterale genera un errore del compilatore  
 In assenza di caratteri di qualsiasi tipo, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] assume i tipi di dati predefiniti come valori letterali.  Il tipo di valore letterale predefinito, racchiuso tra virgolette \(`" "`\), è `String`.  
  
 Il tipo di dati `String` non si amplia in [Char Data Type](../../../../visual-basic/language-reference/data-types/char-data-type.md).  In altre parole se si desidera assegnare un valore letterale a una variabile `Char`, è necessario eseguire una conversione di restrizione o imporre al valore letterale di essere di tipo `Char`.  
  
||  
|-|  
|Per creare un valore letterale Char da assegnare a una variabile o costante|  
|1.  Dichiarare la variabile o la costante come `Char`.<br />2.  Racchiudere il valore del carattere tra virgolette \(`" "`\).<br />3.  Far seguire le virgolette doppie di chiusura dal carattere di tipo letterale `C` per imporre al valore letterale di essere di tipo `Char`.  Si tratta di un'operazione necessaria se l'opzione di controllo dei tipi \([Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) è `On` ed è comunque preferibile in qualsiasi caso.|  
  
 Nell''esempio seguente vengono illustrate le assegnazioni con esito negativo e positivo di un valore letterale a una variabile `Char`.  
  
 [!CODE [VbVbalrStatements#49](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrStatements#49)]  
  
 [!code-vb[VbVbalrDataTypes#12](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_4.vb)]  
  
 Esiste sempre un rischio nell'utilizzo delle conversioni di restrizione in quanto possono avere esito negativo in fase di esecuzione.  Una conversione da `String` a `Char` ad esempio può avere esito negativo se il valore `String` contiene più di un carattere.  Di conseguenza, è preferibile programmare per utilizzare il tipo di carattere `C`.  
  
## L'operazione di conversione della stringa ha esito negativo in fase di esecuzione  
 [String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md) contribuisce a poche conversioni verso un tipo di dati più grande.  `String` viene ampliato solo in se stesso e in `Object` e solo `Char` e `Char()` \(una matrice `Char` \) si ampliano a `String`.  Questo accade poiché le variabili e le costanti `String` sono in grado di contenere valori che gli altri tipi di dati non sono in grado di supportare.  
  
 Quando l'opzione di controllo del tipo \([Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) è `On`, il compilatore impedisce tutte le conversioni di riduzione implicite,  incluse quelle che utilizzano `String`.  Nel codice è ancora possibile specificare le parole chiave di conversione quali `CStr` e [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) che spingono [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] a tentare la conversione.  
  
> [!NOTE]
>  L'errore di conversione verso un tipo di dati più piccolo viene eliminato per le conversioni dagli elementi di una raccolta `For Each…Next` alla variabile di controllo del ciclo.  Per ulteriori informazioni ed esempi, vedere la sezione "Conversioni verso tipi di dati più piccoli" di [Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
### Protezione della conversione di restrizione  
 Lo svantaggio delle conversioni di restrizione è che possono avere esito negativo in fase di esecuzione.  Se ad esempio una variabile `String` contiene esclusivamente "True" o "False", non sarà possibile convertirla in `Boolean`.  Se contiene caratteri di punteggiatura, la conversione a qualsiasi tipo numerico avrà esito negativo.  A meno che si sappia che la variabile `String` contiene sempre valori accettabili dal tipo di destinazione, si sconsiglia di provare a eseguire una conversione.  
  
 Se è necessario eseguire la conversione da `String` a un altro tipo di dati, la procedura più sicura consiste nel racchiudere la conversione effettuata nell'[Try...Catch...Finally Statement](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  In questo modo è possibile gestire un errore in fase di esecuzione.  
  
### Matrici di caratteri  
 Un `Char` singolo e una matrice di elementi `Char` si ampliano entrambi a `String`.  Tuttavia, `String` non si amplia a `Char()`.  Per convertire un valore `String` in una matrice `Char`, è possibile utilizzare il metodo <xref:System.String.ToCharArray%2A> della classe <xref:System.String?displayProperty=fullName>.  
  
### Valori senza significato  
 In generale i valori `String` sono senza significato in altri tipi di dati e la conversione è altamente artificiale e pericolosa.  Se possibile, è opportuno utilizzare le variabili `String` soltanto per le sequenze di caratteri per cui sono progettate.  Non è consentito scrivere codice basato su valori equivalenti di altri tipi.  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Type Characters](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Efficient Use of Data Types](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)