---
title: Risoluzione dei tipi di dati (Visual Basic) | Documenti di Microsoft
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
- Char data type, converting
- Decimal data type, conversions
- data types [Visual Basic], troubleshooting
- literals, default types
- type characters, literal
- Mod operator [Visual Basic], in floating-point operations
- troubleshooting Visual Basic, data types
- troubleshooting data types
- floating-point numbers, precision
- Boolean data type, converting
- literal types
- literal type characters
- floating-point numbers, imprecision
- String data type, converting
- floating-point numbers, comparison
- floating-point numbers
ms.assetid: 90040d67-b630-4125-a6ae-37195b079042
caps.latest.revision: 29
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cfb8fc77d3e0d85ef795a94fc95ab61a8f68ff39
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-data-types-visual-basic"></a>Risoluzione dei problemi relativi ai tipi di dati (Visual Basic)
Questa pagina sono elencati alcuni problemi comuni che possono verificarsi quando si eseguono operazioni su tipi di dati intrinseci.  
  
## <a name="floating-point-expressions-do-not-compare-as-equal"></a>Le espressioni a virgola mobile non vengono considerati uguali  
 Quando si utilizzano numeri a virgola mobile ([singolo tipo di dati](../../../../visual-basic/language-reference/data-types/single-data-type.md) e [tipo di dati Double](../../../../visual-basic/language-reference/data-types/double-data-type.md)), tenere presente che sono archiviati come frazioni binarie. Ciò significa che non possono contenere una rappresentazione esatta di qualsiasi quantità che non è una frazione binaria (nel formato k / (2 ^ n) dove k e n sono numeri interi). Ad esempio 0,5 (= 1/2) e 0,3125 (= 5/16) possono essere mantenuti come valori precisi, mentre 0,2 (= 1/5) e 0,3 (= 3/10) possono essere solo approssimazioni.  
  
 Per questo motivo imprecisione, è possibile basarsi sui risultati esatti quando si opera su valori a virgola mobile. In particolare, due valori teoricamente identici potrebbero avere rappresentazioni leggermente diverse.  
  
