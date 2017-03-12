---
title: "Arithmetic Operators in Visual Basic | Microsoft Docs"
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
  - "type safety"
  - "operators [Visual Basic], bitwise"
  - "operators [Visual Basic], bit-shift"
  - "bitwise operators"
  - "bit-shift operators"
  - "zero, division by zero"
  - "operators [Visual Basic], arithmetic"
  - "division, by zero"
  - "Visual Basic code, operators"
  - "arithmetic operators, about arithmetic operators"
ms.assetid: 325dac7a-ea4f-41d5-8b48-f6e904211569
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Arithmetic Operators in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Gli operatori aritmetici consentono di eseguire molte delle comuni operazioni aritmetiche che comportano il calcolo di valori numerici rappresentati da valori letterali, variabili, altre espressioni, chiamate di funzioni e di proprietà e costanti.  Vengono classificati come operatori aritmetici anche gli operatori di spostamento di bit, che operano a livello dei singoli bit degli operandi spostando gli schemi di bit a sinistra o a destra.  
  
## Operazioni aritmetiche  
 È possibile sommare due valori di un'espressione con l'[\+ Operator](../../../../visual-basic/language-reference/operators/addition-operator.md) oppure sottrarne uno da un altro con l'[\- Operator](../../../../visual-basic/language-reference/operators/subtraction-operator.md), come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#57](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_1.vb)]  
  
 L'[\- Operator](../../../../visual-basic/language-reference/operators/subtraction-operator.md) viene utilizzato anche per la negazione, ma con un solo operando, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#58](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_2.vb)]  
  
 Per la moltiplicazione e la divisione vengono utilizzati rispettivamente l'[\* Operator](../../../../visual-basic/language-reference/operators/multiplication-operator.md) e l'[\/ Operator](../../../../visual-basic/language-reference/operators/floating-point-division-operator.md), come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#59](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_3.vb)]  
  
 L'[^ Operator](../../../../visual-basic/language-reference/operators/exponentiation-operator.md) viene utilizzato per l'elevamento a potenza, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#60](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_4.vb)]  
  
 La divisione di interi viene eseguita con l'[\\ Operator](../../../../visual-basic/language-reference/operators/integer-division-operator.md).  La divisione di interi restituisce il quoziente, ovvero il valore intero che rappresenta il numero di volte in cui il divisore sta nel dividendo senza tenere conto di eventuali resti.  Per questo operatore, sia il divisore che il dividendo devono essere tipi integrali \(`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long` e `ULong`\).  È necessario che tutti gli altri tipi vengano prima convertiti in un tipo integrale.  Nell'esempio riportato di seguito viene illustrata la divisione di interi.  
  
 [!code-vb[VbVbalrOperators#61](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_5.vb)]  
  
 Il modulo aritmetico viene eseguito con l'[Operatore Mod](../../../../visual-basic/language-reference/operators/mod-operator.md).  Questo operatore restituisce il resto dopo che il dividendo è stato diviso per il divisore per un numero intero di volte.  Se sia il divisore che il dividendo sono tipi integrali, il valore restituito è integrale.  Se il divisore e il dividendo sono tipi a virgola mobile, anche il valore restituito è a virgola mobile.  Nell'esempio che segue viene illustrato questo comportamento.  
  
 [!code-vb[VbVbalrOperators#62](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_6.vb)]  
  
 [!code-vb[VbVbalrOperators#63](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_7.vb)]  
  
### Tentativo di divisione per zero  
 La divisione per zero produce risultati diversi a seconda dei tipi di dati utilizzati.  Nelle divisioni di integrali \(`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`\), [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] genera un'eccezione <xref:System.DivideByZeroException>.  Anche nel caso di operazioni di divisione con tipi di dati `Decimal` o `Single`, [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] genera un'eccezione <xref:System.DivideByZeroException>.  
  
 Nelle divisioni a virgola mobile relative a tipi di dati `Double` non viene generata alcuna eccezione e il risultato è il membro della classe che rappresenta <xref:System.Double.NaN>, <xref:System.Double.PositiveInfinity> o <xref:System.Double.NegativeInfinity>, a seconda del dividendo.  Nella tabella seguente sono riassunti i vari risultati ottenuti cercando di dividere un valore `Double` per zero.  
  
|||||  
|-|-|-|-|  
|Tipo di dati del dividendo|Tipo di dati del divisore|Valore del dividendo|Risultato|  
|`Double`|`Double`|0|<xref:System.Double.NaN> \(numero non definito matematicamente\)|  
|`Double`|`Double`|\> 0|<xref:System.Double.PositiveInfinity>|  
|`Double`|`Double`|\< 0|<xref:System.Double.NegativeInfinity>|  
  
 Quando viene rilevata un'eccezione <xref:System.DivideByZeroException>, è possibile gestirla utilizzandone i membri.  Ad esempio, nella proprietà <xref:System.Exception.Message%2A> è memorizzato il testo del messaggio relativo all'eccezione.  Per ulteriori informazioni, vedere [Try...Catch...Finally Statement](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## Operazioni di spostamento di bit  
 Un'operazione di spostamento di bit esegue uno spostamento aritmetico su uno schema di bit.  Lo schema è contenuto nell'operando sulla sinistra, mentre l'operando sulla destra specifica il numero di posizioni di spostamento dello schema.  È possibile spostare lo schema a destra con l'[\>\> Operator](../../../../visual-basic/language-reference/operators/right-shift-operator.md) o a sinistra con l'[\<\< Operator](../../../../visual-basic/language-reference/operators/left-shift-operator.md).  
  
 Il tipo di dati dell'operando dello schema deve essere `SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long` o `ULong`.  Il tipo di dati dell'operando relativo all'entità dello spostamento deve essere `Integer` o deve ampliarsi a `Integer`.  
  
 Gli spostamenti aritmetici non sono circolari. In altre parole, i bit spostati oltre una delle estremità del risultato non vengono reintrodotti all'altra estremità.  Le posizioni di bit liberate da uno spostamento vengono impostate nel modo seguente:  
  
-   0 per uno spostamento aritmetico a sinistra  
  
-   0 per uno spostamento aritmetico a destra di un numero positivo  
  
-   0 per uno spostamento aritmetico a destra di un tipo di dati senza segno \(`Byte`, `UShort`, `UInteger`, `ULong`\)  
  
-   1 per uno spostamento aritmetico a destra di un numero negativo \(`SByte`, `Short`, `Integer` o `Long`\)  
  
 Nell'esempio che segue viene effettuato uno spostamento sia a sinistra che a destra di un valore `Integer`.  
  
 [!code-vb[VbVbalrOperators#64](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/arithmetic-operators_8.vb)]  
  
 Gli spostamenti aritmetici non generano mai eccezioni di overflow.  
  
## Operazioni bit per bit  
 Oltre a essere operatori logici, `Not`, `Or`, `And` e `Xor` possono eseguire anche operazioni aritmetiche bit per bit se utilizzati con valori numerici.  Per ulteriori informazioni, vedere la sezione relativa alle operazioni bit per bit in [Logical and Bitwise Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md).  
  
## Indipendenza dai tipi  
 È solitamente necessario che gli operandi siano dello stesso tipo.  Se, ad esempio, si esegue un'addizione con una variabile `Integer`, è necessario che il secondo termine sia un'altra variabile `Integer` e che la variabile cui viene assegnato il risultato sia anch'essa di tipo `Integer`.  
  
 Nella scrittura di codice indipendente dai tipi è buona norma utilizzare [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md).  Se si imposta `Option Strict On`, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] esegue automaticamente conversioni *indipendenti dai tipi*.  Se, ad esempio, si cerca di sommare una variabile `Integer` a una variabile `Double` e di assegnare il valore a una variabile `Double`, l'operazione viene eseguita normalmente, perché è possibile convertire un valore `Integer` in `Double` senza perdita di dati.  Nel caso di conversioni non indipendenti dai tipi, d'altra parte, l'uso di `Option Strict On` genera un errore di compilazione.  Se, ad esempio, si cerca di sommare una variabile `Integer` a una variabile `Double` e di assegnare il valore a una variabile `Integer`, viene generato un errore di compilazione, perché una variabile `Double` non può essere convertita in modo implicito nel tipo `Integer`.  
  
 Se si imposta `Option Strict Off`, tuttavia, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente conversioni implicite verso un tipo di dati più piccolo, sebbene possano determinare una perdita imprevista di dati o di precisione.  Per questo motivo si raccomanda di utilizzare `Option Strict On` durante la scrittura di codice di produzione.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
## Vedere anche  
 [Arithmetic Operators](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Bit Shift Operators](../../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Concatenation Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [Efficient Combination of Operators](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)