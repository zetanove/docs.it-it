---
title: "Data Types of Operator Results (Visual Basic) | Microsoft Docs"
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
  - "data types [Visual Basic], operator result data types"
  - "result data types"
  - "operator result data types"
  - "operators [Visual Basic], data types"
  - "data types [Visual Basic], ranges"
  - "operators [Visual Basic], result data types"
ms.assetid: 9d524533-e1a1-4aa8-b1b8-622068173d06
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Data Types of Operator Results (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] il tipo di dati del risultato di un'operazione viene determinato in base ai tipi di dati degli operandi.  In alcuni casi, può trattarsi di un tipo di dati con un intervallo di valori maggiore rispetto a quello di uno dei due operandi.  
  
## Intervalli dei tipi di dati  
 Di seguito sono riportati gli intervalli dei principali tipi di dati in ordine crescente:  
  
-   [Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md) \- Due valori possibili.  
  
-   [SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md), [Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md) \- 256 valori integrali possibili.  
  
-   [Short](../../../visual-basic/language-reference/data-types/short-data-type.md), [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md) \- 65.536 valori integrali possibili \(compresi tra 6,5...E\+4\).  
  
-   [Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md), [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md) \- 4.294.967.296 valori integrali possibili \(compresi tra 4,2...E\+9\).  
  
-   [Long](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md) \- 18.446.744.073.709.551.615 valori integrali possibili \(compresi tra 1,8...E\+19\).  
  
-   [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) \- Valori integrali possibili compresi tra 1,5...E\+29; intervallo massimo compreso tra 7,9...E\+28 \(valore assoluto\).  
  
-   [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) \- Intervallo massimo compreso tra 3,4...E\+38 \(valore assoluto\).  
  
-   [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) \- Intervallo massimo compreso tra 1,7...E\+308 \(valore assoluto\).  
  
 Per ulteriori informazioni sui tipi di dati di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], vedere [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
 Se un operando restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), gli operatori aritmetici di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] considerano tale valore uguale a zero.  
  
## Operazioni aritmetiche su valori decimali  
 Si noti che il tipo di dati [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) non è né a virgola mobile, né integer.  
  
 Se un operando di un'operazione `+`, `–`, `*`, `/` o `Mod` è di tipo  `Decimal` e l'altro non è di tipo `Single` o `Double`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte l'altro operando verso il tipo di dati più grande `Decimal`.  L'operazione viene eseguita con il tipo `Decimal` e il tipo di dati del risultato è `Decimal`.  
  
## Operazioni aritmetiche su valori a virgola mobile  
 In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la maggior parte delle operazioni aritmetiche su valori a virgola mobile viene eseguita con [Double](../../../visual-basic/language-reference/data-types/double-data-type.md), il tipo di dati più efficiente per tali operazioni.  Tuttavia, se un operando è di tipo [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) e l'altro non è di tipo `Double`, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] l'operazione viene eseguita con il tipo `Single`.  Ciascun operando viene convertito, se necessario, verso il corrispondente tipo di dati più grande prima dell'operazione. Il risultato ottenuto corrisponde a tale tipo di dati.  
  
### Operatori \/ e ^  
 L'operatore `/` viene definito solo per i tipi di dati [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md), [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) e [Double](../../../visual-basic/language-reference/data-types/double-data-type.md).  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] ciascun operando viene convertito nel corrispondente tipo di dati più grande, secondo necessità, prima di eseguire l'operazione. Il risultato dell'operazione corrisponderà a tale tipo di dati.  
  
 Nella tabella riportata di seguito vengono illustrati i tipi di dati del risultato per l'operatore `/`.  La tabella è simmetrica. Per una specifica combinazione di tipi di dati degli operandi, infatti, il tipo di dati del risultato sarà lo stesso indipendentemente dall'ordine degli operandi stessi.  
  
||||||  
|-|-|-|-|-|  
||`Decimal`|`Single`|`Double`|Qualsiasi tipo di Integer|  
|`Decimal`|Decimal|Single|Double|Decimal|  
|`Single`|Single|Single|Double|Single|  
|`Double`|Double|Double|Double|Double|  
|Qualsiasi tipo di Integer|Decimal|Single|Double|Double|  
  
 L'operatore `^` viene definito solo per il tipo di dati `Double`.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte, se necessario, ciascun operando nel tipo `Double` prima dell'operazione e il tipo di dati del risultato sarà sempre `Double`.  
  
## Operazioni aritmetiche su valori integer  
 Il tipo di dati del risultato di un'operazione su valori integer varia in base ai tipi di dati degli operandi.  In generale, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono utilizzati i seguenti criteri per determinare il tipo di dati del risultato:  
  
-   Se per entrambi gli operandi di un operatore binario è definito lo stesso tipo di dati, il risultato sarà dello stesso tipo.  Un'eccezione è costituita dal tipo `Boolean`, che viene forzatamente convertito in `Short`.  
  
-   Se per l'operazione vengono utilizzati un operando con segno e uno senza segno, il risultato sarà un tipo con segno con un intervallo di grandezza pari almeno a quello di uno dei due operandi.  
  
-   Negli altri casi, il risultato è in genere costituito dal più grande dei due tipi di dati degli operandi.  
  
 Si noti che il tipo di dati del risultato potrebbe essere diverso dal tipo di dati di uno dei due operandi.  
  
> [!NOTE]
>  Il tipo di dati del risultato non sempre è sufficientemente grande da contenere tutti i possibili valori risultanti dall'operazione.  Se il valore è troppo grande per il tipo di dati del risultato, può verificarsi un'eccezione <xref:System.OverflowException>.  
  