| Per confrontare le quantità a virgola mobile | 
|---| 
|1.  Calcolare il valore assoluto della loro differenza utilizzando il <xref:System.Math.Abs%2A>metodo la <xref:System.Math>classe il <xref:System>dello spazio dei nomi.</xref:System> </xref:System.Math> </xref:System.Math.Abs%2A><br />2.  Determinare una differenza massima accettabile, in modo che è possibile prendere in considerazione le due quantità siano uguali ai fini pratici se la differenza non sia superiore.<br />3.  Confrontare il valore assoluto della differenza con la differenza accettabile.|  
  
 Nell'esempio seguente viene illustrato sia corretto e corretto un confronto fra due `Double` valori.  
  
 [!code-vb[VbVbalrDataTypes&#10;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_1.vb)]  
  
 Nell'esempio precedente viene utilizzato il <xref:System.Double.ToString%2A>metodo il <xref:System.Double>struttura in modo che possa specificare una precisione migliore del `CStr` utilizza (parola chiave).</xref:System.Double> </xref:System.Double.ToString%2A> Il valore predefinito è 15 cifre, ma il formato "G17" lo estende a 17 cifre.  
  
## <a name="mod-operator-does-not-return-accurate-result"></a>Operatore Mod non restituisce risultati corretti  
 A causa dell'imprecisione dell'archiviazione a virgola mobile, il [operatore Mod](../../../../visual-basic/language-reference/operators/mod-operator.md) può restituire un risultato imprevisto quando almeno uno degli operandi è a virgola mobile.  
  
 Il [tipo di dati Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md) non la rappresentazione a virgola mobile. Molti numeri inesatti in `Single` e `Double` sono esatti in `Decimal` (ad esempio 0,2 e 0,3). Sebbene il calcolo aritmetico sia più lento nel `Decimal` rispetto in virgola mobile, potrebbe essere utile il rallentamento delle prestazioni per ottenere una maggiore precisione.  
  
|Per trovare il resto intero di quantità a virgola mobile|  
|---|  
|1.  Dichiarare le variabili come `Decimal`.<br />2.  Utilizzare il tipo di valore letterale carattere `D` per imporre i valori letterali per `Decimal`, nel caso in cui i relativi valori sono troppo grandi per il `Long` tipo di dati.|  
  
 Nell'esempio seguente viene illustrata la potenziale imprecisione degli operandi a virgola mobile.  
  
 [!code-vb[VbVbalrDataTypes&#11;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_2.vb)]  
  
 Nell'esempio precedente viene utilizzato il <xref:System.Double.ToString%2A>metodo il <xref:System.Double>struttura in modo che possa specificare una precisione migliore del `CStr` utilizza (parola chiave).</xref:System.Double> </xref:System.Double.ToString%2A> Il valore predefinito è 15 cifre, ma il formato "G17" lo estende a 17 cifre.  
  
 Poiché `zeroPointTwo` è `Double`, il valore per 0,2 è una frazione binaria ripetuta all'infinito con un valore archiviato di 0,20000000000000001. Dividendo 2,0 per questa quantità il risultato è 9,9999999999999995 con il resto di 0,19999999999999991.  
  
 Nell'espressione per `decimalRemainder`, il carattere di tipo letterale `D` forza entrambi gli operandi in `Decimal`, e 0.2 è una rappresentazione precisa. Pertanto il `Mod` operatore produce il resto previsto pari a 0,0.  
  
 Si noti che non è sufficiente dichiarare `decimalRemainder` come `Decimal`. È anche necessario imporre ai valori letterali di `Decimal`, oppure utilizzare `Double` per impostazione predefinita e `decimalRemainder` riceve lo stesso valore impreciso di `doubleRemainder`.  
  
## <a name="boolean-type-does-not-convert-to-numeric-type-accurately"></a>Tipo Boolean non converte in modo accurato in tipo numerico  
 [Tipo di dati Boolean](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) valori non vengono archiviati come numeri e i valori archiviati non vengono considerati equivalenti ai numeri. Per garantire la compatibilità con le versioni precedenti, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce parole chiave di conversione ([funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md), `CBool`, `CInt`e così via) per la conversione tra `Boolean` e tipi numerici. Tuttavia, altri linguaggi talvolta eseguono queste conversioni in modo diverso, come il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] metodi.  
  
 Non scrivere mai codice che si basa su valori numerici equivalenti per `True` e `False`. Quando possibile, è consigliabile limitare l'utilizzo di `Boolean` variabili per i valori logici per il quale sono progettate. Se è necessario combinare `Boolean` e valori numerici, assicurarsi di aver compreso il metodo di conversione selezionato.  
  
### <a name="conversion-in-visual-basic"></a>Conversione in Visual Basic  
 Quando si utilizza il `CType` o `CBool` parole chiave di conversione per convertire i tipi di dati numerici per `Boolean`, diventa 0 `False` e tutti gli altri valori diventano `True`. Quando esegue la conversione `Boolean` valori in tipi numerici utilizzando le parole chiave di conversione, `False` diventa 0 e `True` diventa -1.  
  
### <a name="conversion-in-the-framework"></a>Conversione in Framework  
 Il <xref:System.Convert.ToInt32%2A>metodo la <xref:System.Convert>classe il <xref:System>converte dello spazio dei nomi `True` e +&1;.</xref:System> </xref:System.Convert> </xref:System.Convert.ToInt32%2A>  
  
 Se è necessario convertire un `Boolean` valore a un tipo di dati numerici, assicurarsi che il metodo di conversione da utilizzare.  
  
## <a name="character-literal-generates-compiler-error"></a>Valore letterale a carattere genera l'errore del compilatore  
 In assenza di qualsiasi tipo di carattere, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] assume i tipi di dati per i valori letterali predefiniti. Il tipo predefinito per un valore letterale carattere, racchiusa tra virgolette (`" "`), è `String`.  
  
 Il `String` tipo di dati non si amplia per il [tipo di dati Char](../../../../visual-basic/language-reference/data-types/char-data-type.md). Ciò significa che se si desidera assegnare un valore letterale in un `Char` variabile, è necessario eseguire una conversione di restrizione o imporre al valore letterale per il `Char` tipo.  

|Per creare un carattere letterale da assegnare a una variabile o costante|
|---|  
|1.  Dichiarare la variabile o costante come `Char`.<br />2.  Racchiudere il valore del carattere tra virgolette (`" "`).<br />3.  Seguire il segno di virgolette doppie di chiusura con il carattere di tipo letterale `C` per forzare il valore letterale `Char`. Questa operazione è necessaria se il controllo dei tipi ([istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) è `On`, ed è comunque preferibile in ogni caso.|  
  
 L'esempio seguente illustra le assegnazioni di esito negativa e non riuscite di un valore letterale di un `Char` variabile.  
  
 [!code-vb[VbVbalrDataTypes&#12;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_3.vb)]  
  
 È sempre un rischio utilizzando le conversioni, in quanto si può avere esito negativo in fase di esecuzione. Ad esempio, una conversione da `String` a `Char` può non riuscire se il `String` valore contiene più di un carattere. Pertanto, è preferibile programmare per utilizzare il `C` tipo di carattere.  
  
## <a name="string-conversion-fails-at-run-time"></a>Conversione di stringhe ha esito negativo in fase di esecuzione  
 Il [tipo di dati String](../../../../visual-basic/language-reference/data-types/string-data-type.md) fa parte di un numero molto ridotto le conversioni di ampliamento. `String`Allarga solo a se stesso e `Object`e solo `Char` e `Char()` (un `Char` matrice) ampliarsi `String`. In questo modo `String` variabili e costanti possono contenere valori che non possono contenere altri tipi di dati.  
  
 Quando il controllo del tipo di opzione ([istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) è `On`, il compilatore impedisce tutte le conversioni implicite. Sono inclusi quelli che coinvolgono `String`. Il codice può comunque utilizzare parole chiave di conversione, ad esempio `CStr` e [funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md), che spingono i [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] per tentare la conversione.  
  
> [!NOTE]
>  Viene eliminato l'errore di conversione di restrizione per le conversioni da elementi di un `For Each…Next` insieme alla variabile di controllo del ciclo. Per ulteriori informazioni ed esempi, vedere la sezione "Conversioni di restrizione" [For Each... Istruzione successiva](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
### <a name="narrowing-conversion-protection"></a>Protezione della conversione di restrizione  
 Lo svantaggio di conversioni di restrizione è che può avere esito negativo in fase di esecuzione. Ad esempio, se un `String` variabile contiene esclusivamente "True" o "False", non può essere convertito in `Boolean`. Se sono presenti caratteri di punteggiatura, errore di conversione in qualsiasi tipo numerico. A meno che non si è certi che il `String` variabile contiene sempre valori che può accettare il tipo di destinazione, non è consigliabile provare una conversione.  
  
 Se è necessario convertire da `String` a un altro tipo di dati, la procedura più sicura consiste nel racchiudere la conversione tentata nel [Try... Catch... Istruzione finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md). Ciò consente di gestire un errore in fase di esecuzione.  
  
### <a name="character-arrays"></a>Matrici di caratteri  
 Un singolo `Char` e una matrice di `Char` elementi si ampliano entrambi a `String`. Tuttavia, `String` si amplia in `Char()`. Per convertire un `String` valore a un `Char` matrice, è possibile utilizzare il <xref:System.String.ToCharArray%2A>metodo della <xref:System.String?displayProperty=fullName>classe.</xref:System.String?displayProperty=fullName> </xref:System.String.ToCharArray%2A>  
  
### <a name="meaningless-values"></a>Valori non significativi  
 In generale, `String` valori non sono significativi in altri tipi di dati e la conversione è altamente artificiale e pericolosa. Quando possibile, è consigliabile limitare l'utilizzo di `String` variabili per le sequenze di caratteri per i quali sono progettate. Non scrivere mai codice che si basa su valori equivalenti in altri tipi.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Caratteri tipo](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Uso efficiente dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
