---
title: Gli operatori aritmetici in Visual Basic | Documenti di Microsoft
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
- type safety
- operators [Visual Basic], bitwise
- operators [Visual Basic], bit-shift
- bitwise operators
- bit-shift operators
- zero, division by zero
- operators [Visual Basic], arithmetic
- division, by zero
- Visual Basic code, operators
- arithmetic operators, about arithmetic operators
ms.assetid: 325dac7a-ea4f-41d5-8b48-f6e904211569
caps.latest.revision: 20
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
ms.openlocfilehash: c724bf8b6794e71d49b32c7d3ce9e010f541f68f
ms.lasthandoff: 03/13/2017

---
# <a name="arithmetic-operators-in-visual-basic"></a>Operatori aritmetici in Visual Basic
Operatori aritmetici consentono di eseguire molte delle comuni operazioni aritmetiche che comportano il calcolo di valori numerici rappresentati da valori letterali, variabili, altre espressioni, funzione e chiamate di proprietà e costanti. Vengono classificati come operatori aritmetici sono gli operatori di spostamento di bit, che operano a livello dei singoli bit degli operandi e spostare degli schemi di bit verso sinistra o destra.  
  
## <a name="arithmetic-operations"></a>Operazioni aritmetiche  
 È possibile aggiungere due valori in un'espressione con il [+ (operatore)](../../../../visual-basic/language-reference/operators/addition-operator.md), o sottrarre uno da altro con il [-operatore (Visual Basic)](../../../../visual-basic/language-reference/operators/subtraction-operator.md), come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#57;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_1.vb)]  
  
 Negazione utilizza inoltre il [-operatore (Visual Basic)](../../../../visual-basic/language-reference/operators/subtraction-operator.md), ma con un solo operando, come nell'esempio seguente viene illustrato.  
  
 [!code-vb[VbVbalrOperators&#58;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_2.vb)]  
  
 Utilizzo di moltiplicazione e divisione di [* (operatore)](../../../../visual-basic/language-reference/operators/multiplication-operator.md) e [/ (operatore) (Visual Basic)](../../../../visual-basic/language-reference/operators/floating-point-division-operator.md), rispettivamente, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#59;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_3.vb)]  
  
 Elevamento a potenza utilizza il [^ (operatore)](../../../../visual-basic/language-reference/operators/exponentiation-operator.md), come illustrato nell'esempio seguente.  
  
 [!code-vb[60 VbVbalrOperators](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_4.vb)]  
  
 Divisione di interi viene eseguita con il [\ (operatore) (Visual Basic)](../../../../visual-basic/language-reference/operators/integer-division-operator.md). Divisione di interi restituisce il quoziente, vale a dire il numero intero che rappresenta il numero di volte in cui il divisore possono essere suddivisi in dividendo senza tenere conto di eventuali residui. Sia il divisore e il dividendo devono essere tipi integrali (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, e `ULong`) per l'operatore. Tutti gli altri tipi devono essere convertiti in un tipo integrale prima. L'esempio seguente illustra la divisione di interi.  
  
 [!code-vb[VbVbalrOperators&#61;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_5.vb)]  
  
 Il modulo aritmetico viene eseguito utilizzando il [operatore Mod](../../../../visual-basic/language-reference/operators/mod-operator.md). Questo operatore restituisce il resto dopo aver diviso il divisore per il dividendo per un numero intero di volte. Se il divisore e dividendo sono tipi integrali, il valore restituito è di tipo integrale. Se il divisore e dividendo sono tipi a virgola mobile, il valore restituito è anche a virgola mobile. Nell'esempio seguente viene illustrato questo comportamento.  
  
 [!code-vb[&#62; VbVbalrOperators](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_6.vb)]  
  
 [!code-vb[VbVbalrOperators&#63;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_7.vb)]  
  
### <a name="attempted-division-by-zero"></a>Tentativo di divisione per Zero  
 Divisione per zero produce risultati diversi a seconda dei tipi di dati coinvolti. In integral divisions (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`), the [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] throws a <xref:System.DivideByZeroException> exception.</xref:System.DivideByZeroException> In operazioni di divisione di `Decimal` o `Single` tipo di dati, il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] genera inoltre un <xref:System.DivideByZeroException>(eccezione).</xref:System.DivideByZeroException>  
  
 Divisioni a virgola mobile che coinvolgono il `Double` tipo di dati, viene generata alcuna eccezione e il risultato è il membro della classe che rappresenta <xref:System.Double.NaN>, <xref:System.Double.PositiveInfinity>, o <xref:System.Double.NegativeInfinity>, a seconda del dividendo.</xref:System.Double.NegativeInfinity> </xref:System.Double.PositiveInfinity> </xref:System.Double.NaN> Nella tabella seguente vengono riepilogati i diversi risultati tentativo di dividere un `Double` valore in base zero.  
  
|Tipo di dati dividendo|Tipo di dati divisore|Valore del dividendo|Risultato|  
|---|---|---|---|  
|`Double`|`Double`|0|<xref:System.Double.NaN>(non un numero definito matematicamente)</xref:System.Double.NaN>|  
|`Double`|`Double`|> 0|<xref:System.Double.PositiveInfinity></xref:System.Double.PositiveInfinity>|  
|`Double`|`Double`|\< 0|<xref:System.Double.NegativeInfinity></xref:System.Double.NegativeInfinity>|  
  
 Quando viene rilevata un' <xref:System.DivideByZeroException>che eccezione, è possibile utilizzare i membri che consentono di gestirla.</xref:System.DivideByZeroException> Ad esempio, la <xref:System.Exception.Message%2A>proprietà contiene il testo del messaggio dell'eccezione.</xref:System.Exception.Message%2A> Per ulteriori informazioni, vedere [Try... Catch... Istruzione finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## <a name="bit-shift-operations"></a>Operazioni di spostamento di bit  
 Un'operazione di spostamento bit esegue uno spostamento aritmetico in uno schema di bit. Il modello di contenuto dell'operando di sinistra, mentre l'operando a destra specifica il numero di posizioni per spostare lo schema. È possibile spostare lo schema a destra con il [>> operatore](../../../../visual-basic/language-reference/operators/right-shift-operator.md) o a sinistra con la [ <> </> ](../../../../visual-basic/language-reference/operators/left-shift-operator.md).  
  
 Il tipo di dati dell'operando dello schema deve essere `SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, o `ULong`. Il tipo di dati dell'operando quantità MAIUSC deve essere `Integer` o deve ampliarsi a `Integer`.  
  
 Aritmetici non sono circolare, ovvero i bit spostati oltre un'estremità del risultato non vengono reinstallati a altra estremità. Le posizioni dei bit liberate da uno spostamento sono impostate come segue:  
  
-   0 per uno spostamento aritmetico a sinistra  
  
-   0 per uno spostamento aritmetico a destra di un numero positivo  
  
-   0 per uno spostamento aritmetico a destra di un tipo di dati senza segno (`Byte`, `UShort`, `UInteger`, `ULong`)  
  
-   1 per uno spostamento aritmetico a destra di un numero negativo (`SByte`, `Short`, `Integer`, o `Long`)  
  
 Nell'esempio seguente sposta un `Integer` valore sia a sinistra e destra.  
  
 [!code-vb[&#64; VbVbalrOperators](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_8.vb)]  
  
 Aritmetici non generano mai eccezioni di overflow.  
  
## <a name="bitwise-operations"></a>Operazioni bit per bit  
 Oltre a essere operatori logici, `Not`, `Or`, `And`, e `Xor` inoltre eseguire operazioni aritmetiche bit per bit se utilizzati con valori numerici. Per ulteriori informazioni, vedere "Operazioni bit per bit" in [operatori logici e bit per bit in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md).  
  
## <a name="type-safety"></a>Indipendenza dai tipi  
 Gli operandi in genere devono essere dello stesso tipo. Ad esempio, se si esegue un'addizione con un `Integer` variabile, è necessario aggiungerlo a un altro `Integer` variabile ed è necessario assegnare il risultato a una variabile di tipo `Integer` anche.  
  
 Un modo per garantire una buona indipendente dai tipi scrittura di codice consiste nell'utilizzare il [istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md). Se si imposta `Option Strict On`, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esegue automaticamente *indipendente dai tipi* conversioni. Ad esempio, se si tenta di aggiungere un `Integer` variabile a un `Double` variabile e assegnare il valore di un `Double` variabile, l'operazione viene eseguita normalmente, perché un `Integer` valore può essere convertito in `Double` senza perdita di dati. Le conversioni di tipo unsafe, d'altra parte, causano un errore del compilatore con `Option Strict On`. Ad esempio, se si tenta di aggiungere un `Integer` variabile a un `Double` variabile e assegnare il valore di un `Integer` variabile, un errore del compilatore generato, perché un `Double` variabile non può essere convertita in modo implicito nel tipo `Integer`.  
  
 Se si imposta `Option Strict Off`, tuttavia, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente le conversioni di narrowing implicite abbiano luogo, sebbene possano determinare una perdita imprevista di dati o di precisione. Per questo motivo, è consigliabile utilizzare `Option Strict On` durante la scrittura di codice di produzione. Per ulteriori informazioni, vedere [conversioni di ampliamento e restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aritmetici (operatori)](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operatori di scorrimento bit](../../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [Operatori di confronto in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Operatori di concatenazione in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Operatori logici e bit per bit in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [Combinazione efficace di operatori](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