### Operatori unari \+ e –  
 Nella tabella riportata di seguito vengono illustrati i tipi di dati del risultato per i due operatori unari `+` e `–`.  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|Operatore unario `+`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|Operatore unario `–`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
  
### Operatori \<\< e \>\>  
 Nella tabella seguente vengono illustrati i tipi di dati risultanti per i due operatori di scorrimento bit, `<<` e `>>`.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] ogni operatore di scorrimento bit viene trattato come operatore unario sull'operando di sinistra \(lo schema di bit che deve essere fatto scorrere\).  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`<<`, `>>`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 Se l'operando di sinistra è di tipo `Decimal`, `Single`, `Double` o `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo nel tipo `Long` prima dell'operazione e il tipo di dati del risultato sarà `Long`.  L'operando di destra \(il numero di posizioni di bit da spostare\) deve essere di tipo `Integer` oppure di un tipo che viene convertito verso il tipo più grande `Integer`.  
  
### Operatori binari \+, –, \* e Mod  
 Nella tabella riportata di seguito vengono illustrati i tipi di dati del risultato per gli operatori binari `+` e `–`, nonché gli operatori `*` e `Mod`.  La tabella è simmetrica. Per una specifica combinazione di tipi di dati degli operandi, infatti, il tipo di dati del risultato sarà lo stesso indipendentemente dall'ordine degli operandi stessi.  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Decimal|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Decimal|  
|`ULong`|Decimal|Decimal|ULong|Decimal|ULong|Decimal|ULong|Decimal|ULong|  
  
### Operatore \\  
 Nella tabella riportata di seguito vengono illustrati i tipi di dati del risultato per l'operatore `\`.  La tabella è simmetrica. Per una specifica combinazione di tipi di dati degli operandi, infatti, il tipo di dati del risultato sarà lo stesso indipendentemente dall'ordine degli operandi stessi.  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 Se uno dei due operandi dell'operatore `\` è di tipo [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md), [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) o [Double](../../../visual-basic/language-reference/data-types/double-data-type.md), [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo nel tipo [Long](../../../visual-basic/language-reference/data-types/long-data-type.md) prima dell'operazione e il tipo di dati del risultato sarà `Long`.  
  
## Confronti relazionali e bit per bit  
 Il tipo di dati del risultato di un'operazione relazionale \(`=`, `<>`, `<`, `>`, `<=`, `>=`\) è sempre `Boolean`[Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md).  Lo stesso vale anche per le operazioni logiche \(`And`, `AndAlso`, `Not`, `Or`, `OrElse`, `Xor`\) su operandi di tipo `Boolean`.  
  
 Il tipo di dati del risultato di un'operazione logica bit per bit varia in base ai tipi di dati degli operandi.  Si noti che `AndAlso` e `OrElse` sono definiti solo per il tipo `Boolean` e [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte, se necessario, ciascun operando nel tipo `Boolean` prima che venga eseguita l'operazione.  
  
### Operatori \=, \<\>, \<, \>, \<\= e \>\=  
 Se entrambi gli operandi sono di tipo `Boolean`, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] `True` viene considerato inferiore a `False`.  Se un tipo numerico viene confrontato con un tipo `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertire il tipo `String` in `Double` prima dell'operazione.  È possibile confrontare un operando `Char` o `Date` solo con un altro operando dello stesso tipo di dati.  Il tipo di dati del risultato sarà sempre `Boolean`.  
  
### Operatore Not bit per bit  
 Nella tabella riportata di seguito vengono illustrati i tipi di dati del risultato per l'operatore `Not` bit per bit.  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Not`|Boolean|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 Se l'operando è di tipo `Decimal`, `Single`, `Double` o `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo nel tipo `Long` prima dell'operazione e il tipo di dati del risultato sarà `Long`.  
  
### Operatori And, Or e Xor bit per bit  
 Nella tabella riportata di seguito vengono illustrati i tipi di dati del risultato per gli operatori `And`, `Or` e `Xor` bit per bit.  La tabella è simmetrica. Per una specifica combinazione di tipi di dati degli operandi, infatti, il tipo di dati del risultato sarà lo stesso indipendentemente dall'ordine degli operandi stessi.  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Boolean|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 Se un operando è di tipo `Decimal`, `Single`, `Double` o `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo nel tipo `Long` prima dell'operazione e il tipo di dati del risultato sarà lo stesso come se l'operando fosse stato in precedenza di tipo `Long`.  
  
## Operatori vari  
 L'operatore `&` viene definito solo per concatenazione di operandi `String`.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte, se necessario, ciascun operando nel tipo `String` prima dell'operazione e il tipo di dati del risultato sarà sempre `String`.  Per gli scopi dell'operatore `&`, tutte le conversioni nel tipo `String` vengono considerate conversioni verso un tipo di dati più grande, anche se l'istruzione `Option Strict` è impostata su `On`.  
  
 Per gli operatori `Is` e `IsNot` è necessario che entrambi gli operandi siano di un tipo di riferimento.  Per l'espressione `TypeOf`...`Is` è necessario che il primo operando sia di un tipo di riferimento e il secondo sia il nome di un tipo di dati.  In tutti questi casi, il tipo di dati del risultato sarà `Boolean`.  
  
 L'operatore `Like` viene definito solo per criteri di ricerca di operandi `String`.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta, se necessario, di convertire ciascun operando nel tipo `String` prima dell'operazione.  Il tipo di dati del risultato sarà sempre `Boolean`.  
  
## Vedere anche  
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Comparison Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Operators](../../../visual-basic/language-reference/operators/index.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Comparison Operators](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)